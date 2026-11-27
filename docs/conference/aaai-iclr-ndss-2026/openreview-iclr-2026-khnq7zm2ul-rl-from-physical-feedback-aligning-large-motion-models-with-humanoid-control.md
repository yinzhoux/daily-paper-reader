---
title: "RL from Physical Feedback: Aligning Large Motion Models with Humanoid Control"
title_zh: 基于物理反馈的强化学习：将大运动模型与人形控制对齐
authors: "Junpeng Yue, Zepeng Wang, Jiangxing Wang, Yuxuan Wang, Ziluo Ding, Sipeng Zheng, Xinrun Xu, Yu Zhang, Bin Cao, Zongqing Lu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=KhNq7zm2UL"
tags: ["query:humanoid-rl"]
score: 8.0
evidence: 基于物理反馈的强化学习用于人形机器人控制
tldr: 针对文本驱动生成的人体运动常动力学不可行、难以被人形机器人执行的问题，本文提出基于物理反馈的强化学习框架 RLPF。方法在物理仿真中用运动跟踪策略评估动作可行性，并据此生成奖励来微调运动生成器，从而将语言到运动的生成与人形执行对齐。实验表明生成动作的物理可行性与可执行性显著提升，弥合了运动生成与人形控制之间的鸿沟。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 文本驱动的人体运动生成常产生运动学或物理不可行的动作，难以部署到真实人形机器人。
method: 提出 RLPF 框架，用运动跟踪策略在仿真中评估可行性并生成奖励来微调运动生成器。
result: 生成运动的物理可行性和可执行性得到提升，更好地适配人形机器人控制。
conclusion: 将物理反馈强化学习引入运动生成，可有效对齐语言生成与人形执行。
---

## Abstract
This paper focuses on a critical challenge in robotics: translating text-driven generated human motions into executable actions for humanoid robots.
While existing text-to-motion generation methods achieve semantic alignment between language and motion, they often produce kinematically or physically infeasible motions unsuitable for real-world deployment.
To bridge the gap between motion generation and humanoid execution, we propose \textbf{Reinforcement Learning from Physical Feedback (RLPF)}, a novel framework that integrates physics-aware motion evaluation with text-conditioned motion generation.
RLPF employs a motion tracking policy to assess feasibility in a physics simulator, generating rewards for fine-tuning the motion generator.
Furthermore, RLPF introduces an alignment verification module to preserve semantic alignment to text instructions.
This joint optimization ensures both physical feasibility and instruction alignment.
Extensive experiments show that RLPF greatly outperforms baseline methods in generating physically feasible motions while maintaining semantic alignment with text instruction, enabling successful deployment on real humanoid robots.
More visualizations are available at \href{https://anonymous.4open.science/r/RLPF/}{https://anonymous.4open.science/r/RLPF/}.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
基于物理反馈的强化学习用于人形机器人控制。

### 2. 核心内容
针对文本驱动生成的人体运动常动力学不可行、难以被人形机器人执行的问题，本文提出基于物理反馈的强化学习框架 RLPF。方法在物理仿真中用运动跟踪策略评估动作可行性，并据此生成奖励来微调运动生成器，从而将语言到运动的生成与人形执行对齐。实验表明生成动作的物理可行性与可执行性显著提升，弥合了运动生成与人形控制之间的鸿沟。

### 3. 对应检索需求
reinforcement learning methods for controlling embodied agents and humanoid robots。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=KhNq7zm2UL](https://openreview.net/forum?id=KhNq7zm2UL)
