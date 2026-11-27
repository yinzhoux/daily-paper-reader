---
title: Masked Generative Policy for Robotic Control
title_zh: 用于机器人控制的掩码生成策略
authors: "Lipeng Zhuang, Shiyu Fan, Florent P. Audonnet, Yingdong Ru, Edmond S. L. Ho, Gerardo Aragon-Camarasa, Paul Henderson"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=KFu4p3pd11"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 耦合视觉感知与离散动作生成的视觉运动模仿策略
tldr: 针对复杂非马尔可夫机器人任务中视觉运动策略难以兼顾全局一致预测与自适应执行的问题，本文提出掩码生成策略MGP。该方法将动作表示为离散token，用条件掩码Transformer并行生成并快速精修低置信度token，并给出MGP-Short与MGP-Long两种采样范式。在150个机器人操作任务上的实验表明，MGP-Long能够在长时程任务上实现可靠控制，为具身智能体中感知与动作的耦合建模提供了新思路。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 视觉运动模仿学习在复杂长时程非马尔可夫任务中难以兼顾全局一致性与自适应执行。
method: 将动作离散化为token，用条件掩码Transformer并行生成并精修低置信度动作token。
result: 在150个机器人操作任务上验证，MGP-Long在复杂非马尔可夫任务中实现可靠控制。
conclusion: 离散动作token的掩码生成范式可有效提升视觉运动策略的表达与执行能力。
---

## Abstract
We present Masked Generative Policy (MGP), a novel framework for visuomotor imitation learning. We represent actions as discrete tokens, and train a conditional masked transformer that generates tokens in parallel and then rapidly refines only low-confidence tokens. We further propose two new sampling paradigms: MGP-Short, which performs parallel masked generation with score-based refinement for Markovian tasks, and MGP-Long, which predicts full trajectories in a single pass and dynamically refines low-confidence action tokens based on new observations. With globally coherent prediction and robust adaptive execution capabilities, MGP-Long enables reliable control on complex and non-Markovian tasks that prior methods struggle with. Extensive evaluations on 150 robotic manipulation tasks spanning the Meta-World and LIBERO benchmarks show that MGP achieves both rapid inference and superior success rates compared to state-of-the-art diffusion and autoregressive policies. Specifically, MGP increases the average success rate by 9\% across 150 tasks while cutting per-sequence inference time by up to 35×. It further improves the average success rate by 60\% in dynamic and missing-observation environments, and solves two non-Markovian scenarios where other state-of-the-art methods fail.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
耦合视觉感知与离散动作生成的视觉运动模仿策略。

### 2. 核心内容
针对复杂非马尔可夫机器人任务中视觉运动策略难以兼顾全局一致预测与自适应执行的问题，本文提出掩码生成策略MGP。该方法将动作表示为离散token，用条件掩码Transformer并行生成并快速精修低置信度token，并给出MGP-Short与MGP-Long两种采样范式。在150个机器人操作任务上的实验表明，MGP-Long能够在长时程任务上实现可靠控制，为具身智能体中感知与动作的耦合建模提供了新思路。

### 3. 对应检索需求
embodied learning agents that couple perception, representation, and action。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=KFu4p3pd11](https://openreview.net/forum?id=KFu4p3pd11)
