---
title: "From Seeing to Doing: Bridging Reasoning and Decision for Robotic Manipulation"
title_zh: 从看到做：为机器人操作连接推理与决策
authors: "Yifu Yuan, Haiqin Cui, Yibin Chen, Zibin Dong, Fei Ni, Longxin Kou, Jinyi Liu, Pengyi Li, YAN ZHENG, Jianye HAO"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=yngvAamNQi"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 生成结构化空间中间表示以引导机器人操作策略
tldr: 针对具身数据稀缺异质导致视觉-语言-动作模型零样本泛化不足的问题，论文提出FSD模型，通过空间关系推理生成中间表示，并结合分层数据构建流程与自一致性机制为机器人操作提供细粒度引导。实验表明该结构化表示显著提升机器人在新场景与新任务上的泛化与操作成功率，说明空间推理表示可作为连接感知与动作决策的有效桥梁。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有视觉-语言-动作模型受限于具身数据稀缺与异质，难以在未见场景和新任务上实现稳健零样本泛化。
method: 提出FSD模型，通过空间关系推理生成中间表示，并结合分层数据构建流程与自一致性机制为操作提供细粒度引导。
result: 实验表明该中间表示显著提升机器人在新场景与新任务上的泛化能力与操作成功率。
conclusion: 该工作说明结构化空间推理表示可作为连接感知与动作决策的有效桥梁。
---

## Abstract
Achieving generalization in robotic manipulation remains a critical challenge, particularly for unseen scenarios and novel tasks. Current Vision-Language-Action (VLA) models, while building on top of general Vision-Language Models (VLMs), still fall short of achieving robust zero-shot performance due to the scarcity and heterogeneity prevalent in embodied datasets. To address these limitations, we propose FSD (From Seeing to Doing), a novel vision-language model that generates intermediate representations through spatial relationship reasoning, providing fine-grained guidance for robotic manipulation. Our approach combines a hierarchical data construction pipeline for training with a self-consistency mechanism that aligns spatial coordinates with visual signals. Through extensive experiments, we comprehensively validated FSD’s capabilities in both “seeing” and “doing”, achieving outstanding performance across 8 benchmarks for general spatial reasoning and embodied reference abilities, as well as on our proposed more challenging benchmark VABench. We also verified zero-shot capabilities in robot manipulation, demonstrating significant performance improvements over baseline methods in both SimplerEnv and real robot settings. Experimental results show that FSD achieves 40.6% success rate in SimplerEnv and 72% success rate across 8 real-world tasks, outperforming the strongest baseline by 30%.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
生成结构化空间中间表示以引导机器人操作策略。

### 2. 核心内容
针对具身数据稀缺异质导致视觉-语言-动作模型零样本泛化不足的问题，论文提出FSD模型，通过空间关系推理生成中间表示，并结合分层数据构建流程与自一致性机制为机器人操作提供细粒度引导。实验表明该结构化表示显著提升机器人在新场景与新任务上的泛化与操作成功率，说明空间推理表示可作为连接感知与动作决策的有效桥梁。

### 3. 对应检索需求
robotic manipulation policies that leverage structured representations and reinforcement learning。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=yngvAamNQi](https://openreview.net/forum?id=yngvAamNQi)
