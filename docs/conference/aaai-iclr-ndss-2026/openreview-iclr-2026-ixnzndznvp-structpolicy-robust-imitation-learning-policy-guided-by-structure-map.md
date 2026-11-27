---
title: "StructPolicy: Robust Imitation Learning Policy Guided by Structure Map"
title_zh: StructPolicy：结构图引导的鲁棒模仿学习策略
authors: "Zehao Du, Jiude Wei, Cewu Lu, Jianhua Sun"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=IXNZNDZNVp"
tags: ["query:humanoid-rl"]
score: 8.0
evidence: 结构化表示引导的操作模仿学习
tldr: 模仿学习通过视觉到动作的映射实现机器人操作，但易过拟合任务无关的视觉噪声，对分布偏移敏感。本文提出StructPolicy轻量模块，构建稳定且任务相关的结构图，由任务相关物体结构揭示完成操作所需的关键拓扑线索。模块过滤视觉干扰噪声并保留结构信息以引导策略学习。该方法提升了模仿学习策略在域偏移下的鲁棒性，为结构化表示与模仿学习结合提供了思路。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 模仿学习易过拟合任务无关视觉噪声，对分布偏移和域差异敏感。
method: 提出StructPolicy轻量模块，构建任务相关结构图过滤噪声并引导策略。
result: 方法保留关键结构线索，提升模仿学习策略在分布偏移下的鲁棒性。
conclusion: 该工作将结构化表示引入模仿学习，增强了机器人操作策略的鲁棒性。
---

## Abstract
Imitation Learning (IL) offers an effective approach for robot manipulation by learning a mapping function from visual inputs to actions.
However, this paradigm suffers from domain discrepancies and is highly sensitive to distribution shifts, as the mapping function inherent in IL tends to overfit task-irrelevant visual noise, thereby compromising robustness. To address this, we propose StructPolicy, a lightweight module that guides the robot to acquire structural knowledge by constructing a stable and task-relevant Structure Map.
The structure map is composed of task-relevant object structures and reveals the topological cues essential for accomplishing manipulation tasks.
By filtering out visually distracting noise and retaining only the structural attributes, it effectively guides the robot's policy learning toward robust manipulation.
We begin by introducing a general object structure representation based on atomic geometric primitives, enabling flexible composition and scalability to arbitrary objects.
Building on this, we design StructGen, a module that automatically constructs structure maps from visual observations.
Finally, we design StructTransformer, which employs hierarchical attention over structure vertices to extract map features from the structure map for action prediction.
We extensively evaluate StructPolicy across 3 IL models, 3 different simulators, and 50 diverse manipulation tasks.
In addition, through ablation studies under various visual changes, including visual noise, camera viewpoint shifts, light intensity, and background color variations, we demonstrate that StructPolicy consistently improves robustness against distribution shifts.
Results demonstrate consistent and significant performance improvements across all tasks, validating the effectiveness and robustness of StructPolicy. Our code will be released publicly to facilitate reproducibility and further research.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
结构化表示引导的操作模仿学习。

### 2. 核心内容
模仿学习通过视觉到动作的映射实现机器人操作，但易过拟合任务无关的视觉噪声，对分布偏移敏感。本文提出StructPolicy轻量模块，构建稳定且任务相关的结构图，由任务相关物体结构揭示完成操作所需的关键拓扑线索。模块过滤视觉干扰噪声并保留结构信息以引导策略学习。该方法提升了模仿学习策略在域偏移下的鲁棒性，为结构化表示与模仿学习结合提供了思路。

### 3. 对应检索需求
Find work combining object centric representation learning and imitation learning for robot manipulation.

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=IXNZNDZNVp](https://openreview.net/forum?id=IXNZNDZNVp)
