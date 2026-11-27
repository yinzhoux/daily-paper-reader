---
title: Grounding Bodily Awareness in Visual Representations for Efficient Policy Learning
title_zh: 将身体感知扎根于视觉表征以实现高效策略学习
authors: "Junlin Wang, Zhiyun Lin"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=ZaB2fV3TYo"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 面向操作策略的智能体中心视觉表征学习
tldr: 机器人操作中的视觉表征常缺乏身体相关线索，导致策略学习效率受限。作者提出ICon，在视觉Transformer的token级表征上施加对比学习，将智能体专属token与环境token在特征空间分离。由此获得嵌入身体归纳偏置的智能体中心视觉表征，可无缝接入端到端策略学习。该工作说明身体感知的表征有助于提升下游操作任务的策略学习效率。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 机器人操作的视觉表征缺乏身体相关线索，导致动作执行与策略学习效率受限。
method: 提出ICon，在ViT的token级表征上做对比学习，分离智能体与环境token以获得智能体中心表征。
result: 所得表征嵌入身体归纳偏置，可无缝集成到端到端策略学习中，提升下游操作任务表现。
conclusion: 表明携带身体线索的视觉表征能有效促进机器人操作策略的高效学习。
---

## Abstract
Learning effective visual representations for robotic manipulation remains a fundamental challenge due to the complex body dynamics involved in action execution. In this paper, we study how visual representations that carry body-relevant cues can enable efficient policy learning for downstream robotic manipulation tasks. We present $\textbf{I}$nter-token $\textbf{Con}$trast ($\textbf{ICon}$), a contrastive learning method applied to the token-level representations of Vision Transformers (ViTs). ICon enforces a separation in the feature space between agent-specific and environment-specific tokens, resulting in agent-centric visual representations that embed body-specific inductive biases. This framework can be seamlessly integrated into end-to-end policy learning by incorporating the contrastive loss as an auxiliary objective. Our experiments show that ICon not only improves policy performance across various manipulation tasks but also facilitates policy transfer across different robots. The project website: https://anonymous.4open.science/w/ICon/

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向操作策略的智能体中心视觉表征学习。

### 2. 核心内容
机器人操作中的视觉表征常缺乏身体相关线索，导致策略学习效率受限。作者提出ICon，在视觉Transformer的token级表征上施加对比学习，将智能体专属token与环境token在特征空间分离。由此获得嵌入身体归纳偏置的智能体中心视觉表征，可无缝接入端到端策略学习。该工作说明身体感知的表征有助于提升下游操作任务的策略学习效率。

### 3. 对应检索需求
representation learning for control, robotics, and embodied decision making。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=ZaB2fV3TYo](https://openreview.net/forum?id=ZaB2fV3TYo)
