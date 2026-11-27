---
title: "Learning Primitive Embodied World Models: Towards Scalable Robotic Learning"
title_zh: 学习原始具身世界模型：迈向可扩展的机器人学习
authors: "Qiao Sun, Liujia Yang, Wei Tang, Wei Huang, Kaixin Xu, Yongchao Chen, Mingyu Liu, Haoyi Zhu, Jiange Yang, Yating Wang, Yilun Chen, Xili Dai, Nanyang Ye, Qinying Gu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=W0AY49wWrb"
tags: ["query:humanoid-rl"]
score: 8.0
evidence: 面向可扩展机器人学习的原始动作具身世界模型
tldr: 针对视频生成式具身世界模型依赖大规模交互数据、长时程生成困难的问题，论文观察到具身数据多样性远超基本动作空间，提出原始具身世界模型PEWM，将视频生成限制在固定的短原始动作片段上。该范式旨在降低数据需求并提升语言与动作对齐粒度，从而支持更具可扩展性的机器人学习，为结构化世界模型提供了新的建模范式。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 视频生成式具身世界模型受限于大规模交互数据稀缺和长时程生成困难。
method: 提出PEWM，将视频生成限制在固定的短原始动作片段上，以结构化方式建模具身世界。
result: 摘要强调该范式可降低数据瓶颈并改善语言动作对齐，具体实验指标未展开。
conclusion: 为可扩展机器人学习提供了一种以原始动作为核心的世界模型构建思路。
---

## Abstract
While video-generation-based embodied world models have gained increasing
attention, their reliance on large-scale embodied interaction data remains a key
bottleneck. The scarcity, difficulty of collection, and high dimensionality of em-
bodied data fundamentally limit the alignment granularity between language and
actions and exacerbate the challenge of long-horizon video generation—hindering
generative models from achieving a "GPT moment" in the embodied domain. There
is a naive observation: the diversity of embodied data far exceeds the relatively
small space of possible primitive motions. Based on this insight, we propose a novel
paradigm for world modeling–Primitive Embodied World Models (PEWM). By
restricting video generation to fixed short horizons, our approach 1) enables fine-
grained alignment between linguistic concepts and visual representations of robotic
actions, 2) reduces learning complexity, 3) improves data efficiency in embodied
data collection, and 4) decreases inference latency. By equipping with a modular
Vision-Language Model (VLM) planner and a Start-Goal heatmap Guidance mech-
anism (SGG), PEWM further enables flexible closed-loop control and supports
compositional generalization of primitive-level policies over extended, complex
tasks. Our framework leverages the spatiotemporal vision priors in video mod-
els and the semantic awareness of VLMs to bridge the gap between fine-grained
physical interaction and high-level reasoning, paving the way toward scalable,
interpretable, and general-purpose embodied intelligence.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向可扩展机器人学习的原始动作具身世界模型。

### 2. 核心内容
针对视频生成式具身世界模型依赖大规模交互数据、长时程生成困难的问题，论文观察到具身数据多样性远超基本动作空间，提出原始具身世界模型PEWM，将视频生成限制在固定的短原始动作片段上。该范式旨在降低数据需求并提升语言与动作对齐粒度，从而支持更具可扩展性的机器人学习，为结构化世界模型提供了新的建模范式。

### 3. 对应检索需求
Find methods that use structured world models to improve sample efficiency in robotic reinforcement learning.

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=W0AY49wWrb](https://openreview.net/forum?id=W0AY49wWrb)
