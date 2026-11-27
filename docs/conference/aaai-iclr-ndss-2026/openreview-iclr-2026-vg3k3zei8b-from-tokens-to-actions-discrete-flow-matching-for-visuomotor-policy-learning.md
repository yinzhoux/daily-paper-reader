---
title: "From Tokens to Actions: Discrete Flow Matching for Visuomotor Policy Learning"
title_zh: 从Token到动作：面向视觉运动策略学习的离散流匹配
authors: "Kexin Shi, Shikhar Bahl, Deepak Pathak"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=Vg3K3ZEi8B"
tags: ["query:humanoid-rl"]
score: 6.0
evidence: 离散token动作表示结合流匹配的视觉运动操作策略
tldr: 针对连续动作策略学习中稳定性、多模态性与推理效率难以兼顾的问题，本文提出离散流匹配策略DFMP。该方法把动作表示为离散token，将动作生成建模为连续时间马尔可夫链并学习token间转移概率，从而结合流匹配目标、概率分支带来的多模态行为建模与快速推理。作者系统研究了连续控制与离散表示的桥接方式，在视觉运动策略学习任务上验证了该结构化动作表示的有效性。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 连续动作策略难以同时兼顾训练稳定性、多模态行为表达与快速推理。
method: 将动作离散为token，用连续时间马尔可夫链与流匹配学习token转移概率。
result: 方法在视觉运动策略学习中实现稳定优化、多模态建模与快速推理。
conclusion: 离散动作表示结合流匹配为机器人策略学习提供了高效且多模态的范式。
---

## Abstract
Although actions in the physical world are inherently continuous, representing them in a discrete space can unlock stability, efficiency, and multimodality in policy learning. We present Discrete Flow Matching Policy (DFMP), a novel method that learns continuous robot actions in a discrete space using score-based generative modeling. DFMP formulates action generation as a Continuous-Time Markov Chain, learning transition probabilities over action tokens. Through this, DFMP unifies three desirable properties: (i) stable optimization through flow-matching objectives, (ii) multimodal behavior modeling via probabilistic branching between tokens, and (iii) fast inference. To bridge continuous control with discrete representations, we systematically study tokenization schemes and analyze their trade-offs, proposing the optimal approach for real world robot policies. We thoroughly evaluate DFMP across many challenging simulated manipulation benchmarks and two real-world robot deployments, showing that our approach provides not only strong task performance, but also better scalability and robustness compared to existing continuous-space methods. These results position DFMP as a new, principled approach to efficient, robust, and multimodal visuomotor policy learning, advancing the integration of discrete generative modeling into real-world robotics. Videos and code are provided on the project page https://dfm-policy.github.io.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
离散token动作表示结合流匹配的视觉运动操作策略。

### 2. 核心内容
针对连续动作策略学习中稳定性、多模态性与推理效率难以兼顾的问题，本文提出离散流匹配策略DFMP。该方法把动作表示为离散token，将动作生成建模为连续时间马尔可夫链并学习token间转移概率，从而结合流匹配目标、概率分支带来的多模态行为建模与快速推理。作者系统研究了连续控制与离散表示的桥接方式，在视觉运动策略学习任务上验证了该结构化动作表示的有效性。

### 3. 对应检索需求
robotic manipulation policies that leverage structured representations and reinforcement learning。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=Vg3K3ZEi8B](https://openreview.net/forum?id=Vg3K3ZEi8B)
