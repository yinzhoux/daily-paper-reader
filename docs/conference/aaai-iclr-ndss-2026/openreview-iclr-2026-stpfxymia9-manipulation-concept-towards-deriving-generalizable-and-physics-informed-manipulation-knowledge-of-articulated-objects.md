---
title: "Manipulation Concept: Towards Deriving Generalizable and Physics-informed Manipulation Knowledge of Articulated Objects"
title_zh: 操作概念：面向关节物体可泛化物理知情操作知识的推导
authors: "Yixuan Jiang, Jiude Wei, Cewu Lu, Jianhua Sun"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=StpFxymia9"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 将物体结构与夹爪动作联系起来的解析式结构化操作表征
tldr: 针对夹爪式关节物体操作中忽视夹爪特性与物体结构交互的问题，本文提出 Manipulation Concept 这一解析式表征，将可操作部件（如立方体门、环形把手）与夹爪动作（推、提）形式化为参数化程序模板。方法把几何、语义与可执行动作相链接，从而支撑物理约束下的泛化操作。实验表明该表征可提升对未见关节物体的操作泛化与物理一致性，为结构化操作知识提供了可复用的表示基础。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有夹爪式关节物体操作忽视夹爪特性与物体结构之间的交互，缺乏可泛化的结构化操作知识。
method: 提出 Manipulation Concept 解析式表征，用参数化程序模板把可操作部件结构与夹爪动作链接起来。
result: 该表征将几何、语义与可执行动作统一，提升了对关节物体操作的泛化性与物理一致性。
conclusion: 结构化操作概念为机器人操作知识提供可复用、物理知情的表示形式。
---

## Abstract
Gripper-based articulated object manipulation requires robots to reason about both object structure and the physical constraints of grippers, yet prior work has paid little consideration to grippers’ unique characteristics and their interaction with object structures. To alleviate this gap, we introduce **Manipulation Concept**, a novel analytic representation that encodes gripper manipulation skills as parameterized program templates. Each concept formalizes the interaction between a specific actionable part featuring structure and semantic (*e.g.*, cuboid door, ring handle) and a gripper action (*e.g.*, push, lift), linking geometries and semantics with executable robot actions. Building on this representation, we develop an end-to-end framework that (i) leverages a vision-language model to select the most suitable concept for the actionable part, (ii) estimates geometric and affordance parameters to instantiate the selected concept and ground it in the physical world, and (iii) generates precise gripper-specific actions to complete the task. Extensive experiments in simulation and real world demonstrate that our method outperforms prior approaches in both accuracy and generalization, achieving stronger generalization across object categories, and reliable execution in manipulation tasks.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
将物体结构与夹爪动作联系起来的解析式结构化操作表征。

### 2. 核心内容
针对夹爪式关节物体操作中忽视夹爪特性与物体结构交互的问题，本文提出 Manipulation Concept 这一解析式表征，将可操作部件（如立方体门、环形把手）与夹爪动作（推、提）形式化为参数化程序模板。方法把几何、语义与可执行动作相链接，从而支撑物理约束下的泛化操作。实验表明该表征可提升对未见关节物体的操作泛化与物理一致性，为结构化操作知识提供了可复用的表示基础。

### 3. 对应检索需求
robotic manipulation policies that leverage structured representations and reinforcement learning。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=StpFxymia9](https://openreview.net/forum?id=StpFxymia9)
