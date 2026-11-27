---
title: "VLBiMan: Vision-Language Anchored One-Shot Demonstration Enables Generalizable Bimanual Robotic Manipulation"
title_zh: VLBiMan：视觉语言锚定的单次示范实现可泛化双臂机器人操作
authors: "Huayi Zhou, Kui Jia"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=he86smZzRk"
tags: ["query:humanoid-rl"]
score: 6.0
evidence: 面向双臂操作的单次示范模仿学习
tldr: 双臂操作需要从极少人类输入中高效学习并适应真实环境的不确定性，但模仿策略需大量示范而模块化方法缺乏灵活性。本文提出VLBiMan，通过任务感知分解从单个人类示例中提取可复用技能，保留不变基元并用视觉语言对齐动态调整可变部分。该机制可化解背景变化与物体移动带来的场景歧义，实现可泛化的双臂操作。工作展示了单次示范驱动的高效机器人模仿学习路径。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 双臂操作面临示范数据需求大与动态场景灵活性不足的两难困境。
method: 提出从单个人类示范中做任务感知分解，用视觉语言对齐动态调整可复用技能。
result: 方法能化解背景变化与物体重定位带来的歧义，实现可泛化双臂操作。
conclusion: 该框架展示了极少示范下高效且可泛化的机器人模仿学习能力。
---

## Abstract
Achieving generalizable bimanual manipulation requires systems that can learn efficiently from minimal human input while adapting to real-world uncertainties and diverse embodiments. Existing approaches face a dilemma: imitation policy learning demands extensive demonstrations to cover task variations, while modular methods often lack flexibility in dynamic scenes. We introduce VLBiMan, a framework that derives reusable skills from a single human example through task-aware decomposition, preserving invariant primitives as anchors while dynamically adapting adjustable components via vision-language grounding. This adaptation mechanism resolves scene ambiguities caused by background changes, object repositioning, or visual clutter without policy retraining, leveraging semantic parsing and geometric feasibility constraints. Moreover, the system inherits human-like hybrid control capabilities, enabling mixed synchronous and asynchronous use of both arms. Extensive experiments validate VLBiMan across tool-use and multi-object tasks, demonstrating: (1) a drastic reduction in demonstration requirements compared to imitation baselines, (2) compositional generalization through atomic skill splicing for long-horizon tasks, (3) robustness to novel but semantically similar objects and external disturbances, and (4) strong cross-embodiment transfer, showing that skills learned from human demonstrations can be instantiated on different robotic platforms without retraining. By bridging human priors with vision-language anchored adaptation, our work takes a step toward practical and versatile dual-arm manipulation in unstructured settings.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向双臂操作的单次示范模仿学习。

### 2. 核心内容
双臂操作需要从极少人类输入中高效学习并适应真实环境的不确定性，但模仿策略需大量示范而模块化方法缺乏灵活性。本文提出VLBiMan，通过任务感知分解从单个人类示例中提取可复用技能，保留不变基元并用视觉语言对齐动态调整可变部分。该机制可化解背景变化与物体移动带来的场景歧义，实现可泛化的双臂操作。工作展示了单次示范驱动的高效机器人模仿学习路径。

### 3. 对应检索需求
Find work combining object centric representation learning and imitation learning for robot manipulation.

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=he86smZzRk](https://openreview.net/forum?id=he86smZzRk)
