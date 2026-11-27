---
title: Flow Policy Gradients for Legged Robots
title_zh: 面向足式机器人的流策略梯度
authors: "Brent Yi, Hongsuk Choi, Himanshu Gaurav Singh, Xiaoyu Huang, Takara E. Truong, Carmelo Sferrazza, Yi Ma, Yan Duan, Pieter Abbeel, Guanya Shi, Karen Liu, Angjoo Kanazawa"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=BA6n0nmagi"
tags: ["query:humanoid-rl"]
score: 8.0
evidence: 可部署于真实人形机器人的在线强化学习人形运动跟踪
tldr: 针对基于流的策略优化在困难连续控制任务中易发生策略崩溃的问题，本文提出 FPO++，通过降低梯度方差和正则化熵等设计改进在线强化学习算法。方法成功训练出用于足式运动与人形运动跟踪的流策略，能够稳定学习并刻画动作间相关性。实验显示该算法训练稳定，并可部署到真实人形机器人上，扩展了流策略强化学习在机器人控制中的适用范围。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 基于流的策略优化在较难连续控制任务中易出现策略崩溃，限制其在机器人控制中的应用。
method: 提出 FPO++，通过降低梯度方差与正则化熵等设计改进流策略在线强化学习算法。
result: FPO++ 训练稳定，可用于足式运动与人形运动跟踪，并能部署到真实人形机器人。
conclusion: 改进后的流策略梯度为人形等连续控制任务提供了稳定可部署的强化学习方法。
---

## Abstract
We study robot control with flow policy optimization (FPO), an online reinforcement learning algorithm for flow-based action distributions. We demonstrate how flow policy optimization can succeed for more difficult continuous control tasks than shown in prior work, using a set of design choices that reduce gradient variance and regularize entropy. We show that these design choices mitigate policy collapse challenges faced by the original FPO algorithm and use the resulting algorithm, FPO++, to train flow policies for legged robot locomotion and humanoid motion tracking. We find that FPO++ is stable to train, interpretably models cross-action correlations, and can be deployed to real humanoid robots.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
可部署于真实人形机器人的在线强化学习人形运动跟踪。

### 2. 核心内容
针对基于流的策略优化在困难连续控制任务中易发生策略崩溃的问题，本文提出 FPO++，通过降低梯度方差和正则化熵等设计改进在线强化学习算法。方法成功训练出用于足式运动与人形运动跟踪的流策略，能够稳定学习并刻画动作间相关性。实验显示该算法训练稳定，并可部署到真实人形机器人上，扩展了流策略强化学习在机器人控制中的适用范围。

### 3. 对应检索需求
reinforcement learning methods for controlling embodied agents and humanoid robots。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=BA6n0nmagi](https://openreview.net/forum?id=BA6n0nmagi)
