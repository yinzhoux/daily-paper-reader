---
title: "Learning Across the Noise Spectrum: An Approach to Reinforcement Learning with Asynchronous Signals"
title_zh: 跨噪声频谱学习：一种异步信号强化学习方法
authors: "Stefano Rando, Masashi Okada"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=Id1YBclGbz"
tags: ["query:humanoid-rl"]
score: 6.0
evidence: 面向真实机器人异步传感器信号的强化学习
tldr: 针对真实机器人传感器更新频率不同、强化学习通常假设完整同步观测的问题，论文将异步环境建模为噪声参数化POMDP族，提出跨噪声频谱学习LANS，在训练中让智能体经历多种异步噪声状态。方法基于SAC与循环神经网络，促使策略适应不同信号延迟与缺失模式。该工作提升了强化学习在真实机器人异步感知条件下的鲁棒性，为部分可观测具身控制提供了训练策略。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 真实机器人传感器异步更新，而常规强化学习假设每步获得完整同步观测。
method: 将异步环境建模为噪声参数化POMDP，并用SAC与RNN在多种异步噪声状态下训练。
result: 摘要强调通过采样不同异步率增强策略适应能力，具体实验数值未给出。
conclusion: 为真实机器人部分可观测强化学习提供了一种面向异步信号的鲁棒训练思路。
---

## Abstract
Reinforcement learning (RL) frameworks assume agents receive complete observation vectors at each timestep. However, real-world robotic systems typically operate in environments with asynchronous signals, i.e. sensors that update at different frequencies. We model \textbf{asynchronous environments} as an instance of a noise-parameterized family of partially observable Markov decision processes (POMDPs). Our primary contribution, **Learning Across the Noise Spectrum (LANS)**, is a novel strategy that exposes the agent to multiple simulated noise regimes during training, implemented using Soft Actor-Critic (SAC) with recurrent neural networks (RNNs). By sampling different asynchronicity rates, we encourage the development of robust estimators. We prove that LANS acts a _time-aware_ regularization term, equivalent to a Jacobian penalty along time-sensitive directions. Experiments on MuJoCo environments with simulated asynchronicity demonstrate that LANS outperforms alternative methods on a variety of tasks—up to a factor of $>1.5\times$ in some instances—offering a solution for robotic systems that must operate with imperfect sensory information.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向真实机器人异步传感器信号的强化学习。

### 2. 核心内容
针对真实机器人传感器更新频率不同、强化学习通常假设完整同步观测的问题，论文将异步环境建模为噪声参数化POMDP族，提出跨噪声频谱学习LANS，在训练中让智能体经历多种异步噪声状态。方法基于SAC与循环神经网络，促使策略适应不同信号延迟与缺失模式。该工作提升了强化学习在真实机器人异步感知条件下的鲁棒性，为部分可观测具身控制提供了训练策略。

### 3. 对应检索需求
reinforcement learning methods for controlling embodied agents and humanoid robots。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=Id1YBclGbz](https://openreview.net/forum?id=Id1YBclGbz)
