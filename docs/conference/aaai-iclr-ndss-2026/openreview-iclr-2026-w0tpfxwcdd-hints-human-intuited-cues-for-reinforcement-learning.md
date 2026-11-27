---
title: "HINTs: Human-INTuited Cues for Reinforcement Learning"
title_zh: HINTs：面向强化学习的人类直觉线索
authors: "Bilha-Catherine Githinji, Julie Shah"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=W0tpFxWcdd"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 面向真实机器人连续控制的具身强化学习与人类线索
tldr: 针对真实机器人高维连续控制中强化学习样本需求大、部分可观测且难以直接迁移的问题，论文提出引入人类直觉线索的学习框架，以引导具身智能体更快建立从感知输入到动作的映射。该方法缓解合成数据或直接人类监督带来的分布偏移，目标是在真实机器人场景中提升学习效率与控制表现，为具身强化学习提供可迁移的线索注入思路。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 真实机器人高维连续控制下，具身强化学习样本需求大且存在部分可观测与分布偏移问题。
method: 提出引入人类直觉线索的新型学习框架，引导智能体建立感知输入到动作的映射。
result: 摘要未给出完整实验数据，但方法旨在降低真实机器人强化学习的经验需求与迁移难度。
conclusion: 为具身强化学习在真实机器人控制中高效利用人类线索提供了可行方向。
---

## Abstract
In real-world scenarios, robots can leverage embodied reinforcement learning (RL) agents to solve continuous control problems that are difficult to model under partial observability. Especially when the control inputs are high-dimensional, RL agents can require extensive experience to learn correct mappings from the input space to action space, a serious limitation given the lack of sufficiently large real-world robotics datasets. Recent work approaches this problem by training agents in synthetic data domains or bootstrapping learning with direct human supervision. They are often difficult to apply to the target domain due to large distribution shift between the training and deployment setting \citep{Zhao+20,ChenHu+22,Chae+22}.
    %
    We propose a novel learning framework, called Human-INTuited cues for RL, or \hints, in which agents quickly learn to solve tasks by leveraging human coaching. Our experiments in classic control, navigation, and locomotion reveal that \hints\ enables agents to learn more quickly than vision-only agents and to obtain strategies that apply to more challenging settings.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向真实机器人连续控制的具身强化学习与人类线索。

### 2. 核心内容
针对真实机器人高维连续控制中强化学习样本需求大、部分可观测且难以直接迁移的问题，论文提出引入人类直觉线索的学习框架，以引导具身智能体更快建立从感知输入到动作的映射。该方法缓解合成数据或直接人类监督带来的分布偏移，目标是在真实机器人场景中提升学习效率与控制表现，为具身强化学习提供可迁移的线索注入思路。

### 3. 对应检索需求
reinforcement learning methods for controlling embodied agents and humanoid robots。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=W0tpFxWcdd](https://openreview.net/forum?id=W0tpFxWcdd)
