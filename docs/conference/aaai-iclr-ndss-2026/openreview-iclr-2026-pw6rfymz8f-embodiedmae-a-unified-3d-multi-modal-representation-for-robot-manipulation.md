---
title: "EmbodiedMAE: A Unified 3D Multi-Modal Representation for Robot Manipulation"
title_zh: EmbodiedMAE：面向机器人操作的统一三维多模态表征
authors: "Zibin Dong, Fei Ni, Yifu Yuan, Yinchuan Li, Jianye HAO"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=pW6rFymZ8F"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 面向机器人操作的三维多模态统一表征学习
tldr: 现有方法在训练数据与操作任务间存在域差距，且缺乏有效融合三维信息的架构。作者为DROID数据集补充高质量深度图与点云，构建DROID-3D，并提出EmbodiedMAE多模态掩码自编码器。该方法通过随机掩码与跨模态融合同时学习RGB、深度与点云表征。实验表明其持续优于现有视觉表征方法，为具身三维感知与策略学习提供基础。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有方法存在训练数据与操作任务的域差距，且缺乏有效融合三维信息的模型架构。
method: 构建含深度与点云的DROID-3D，并提出跨RGB、深度与点云的多模态掩码自编码器EmbodiedMAE。
result: 通过随机掩码与跨模态融合学习统一表征，持续优于现有视觉编码器。
conclusion: 为具身三维视觉与机器人操作提供统一可复用的多模态表征基础。
---

## Abstract
We present EmbodiedMAE, a unified 3D multi-modal representation for robot manipulation. Current approaches suffer from significant domain gaps between training datasets and robot manipulation tasks, while also lacking model architectures that can effectively incorporate 3D information. To overcome these limitations, we enhance the DROID dataset with high-quality depth maps and point clouds, constructing DROID-3D as a valuable supplement for 3D embodied vision research. Then we develop EmbodiedMAE, a multi-modal masked autoencoder that simultaneously learns representations across RGB, depth, and point cloud modalities through stochastic masking and cross-modal fusion. Trained on DROID-3D, EmbodiedMAE consistently outperforms state-of-the-art vision foundation models (VFMs) in both training efficiency and final performance across 70 simulation tasks and 20 real-world robot manipulation tasks on two robot platforms. The model exhibits strong scaling behavior with size and promotes effective policy learning from 3D inputs. Experimental results establish EmbodiedMAE as a reliable unified 3D multi-modal VFM for embodied AI systems, particularly in precise tabletop manipulation settings where spatial perception is critical.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向机器人操作的三维多模态统一表征学习。

### 2. 核心内容
现有方法在训练数据与操作任务间存在域差距，且缺乏有效融合三维信息的架构。作者为DROID数据集补充高质量深度图与点云，构建DROID-3D，并提出EmbodiedMAE多模态掩码自编码器。该方法通过随机掩码与跨模态融合同时学习RGB、深度与点云表征。实验表明其持续优于现有视觉表征方法，为具身三维感知与策略学习提供基础。

### 3. 对应检索需求
representation learning for control, robotics, and embodied decision making。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=pW6rFymZ8F](https://openreview.net/forum?id=pW6rFymZ8F)
