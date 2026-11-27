---
title: Primary-Fine Decoupling for Action Generation in Robotic Imitation
title_zh: 机器人模仿中动作生成的主-细粒度解耦
authors: "Xiaohan Lei, Min Wang, Wengang Zhou, Xingyu Lu, Houqiang Li"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=wySMuWHmt4"
tags: ["query:humanoid-rl"]
score: 5.0
evidence: 面向机器人操作模仿学习的解耦式动作生成
tldr: 针对机器人操作动作序列多模态分布给模仿学习带来的挑战，本文指出现有离散化或单阶段连续生成方法各有权衡。作者提出 Primary-Fine Decoupling for Action Generation 两阶段框架，先将动作块压缩为少量离散模式以保证粗粒度一致性，再生成细粒度变化。方法在保持动作多样性的同时缓解了模式切换不稳定问题，提升了操作模仿学习的动作生成质量。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 机器人操作动作序列的多模态分布使模仿学习在离散化与连续生成之间面临权衡。
method: 提出 PF-DAG 两阶段框架，先压缩动作块为离散模式，再生成细粒度动作变化。
result: 方法在保持细粒度动作多样性的同时缓解了模式切换不稳定，提升动作生成质量。
conclusion: 粗细分层解耦为机器人模仿学习中的多模态动作建模提供了有效方案。
---

## Abstract
Multi-modal distribution in robotic manipulation action sequences poses critical challenges for imitation learning. 
To this end, existing approaches often model the action space as either a discrete set of tokens or a continuous, latent-variable distribution.
However, both approaches present trade-offs: some methods discretize actions into tokens and therefore lose fine-grained action variations, while others generate continuous actions in a single stage tend to produce unstable mode transitions.
To address these limitations, we propose Primary-Fine Decoupling for Action Generation (PF-DAG), a two-stage framework that decouples coarse action consistency from fine-grained variations. First, we compress action chunks into a small set of discrete modes, enabling a lightweight policy to select consistent coarse modes and avoid mode bouncing. Second, a mode conditioned MeanFlow policy is learned to generate high-fidelity continuous actions.
Theoretically, we prove PF-DAG’s two-stage design achieves a strictly lower MSE bound than single-stage generative policies. 
Empirically, PF-DAG outperforms state-of-the-art baselines across 56 tasks from Adroit, DexArt, and MetaWorld benchmarks. It further generalizes to real-world tactile dexterous manipulation tasks. Our work demonstrates that explicit mode-level decoupling enables both robust multi-modal modeling and reactive closed-loop control for robotic manipulation.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向机器人操作模仿学习的解耦式动作生成。

### 2. 核心内容
针对机器人操作动作序列多模态分布给模仿学习带来的挑战，本文指出现有离散化或单阶段连续生成方法各有权衡。作者提出 Primary-Fine Decoupling for Action Generation 两阶段框架，先将动作块压缩为少量离散模式以保证粗粒度一致性，再生成细粒度变化。方法在保持动作多样性的同时缓解了模式切换不稳定问题，提升了操作模仿学习的动作生成质量。

### 3. 对应检索需求
Find work combining object centric representation learning and imitation learning for robot manipulation.

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=wySMuWHmt4](https://openreview.net/forum?id=wySMuWHmt4)
