---
title: One-shot Learning for Robot Manipulation through Egocentric Video Demonstration
title_zh: 通过第一视角视频示教实现机器人操作的一次性学习
authors: "Xiwen Dengxiong, Xueting Wang, Rui Li, Jiebo Luo, Dongfang Liu, Yunbo Zhang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=cz6SbHgGEn"
tags: ["query:humanoid-rl"]
score: 6.0
evidence: 第一视角视频模仿结合强化学习精化的机器人操作
tldr: 从第一视角视频示教学习机器人操作面临视角动态变化与环境不确定，现有单样本方法难以直接适用。作者提出由粗到细的方向性操作学习框架，先用集成动作预测模块生成粗略动作，再用基于强化学习的精化模块细调轨迹。实验表明机器人可仅凭单段第一视角视频示教习得操作技能，提升了真实场景的可部署性。该工作为示教稀缺条件下模仿学习与强化学习的结合提供了可行方案。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 从第一视角视频示教学习机器人操作面临动态视角与不确定环境，现有单样本方法难以适用。
method: 提出由粗到细的方向性操作学习框架，结合集成动作预测模块与基于强化学习的精化模块。
result: 机器人可仅凭单段第一视角视频示教习得操作技能，提升真实场景可部署性。
conclusion: 为示教稀缺条件下机器人模仿学习与强化学习的结合提供了可行方案。
---

## Abstract
Learning robot manipulation from egocentric video demonstrations is a challenging and promising direction for embodied intelligence, as it involves dynamic perspectives and uncertain environments. While existing methods have shown success in one-shot or few-shot learning from static videos, they are not applicable to egocentric video inputs, which significantly limits their scalability and real-world deployment. In this paper, we propose a novel coarse-to-fine directional manipulation learning framework that enables robots to acquire manipulation skills from a single egocentric video demonstration. Our method integrates an ensemble action prediction module for coarse action generation and a reinforcement learning-based refinement module for fine-grained, adaptive control. The ensemble module improves robustness by combining multiple diffusion policies, while the reinforcement module ensures accurate execution by refining motions based on real-time feedback. We evaluate our framework on three complex, multi-step manipulation tasks and demonstrate its superior performance over three state-of-the-art baselines in terms of both success rate and task robustness under one-shot egocentric settings.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
第一视角视频模仿结合强化学习精化的机器人操作。

### 2. 核心内容
从第一视角视频示教学习机器人操作面临视角动态变化与环境不确定，现有单样本方法难以直接适用。作者提出由粗到细的方向性操作学习框架，先用集成动作预测模块生成粗略动作，再用基于强化学习的精化模块细调轨迹。实验表明机器人可仅凭单段第一视角视频示教习得操作技能，提升了真实场景的可部署性。该工作为示教稀缺条件下模仿学习与强化学习的结合提供了可行方案。

### 3. 对应检索需求
Find work combining object centric representation learning and imitation learning for robot manipulation.

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=cz6SbHgGEn](https://openreview.net/forum?id=cz6SbHgGEn)
