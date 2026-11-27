---
title: "Bridging the Perception Gap: Probe-Guided Data Optimization Framework for Robotic Imitation Learning"
title_zh: 弥合感知差距：面向机器人模仿学习的探针引导数据优化框架
authors: "Xueqi Li, Zheng Wang, Han Xue, Xiaotong Liu, Zhaofengnian Wang, Guo-Ping Liu, Cewu Lu, Nanyang Ye"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=9n5mcj9onO"
tags: ["query:humanoid-rl"]
score: 6.0
evidence: 面向机器人模仿学习的感知差距数据优化
tldr: 针对机器人模仿学习中人类示范与机器人感知之间存在感知差距、导致策略表现不佳的问题，论文提出策略意图探针PIP，用小量示范训练代理模型并依据策略分布量化感知能力。方法据此划分鲁棒操作区与非鲁棒操作区，对非鲁棒区轨迹进行标准化并在进入鲁棒区后执行，从而优化示范数据。该框架旨在提升机器人操作模仿学习的可靠性，为感知与动作耦合的数据设计提供工具。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 传统示范数据采集忽视人机感知差距，使模仿学习策略在实际机器人上表现下降。
method: 提出策略意图探针PIP，量化模型感知能力并划分鲁棒与非鲁棒操作区以优化轨迹。
result: 摘要表明该框架可针对感知薄弱区域标准化轨迹，具体性能提升数值未给出。
conclusion: 为机器人模仿学习提供了一种以感知反馈指导数据优化的实用框架。
---

## Abstract
Imitation learning allows robots to acquire complex manipulation skills from human demonstrations. However, traditional data collection methods often haven't account for the "perceptual gap" between humans and robots, which leads to models that don't perform as expected. To solve this, we introduce Policy-Intent Probe (PIP). This method trains a proxy model with a small amount of demonstration data, then quantifies the model's perceptual capabilities based on its policy distribution. Based on the model's feedback, we divide the task's operational space into a Robust Operation Zone (ROZ) and a Non-Robust Operation Zone (NROZ). By standardizing the trajectories in the NROZ and waiting until the robot enters the ROZ to perform precise operations, we have optimized the data collection trajectories. Furthermore, aided by PIP, we can correctly carry out subtask segmentation. We can supplement data collection based on subtask complexity, which enhances the model's generalization and robustness. By cleaning only the subtask data containing anomalous trajectories or failure, we minimize data loss. Based on an empirical evaluation on three real-world tasks, we proved that perceptual capabilities can affect a task's success rate and that arbitrary subtask decomposition can lead to negative consequences. Our model-in-the-loop data optimization framework can significantly boost the success rate of long-horizon precision manipulation tasks, enhance model robustness, and increase data collection efficiency.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向机器人模仿学习的感知差距数据优化。

### 2. 核心内容
针对机器人模仿学习中人类示范与机器人感知之间存在感知差距、导致策略表现不佳的问题，论文提出策略意图探针PIP，用小量示范训练代理模型并依据策略分布量化感知能力。方法据此划分鲁棒操作区与非鲁棒操作区，对非鲁棒区轨迹进行标准化并在进入鲁棒区后执行，从而优化示范数据。该框架旨在提升机器人操作模仿学习的可靠性，为感知与动作耦合的数据设计提供工具。

### 3. 对应检索需求
Find work combining object centric representation learning and imitation learning for robot manipulation.

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=9n5mcj9onO](https://openreview.net/forum?id=9n5mcj9onO)
