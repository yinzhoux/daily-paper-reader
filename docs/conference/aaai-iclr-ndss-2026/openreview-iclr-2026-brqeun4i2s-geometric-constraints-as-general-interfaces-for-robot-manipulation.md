---
title: Geometric Constraints as General Interfaces for Robot Manipulation
title_zh: 几何约束作为机器人操作的通用接口
authors: "Weiliang Tang, Jia-Hui Pan, Yun-Hui Liu, Masayoshi Tomizuka, Li Erran Li, Chi-Wing Fu, Mingyu Ding"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=brqEUN4i2s"
tags: ["query:humanoid-rl"]
score: 6.0
evidence: 符号化几何约束表示被翻译为机器人操作动作
tldr: 针对通用机器人操作难以泛化到新任务与新物体、视觉-语言-动作模型依赖大规模训练的问题，论文提出GeoManip，用符号语言表示物体部件间的几何约束，并借助大模型生成约束后翻译为底层动作实现免训练操作。实验表明该方法在多样甚至未见任务与物体上提升泛化能力且无需额外训练，说明几何约束可作为连接语言指令与机器人执行的通用接口。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 通用机器人操作难以泛化到新任务与新物体，视觉-语言-动作模型又依赖大规模训练。
method: 提出GeoManip，用符号语言表示物体部件间的几何约束，并由大模型生成约束再翻译为底层动作，实现免训练操作。
result: 实验表明该方法在多样甚至未见任务与物体上提升泛化能力，无需额外训练。
conclusion: 该工作证明几何约束可作为通用接口，连接语言指令与机器人执行。
---

## Abstract
We present GeoManip, a framework to enable generalist robots to leverage essential geometric constraints derived from object-part relations for robot manipulation. For example, cutting a carrot typically requires the knife’s blade to be perpendicular to the carrot’s medial axis. By capturing geometric constraints through symbolic language representations and translating them into low-level actions, GeoManip bridges the gap between natural language and robotic execution, boosting the generalizability across diverse, even unseen tasks, objects, and scenarios. Beyond vision-language-action models that require extensive training, GeoManip operates training-free by leveraging large foundational models: a constraint generator to predict stage-specific geometric constraints and a geometry parser to locate the involved object parts. A solver then optimizes trajectories for the inferred constraints from the task descriptions and scenes. Further, GeoManip learns in-context and provides five appealing human-robot interaction features: on-the-fly policy adaptation, learning from human demonstrations, learning from failure cases, long-horizon action planning, and efficient data collection for imitation learning. Extensive evaluations on both simulations and real-world scenarios demonstrate GeoManip’s state-of-the-art performance, with superior out-of-distribution generalization while avoiding costly model training.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
符号化几何约束表示被翻译为机器人操作动作。

### 2. 核心内容
针对通用机器人操作难以泛化到新任务与新物体、视觉-语言-动作模型依赖大规模训练的问题，论文提出GeoManip，用符号语言表示物体部件间的几何约束，并借助大模型生成约束后翻译为底层动作实现免训练操作。实验表明该方法在多样甚至未见任务与物体上提升泛化能力且无需额外训练，说明几何约束可作为连接语言指令与机器人执行的通用接口。

### 3. 对应检索需求
robotic manipulation policies that leverage structured representations and reinforcement learning。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=brqEUN4i2s](https://openreview.net/forum?id=brqEUN4i2s)
