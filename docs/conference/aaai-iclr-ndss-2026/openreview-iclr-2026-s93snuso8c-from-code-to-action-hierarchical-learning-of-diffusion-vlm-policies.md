---
title: "From Code to Action: Hierarchical Learning of Diffusion-VLM Policies"
title_zh: 从代码到动作：扩散-VLM策略的分层学习
authors: "Markus Peschl, Pietro Mazzaglia, Daniel Dijkman"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=S93SnUsO8c"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 结合VLM代码生成与扩散策略的分层模仿学习用于机器人操作
tldr: 针对机器人操作模仿学习在长时程复杂任务中泛化性差、数据稀缺的问题，本文提出一种分层框架。该方法把开源机器人API的子任务函数视为结构化监督信号，训练代码生成视觉语言模型将任务描述分解为可执行子程序，再由低层扩散策略模仿对应动作进行落地。实验表明该结构化分层方案能提升模仿学习的泛化能力，展示了结构化表示与模仿学习结合在机器人操作中的潜力。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 机器人操作模仿学习在复杂长时程任务中泛化性差且示范数据稀缺。
method: 用代码生成VLM分解任务为子程序，将其作为结构化监督，由扩散策略落地执行。
result: 实验表明该分层框架能提升模仿行为的泛化能力与长时程任务表现。
conclusion: 结构化子任务监督与扩散策略结合可增强机器人操作模仿学习的泛化性。
---

## Abstract
Imitation learning for robotic manipulation often suffers from limited generalization and data scarcity, especially in complex, long-horizon tasks. In this work, we introduce a hierarchical framework that leverages code-generating vision-language models (VLMs) in combination with low-level diffusion policies to effectively imitate and generalize robotic behavior. Our key insight is to treat open-source robotic APIs not only as execution interfaces but also as sources of structured supervision: the associated subtask functions - when exposed - can serve as modular, semantically meaningful labels. We train a VLM to decompose task descriptions into executable subroutines, which are then grounded through a diffusion policy trained to imitate the corresponding robot behavior. To handle the non-Markovian nature of both code execution and certain real-world tasks, such as object swapping, our architecture incorporates a memory mechanism that maintains subtask context across time. We find that this design enables interpretable policy decomposition, improves generalization when compared to flat policies and enables separate evaluation of high-level planning and low-level control.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
结合VLM代码生成与扩散策略的分层模仿学习用于机器人操作。

### 2. 核心内容
针对机器人操作模仿学习在长时程复杂任务中泛化性差、数据稀缺的问题，本文提出一种分层框架。该方法把开源机器人API的子任务函数视为结构化监督信号，训练代码生成视觉语言模型将任务描述分解为可执行子程序，再由低层扩散策略模仿对应动作进行落地。实验表明该结构化分层方案能提升模仿学习的泛化能力，展示了结构化表示与模仿学习结合在机器人操作中的潜力。

### 3. 对应检索需求
Find work combining object centric representation learning and imitation learning for robot manipulation.

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=S93SnUsO8c](https://openreview.net/forum?id=S93SnUsO8c)
