---
title: Making Offline Model-Based Reinforcement Learning Work on Real Robots
title_zh: 让离线基于模型的强化学习在真实机器人上奏效
authors: "Chenhao Li, Andreas Krause, Marco Hutter"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=rbNOhbdQ0v"
tags: ["query:humanoid-rl"]
score: 8.0
evidence: 面向真实机器人的离线基于模型强化学习与世界模型
tldr: 针对离线基于模型的强化学习在真实机器人上受复合误差、分布偏移和噪声数据困扰的问题，论文提出面向物理机器人的离线MBRL流程RWM-O，在自回归世界模型中加入认知不确定性估计以支持更稳健的长时程推演。该方法旨在仅利用已有数据训练策略并提升数据效率，使离线世界模型方法从仿真基准走向真实机器人部署，为机器人强化学习提供可复用管线。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 离线基于模型强化学习虽数据高效，但在真实机器人噪声与部分观测数据上难以稳健应用。
method: 提出RWM-O，在自回归世界模型中加入认知不确定性估计，构建真实机器人离线MBRL流程。
result: 摘要强调该管线旨在提升离线MBRL在真实机器人长时程推演中的稳健性，具体数值未给出。
conclusion: 为离线世界模型强化学习在物理机器人上的可靠落地提供了系统化方案。
---

## Abstract
Reinforcement Learning (RL) has achieved impressive results in robotics, yet high-performing pipelines remain highly task-specific, with little reuse of prior data. Offline Model-based RL (MBRL) offers greater data efficiency by training policies entirely from existing datasets, but suffers from compounding errors and distribution shift in long-horizon rollouts. Although existing methods have shown success in controlled simulation benchmarks, robustly applying them to the noisy, biased, and partially observed datasets typical of real-world robotics remains challenging. We present a principled pipeline for making offline MBRL effective on physical robots. Our RWM-O extends autoregressive world models with epistemic uncertainty estimation, enabling temporally consistent multi-step rollouts with uncertainty effectively propagated over long horizons. We combine RWM-O with MOPO-PPO, which adapts uncertainty-penalized policy optimization to the stable, on-policy PPO framework for real-world control. We evaluate our approach on diverse manipulation and locomotion tasks in simulation and on a real quadruped, training policies entirely from offline datasets. The resulting policies consistently outperform model-free and uncertainty-unaware model-based baselines, and fusing real-world data in model learning further yields robust policies that surpass online model-free baselines trained solely in simulation.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向真实机器人的离线基于模型强化学习与世界模型。

### 2. 核心内容
针对离线基于模型的强化学习在真实机器人上受复合误差、分布偏移和噪声数据困扰的问题，论文提出面向物理机器人的离线MBRL流程RWM-O，在自回归世界模型中加入认知不确定性估计以支持更稳健的长时程推演。该方法旨在仅利用已有数据训练策略并提升数据效率，使离线世界模型方法从仿真基准走向真实机器人部署，为机器人强化学习提供可复用管线。

### 3. 对应检索需求
Find methods that use structured world models to improve sample efficiency in robotic reinforcement learning.

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=rbNOhbdQ0v](https://openreview.net/forum?id=rbNOhbdQ0v)
