---
title: Towards Bridging the Gap between Large-Scale Pretraining and Efficient Finetuning for Humanoid Control
title_zh: 弥合人形机器人控制中大规模预训练与高效微调之间的差距
authors: "Weidong Huang, Zhehan Li, Hangxin Liu, Biao Hou, Yao Su, Jingwen Zhang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=NEOTsyyYH7"
tags: ["query:humanoid-rl"]
score: 9.0
evidence: 面向人形机器人运动控制的离策略强化学习预训练与高效微调
tldr: 针对人形机器人控制中在策略算法样本效率低、难以安全适应新环境的问题，本文系统研究了离策略强化学习的训练配置。作者发现采用大批量更新与高更新数据比（UTD）的SAC能够稳定支撑人形运动策略的大规模预训练，并在微调阶段显著提升样本效率。实验表明该方案在保持鲁棒性的同时缩小了预训练与高效微调之间的差距，为人形机器人策略的规模化训练与快速适配提供了实用范式。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 人形控制常用PPO等在线策略方法，样本效率低，难以安全高效地适应新环境。
method: 采用离策略SAC并结合大批量更新与高更新数据比（UTD）进行大规模预训练与微调。
result: 实验表明该配置可稳定训练人形运动策略，并显著提升微调阶段的样本效率。
conclusion: 该工作缩小了人形控制中大规模预训练与高效微调之间的差距。
---

## Abstract
Reinforcement learning (RL) is widely used for humanoid control, with on-policy methods such as Proximal Policy Optimization (PPO) enabling robust training via large-scale parallel simulation and, in some cases, zero-shot deployment to real robots. However, the low sample efficiency of on-policy algorithms limits safe adaptation to new environments. Although off-policy RL and model-based RL have shown improved sample efficiency, the gap between large-scale pretraining and efficient finetuning on humanoids still exists. In this paper, we find that off-policy Soft Actor-Critic (SAC), with large-batch update and a high Update-To-Data (UTD) ratio, reliably supports large-scale pretraining of humanoid locomotion policies, achieving zero-shot deployment on real robots. For adaptation, we demonstrate that these SAC-pretrained policies can be finetuned in new environments and out-of-distribution tasks using model-based methods. Data collection in the new environment executes a deterministic policy while stochastic exploration is instead confined to a physics-informed world model.  This separation mitigates the risks of random exploration during adaptation while preserving exploratory coverage for improvement. Overall, the approach couples the wall-clock efficiency of large-scale simulation during pretraining with the sample efficiency of model-based learning during fine-tuning. Code and videos: https://lift-humanoid.github.io

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向人形机器人运动控制的离策略强化学习预训练与高效微调。

### 2. 核心内容
针对人形机器人控制中在策略算法样本效率低、难以安全适应新环境的问题，本文系统研究了离策略强化学习的训练配置。作者发现采用大批量更新与高更新数据比（UTD）的SAC能够稳定支撑人形运动策略的大规模预训练，并在微调阶段显著提升样本效率。实验表明该方案在保持鲁棒性的同时缩小了预训练与高效微调之间的差距，为人形机器人策略的规模化训练与快速适配提供了实用范式。

### 3. 对应检索需求
reinforcement learning methods for controlling embodied agents and humanoid robots。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=NEOTsyyYH7](https://openreview.net/forum?id=NEOTsyyYH7)
