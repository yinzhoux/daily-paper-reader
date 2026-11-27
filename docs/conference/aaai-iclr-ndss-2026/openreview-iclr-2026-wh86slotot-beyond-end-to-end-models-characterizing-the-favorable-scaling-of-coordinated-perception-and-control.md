---
title: "Beyond End-to-End Models: Characterizing the Favorable Scaling of Coordinated Perception and Control"
title_zh: 超越端到端模型：刻画感知与控制协调架构的有利扩展性
authors: "Jiayue Jin, Chishui Chen, Lang Qian, jingnan cai, Liang Song"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=Wh86SLotOT"
tags: ["query:humanoid-rl"]
score: 6.0
evidence: 具身智能体中解耦感知与控制
tldr: 端到端模型直接映射原始感知到控制，是具身智能体的主流范式，但其紧耦合导致随规模与环境复杂度上升计算与样本效率急剧下降。本文系统刻画一种解耦感知与控制的协调架构的缩放规律，其中感知与决策由不同智能体通过闭环交互完成。研究揭示了该架构更有利的扩展特性。工作为具身智能体中感知、表示与动作的协同设计提供了新视角。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 端到端具身模型紧耦合导致计算与样本效率随规模增长而恶化。
method: 系统刻画解耦感知与控制的协调架构的缩放规律，感知与决策由不同智能体闭环交互。
result: 研究表明该解耦架构具有比端到端更有利的扩展特性。
conclusion: 工作为具身智能体感知与控制的协同架构设计提供了新依据。
---

## Abstract
End-to-end models have become a dominant paradigm for learning in embodied agents, directly mapping raw sensory inputs to control outputs. However, their tightly coupled nature often leads to unfavorable scaling properties: as model size and environmental complexity increase, their computational and sample efficiency drastically deteriorates, posing a barrier to sustainable, long-term deployments in the real world. In this work, we move beyond the end-to-end approach and systematically characterize the scaling laws of an alternative paradigm: a coordinated architecture that decouples perception and control. In this architecture, perception and decision-making are handled by distinct agents that interact through a closed-loop feedback mechanism, where task-level feedback from control agents continuously guides the online evolutive learning of the perception modules. We conduct the first empirical study that investigates the computational scaling of these two paradigms across two critical dimensions: increasing model parameter scale and escalating environmental complexity. Our experiments show that the coordinated perception and control architecture achieves nearly linear or sub-linear growth (scaling exponents $\alpha \approx 1.11$ for parameters and $\delta \approx 0.95$ for complexity), while end-to-end models exhibit super-linear or exponential growth ($\alpha \approx 1.27$, $\delta \approx 2.70$). These results demonstrate that coordinated perception and control offers a fundamentally more scalable and robust design, providing practical guidance for building next-generation embodied AI systems that are both adaptive and computationally efficient.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
具身智能体中解耦感知与控制。

### 2. 核心内容
端到端模型直接映射原始感知到控制，是具身智能体的主流范式，但其紧耦合导致随规模与环境复杂度上升计算与样本效率急剧下降。本文系统刻画一种解耦感知与控制的协调架构的缩放规律，其中感知与决策由不同智能体通过闭环交互完成。研究揭示了该架构更有利的扩展特性。工作为具身智能体中感知、表示与动作的协同设计提供了新视角。

### 3. 对应检索需求
embodied learning agents that couple perception, representation, and action。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=Wh86SLotOT](https://openreview.net/forum?id=Wh86SLotOT)
