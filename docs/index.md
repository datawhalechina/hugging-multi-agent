# Hugging Multi-Agent

## 项目简介
Hugging Multi-Agent 是一套专为期望深入了解并实践多智能体系统的开发者设计的实用指南。本书旨在帮助读者掌握多智能体系统的核心概念，并提供一套全面的学习路径，从智能体的基础理解到复杂系统的实际开发。  

**由于12月版本迭代较快，本教程 task1-4 基于 MetaGPTv0.4 版本开发，其中旧版本仍能够实现单智能体的特性 role 与 action 能力的编排，其中内测使用的是 0.4 版本另外 0.5.2 版本(推荐)也做过旧版本的兼容**  

在线飞书文档：[Hugging Multi-Agent](https://deepwisdom.feishu.cn/docx/RJmTdvZuPozAxFxEpFxcbiPwnQf)

## 适合谁来学？

职业发展定位：本课程特别适合那些希望在大模型和智能体开发领域取得职业发展的工程师。与仅仅关注prompt工程的学习者不同，我们的目标受众是那些渴望深入了解并实践MetaGPT框架以及智能体系统的开发者。

技术基础：适合拥有Python编程基础，并能熟练阅读和理解大模型源代码的学习者。我们的课程将直接从代码层面探索智能体的个性化开发，因此对自然语言编程有一定了解的学习者将能更好地吸收课程内容。

兴趣与动机：适合对AI智能体领域充满热情的学习者，特别是那些希望从代码层面对智能体进行个性化能力开发的人。我们的课程旨在帮助学习者将理论知识转化为实际应用。

首次体验者：适合那些有意愿首次参加AI黑客松，并希望成为大模型技术开发者的初学者。本课程将为他们提供一个理想的起点。

## 不适合谁来学？

理论兴趣者：对于仅希望了解智能体相关概念而对实际的Agent开发不感兴趣的学习者，本课程可能不太适合。我们的重点是在实战中应用智能体技术。

经验丰富的研究人员：已经对市面上智能体项目非常熟悉，并且具备丰富智能体开发经验的研究人员可能会发现课程内容对他们来说过于基础。

理论深入者：想要通过本课程深入理解智能体相关理论和论文观点的学习者可能会发现，课程内容更侧重于实际的代码开发和应用实践，而不是理论研究。

## 目录

第一章：前期准备

1. 获取MetaGPT  

2. 配置MetaGPT  
  2.1 调用 ChatGPT API 服务  
    2.1.1 获取 OpenAI API Key  
    2.1.2 配置 OpenAI API Key  
    2.1.3 首次尝试

第二章：AI Agent知识体系结构  

1. 智能体的定义  
  1.1 什么是智能体?  
  1.2 智能体举例  
  1.3 相关资料  

2. 热门智能体案例  
  2.1 流行的GPTs  
  2.2 Openai time line 案例迅速体验  
  2.3 代码产品  
  2.4 更多仓库以及产品  
  
3. 智能体的宏观机会  

4. AI Agent 与Sy1&Sy2  
  4.1 Agent：LLM时代的新软件  
  4.2 Sy1&Sy2给Agent的启发  
  4.3 相关资料  
  
5. 第二章课程任务

第三章：MetaGPT框架组件介绍  

1. Agent组件介绍  
  1.1 Agent概念概述  
  1.2 实现一个单动作Agent  
  1.3 实现一个多动作Agent  
  
2. 第三章课程任务

第四章：OSS - 订阅智能体  

1. 基本介绍  
  1.1 什么是订阅智能体  
  1.2 如何用MetaGPT实现订阅智能体  
  
2. 教程信息  
  2.1 前置准备  
  2.2 教程目标
  
3. OSS订阅智能体实现  
  3.1 前置介绍  
  3.2 OSSWatcher Role实现  
  3.3 Trigger实现  
  3.4 Callback设计  
  
4. 运行示例  

5. 第四章课程任务

## Roadmap

- [x] 发布第一版内容内测
- [x] 发布第一版内容公测
- [x] 飞书内容迁移仓库
- [ ] 更新多智能体内容

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



## 关注我们

<div align=center>
<p>扫描下方二维码关注公众号：Datawhale</p>
<img src="https://raw.githubusercontent.com/datawhalechina/pumpkin-book/master/res/qrcode.jpeg" width = "180" height = "180">
</div>

## LICENSE

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://img.shields.io/badge/license-CC%20BY--NC--SA%204.0-lightgrey" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享署名-非商业性使用-相同方式共享 4.0 国际许可协议</a>进行许可。

*注：默认使用CC 4.0协议，也可根据自身项目情况选用其他协议*
