---
title: Geometry-aware Policy Imitation
title_zh: 几何感知的策略模仿
authors: "Yiming Li, Nael Darwiche, Amirreza Razmjoo, Sichao Liu, Yilun Du, Auke Ijspeert, Sylvain Calinon"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=ggofj6tyr3"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 以几何曲线结构化表示示教的机器人模仿学习
tldr: 模仿学习通常将示教拆成离散的状态动作样本，丢失轨迹几何结构，难以兼顾多模态与高维感知输入。作者提出几何感知策略模仿GPI，把示教视为几何曲线并导出距离场，进而得到沿轨迹推进与偏差纠正两类控制流，组合成可控非参数向量场直接驱动机器人。实验表明该方法可在低维状态与高维视觉输入间模块化适配，并天然保留多模态示教。其贡献在于解耦度量学习与策略合成，为结构化表示驱动的机器人模仿提供通用范式。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有模仿学习把示教当作离散状态动作样本，忽略轨迹的几何结构，导致泛化与多模态能力受限。
method: 将示教建模为几何曲线并构建距离场，导出推进流与吸引流，合成可控非参数向量场引导机器人行为。
result: 在低维机器人状态与高维感知输入上均能模块化适配，保留多模态示教并支持高效组合。
conclusion: 该框架把度量学习与策略合成解耦，为几何结构驱动的机器人模仿学习提供了通用范式。
---

## Abstract
We propose a Geometry-Aware Policy Imitation (GPI) approach that rethinks imitation learning by treating demonstrations as geometric curves rather than collections of state–action samples. From these curves, GPI derives distance fields that give rise to two complementary control primitives: a progression flow that advances along expert trajectories and an attraction flow that corrects deviations. Their combination defines a controllable, non-parametric vector field that directly guides robot behavior. This formulation decouples metric learning from policy synthesis, enabling modular adaptation across low-dimensional robot states and high-dimensional perceptual inputs. GPI naturally supports multimodality by preserving distinct demonstrations as separate models and allows efficient composition of new demonstrations through simple additions to the distance field. We evaluate GPI in simulation and on real robots across diverse tasks. Experiments show that GPI achieves higher success rates than diffusion-based policies while running 20× faster, requiring less memory, and remaining robust to perturbations. These results establish GPI as an efficient, interpretable, and scalable alternative to generative approaches for robotic imitation learning.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
以几何曲线结构化表示示教的机器人模仿学习。

### 2. 核心内容
模仿学习通常将示教拆成离散的状态动作样本，丢失轨迹几何结构，难以兼顾多模态与高维感知输入。作者提出几何感知策略模仿GPI，把示教视为几何曲线并导出距离场，进而得到沿轨迹推进与偏差纠正两类控制流，组合成可控非参数向量场直接驱动机器人。实验表明该方法可在低维状态与高维视觉输入间模块化适配，并天然保留多模态示教。其贡献在于解耦度量学习与策略合成，为结构化表示驱动的机器人模仿提供通用范式。

### 3. 对应检索需求
Find work combining object centric representation learning and imitation learning for robot manipulation.

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=ggofj6tyr3](https://openreview.net/forum?id=ggofj6tyr3)
