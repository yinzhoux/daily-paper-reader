---
title: Executable Analytic Concepts as the Missing Link Between VLM Insight and Precise Manipulation
title_zh: 可执行解析概念：连接视觉语言模型洞察与精确操作的缺失环节
authors: "Mingyang Sun, Jiude Wei, Qichen He, Donglin Wang, Cewu Lu, Jianhua Sun"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=SESeW4EvPd"
tags: ["query:humanoid-rl"]
score: 6.0
evidence: 以结构化解析概念表征为视觉语言模型推理落地于操作
tldr: 视觉语言模型具备语义推理能力，却难以支撑真实世界精确操作，存在语义到物理的鸿沟。作者提出GRACE框架，用可执行解析概念作为桥梁，以数学化蓝图编码物体可供性、几何约束与操作语义。这些结构化概念被整合进策略脚手架流程，将高层推理落地为精确动作。工作展示了结构化表征在提升操作精度与泛化性方面的作用。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 视觉语言模型高层语义理解与真实世界精确物理执行之间存在语义到物理的鸿沟。
method: 提出GRACE，用编码可供性、几何约束与语义的可执行解析概念构建结构化策略脚手架。
result: 将视觉语言模型推理落地为精确操作动作，提升非结构化环境下的操作表现。
conclusion: 表明结构化解析概念可作为连接语义推理与精确操作的桥梁。
---

## Abstract
Enabling robots to perform precise and generalized manipulation in unstructured environments remains a fundamental challenge in embodied AI. While Vision-Language Models (VLMs) have demonstrated remarkable capabilities in semantic reasoning and task planning, a significant gap persists between their high-level understanding and the precise physical execution required for real-world manipulation. To bridge this “semantic-to-physical” gap, we introduce GRACE, a novel framework that grounds VLM-based reasoning through executable analytic concepts (EAC)—mathematically defined blueprints that encode object affordances, geometric constraints, and semantics of manipulation. Our approach integrates a structured policy scaffolding pipeline that turn natural language instructions and visual information into an instantiated EAC, from which we derive grasp poses, force directions and plan physically feasible motion trajectory for robot execution. GRACE thus provides a unified and interpretable interface between high-level instruction understanding and low-level robot control, effectively enabling precise and generalizable manipulation through semantic-physical grounding. Extensive experiments demonstrate that GRACE achieves strong zero-shot generalization across a variety of articulated objects in both simulated and real-world environments, without requiring task-specific training.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
以结构化解析概念表征为视觉语言模型推理落地于操作。

### 2. 核心内容
视觉语言模型具备语义推理能力，却难以支撑真实世界精确操作，存在语义到物理的鸿沟。作者提出GRACE框架，用可执行解析概念作为桥梁，以数学化蓝图编码物体可供性、几何约束与操作语义。这些结构化概念被整合进策略脚手架流程，将高层推理落地为精确动作。工作展示了结构化表征在提升操作精度与泛化性方面的作用。

### 3. 对应检索需求
robotic manipulation policies that leverage structured representations and reinforcement learning。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=SESeW4EvPd](https://openreview.net/forum?id=SESeW4EvPd)
