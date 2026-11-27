---
title: "ReLAM: Learning Anticipation Model for Rewarding Visual Robotic Manipulation"
title_zh: ReLAM：为视觉机器人操作学习预期模型以生成奖励
authors: "Nan Tang, Jing-Cheng Pang, Guanlin Li, Chao Qian, Yang Yu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=vBFVaVf8aj"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 关键点结构化奖励与预期模型用于视觉机器人操作强化学习
tldr: 视觉强化学习用于机器人操作时奖励设计是主要瓶颈，而真实场景往往无法获得精确的目标位置信息。作者提出ReLAM，先从图像中提取关键点以隐式推断空间距离，再学习一个充当规划器的预期模型，从无动作视频示教中自动生成稠密且结构化的奖励。实验显示该方法能在缺乏位置真值的视觉操作任务中提供有效奖励信号。其意义在于用结构化感知与预期建模替代人工奖励工程，提升视觉机器人强化学习的可扩展性。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 视觉强化学习做机器人操作时奖励设计困难，真实场景难以获得精确的目标位置信息。
method: 通过图像关键点隐式推断空间距离，并学习充当规划器的预期模型，从无动作视频中生成稠密结构化奖励。
result: 在视觉操作任务中提供稠密结构化奖励，缓解了奖励稀疏与位置信息缺失问题。
conclusion: 表明以结构化关键点与预期模型自动构造奖励，可提升视觉机器人强化学习的可扩展性。
---

## Abstract
Reward design remains a critical bottleneck in visual reinforcement learning (RL) for robotic manipulation. In simulated environments, rewards are conventionally designed based on the distance to a target position. However, such precise positional information is often unavailable in real-world visual settings due to sensory and perceptual limitations. In this study, we propose a method that implicitly infers spatial distances through keypoints extracted from images. Building on this, we introduce Reward Learning with Anticipation Model (ReLAM), a novel framework that automatically generates dense, structured rewards from action-free video demonstrations. ReLAM first learns an anticipation model that serves as a planner and proposes intermediate keypoint-based subgoals on the optimal path to the final goal, creating a structured learning curriculum directly aligned with the task's geometric objectives. Based on the anticipated subgoals, a continuous reward signal is provided to train a low-level, goal-conditioned policy under the hierarchical reinforcement learning (HRL) framework with provable sub-optimality bound. Extensive experiments on complex, long-horizon manipulation tasks show that ReLAM significantly accelerates learning and achieves superior performance compared to state-of-the-art methods.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
关键点结构化奖励与预期模型用于视觉机器人操作强化学习。

### 2. 核心内容
视觉强化学习用于机器人操作时奖励设计是主要瓶颈，而真实场景往往无法获得精确的目标位置信息。作者提出ReLAM，先从图像中提取关键点以隐式推断空间距离，再学习一个充当规划器的预期模型，从无动作视频示教中自动生成稠密且结构化的奖励。实验显示该方法能在缺乏位置真值的视觉操作任务中提供有效奖励信号。其意义在于用结构化感知与预期建模替代人工奖励工程，提升视觉机器人强化学习的可扩展性。

### 3. 对应检索需求
robotic manipulation policies that leverage structured representations and reinforcement learning。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=vBFVaVf8aj](https://openreview.net/forum?id=vBFVaVf8aj)
