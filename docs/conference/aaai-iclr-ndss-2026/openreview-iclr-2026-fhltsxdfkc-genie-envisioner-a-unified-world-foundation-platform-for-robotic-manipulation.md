---
title: "Genie Envisioner: A Unified World Foundation Platform for Robotic Manipulation"
title_zh: Genie Envisioner：面向机器人操作的统一世界基础平台
authors: "Yue Liao, Pengfei Zhou, Siyuan Huang, Donglin Yang, Shengcong Chen, Yuxin Jiang, Yue Hu, Si Liu, Jianlan Luo, Liliang Chen, Shuicheng YAN, Maoqing Yao, Guanghui Ren"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=fHLtSxDFKC"
tags: ["query:humanoid-rl"]
score: 8.0
evidence: 面向机器人操作的视觉表示与动作策略联合学习
tldr: 针对机器人操作中视觉表示与动作策略往往分离学习、难以跨形态泛化的问题，论文提出Genie Envisioner统一世界基础平台，在视频生成框架内联合学习视觉表示与动作策略。其GE-Base在结构化隐空间建模时空与语义动态，GE-Act用轻量流匹配解码器将隐表示映射为可执行动作轨迹。基于百万级操作片段训练，该平台支持短长时程操作，为表示学习与策略学习的融合提供了通用基础。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 机器人操作需要同时理解视觉动态并生成动作，现有方法常将表示与策略分离。
method: 提出统一视频生成平台，联合学习结构化视觉表示，并用流匹配解码器输出动作轨迹。
result: 基于超百万操作片段训练，支持跨形态的短长时程操作策略推理。
conclusion: 为机器人操作提供了表示学习与动作生成一体化的世界基础平台。
---

## Abstract
We introduce Genie Envisioner (GE), a unified world foundation platform for robotic manipulation that jointly learns visual representations and action policies within a single video-generative framework. At its core, GE-Base is a large-scale instruction-conditioned video diffusion model that captures the spatial, temporal, and semantic dynamics of real-world robotic interactions in a structured latent space. Building on this foundation, GE-Act employs a lightweight flow-matching decoder to map latent representations into executable action trajectories, enabling precise and generalizable policy inference across diverse embodiments with minimal supervision. Trained on over 1 million manipulation episodes, GE supports both short- and long-horizon tasks, and generalizes across embodiments.  All code, models, and benchmarks will be released publicly.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向机器人操作的视觉表示与动作策略联合学习。

### 2. 核心内容
针对机器人操作中视觉表示与动作策略往往分离学习、难以跨形态泛化的问题，论文提出Genie Envisioner统一世界基础平台，在视频生成框架内联合学习视觉表示与动作策略。其GE-Base在结构化隐空间建模时空与语义动态，GE-Act用轻量流匹配解码器将隐表示映射为可执行动作轨迹。基于百万级操作片段训练，该平台支持短长时程操作，为表示学习与策略学习的融合提供了通用基础。

### 3. 对应检索需求
representation learning for control, robotics, and embodied decision making。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=fHLtSxDFKC](https://openreview.net/forum?id=fHLtSxDFKC)
