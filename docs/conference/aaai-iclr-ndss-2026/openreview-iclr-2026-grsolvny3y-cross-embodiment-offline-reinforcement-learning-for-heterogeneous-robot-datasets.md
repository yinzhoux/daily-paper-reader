---
title: Cross-Embodiment Offline Reinforcement Learning for Heterogeneous Robot Datasets
title_zh: 面向异构机器人数据集的跨本体离线强化学习
authors: "Haruki Abe, Takayuki Osa, Yusuke Mukuta, Tatsuya Harada"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=GrsoLVNy3Y"
tags: ["query:humanoid-rl"]
score: 6.0
evidence: 利用跨本体离线强化学习获取通用机器人控制先验
tldr: 针对为每个机器人平台采集高质量示范成本高昂、制约策略预训练规模化的问题，本文将离线强化学习与跨本体学习相结合。离线RL可利用专家与大量次优数据，跨本体学习则聚合不同形态机器人的轨迹以获取通用控制先验。作者构建了覆盖16种机器人平台的运动数据集进行系统分析，揭示了该范式的优势与局限，为具身智能体的通用控制策略预训练提供了原理性理解与评测基准。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 为每个平台采集高质量示范成本高，限制了机器人策略预训练的规模化。
method: 将离线强化学习与跨本体学习结合，聚合同构与异构机器人轨迹获取通用控制先验。
result: 构建覆盖16种机器人平台的运动数据集，系统分析该范式的优势与局限。
conclusion: 离线RL与跨本体学习的结合为通用机器人控制先验提供了可行路径与评测基础。
---

## Abstract
Scalable robot policy pre-training has been hindered by the high cost of collecting high-quality demonstrations for each platform. In this study, we address this issue by uniting offline reinforcement learning (offline RL) with cross-embodiment learning. Offline RL leverages both expert and abundant suboptimal data, and cross-embodiment learning aggregates heterogeneous robot trajectories across diverse morphologies to acquire universal control priors. We perform a systematic analysis of this offline RL and cross-embodiment paradigm, providing a principled understanding of its strengths and limitations. To evaluate this offline RL and cross-embodiment paradigm, we construct a suite of locomotion datasets spanning 16 distinct robot platforms. Our experiments confirm that this combined approach excels at pre-training with datasets rich in suboptimal trajectories, outperforming pure behavior cloning. However, as the proportion of suboptimal data and the number of robot types increase, we observe that conflicting gradients across morphologies begin to impede learning. To mitigate this, we introduce an embodiment-based grouping strategy in which robots are clustered by morphological similarity and the model is updated with a group gradient. This simple, static grouping substantially reduces inter-robot conflicts and outperforms existing conflict-resolution methods. Project page: https://haruki-abe.github.io/cross_embodiment_offline_rl_website

---

## 论文详细总结（自动生成）

### 1. 检索相关性
利用跨本体离线强化学习获取通用机器人控制先验。

### 2. 核心内容
针对为每个机器人平台采集高质量示范成本高昂、制约策略预训练规模化的问题，本文将离线强化学习与跨本体学习相结合。离线RL可利用专家与大量次优数据，跨本体学习则聚合不同形态机器人的轨迹以获取通用控制先验。作者构建了覆盖16种机器人平台的运动数据集进行系统分析，揭示了该范式的优势与局限，为具身智能体的通用控制策略预训练提供了原理性理解与评测基准。

### 3. 对应检索需求
reinforcement learning methods for controlling embodied agents and humanoid robots。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=GrsoLVNy3Y](https://openreview.net/forum?id=GrsoLVNy3Y)
