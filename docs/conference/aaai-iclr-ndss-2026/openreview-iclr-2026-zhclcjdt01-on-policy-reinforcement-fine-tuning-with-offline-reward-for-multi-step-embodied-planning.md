---
title: On-policy Reinforcement Fine-tuning with Offline reward for Multi-step Embodied Planning
title_zh: 面向多步具身规划的离线奖励在线强化微调
authors: "Di Wu, Jiaxin Fan, Junzhe Zang, Guanbo Wang, Wei Yin, Wenhao Li, Bo Jin"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=ZhClCjdT01"
tags: ["query:humanoid-rl"]
score: 6.0
evidence: 面向具身规划智能体的在线强化微调
tldr: 具身规划要求智能体根据动态视觉观测和语言目标做出连贯的多步决策，而现有视觉语言模型在交互环境中表现欠佳。本文提出一种带离线奖励的在线强化微调框架，在保留强化微调泛化优势的同时缓解稀疏奖励与交互代价高的问题，并给出理论保证。在Embench交互式具身基准上，方法在域内与域外场景均显著优于基线。该工作为具身智能体的强化学习控制提供了高效可扩展的训练范式。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 视觉语言模型擅长静态感知，但在动态交互的具身规划中多步决策能力不足。
method: 提出带离线奖励的在线强化微调框架，兼顾泛化性与稀疏奖励、交互成本问题。
result: 在Embench基准的域内与域外场景中，方法显著超越现有基线。
conclusion: 该框架为具身智能体的强化学习训练提供了高效且具理论保证的方案。
---

## Abstract
Embodied planning requires agents to make coherent multi-step decisions based on dynamic visual observations and natural language goals. 
  While recent vision-language models (VLMs) excel at static perception tasks, they struggle in interactive environments.
  In this work, we introduce an on-policy reinforcement fine-tuning framework with offline rewards, that preserves the generalization benefits of RFT while addressing the challenges of sparse rewards and costly interaction, supported by solid theoretical guarantees.
  Our approach is evaluated on Embench, a recent benchmark for interactive embodied tasks, covering both in-domain and out-of-domain scenarios. 
  Experimental results show that our method significantly outperforms models of similar or larger scale, including GPT-4o-mini and 70B+ open-source baselines, and exhibits strong generalization to unseen environments. 
  This work highlights the potential of reinforcement-driven reasoning to advance multi-step planning in embodied AI.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向具身规划智能体的在线强化微调。

### 2. 核心内容
具身规划要求智能体根据动态视觉观测和语言目标做出连贯的多步决策，而现有视觉语言模型在交互环境中表现欠佳。本文提出一种带离线奖励的在线强化微调框架，在保留强化微调泛化优势的同时缓解稀疏奖励与交互代价高的问题，并给出理论保证。在Embench交互式具身基准上，方法在域内与域外场景均显著优于基线。该工作为具身智能体的强化学习控制提供了高效可扩展的训练范式。

### 3. 对应检索需求
reinforcement learning methods for controlling embodied agents and humanoid robots。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=ZhClCjdT01](https://openreview.net/forum?id=ZhClCjdT01)
