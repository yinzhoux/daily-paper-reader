---
title: Learning Task-Sufficient World Models via Intervention-Curriculum Co-Design
title_zh: 通过干预-课程协同设计学习任务充分的世界模型
authors: "Fan Feng, Yujia Zheng, Minghao Fu, Yongqiang Chen, Guangyi Chen, Kevin Patrick Murphy, Biwei Huang, Kun Zhang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=xFmxnyNYZJ"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 为控制学习任务充分的结构化潜在世界模型
tldr: 针对世界模型常依赖像素预测或通用嵌入、包含冗余信息的问题，本文研究如何学习任务特定、最小且充分的潜在表征。方法将问题建模为智能体与环境交互的闭环，对每个新任务先用主动干预采集揭示任务相关潜在因子的轨迹，再训练世界模型获得最小充分潜空间。该干预与课程协同设计提升了表征对控制的适配性，为结构化世界模型学习提供了新范式。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有世界模型常预测像素或依赖通用嵌入，难以获得控制所需的最小充分表征。
method: 将学习建模为交互闭环，用主动干预获取信息轨迹并训练任务特定的最小充分潜空间。
result: 干预与课程协同设计使学到的潜在表征更贴合控制需求，提升序贯决策表现。
conclusion: 任务充分的结构化世界模型为高效决策提供了可解释且精简的表征基础。
---

## Abstract
We study how agents learn world models with latent representations that are task-specific, minimal, and sufficient for sequential decision making. Rather than predicting pixels or relying on generic embeddings, we aim to learn representations that retain exactly the information needed for control across tasks. We model the problem end-to-end as a closed loop of agent–environment interaction, enabling the agent to sequentially acquire minimal and sufficient latent representations over a series of tasks.
On the agent side, for each new task, it begins with active intervention to acquire informative trajectories that implicitly reveal task-relevant latent factors, and then trains the world model to learn a latent space that is both minimal and task-sufficient.
On the environment side, learning is facilitated through an adaptive curriculum that co-evolves with the agent. By tailoring environment settings and task order to the agent's learning progress, the curriculum exposes control-relevant mechanisms at the right level of difficulty, while jointly scheduling world-model updates with policy learning. This co-design of intervention and curriculum leads to a compact, structured latent space that supports efficient, transferable policy learning and generalization. Empirically, our approach improves sample efficiency and generalization across skills, object–skill compositions, and unseen tasks on standard continuous control and robotic manipulation benchmarks.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
为控制学习任务充分的结构化潜在世界模型。

### 2. 核心内容
针对世界模型常依赖像素预测或通用嵌入、包含冗余信息的问题，本文研究如何学习任务特定、最小且充分的潜在表征。方法将问题建模为智能体与环境交互的闭环，对每个新任务先用主动干预采集揭示任务相关潜在因子的轨迹，再训练世界模型获得最小充分潜空间。该干预与课程协同设计提升了表征对控制的适配性，为结构化世界模型学习提供了新范式。

### 3. 对应检索需求
Find methods that use structured world models to improve sample efficiency in robotic reinforcement learning.

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=xFmxnyNYZJ](https://openreview.net/forum?id=xFmxnyNYZJ)
