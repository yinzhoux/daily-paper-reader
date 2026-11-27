---
title: Hierarchical Value-Decomposed Offline Reinforcement Learning for Whole-Body Control
title_zh: 面向全身控制的分层价值分解离线强化学习
authors: "Zhilong Zhang, Yunpeng Mei, Xinghao Du, Hongjie Cao, Haonan Wang, Pengyuan Min, Chenyu Wang, Pengfei Chen, Chenbo Xin, Yijie Wang, Wenyu Luo, Yihao Sun, Yidi Wang, Lei Yuan, Gang Wang, Yang Yu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=eSkDNIGbcd"
tags: ["query:humanoid-rl"]
score: 8.0
evidence: 面向高自由度全身控制的分层价值分解离线强化学习
tldr: 针对高自由度全身机器人模仿学习受限于专家示范稀缺的问题，本文提出分层价值分解离线强化学习HVD。该方法利用大量易获取的次优数据，通过离线RL的价值分解实现有原则的数据筛选，使策略优先学习高价值片段，并借助分层结构应对高维控制带来的学习复杂度。该工作为真实世界全身控制中利用不完美轨迹提供了有效途径，与全身操作和具身控制的需求高度契合。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 高自由度全身机器人模仿学习受专家示范稀缺限制，而次优数据虽多却难利用。
method: 提出HVD，用分层价值分解的离线强化学习对次优数据进行有原则的筛选与学习。
result: 该方法可从次优数据中提取有效信号并缓解高维控制带来的学习复杂度。
conclusion: 分层价值分解离线RL为真实世界全身控制提供了利用次优数据的实用方案。
---

## Abstract
Scaling imitation learning to high-DoF whole-body robots is fundamentally constrained by the scarcity of expert demonstrations. In contrast, large amounts of suboptimal data are readily available and offer a practical way to alleviate supervision bottlenecks in real-world whole-body control. However, leveraging such data introduces two central challenges: how to extract informative signals from imperfect trajectories, and how to cope with the increased learning complexity induced by high-dimensional control. To overcome this, we propose **HVD** (Hierarchical Value-Decomposed Offline Reinforcement Learning). The offline RL formulation provides principled data selection over suboptimal datasets, enabling the policy to prioritize high-value behaviors while down-weighting harmful ones. Complementarily, hierarchical value decomposition organizes learning along the robot’s kinematic structure, improving credit assignment and reducing learning complexity in high-DoF systems. Built on a Transformer-based architecture, HVD supports *multi-modal* and *multi-task* learning, allowing flexible integration of diverse sensory inputs. To enable realistic evaluation and training, we further introduce **WB-50**, a 50-hour dataset of teleoperated and policy rollout trajectories annotated with rewards and preserving natural imperfections, including partial successes, corrections, and failures. Experiments show HVD significantly outperforms existing baselines in success rate across complex whole-body tasks. Our results suggest effective policy learning for high-DoF systems can emerge not from perfect demonstrations, but from structured learning over realistic, imperfect data. Our code is available at https://github.com/LAMDA-RL/HVD.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向高自由度全身控制的分层价值分解离线强化学习。

### 2. 核心内容
针对高自由度全身机器人模仿学习受限于专家示范稀缺的问题，本文提出分层价值分解离线强化学习HVD。该方法利用大量易获取的次优数据，通过离线RL的价值分解实现有原则的数据筛选，使策略优先学习高价值片段，并借助分层结构应对高维控制带来的学习复杂度。该工作为真实世界全身控制中利用不完美轨迹提供了有效途径，与全身操作和具身控制的需求高度契合。

### 3. 对应检索需求
humanoid robots interacting with objects through whole-body control and manipulation。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=eSkDNIGbcd](https://openreview.net/forum?id=eSkDNIGbcd)
