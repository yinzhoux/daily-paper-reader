---
title: "Correspondence-Oriented Imitation Learning: Flexible Visuomotor Control with 3D Conditioning"
title_zh: 对应导向模仿学习：基于3D条件的灵活视觉运动控制
authors: "Yunhao Cao, Zubin Bhaumik, Jessie Jia, Xingyi He, Kuan Fang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=U6Efnba2i9"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 基于3D关键点任务表征的对应导向模仿学习
tldr: 针对视觉运动控制中任务表征僵化、难以适配不同用户意图的问题，本文提出对应导向模仿学习框架 COIL。方法用场景中物体关键点的预期运动来定义任务，支持可变的空间与时间粒度，并设计带时空注意力的条件策略将这种3D对应表征稳健地落地为动作。该框架能灵活融合多模态输入，提升了操作任务表征的通用性与动作生成可靠性。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有视觉运动控制的任务表征较僵化，难以适配不同空间与时间粒度的用户意图。
method: 提出 COIL，用物体关键点预期运动定义任务，并以时空注意力条件策略将3D对应落地为动作。
result: 该框架支持可变粒度的任务规格并稳健融合多模态输入，提升操作控制的通用性。
conclusion: 对应导向的3D任务表征为灵活可复用的操作模仿学习提供了新范式。
---

## Abstract
We introduce Correspondence-Oriented Imitation Learning(COIL), a conditional policy learning framework for visuomotor control with a flexible task representation in 3D. At the core of our approach, each task is defined by the intended motion of keypoints selected on objects in the scene. Instead of assuming a fixed number of keypoints or uniformly spaced time intervals, COIL supports task specifications with variable spatial and temporal granularity, adapting to different user intents and task requirements. To robustly ground this correspondence-oriented task representation into actions, we design a conditional policy with a spatio-temporal attention mechanism that effectively fuses information across multiple input modalities. The policy is trained via a scalable self-supervised pipeline using demonstrations collected in simulation, with correspondence labels automatically generated in hindsight. COIL generalizes across tasks, objects, and motion patterns, achieving superior performance compared to prior methods on real-world manipulation tasks under both sparse and dense specifications.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
基于3D关键点任务表征的对应导向模仿学习。

### 2. 核心内容
针对视觉运动控制中任务表征僵化、难以适配不同用户意图的问题，本文提出对应导向模仿学习框架 COIL。方法用场景中物体关键点的预期运动来定义任务，支持可变的空间与时间粒度，并设计带时空注意力的条件策略将这种3D对应表征稳健地落地为动作。该框架能灵活融合多模态输入，提升了操作任务表征的通用性与动作生成可靠性。

### 3. 对应检索需求
Find work combining object centric representation learning and imitation learning for robot manipulation.

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=U6Efnba2i9](https://openreview.net/forum?id=U6Efnba2i9)
