---
title: "Embodied-R1: Reinforced Embodied Reasoning for General Robotic Manipulation"
title_zh: Embodied-R1：面向通用机器人操作的强化具身推理
authors: "Yifu Yuan, Haiqin Cui, Yaoting Huang, Yibin Chen, Fei Ni, Zibin Dong, Pengyi Li, YAN ZHENG, Hongyao Tang, Jianye HAO"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=i5wlozMFsQ"
tags: ["query:humanoid-rl"]
score: 6.0
evidence: 以指向作为中间表征并结合强化微调的具身推理
tldr: 具身智能因数据稀缺与形态异构而存在从看到做的鸿沟。作者将指向定义为统一的、与形态无关的中间表征，并界定四类核心具身指向能力。基于构建的大规模数据集Embodied-Points-200K，用两阶段强化微调训练3B视觉语言模型Embodied-R1。该工作以结构化中间表征连接高层语义理解与底层动作原语，为通用机器人操作提供新思路。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 具身智能存在从感知到执行的鸿沟，源于数据稀缺与形态异构。
method: 以指向为形态无关的中间表征，构建数据集并用两阶段强化微调训练视觉语言模型。
result: 模型具备多类具身指向能力，将高层语义理解与底层动作原语相连接。
conclusion: 表明结构化中间表征结合强化微调可缓解通用操作中的泛化难题。
---

## Abstract
Generalization in embodied AI is hindered by the "seeing-to-doing gap", stemming from data scarcity and embodiment heterogeneity. To address this, we pioneer "pointing" as a unified, embodiment-agnostic intermediate representation, defining four core embodied pointing abilities that bridge high-level vision-language comprehension with low-level action primitives. We introduce Embodied-R1, a 3B Vision-Language Model (VLM) specifically designed for embodied reasoning and pointing. We use a wide range of embodied and general visual reasoning datasets as sources to construct a large-scale dataset, Embodied-Points-200K, which supports key embodied pointing capabilities. Then we train Embodied-R1 using a two-stage Reinforced Fine-tuning (RFT) curriculum with specialized multi-task reward design. Embodied-R1 achieves state-of-the-art performance on 11 embodied spatial and pointing benchmarks. Critically, it demonstrates robust zero-shot generalization by achieving a 56.2% success rate in the SIMPLEREnv and 87.5% across 8 real-world XArm tasks without any task-specific fine-tuning, representing a 62% improvement over strong baselines. Furthermore, the model exhibits high robustness against diverse visual disturbances. Our work shows that a pointing-centric representation, combined with an RFT training paradigm, offers an effective and generalizable pathway to closing the perception-action gap in robotics.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
以指向作为中间表征并结合强化微调的具身推理。

### 2. 核心内容
具身智能因数据稀缺与形态异构而存在从看到做的鸿沟。作者将指向定义为统一的、与形态无关的中间表征，并界定四类核心具身指向能力。基于构建的大规模数据集Embodied-Points-200K，用两阶段强化微调训练3B视觉语言模型Embodied-R1。该工作以结构化中间表征连接高层语义理解与底层动作原语，为通用机器人操作提供新思路。

### 3. 对应检索需求
embodied learning agents that couple perception, representation, and action。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=i5wlozMFsQ](https://openreview.net/forum?id=i5wlozMFsQ)
