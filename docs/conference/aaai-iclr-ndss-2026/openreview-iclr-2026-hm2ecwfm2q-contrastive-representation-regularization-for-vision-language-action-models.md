---
title: Contrastive Representation Regularization for Vision-Language-Action Models
title_zh: 面向视觉语言动作模型的对比表示正则化
authors: "Taeyoung Kim, Jimin Lee, Myungkyu Koo, Dongyoung Kim, Kyungmin Lee, Changyeon Kim, Younggyo Seo, Jinwoo Shin"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=hm2EcwFm2Q"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 对齐机器人状态的表示正则化用于操作控制
tldr: 视觉语言动作模型借助预训练视觉语言表示在机器人操作中表现优异，但其表示对控制动作与本体状态等机器人信号不敏感。本文提出机器人状态感知对比损失RS-CL，以状态间相对距离作为软监督，将表示与机器人本体状态对齐。该正则化弥补了视觉语言表示与机器人信号之间的鸿沟，并补充原有动作预测目标。工作提升了机器人操作中表示学习与控制信号的一致性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 视觉语言动作模型的表示对控制动作与本体状态等机器人信号不敏感。
method: 提出机器人状态感知对比损失，用状态相对距离软监督对齐表示与本体状态。
result: 该正则化弥合视觉语言表示与机器人信号的鸿沟，改善操作控制表示质量。
conclusion: 工作为机器人操作中的表示学习与控制信号对齐提供了简洁有效的方案。
---

## Abstract
Vision-Language-Action (VLA) models have shown its capabilities in robot manipulation by leveraging rich representations from pre-trained Vision-Language Models (VLMs).
However, their representations arguably remain suboptimal, lacking sensitivity to robotic signals such as control actions and proprioceptive states. 
To address the issue, we introduce Robot State-aware Contrastive Loss (RS-CL), a simple and effective representation regularization for VLA models, designed to bridge the gap between VLM representations and robotic signals.
In particular, RS-CL aligns the representations more closely with the robot's proprioceptive states, by using relative distances between the states as soft supervision.
Complementing the original action prediction objective, RS-CL effectively enhances control-relevant representation learning, while being lightweight and fully compatible with standard VLA training pipeline.
Our empirical results demonstrate that RS-CL substantially improves the manipulation performance of state-of-the-art VLA models;
it pushes the prior art from 30.8% to 41.5% on pick-and-place tasks in RoboCasa-Kitchen, through more accurate positioning during grasping and placing,
and boosts success rates from 45.0% to 58.3% on challenging real-robot manipulation tasks.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
对齐机器人状态的表示正则化用于操作控制。

### 2. 核心内容
视觉语言动作模型借助预训练视觉语言表示在机器人操作中表现优异，但其表示对控制动作与本体状态等机器人信号不敏感。本文提出机器人状态感知对比损失RS-CL，以状态间相对距离作为软监督，将表示与机器人本体状态对齐。该正则化弥补了视觉语言表示与机器人信号之间的鸿沟，并补充原有动作预测目标。工作提升了机器人操作中表示学习与控制信号的一致性。

### 3. 对应检索需求
representation learning for control, robotics, and embodied decision making。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=hm2EcwFm2Q](https://openreview.net/forum?id=hm2EcwFm2Q)
