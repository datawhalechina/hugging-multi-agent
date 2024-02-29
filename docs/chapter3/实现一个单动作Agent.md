## 3.3 实现一个单动作Agent

下面将带领大家利用 MetaGPT 框架实现一个生成代码的 Agent SimpleCoder 我们希 望这个Agent 能够根据我们的需求来生成代码 要自己实现一个最简单的Role，只需要重写Role 基类的 _init_ 与 _act 方法 在 `_init_` 方法中，我们需要声明 Agent 的 `name`（名称）`profile`（类型）

我们使用 `self._init_action` 函数为其配备期望的动作 `SimpleWriteCode` 这个Action 应该能根据我们的需求生成我们期望的代码 在`_act`方法中，我们需要编写智能体具体的行动逻辑，智能体将从最新的记忆中获取 人类指令，运行配备的动作，MetaGPT 将其作为待办事项 (`self.rc.todo`) 在幕后 处理，最后返回一个完整的消息。

### 3.3.1 需求分析

要实现一个 `SimpleCoder` 我们需要分析这个Agent 它需要哪些能力

![analyse](/docs/chapter3/img/analyse.png)

首先我们需要让他接受用户的输入的需求，并记忆我们的需求，接着这个Agent它需 要根据自己已知的信息和需求来编写我们需要的代码。