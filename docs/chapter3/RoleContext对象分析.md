---
comments: true
---

## 3.2 RoleContext 

而 Role 在与环境上下文进行交互时，是通过内部的 RoleContext 对象来实现的。本篇我们就来看看 RoleContext 中都有哪些内容。

> 代码版本使用 v0.6.6

```python
class RoleContext(BaseModel):
    """Role Runtime Context"""

    model_config = ConfigDict(arbitrary_types_allowed=True)

    # # env exclude=True to avoid `RecursionError: maximum recursion depth exceeded in comparison`
    env: "Environment" = Field(default=None, exclude=True)  # # avoid circular import
    # TODO judge if ser&deser
    msg_buffer: MessageQueue = Field(
        default_factory=MessageQueue, exclude=True
    )  # Message Buffer with Asynchronous Updates
    memory: Memory = Field(default_factory=Memory)
    # long_term_memory: LongTermMemory = Field(default_factory=LongTermMemory)
    state: int = Field(default=-1)  # -1 indicates initial or termination state where todo is None
    todo: Action = Field(default=None, exclude=True)
    watch: set[str] = Field(default_factory=set)
    news: list[Type[Message]] = Field(default=[], exclude=True)  # TODO not used
    react_mode: RoleReactMode = (
        RoleReactMode.REACT
    )  # see `Role._set_react_mode` for definitions of the following two attributes
    max_react_loop: int = 1
```

**env**：Environment 对象，当在 Environment 添加 Role 时会同时设置 Role 对 Environment 的引用。

**msg_buffer**：一个 MessageQueue 对象，该对象是对 asyncio 的 Queue 进行简单封装，主要是提供了非阻塞的 pop / push 方法。Role 通过该对象与环境中的其他 Role 进行信息交互。

**memory**：记忆对象。当 Role 执行 _act 时，会将执行得到的响应转换为 Message 对象放入 memory 中。另外当 Role 执行 _observe 时，会把 msg_buffer 的所有消息转移到 memory 中。

**state**：记录 Role 的执行状态。初始状态值为 -1，当全部 Action 执行完成之后也会被重置为 -1。

**todo**：下一个待执行的 Action。当 state >= 0 时会指向最后一个 Action。

**watch**：用 str 表示的当前 Role 观察的 Action 列表，目前用在 _observe 获取 news 时进行消息过滤。

**news**：存储那些在本次执行  _observe 时读取到的与当前 Role 上下游相关的消息。

**react_mode**：ReAct 循环的模式，目前支持 REACT、BY_ORDER、PLAN_AND_ACT 3种模式，默认使用 REACT 模式。在 _set_react_mode 方法中有相关说明。简单来说，BY_ORDER 模式按照指定的 Action 顺序执行。PLAN_AND_ACT 则为一次思考后执行多个动作，即 _think -> _act -> act -> ...，而 REACT 模式按照 ReAct 论文中的思考——行动循环来执行，即 _think -> _act -> _think -> _act -> ...。

**max_react_loop**：在 react_mode 为 REACT 模式时生效，用于设置最大的思考-循环次数，超过后会停止 _react 执行。

**部分参数的讲解将在多智能体篇详解**