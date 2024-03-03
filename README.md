# Hugging Multi-Agent

## 项目简介
- 课程说明：Hugging Multi-Agent 是一套专为期望深入了解并实践多智能体系统的开发者设计的实用指南。基于国内领先的多智能体框架 MetaGPT（iclr 2024 oral） 旨在帮助读者掌握多智能体系统的核心概念，并提供一套全面的学习路径，从智能体的基础理解到复杂系统的实际开发。
- 面向人群：
  - 职业发展定位：本课程适合那些希望在**大模型和智能体开发**领域取得职业发展的工程师。与仅仅关注prompt工程的学习者不同，我们的目标受众是那些渴望**深入了解并实践****Agent****框架以及智能体系统的开发者**。
  - 技术基础：
    - 我们的课程将**直接从代码层面探索智能体的个性化开发**
    - 适合拥有**Python编程基础**（最好拥有一定异步编程基础）
    - 能**熟练阅读和理解项目源代码**的学习者
  - 兴趣与动机：适合对AI智能体领域充满热情的学习者，特别是那些希望从代码层面对智能体进行个性化能力开发的人。我们的课程旨在帮助学习者将理论知识转化为实际应用。

项目在线教程：https://deepwisdom.feishu.cn/wiki/MLILw0EdRiyiYRkJLgOcskyAnUh
MetaGPT:https://github.com/geekan/MetaGPT

## 目录

**第一章：前期准备**

**1.1 获取MetaGPT**

**1.2 配置MetaGPT**
> **1.2.1 申请 ChatGPT API 接口**
>> - **1.2.1.1 获取 OpenAI API Key**
>> - **1.2.1.2 配置 OpenAI API Key**
>> - **1.2.1.3 配置Gemini 智谱/星火等LLM**
>>- **1.3 首次尝试**

**第二章：智能体结构及多智能体框架介绍**

**2.1 AI Agent体系介绍**
> - **单体AI Agent**
> - **智能体用例**
>> - 概念验证Agent-BabyAGI
>> - 生成Agents模拟
>> - 应用层的Moe-多人求解
> - **2.1.3 Sy1&Sy2给Agent的启发**
> - **2.1.4 更多仓库以及产品**

**2.2 多智能体框架介绍**
> - **2.2.1 什么是MetaGPT**
> - **2.2.2 经典案例：软件公司**
> - **2.2.3 更多关于MetaGPT**
> - **2.2.4 其他多智能体框架**
>> - ChatDev
>> - AutoAgents
>> - agents
>> - Camel
>> - AutoGen

**第三章：智能体开发**

**3.1 Agent概念模块**

**3.2 RoleContext**

**3.3 实现一个简洁的Agent**
> - **3.3.1 需求分析**
> - **3.3.2 编写SimpleWriteCode助手**
> - **3.3.3 设计SimpleCoder角色**

**3.4 实现一个多功能Agent**
> - **3.4.1 需求分析**
> - **3.4.2 编写SimpleWriteCode助手**
> - **3.4.3 编写 SimpleRunCode 助手**
> - **3.4.4 定义 RunnableCoder 角色**
> - **3.4.5 运行 RunnableCoder 角色**

**3.5 实现一个管理类Agent: 技术文档助手**
> - **3.5.1 需求分析**
> - **3.5.2 编写 WriteDirectory 助手**
> - **3.5.3 编写 WriteContent 助手**
> - **3.5.4 编写 TutorialAssistant 角色**
> - **3.5.5 运行 TutorialAssistant 角色**

**3.6 智能体案例剖析**

**3.7 智能体开发作业**

**第四章：多智能体开发**

**4.1 Multi Agent概念模块**

**4.2 多智能体组件介绍**
> - **4.2.1 Environment**
> - **4.2.2 开发一个简单的多智能体系统**
> - **4.2.3 Team**
> - **4.2.4 基于Team开发的第一个智能体团队**

**4.3 多智能体案例: 辩论**
> - **4.3.1 定义动作**
> - **4.3.2 定义角色Role**
> - **4.3.3 实例化**

**4.4 多智能体开发作业**


## Roadmap

- [x] 发布第一版内容内测
- [x] 发布第一版内容公测
- [x] 更新多智能体内容
- [ ] 飞书内容迁移仓库
- [ ] 引入 python 并发编程基础
- [ ] werewolf_game 复现分析
- [ ] minecraft 项目复现分析
- [ ] agent + RL OverCooked AI Agent 解决方案
- [ ] llm 角度看agent实现（agent实现的底层原理）


## 参与贡献

- 如果你想参与到项目中来欢迎查看项目的 [Issue]() 查看没有被分配的任务。
- 如果你发现了一些问题，欢迎在 [Issue]() 中进行反馈🐛。
- 如果你对本项目感兴趣想要参与进来可以通过 [Discussion]() 进行交流💬。

如果你对 Datawhale 很感兴趣并想要发起一个新的项目，欢迎查看 [Datawhale 贡献指南](https://github.com/datawhalechina/DOPMC#%E4%B8%BA-datawhale-%E5%81%9A%E5%87%BA%E8%B4%A1%E7%8C%AE)。

## 贡献者名单

| 姓名 | 职责 | 简介 |
| :----| :---- | :---- |
| 潘笃驿 | 项目负责人 | 西安电子科技大学本科在读 |
| 陈叶帆 | 核心贡献者 | MetaGPT成员 |
| 沈楚城 | 核心贡献者 | MetaGPT成员 |
| 郑蕲 | 核心贡献者 | MetaGPT成员 |
| 徐宗泽 | 核心贡献者 | MetaGPT成员 |
| 李柯辰 | 贡献者 | Datawhale成员 |
| 丁世奇 | 贡献者 |  |
| 回车 | 贡献者 |  |


## 关注我们

<div align=center>
<p>扫描下方二维码关注公众号：Datawhale</p>
<img src="https://raw.githubusercontent.com/datawhalechina/pumpkin-book/master/res/qrcode.jpeg" width = "180" height = "180">
</div>

<div align=center>
<p>扫描下方二维码关注公众号：MetaGPT</p>
<img src="overrides\assets\images\metagpt.jpg" width = "180" height = "180">
</div>

## LICENSE

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://img.shields.io/badge/license-CC%20BY--NC--SA%204.0-lightgrey" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享署名-非商业性使用-相同方式共享 4.0 国际许可协议</a>进行许可。

*注：默认使用CC 4.0协议，也可根据自身项目情况选用其他协议*
