---
title: Unified Latent Steering and Residual Refinement for Online Improvement of Diffusion Policy Models
title_zh: 统一潜在引导与残差精炼用于扩散策略模型的在线改进
authors: "Zhengbang Zhu, Ziyan Li, Xiu Yuan, Hanbo Zhang, Yuxiao Liu, Chongjie Zhang, Yong Yu, Weinan Zhang, Minghuan Liu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=DbBD2aT1OG"
tags: ["query:humanoid-rl"]
score: 5.0
evidence: 对模仿学习得到的扩散操作策略进行在线改进
tldr: 纯模仿学习训练的扩散策略在分布偏移与新场景下较为脆弱，需要在线改进，但直接微调大策略样本效率极低。作者提出USR统一框架，将潜在空间引导与残差精炼相结合，对预训练扩散策略进行高效在线改进。该方法兼顾预训练策略的多模态分布并突破示范覆盖范围。工作聚焦模仿学习策略的在线提升，与物体中心结构化表征关联有限。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 纯模仿学习的扩散策略在分布偏移下脆弱，而全参数微调样本效率低、成本高。
method: 提出USR框架，结合潜在空间引导与残差精炼对预训练扩散策略进行在线改进。
result: 在无需昂贵全量微调的情况下实现高效在线提升，并利用预训练策略的多模态分布。
conclusion: 为模仿学习操作策略的持续改进提供高效方案，但未涉及结构化物体表征。
---

## Abstract
Imitation learning has driven major advances in robotic manipulation by exploiting large and diverse demonstrations, yet policies trained purely by imitation remain brittle under distribution shift and novel scenarios, making online improvement essential. 
Directly finetuning the parameters of modern large policies is prohibitively sample inefficient and computationally expensive,
while recent finetuning-free adaptation methods either fail to exploit the multimodal distributions learned by pretrained policies or remain confined to the coverage of demonstrations.
We propose USR, a Unified framework for latent Steering and residual Refinement that enables efficient online improvement of diffusion policy models. A lightweight actor jointly outputs latent noise to steer the diffusion process toward promising modes and residual corrections to adapt beyond the diffusion policy's support, combining stable mode selection with flexible refinement. This unified design stabilizes training and fully leverages both components. Experiments on standard benchmarks and our MultiModalBench demonstrate USR's state-of-the-art performance. Furthermore, we validate its real-world applicability by improving a Vision-Language-Action (VLA) model on a physical robot, setting a new paradigm for sample-efficient adaptation of diffusion-based policies.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
对模仿学习得到的扩散操作策略进行在线改进。

### 2. 核心内容
纯模仿学习训练的扩散策略在分布偏移与新场景下较为脆弱，需要在线改进，但直接微调大策略样本效率极低。作者提出USR统一框架，将潜在空间引导与残差精炼相结合，对预训练扩散策略进行高效在线改进。该方法兼顾预训练策略的多模态分布并突破示范覆盖范围。工作聚焦模仿学习策略的在线提升，与物体中心结构化表征关联有限。

### 3. 对应检索需求
Find work combining object centric representation learning and imitation learning for robot manipulation.

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=DbBD2aT1OG](https://openreview.net/forum?id=DbBD2aT1OG)
