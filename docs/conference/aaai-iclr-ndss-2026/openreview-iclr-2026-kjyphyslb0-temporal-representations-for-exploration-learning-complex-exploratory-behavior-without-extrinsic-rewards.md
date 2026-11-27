---
title: "Temporal Representations for Exploration: Learning Complex Exploratory Behavior without Extrinsic Rewards"
title_zh: 面向探索的时序表示：无需外部奖励学习复杂探索行为
authors: "Faisal Mohamed, Catherine Ji, Benjamin Eysenbach, Glen Berseth"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=KjYpHySlb0"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 利用时序对比表示学习引导强化学习中的探索
tldr: 针对强化学习探索需要智能体理解自身如何感知与表示世界的问题，本文提出一种基于时序表示的学习方法。该方法利用时序对比表示捕捉完成任务所需的信息，避免完整状态重建的计算开销，并优先探索未来结果难以预测的状态。实验表明这种表示能够驱动智能体在无外部奖励条件下学习复杂的探索行为，说明表示学习与决策过程的耦合对具身智能体具有重要意义。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 强化学习探索不仅需记录访问过何处，还需理解智能体如何感知和表示世界。
method: 提出基于时序对比表示的探索方法，优先探索未来结果不可预测的状态。
result: 实验表明该表示可驱动智能体在无外部奖励下学习复杂探索行为。
conclusion: 时序表示学习与探索策略的结合可提升具身智能体的自主学习能力。
---

## Abstract
Effective exploration in reinforcement learning requires not only tracking where an agent has been, but also understanding how the agent perceives and represents the world. To learn powerful representations, an agent should actively explore states that contribute to its knowledge of the environment. Temporal representations can capture the information necessary to solve a wide range of potential tasks while avoiding the computational cost associated with full state reconstruction. In this paper, we propose an exploration method that leverages temporal contrastive representations to guide exploration, prioritizing states with unpredictable future outcomes. We demonstrate that such representations can enable the learning of complex exploratory behaviors in locomotion, manipulation, and embodied-AI tasks, revealing capabilities and behaviors that traditionally require extrinsic rewards. Unlike approaches that rely on explicit distance learning or episodic memory mechanisms (e.g., quasimetric-based methods), our method builds directly on temporal similarities, yielding a simpler yet effective strategy for exploration.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
利用时序对比表示学习引导强化学习中的探索。

### 2. 核心内容
针对强化学习探索需要智能体理解自身如何感知与表示世界的问题，本文提出一种基于时序表示的学习方法。该方法利用时序对比表示捕捉完成任务所需的信息，避免完整状态重建的计算开销，并优先探索未来结果难以预测的状态。实验表明这种表示能够驱动智能体在无外部奖励条件下学习复杂的探索行为，说明表示学习与决策过程的耦合对具身智能体具有重要意义。

### 3. 对应检索需求
representation learning for control, robotics, and embodied decision making。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=KjYpHySlb0](https://openreview.net/forum?id=KjYpHySlb0)
