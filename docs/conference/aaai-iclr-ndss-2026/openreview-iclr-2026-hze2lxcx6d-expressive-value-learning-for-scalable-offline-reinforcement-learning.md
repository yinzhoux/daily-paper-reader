---
title: Expressive Value Learning for Scalable Offline Reinforcement Learning
title_zh: 面向可扩展离线强化学习的表达性价值学习
authors: "Nicolas Espinosa-Dice, Kianté Brantley, Wen Sun"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=Hze2lxCX6D"
tags: ["query:humanoid-rl"]
score: 4.0
evidence: 面向机器人决策的可扩展离线强化学习价值学习
tldr: 强化学习在机器人领域受限于可扩展性，离线强化学习虽能避免在线交互成本，但扩散与流匹配等表达性模型训练代价高。作者研究可扩展的离线强化学习价值学习问题，力图规避沿时间反向传播的高计算开销与策略蒸馏带来的累积误差。摘要未给出具体数值结果，但方法目标是在更大规模数据集与更大基策略上保持可训练性。该工作为机器人等复杂决策场景提供了更具可扩展性的离线强化学习路径。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 强化学习在机器人领域受限于可扩展性，离线强化学习虽可避免在线交互，但表达性生成模型训练代价高。
method: 研究可扩展的离线强化学习价值学习方法，规避沿时间反向传播与策略蒸馏带来的计算和误差问题。
result: 摘要未给出具体数值结果，方法旨在支持更大规模数据与更大基策略的训练。
conclusion: 为机器人等复杂决策场景提供更具可扩展性的离线强化学习价值学习路径。
---

## Abstract
Reinforcement learning (RL) is a powerful paradigm for learning to make sequences of decisions. However, RL has yet to be fully leveraged in robotics, principally due to its lack of scalability. Offline RL offers a promising avenue by training agents on  large, diverse datasets, avoiding the costly real-world interactions of online RL. Scaling offline RL to increasingly complex datasets requires expressive generative models such as diffusion and flow matching. However, existing methods typically depend on either backpropagation through time (BPTT), which is computationally prohibitive, or policy distillation, which introduces compounding errors and limits scalability to larger base policies. In this paper, we consider the question of how to develop a scalable offline RL approach without relying on distillation or backpropagation through time. We introduce Expressive Value Learning for Offline Reinforcement Learning (EVOR): a scalable offline RL approach that integrates both expressive policies and expressive value functions. EVOR learns an optimal, regularized $Q$-function via flow matching during training. At inference-time, EVOR performs inference-time policy extraction via rejection sampling against the expressive value function, enabling efficient optimization, regularization, and compute-scalable search without retraining. Empirically, we show that EVOR outperforms baselines on a diverse set of offline RL tasks, demonstrating the benefit of integrating expressive value learning into offline RL.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向机器人决策的可扩展离线强化学习价值学习。

### 2. 核心内容
强化学习在机器人领域受限于可扩展性，离线强化学习虽能避免在线交互成本，但扩散与流匹配等表达性模型训练代价高。作者研究可扩展的离线强化学习价值学习问题，力图规避沿时间反向传播的高计算开销与策略蒸馏带来的累积误差。摘要未给出具体数值结果，但方法目标是在更大规模数据集与更大基策略上保持可训练性。该工作为机器人等复杂决策场景提供了更具可扩展性的离线强化学习路径。

### 3. 对应检索需求
reinforcement learning methods for controlling embodied agents and humanoid robots。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=Hze2lxCX6D](https://openreview.net/forum?id=Hze2lxCX6D)
