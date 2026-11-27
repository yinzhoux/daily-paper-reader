---
title: "ExoPredicator: Learning Abstract Models of Dynamic Worlds for Robot Planning"
title_zh: ExoPredicator：为机器人规划学习动态世界的抽象模型
authors: "Yichao Liang, Thanh Dat Nguyen, Cambridge Yang, Tianyang Li, Joshua B. Tenenbaum, Carl Edward Rasmussen, Adrian Weller, Zenna Tavares, Tom Silver, Kevin Ellis"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=a1zfcaNTkM"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 带符号状态的学习型抽象世界模型用于高效机器人规划
tldr: 长程具身规划中，世界不仅因智能体动作改变，还存在并行发生的外生过程。作者提出抽象世界模型框架，联合学习符号状态表征以及内生动作与外生机制的因果过程。借助变分贝叶斯推断与语言模型提议，从有限数据中学习这些模型。在五个桌面机器人仿真环境中，学习到的模型支持快速规划并能泛化到含更多物体与更复杂任务的场景。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 长程具身规划需应对与智能体动作并行发生的外生过程，传统建模难以兼顾。
method: 联合学习符号状态表征与内外生因果过程，用变分贝叶斯推断结合语言模型提议学习世界模型。
result: 在五个桌面机器人仿真环境中实现快速规划，并泛化到更多物体与更复杂任务。
conclusion: 说明结构化抽象世界模型可在有限数据下支撑高效且可泛化的机器人规划。
---

## Abstract
Long-horizon embodied planning is challenging because the world does not only change through an agent's actions: exogenous processes (e.g., water heating, dominoes cascading) unfold concurrently with the agent's actions. We propose a framework for abstract world models that jointly learns (i) symbolic state representations and (ii) causal processes for both endogenous actions and exogenous mechanisms. Each causal process models the time course of a stochastic cause-effect relation. We learn these world models from limited data via variational Bayesian inference combined with LLM proposals. Across five simulated tabletop robotics environments, the learned models enable fast planning that generalizes to held-out tasks with more objects and more complex goals, outperforming a range of baselines.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
带符号状态的学习型抽象世界模型用于高效机器人规划。

### 2. 核心内容
长程具身规划中，世界不仅因智能体动作改变，还存在并行发生的外生过程。作者提出抽象世界模型框架，联合学习符号状态表征以及内生动作与外生机制的因果过程。借助变分贝叶斯推断与语言模型提议，从有限数据中学习这些模型。在五个桌面机器人仿真环境中，学习到的模型支持快速规划并能泛化到含更多物体与更复杂任务的场景。

### 3. 对应检索需求
Find methods that use structured world models to improve sample efficiency in robotic reinforcement learning.

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=a1zfcaNTkM](https://openreview.net/forum?id=a1zfcaNTkM)
