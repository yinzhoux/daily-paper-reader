---
title: "ROBOWHEEL: A HELICAL DATA ENGINE FROM REAL-WORLD HUMAN DEMONSTRATIONS FOR CROSS-DOMAIN ROBOTIC LEARNING"
title_zh: RoboWheel：面向跨域机器人学习的真实人类示范螺旋数据引擎
authors: "Yuhong Zhang, Zihan Gao, Shengpeng Li, Ling-Hao Chen, Kaisheng Liu, Runqing Cheng, Xiao Lin, Junjia Liu, Zhuoheng Li, Jingyi Feng, Ziyan He, Jintian Lin, Zheyan Huang, Zhifang Liu, Haoqian Wang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=VBVCqm2t1J"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 将重建的人-物交互轨迹重定向到人形机器人与灵巧手
tldr: 针对跨形态机器人学习缺乏大规模高质量监督、真实人-物交互视频难以直接转为可执行动作的问题，论文提出RoboWheel数据引擎，从单目视频重建高精度手物交互，用强化学习优化器在接触与穿透约束下保证物理可行，并重定向到机械臂、灵巧手与人形机器人。实验表明该流程可生成接触丰富且可执行的轨迹，并在仿真增强下提升跨域机器人学习效果。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 跨形态机器人学习缺乏大规模高质量监督数据，真实人手-物体交互视频难以直接转化为可执行动作。
method: 提出RoboWheel数据引擎，从单目视频重建高精度手物交互，用强化学习优化器保证物理可行性，并重定向到机械臂、灵巧手与人形机器人。
result: 实验表明该流程可生成接触丰富且可执行的轨迹，并在仿真增强下提升跨域机器人学习效果。
conclusion: 该工作为跨形态机器人学习提供了可扩展的真实世界示范数据转化方案。
---

## Abstract
We introduce robowheel, a helical data engine that converts in-the-wild human hand–object interaction (HOI) videos into training-ready supervision for cross-morphology robotic learning. From monocular RGB/RGB-D inputs, we perform high-precision HOI reconstruction and enforce physical plausibility via a reinforcement learning optimizer that refines hand–object relative poses under contact and penetration constraints. The reconstructed, contact-rich trajectories are then retargetted to cross-domain embodiments, robot arms with simple end-effectors, dexterous hands, and humanoids, yielding executable actions and rollouts. To scale coverage, we build a simulation-augmented framework on Isaac Sim with diverse domain randomization (body variants, trajectories, object replacement, background changes, hand motion mirroring), which expands observations and labels while preserving contact semantics. This process forms an end-to-end pipeline from video → reconstruction → retargeting → augmentation → data acquisition, closing the loop for iterative policy improvement. Across vision-language-action and imitation-learning settings, \nbname-generated data provides reliable supervision and consistently improves task performance over baselines, enabling direct use of Internet HOI videos (hand-only or upper-body) as labels for scenario-specific training. We further assemble a large-scale multimodal dataset combining multi-camera captures, monocular videos, and public HOI corpora, and demonstrate transfer on dexterous-hand and humanoid platforms.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
将重建的人-物交互轨迹重定向到人形机器人与灵巧手。

### 2. 核心内容
针对跨形态机器人学习缺乏大规模高质量监督、真实人-物交互视频难以直接转为可执行动作的问题，论文提出RoboWheel数据引擎，从单目视频重建高精度手物交互，用强化学习优化器在接触与穿透约束下保证物理可行，并重定向到机械臂、灵巧手与人形机器人。实验表明该流程可生成接触丰富且可执行的轨迹，并在仿真增强下提升跨域机器人学习效果。

### 3. 对应检索需求
humanoid robots interacting with objects through whole-body control and manipulation。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=VBVCqm2t1J](https://openreview.net/forum?id=VBVCqm2t1J)
