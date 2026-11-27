---
title: "Hierarchical Contrastive Reinforcement Learning: learn representation more suitable for RL environments"
title_zh: 分层对比强化学习：学习更适合强化学习环境的表征
authors: "Haomin Li, Yiran Xu, Haoyu Pan, Wei Tong, Guangyu Zhu, Edmond Qi Wu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=rTCSFOzVcK"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 面向强化学习环境的对比表征学习
tldr: 目标条件强化学习因稀疏奖励而难以训练，已有对比强化学习虽不依赖奖励但难以适配RL场景。作者提出分层对比强化学习HCRL，引入中间表征来降低目标表征的学习难度。该方法使对比学习更适合强化学习设定，从而更好地服务于下游RL任务。工作聚焦可迁移的表征学习工具，对结构化表征驱动的机器人RL具有方法借鉴价值。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 目标条件强化学习稀疏奖励难训练，对比学习如何适配RL设定仍待解决。
method: 提出分层对比强化学习HCRL，引入中间表征以降低目标表征的学习难度。
result: 使对比学习更好适配强化学习场景，在RL任务上取得更好表现。
conclusion: 为强化学习中更优表征学习提供通用方法，可迁移至机器人决策任务。
---

## Abstract
Goal-conditioned reinforcement learning holds significant importance for real-world environment, but its inherent sparse reward structure brings challenges. In recent years, some researchers have attempted to learn better representations to solve RL tasks, among which the contrastive reinforcement learning that is independent of rewards demonstrating strong performance. However, how to make contrastive learning better applicable to reinforcement learning settings is still a problem. In this paper, instead of learning representations related to goals in environments, we present hierarchical contrastive reinforcement learning (HCRL) method that reduces the difficulty of learn goal representations by introducing intermediate representations related to states. HCRL expresses such an idea that the agent should first understand the environment and then understand the tasks in the environment. Our method fully utilizes the information in the GCRL setting and provides a better representation learning method, which has better performance in various complex and sparse environments without adding additional assumptions or constraints. The results of comparison experiments show that HCRL has faster convergence speed and higher success rate than prior work on a range of goal-conditional RL tasks. We further conduct ablation studies and additional evaluations to validate our method. Anonymous code: https://anonymous.4open.science/r/HCRL-6E88.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向强化学习环境的对比表征学习。

### 2. 核心内容
目标条件强化学习因稀疏奖励而难以训练，已有对比强化学习虽不依赖奖励但难以适配RL场景。作者提出分层对比强化学习HCRL，引入中间表征来降低目标表征的学习难度。该方法使对比学习更适合强化学习设定，从而更好地服务于下游RL任务。工作聚焦可迁移的表征学习工具，对结构化表征驱动的机器人RL具有方法借鉴价值。

### 3. 对应检索需求
representation learning for control, robotics, and embodied decision making。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=rTCSFOzVcK](https://openreview.net/forum?id=rTCSFOzVcK)
