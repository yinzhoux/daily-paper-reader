---
title: Adapting World Models with Latent-State Dynamics Residuals
title_zh: 利用潜在状态动态残差适配世界模型
authors: "JB Lanier, Kyungmin Kim, Armin Karamzade, Yifei Liu, Ankita sinha, Kathleen He, Davide Corsi, Roy Fox"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=W5e6Kkr2WN"
tags: ["query:humanoid-rl"]
score: 8.0
evidence: 带潜在状态动态残差校正的世界模型用于提升强化学习样本效率
tldr: 针对仿真到现实强化学习中动力学失配且高维图像状态难以直接做残差校正的问题，本文提出ReDRAW。该方法在仿真中预训练潜在状态自回归世界模型，并通过潜在状态动力学的残差校正将其校准到目标环境，而非在显式观测状态上修正。借助校正后的世界模型，智能体可在想象 rollout 上优化策略，从而在真实数据稀缺时提升样本效率与部署性能，为结构化世界模型用于机器人强化学习提供了可行方案。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 仿真到现实的动力学差异会降低智能体性能，而图像等高维状态难以直接做残差校正。
method: 在仿真预训练潜在状态自回归世界模型，并对潜在动力学施加残差校正以适配目标环境。
result: 校正后的世界模型支持在想象rollout上优化策略，在真实数据稀缺时提升表现。
conclusion: 潜在空间的世界模型残差适配可有效缓解仿真到现实的动力学差距。
---

## Abstract
Simulation-to-reality reinforcement learning (RL) faces the challenge of reconciling discrepancies between simulated and real-world dynamics, which can degrade agent performance. When real data is scarce, a promising approach involves learning corrections to simulator forward dynamics represented as a residual error function, however this operation is impractical with high-dimensional states such as images. To overcome this, we propose ReDRAW, a latent-state autoregressive world model pretrained in simulation and calibrated to a target environment through residual corrections of latent-state dynamics rather than of explicit observed states. Using this adapted world model, ReDRAW enables RL agents to be optimized with imagined rollouts under corrected dynamics and then deployed in the real world. In multiple vision-based DeepMind Control Suite domains and a physical robot visual lane-following task, ReDRAW effectively models changes to dynamics and avoids overfitting in low data regimes where traditional transfer methods fail.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
带潜在状态动态残差校正的世界模型用于提升强化学习样本效率。

### 2. 核心内容
针对仿真到现实强化学习中动力学失配且高维图像状态难以直接做残差校正的问题，本文提出ReDRAW。该方法在仿真中预训练潜在状态自回归世界模型，并通过潜在状态动力学的残差校正将其校准到目标环境，而非在显式观测状态上修正。借助校正后的世界模型，智能体可在想象 rollout 上优化策略，从而在真实数据稀缺时提升样本效率与部署性能，为结构化世界模型用于机器人强化学习提供了可行方案。

### 3. 对应检索需求
Find methods that use structured world models to improve sample efficiency in robotic reinforcement learning.

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=W5e6Kkr2WN](https://openreview.net/forum?id=W5e6Kkr2WN)
