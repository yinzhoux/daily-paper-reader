---
title: "BFM-Zero: A Promptable Behavioral Foundation Model for Humanoid Control Using Unsupervised Reinforcement Learning"
title_zh: BFM-Zero：基于无监督强化学习的可提示人形控制行为基础模型
authors: "Yitang Li, Zhengyi Luo, Tonghe Zhang, Cunxi Dai, Anssi Kanervisto, Andrea Tirinzoni, Haoyang Weng, Kris Kitani, Mateusz Guzek, Ahmed Touati, Alessandro Lazaric, Matteo Pirotta, Guanya Shi"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=jkhl2oI0g5"
tags: ["query:humanoid-rl"]
score: 9.0
evidence: 用共享结构化隐表示的无监督强化学习实现真实人形全身控制
tldr: 人形机器人行为基础模型多局限于仿真角色或特定任务，缺乏可提示的通用策略。作者提出BFM-Zero，用无监督强化学习学习一个共享隐空间，将动作、目标与奖励嵌入同一表示，使单一策略无需重训练即可被提示执行多种下游任务。实验在真实Unitree G1人形机器人上实现了多样且鲁棒的全身体技能，并通过多种推理方式调用。该工作表明结构化隐表示可支撑可提示的人形全身控制基础模型。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有人形行为基础模型多局限于仿真角色或跟踪等特定任务，缺少可提示的通用全身策略。
method: 用无监督强化学习学习共享隐空间，把动作、目标与奖励嵌入同一表示，使单策略可被提示执行多任务。
result: 在真实Unitree G1人形机器人上实现多样且鲁棒的全身体技能，且无需重新训练。
conclusion: 表明结构化隐表示能够支撑可提示的人形全身控制基础模型走向真实部署。
---

## Abstract
Building Behavioral Foundation Models (BFMs) for humanoid robots has the potential to unify diverse control tasks under a single, promptable generalist policy. However, existing approaches are either exclusively deployed on simulated humanoid characters, or specialized to specific tasks such as tracking. We propose BFM-Zero, a framework that learns an effective shared latent representation that embeds motions, goals, and rewards into a common space, enabling a single policy to be prompted for multiple downstream tasks without retraining. This well-structured latent space in BFM-Zero enables versatile and robust whole-body skills on a Unitree G1 humanoid in the real world, via diverse inference methods, including zero-shot motion tracking, goal reaching, and reward inference, and few-shot optimization-based adaptation. Unlike prior on-policy reinforcement learning (RL) frameworks, BFM-Zero builds upon recent advancements in unsupervised RL and Forward-Backward (FB) models, which offer an objective-centric, explainable, and smooth latent representation of whole-body motions. We further extend BFM-Zero with critical reward shaping, domain randomization, and history-dependent asymmetric learning to bridge the sim-to-real gap. Those key design choices are quantitatively ablated in simulation. A first-of-its-kind model, BFM-Zero establishes a step toward scalable, promptable behavioral foundation models for whole-body humanoid control. Webpage:
https://lecar-lab.github.io/BFM-Zero/

---

## 论文详细总结（自动生成）

### 1. 检索相关性
用共享结构化隐表示的无监督强化学习实现真实人形全身控制。

### 2. 核心内容
人形机器人行为基础模型多局限于仿真角色或特定任务，缺乏可提示的通用策略。作者提出BFM-Zero，用无监督强化学习学习一个共享隐空间，将动作、目标与奖励嵌入同一表示，使单一策略无需重训练即可被提示执行多种下游任务。实验在真实Unitree G1人形机器人上实现了多样且鲁棒的全身体技能，并通过多种推理方式调用。该工作表明结构化隐表示可支撑可提示的人形全身控制基础模型。

### 3. 对应检索需求
reinforcement learning methods for controlling embodied agents and humanoid robots。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=jkhl2oI0g5](https://openreview.net/forum?id=jkhl2oI0g5)
