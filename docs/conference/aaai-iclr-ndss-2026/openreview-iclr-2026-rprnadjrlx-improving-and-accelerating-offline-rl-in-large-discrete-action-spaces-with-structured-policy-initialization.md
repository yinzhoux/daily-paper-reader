---
title: Improving and Accelerating Offline RL in Large Discrete Action Spaces with Structured Policy Initialization
title_zh: 通过结构化策略初始化改进并加速大离散动作空间离线强化学习
authors: "Matthew Landers, Taylor W. Killian, Thomas Hartvigsen, Afsaneh Doryab"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=rPrNaDJrLx"
tags: ["query:humanoid-rl"]
score: 6.0
evidence: 面向离线强化学习的结构化动作表示与策略初始化
tldr: 针对组合动作空间中离线强化学习需搜索指数级联合动作、现有方法难以兼顾动作协调与学习效率的问题，论文提出结构化策略初始化SPIN。该方法先预训练动作结构模型以捕捉有效动作流形，再冻结该表示并训练轻量策略头进行控制。两阶段设计旨在加速并稳定大规模离散动作空间中的离线RL，为结构化表示与策略学习结合提供了可迁移方案，尽管其场景并非机器人连续控制。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 大规模离散组合动作空间中，离线强化学习面临指数搜索与动作协调困难。
method: 提出SPIN，先预训练动作结构模型捕捉有效动作流形，再冻结表示训练策略头。
result: 摘要称该方法在挑战性离散动作基准上可改进并加速离线RL，具体数值未展开。
conclusion: 为结构化动作表示与离线强化学习结合提供了两阶段初始化框架。
---

## Abstract
Reinforcement learning in combinatorial action spaces requires searching over exponentially many joint actions to simultaneously select multiple sub-actions that form coherent combinations. Existing approaches either simplify policy learning by assuming independence across sub-actions, which often yields incoherent or invalid actions when coordination is required, or attempt to learn action structure and control jointly, which is slow and unstable. We introduce Structured Policy Initialization (SPIN), a two-stage framework that first pre-trains an Action Structure Model (ASM) to capture the manifold of valid actions, then freezes this representation and trains lightweight policy heads for control. On challenging DM Control benchmarks, SPIN improves average return by up to $39\%$ over the state of the art while reducing time to convergence by up to $12.8\times$.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向离线强化学习的结构化动作表示与策略初始化。

### 2. 核心内容
针对组合动作空间中离线强化学习需搜索指数级联合动作、现有方法难以兼顾动作协调与学习效率的问题，论文提出结构化策略初始化SPIN。该方法先预训练动作结构模型以捕捉有效动作流形，再冻结该表示并训练轻量策略头进行控制。两阶段设计旨在加速并稳定大规模离散动作空间中的离线RL，为结构化表示与策略学习结合提供了可迁移方案，尽管其场景并非机器人连续控制。

### 3. 对应检索需求
robotic manipulation policies that leverage structured representations and reinforcement learning。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=rPrNaDJrLx](https://openreview.net/forum?id=rPrNaDJrLx)
