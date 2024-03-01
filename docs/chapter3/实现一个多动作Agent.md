## 3.4 实现一个多动作 Agent

### 3.4.1 需求分析

![require](/docs/chapter3/img/require.png)

假设现在我们不仅希望用自然语言编写代码，而且还希望生成的代码立即执行。一个拥有多个动作的智能体可以满足我们的需求。让我们称之为RunnableCoder，一个既写代码又立即运行的 Role。我们需要两个 Action：SimpleWriteCode 和 SimpleRunCode

### 3.4.2 编写 SimpleWriteCode 动作

这部分与我们在前文中讲到的基本一致

```python
class SimpleWriteCode(Action):

    PROMPT_TEMPLATE: str = """
    Write a python function that can {instruction} and provide two runnnable test cases.
    Return ```python your_code_here ``` with NO other texts,
    your code:
    """

    name: str = "SimpleWriteCode"

    async def run(self, instruction: str):
        prompt = self.PROMPT_TEMPLATE.format(instruction=instruction)
        rsp = await self._aask(prompt)
        code_text = SimpleWriteCode.parse_code(rsp)
        return code_text

    @staticmethod
    def parse_code(rsp):
        pattern = r'```python(.*)```'
        match = re.search(pattern, rsp, re.DOTALL)
        code_text = match.group(1) if match else rsp
        return code_text
```

### 3.4.3 编写 SimpleRunCode 动作

从概念上讲，一个动作可以利用LLM，也可以在没有LLM的情况下运行。在SimpleRunCode的情况下，LLM不涉及其中。我们只需启动一个子进程来运行代码并 获取结果
在 Python 中，我们通过标准库中的 `subprocess` 包来 fork 一个子进程，并运行一个外 部的程序。
subprocess包中定义有数个创建子进程的函数，这些函数分别以不同的方式创建子进 程，所以我们可以根据需要来从中选取一个使用。
第一个进程是你的Python 程序本身，它执行了包含 `SimpleRunCode` 类定义的代码。第二个进程是由 `subprocess.run` 创建的，它执行了 `python3 -c` 命令，用于运行 `code_text` 中包含的 Python 代码。这两个进程相互独立，通过 `subprocess.run` 你的Python 程序可以启动并与第二个进程进行交互，获取其输出结果。

```python
class SimpleRunCode(Action):

    name: str = "SimpleRunCode"

    async def run(self, code_text: str):
        # 在Windows环境下，result可能无法正确返回生成结果，在windows中在终端中输入python3可能会导致打开微软商店
        result = subprocess.run(["python3", "-c", code_text], capture_output=True, text=True)
        # 采用下面的可选代码来替换上面的代码
        # result = subprocess.run(["python", "-c", code_text], capture_output=True, text=True)
        # import sys
        # result = subprocess.run([sys.executable, "-c", code_text], capture_output=True, text=True)
        code_result = result.stdout
        logger.info(f"{code_result=}")
        return code_result
```



### 3.4.4 定义 RunnableCoder 角色

与定义单一动作的智能体没有太大不同！让我们来映射一下：
1. 用 `self._init_actions` 初始化所有 Action 

2. 2. 指定每次 Role 会选择哪个 `Action`。我们将 `react_mode` 设置为 "by_order"，这意味着 `Role` 将按照 `self._init_actions` 中指定的顺序执行其能 够执行的 `Action`。在这种情况下，当 `Role` 执行 `_act` 时，`self.rc.todo` 将首先 是 `SimpleWriteCode`，然后是 `SimpleRunCode`。

3. 覆盖 `_act` 函数。Role 从上一轮的人类输入或动作输出中检索消息，用适当的`Message` 内容提供当前的 `Action (self.rc.todo)`，最后返回由当前 `Action` 输出 组成的 `Message`。这里我们用 Role 类的 _set_react_mode 方法来设定我们 action 执行的先后顺序，事实上Role基类中还包含了很多有用的方法，你可以自己查看它的定义，在后面的章节 内容中，我们也将一步一步揭开他们的面纱。

  ```python
  class RunnableCoder(Role):
  
      name: str = "Alice"
      profile: str = "RunnableCoder"
  
      def __init__(self, **kwargs):
          super().__init__(**kwargs)
          self._init_actions([SimpleWriteCode, SimpleRunCode])
          self._set_react_mode(react_mode="by_order")
  
      async def _act(self) -> Message:
          logger.info(f"{self._setting}: 准备 {self.rc.todo}")
          # 通过在底层按顺序选择动作
          # todo 首先是 SimpleWriteCode() 然后是 SimpleRunCode()
          todo = self.rc.todo
  
          msg = self.get_memories(k=1)[0] # 得到最相似的 k 条消息
          result = await todo.run(msg.content)
  
          msg = Message(content=result, role=self.profile, cause_by=type(todo))
          self.rc.memory.add(msg)
          return msg
  ```

  ### 3.4.5 运行 RunnableCoder 角色

  这部分与 SimpleCoder 基本一致，只需要修改我们使用的 role 为 RunnableCoder

  ```python
  import asyncio
  
  async def main():
      msg = "write a function that calculates the sum of a list"
      role = RunnableCoder()
      logger.info(msg)
      result = await role.run(msg)
      logger.info(result)
  
  asyncio.run(main())
  ```

  完整代码如下：

  ```python
  import os
  import re
  import subprocess
  import asyncio
  
  import fire
  import sys
  from metagpt.llm import LLM
  from metagpt.actions import Action
  from metagpt.roles import Role
  from metagpt.schema import Message
  from metagpt.logs import logger
  
  class SimpleWriteCode(Action):
  
      PROMPT_TEMPLATE :str = """
      Write a python function that can {instruction} and provide two runnnable test cases.
      Return ```python your_code_here ``` with NO other texts,
      your code:
      """
  
      name: str = "SimpleWriteCode"
  
      async def run(self, instruction: str):
          prompt = self.PROMPT_TEMPLATE.format(instruction=instruction)
          rsp = await self._aask(prompt)
          code_text = SimpleWriteCode.parse_code(rsp)
          return code_text
  
      @staticmethod
      def parse_code(rsp):
          pattern = r'```python(.*)```'
          match = re.search(pattern, rsp, re.DOTALL)
          code_text = match.group(1) if match else rsp
          return code_text
  
  class SimpleRunCode(Action):
  
      name: str = "SimpleRunCode"
  
      async def run(self, code_text: str):
          result = subprocess.run([sys.executable, "-c", code_text], capture_output=True, text=True)
          code_result = result.stdout
          logger.info(f"{code_result=}")
          return code_result
  
  class RunnableCoder(Role):
  
      name: str = "Alice"
      profile: str = "RunnableCoder"
  
      def __init__(self, **kwargs):
          super().__init__(**kwargs)
          self._init_actions([SimpleWriteCode, SimpleRunCode])
          self._set_react_mode(react_mode="by_order")
  
      async def _act(self) -> Message:
          logger.info(f"{self._setting}: ready to {self.rc.todo}")
          # By choosing the Action by order under the hood
          # todo will be first SimpleWriteCode() then SimpleRunCode()
          todo = self.rc.todo
  
          msg = self.get_memories(k=1)[0] # find the most k recent messagesA
          result = await todo.run(msg.content)
  
          msg = Message(content=result, role=self.profile, cause_by=type(todo))
          self.rc.memory.add(msg)
          return msg
  
  async def main():
      msg = "write a function that calculates the sum of a list"
      role = RunnableCoder()
      logger.info(msg)
      result = await role.run(msg)
      logger.info(result)
  
  asyncio.run(main())
  ```

  

