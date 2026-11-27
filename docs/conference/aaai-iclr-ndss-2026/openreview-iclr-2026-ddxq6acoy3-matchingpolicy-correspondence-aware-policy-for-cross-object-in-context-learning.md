---
title: "MatchingPolicy: Correspondence-aware Policy For Cross-object In-context Learning"
title_zh: MatchingPolicy：面向跨物体上下文学习的对应感知策略
authors: "Qijin She, Hanyang Yu, Zeming Li, Ping Tan"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=ddxq6ACoY3"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 结合对应关系与图扩散策略的跨物体模仿学习操作
tldr: 针对上下文模仿学习在未见物体与新场景上泛化差的问题，本文提出 MatchingPolicy 框架，将演示与场景的对应匹配从策略学习中解耦。方法借助视觉基础模型提取稠密对应，并采用图扩散策略据此自适应调整机器人动作，同时引入在线自适应匹配算法动态建立可靠对应。实验表明该方法在跨物体、跨任务迁移上更为鲁棒，为对象级对应驱动的模仿学习操作提供了新思路。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有上下文模仿学习在未见物体和新场景中常失败，难以实现少样本任务泛化。
method: 提出对应感知框架，将演示与场景匹配和策略学习解耦，用图扩散策略结合视觉基础模型对应。
result: 结合在线自适应匹配后，方法在多样任务上实现更鲁棒的跨物体动作迁移。
conclusion: 显式解耦对应与策略学习是提升操作模仿泛化性的有效途径。
---

## Abstract
In-context imitation learning enables few-shot task generalization by conditioning policies on demonstrations, but existing methods often fail on unseen objects or novel scenarios. We introduce MatchingPolicy, a correspondence-aware framework that explicitly decouples demonstration–scene matching from policy learning. At its core, MatchingPolicy employs a graph-based diffusion policy that adapts robot actions based on dense correspondences extracted by vision foundation models. This separation alleviates the burden of simultaneous correspondence inference and action adaptation, enabling robust transfer across diverse tasks. Our approach further integrates an online adaptive matching algorithm to dynamically establish reliable correspondences during execution. Empirical results on both RLBench and real-world manipulation tasks show that MatchingPolicy achieves strong few-shot performance, demonstrating consistent generalization across unseen object instances and categories.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
结合对应关系与图扩散策略的跨物体模仿学习操作。

### 2. 核心内容
针对上下文模仿学习在未见物体与新场景上泛化差的问题，本文提出 MatchingPolicy 框架，将演示与场景的对应匹配从策略学习中解耦。方法借助视觉基础模型提取稠密对应，并采用图扩散策略据此自适应调整机器人动作，同时引入在线自适应匹配算法动态建立可靠对应。实验表明该方法在跨物体、跨任务迁移上更为鲁棒，为对象级对应驱动的模仿学习操作提供了新思路。

### 3. 对应检索需求
Find work combining object centric representation learning and imitation learning for robot manipulation.

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=ddxq6ACoY3](https://openreview.net/forum?id=ddxq6ACoY3)
