---
title: Training Active Vision Reasoners with Multi-Turn Reinforcement Learning
title_zh: 使用多轮强化学习训练主动视觉推理器
authors: "Yifan Liu, Gabriel Herbert Sarch, Ayush Jain, Naitik Khandelwal, Katerina Fragkiadaki"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=wYgtymmOFC"
tags: ["query:humanoid-rl"]
score: 4.0
evidence: 用强化学习训练视觉语言智能体决定观察位置，耦合感知与行动
tldr: 针对视觉语言模型在三维环境中难以决定观察位置的问题，论文提出AViRRL多轮强化学习方法，先用树搜索引导的数据生成预热主动视觉推理策略，再通过多轮强化学习训练模型习得探索策略。实验显示模型在主动视觉问答与目标定位任务上性能提升，表明基于推理的强化学习可有效扩展到主动感知场景，为具身视觉决策提供新思路。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 视觉语言模型在三维主动视觉中难以决定观察位置，现有基于思维链的强化学习仅适用于静态图像输入。
method: 提出AViRRL多轮强化学习方法，结合树搜索引导的数据生成对视觉语言模型进行主动视觉推理策略的预热训练。
result: 实验表明该方法使模型习得主动探索的推理策略，在需要主动观察的视觉问答与目标定位任务上取得提升。
conclusion: 该工作将多轮强化学习引入主动视觉推理，为具身感知与决策结合的模型训练提供了可行范式。
---

## Abstract
Vision-Language Models (VLMs) face a critical challenge in active vision: determining where to look in 3D environments to answer questions or locate objects. While reinforcement learning (RL) over chains of thought has boosted performance in visual tasks with static inputs like passive image understanding, extending this reasoning-based approach to active vision remains an open challenge. We introduce AViRRL—Active Visual Reasoning with Reinforcement Learning—a multi-turn reinforcement learning approach to train vision-language models to acquire reasoning strategies for active visual exploration. Our approach combines two key components: (1) a tree-search-guided data generation method for warm starting active vision reasoning strategies in VLMs, and (2) online multi-turn reinforcement learning that optimizes full thought–action trajectories based on task success. On TinyNav, a benchmark for visual search of small objects in realistic 3D environments, we show that our method significantly outperforms both visual navigation prompting methods and single-step reinforcement learning with behavior cloning rewards. Compared to baselines, our agent exhibits more effective active vision behaviors, including exploration efficiency and reasoning aligned with visual state. Our work shows that reinforcement learning on thought-action trajectories enables VLMs to develop active visual reasoning, shifting from passive perception to autonomous, goal-directed 3D exploration.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
用强化学习训练视觉语言智能体决定观察位置，耦合感知与行动。

### 2. 核心内容
针对视觉语言模型在三维环境中难以决定观察位置的问题，论文提出AViRRL多轮强化学习方法，先用树搜索引导的数据生成预热主动视觉推理策略，再通过多轮强化学习训练模型习得探索策略。实验显示模型在主动视觉问答与目标定位任务上性能提升，表明基于推理的强化学习可有效扩展到主动感知场景，为具身视觉决策提供新思路。

### 3. 对应检索需求
embodied learning agents that couple perception, representation, and action。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=wYgtymmOFC](https://openreview.net/forum?id=wYgtymmOFC)
