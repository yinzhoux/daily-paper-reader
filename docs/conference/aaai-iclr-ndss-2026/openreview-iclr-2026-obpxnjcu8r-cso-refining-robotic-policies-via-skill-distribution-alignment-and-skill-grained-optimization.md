---
title: "CSO: Refining Robotic Policies via Skill Distribution Alignment and Skill-Grained Optimization"
title_zh: CSO：通过技能分布对齐与技能粒度优化精炼机器人策略
authors: "Zhiyuan Xiang, Xiang Deng, Jianye HAO, Weili Guan, Liqiang Nie"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=oBpxNjcu8R"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 基于技能的结构化动作表征并用强化学习精炼
tldr: 用VQ-VAE将连续动作离散为技能已成为机器人操作的有效范式，但量化误差导致先验训练分布次优、性能下降。作者提出级联技能优化CSO两阶段后训练框架：先用拒绝采样监督微调校正初始策略分布，再以技能粒度优化进行强化学习精炼。该设计缓解编码器更新不稳定与重要性采样粒度困境。工作体现了结构化技能表征与强化学习结合的思路。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 技能离散化的量化误差使先验训练分布次优，直接强化学习精炼又面临不稳定问题。
method: 提出CSO两阶段后训练框架，结合拒绝采样监督微调与技能粒度优化的强化学习精炼。
result: 缓解编码器更新不稳定与重要性采样粒度困境，稳定提升操作策略性能。
conclusion: 表明结构化技能表征配合强化学习精炼可有效提升机器人操作策略。
---

## Abstract
Discretizing continuous actions into skills using methods like VQ-VAE has emerged as a powerful paradigm for robotic manipulation.
However, the quantization errors in discretizing continuous actions yield a suboptimal training distribution for the prior, degrading its performance.
While reinforcement learning offers a path for refinement, its direct application is challenging, suffering from unstable encoder updates and a granularity dilemma in importance sampling.
To address these challenges, we introduce Cascaded Skills Optimization (CSO), a two-stage post-training framework.
First, to rectify the initial policy's suboptimal distribution, CSO employs Rejection-Sampling Supervised Fine-tuning to align the model's observation-to-skill mapping with the distribution of successful online trajectories via supervised fine-tuning.
Second, to resolve the granularity dilemma, CSO introduces Skills Policy Optimization, which computes an independent, clipped importance ratio for each skill, enabling more stable and efficient updates.
Our post-training strategy delivers highly competitive performance on challenging benchmarks like LIBERO and MetaWorld, with its effectiveness further validated on a physical robot.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
基于技能的结构化动作表征并用强化学习精炼。

### 2. 核心内容
用VQ-VAE将连续动作离散为技能已成为机器人操作的有效范式，但量化误差导致先验训练分布次优、性能下降。作者提出级联技能优化CSO两阶段后训练框架：先用拒绝采样监督微调校正初始策略分布，再以技能粒度优化进行强化学习精炼。该设计缓解编码器更新不稳定与重要性采样粒度困境。工作体现了结构化技能表征与强化学习结合的思路。

### 3. 对应检索需求
robotic manipulation policies that leverage structured representations and reinforcement learning。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=oBpxNjcu8R](https://openreview.net/forum?id=oBpxNjcu8R)
