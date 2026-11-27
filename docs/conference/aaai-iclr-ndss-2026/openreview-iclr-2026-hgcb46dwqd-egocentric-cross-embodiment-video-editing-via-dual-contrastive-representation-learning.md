---
title: Egocentric Cross-Embodiment Video Editing via Dual Contrastive Representation Learning
title_zh: 通过双重对比表示学习的第一人称跨本体视频编辑
authors: "Zhiyuan Li, Wenyan Yang, Wenshuai Zhao, Yue Ma, Yuanpeng Tu, Pekka Marttinen, Joni Pajarinen"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=hGcb46DWQD"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 面向操作的任务与本体解耦表示学习
tldr: 从人类视频学习机器人操作可缓解数据瓶颈，但人与机器人之间的分布差异仍是关键挑战，现有方法常产生纠缠表示。本文提出跨本体视频编辑生成框架，通过双重对比目标将示范视频分解为正交的任务与本体潜空间，最小化空间间互信息并最大化空间内一致性。方法获得显式解耦的表示，提升跨本体适应性。该工作为机器人操作中结构化表示学习提供了新方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 从人类视频学习机器人操作时人与机器人的分布差异导致表示纠缠。
method: 提出跨本体视频编辑框架，用双重对比目标将任务与本体表示解耦到正交空间。
result: 方法获得显式解耦表示，提升跨本体适应性并缓解分布偏移。
conclusion: 该工作为机器人操作中结构化、解耦的表示学习提供了有效途径。
---

## Abstract
Learning robotic manipulation from human videos is a promising solution to the data bottleneck in robotics, but the distribution shift between humans and robots remains a critical challenge. Existing approaches often produce entangled representations, where task-relevant information is coupled with human-specific kinematics, limiting their adaptability. We propose a generative framework for cross-embodiment video editing that directly addresses this by learning explicitly disentangled task and embodiment representations. Our method factorizes a demonstration video into two orthogonal latent spaces by enforcing a dual contrastive objective: it minimizes mutual information between the spaces to ensure independence while maximizing intra-space consistency to create stable representations. A parameter-efficient adapter injects these latent codes into a frozen video diffusion model, enabling the synthesis of a coherent robot execution video from a single human demonstration, without requiring paired cross-embodiment data. Experiments show our approach generates temporally consistent and morphologically accurate robot demonstrations, offering a scalable solution to leverage internet-scale human video for robot learning.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向操作的任务与本体解耦表示学习。

### 2. 核心内容
从人类视频学习机器人操作可缓解数据瓶颈，但人与机器人之间的分布差异仍是关键挑战，现有方法常产生纠缠表示。本文提出跨本体视频编辑生成框架，通过双重对比目标将示范视频分解为正交的任务与本体潜空间，最小化空间间互信息并最大化空间内一致性。方法获得显式解耦的表示，提升跨本体适应性。该工作为机器人操作中结构化表示学习提供了新方案。

### 3. 对应检索需求
representation learning for control, robotics, and embodied decision making。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=hGcb46DWQD](https://openreview.net/forum?id=hGcb46DWQD)
