---
title: "Humanoid-R0: Bridging Text-to-Motion Generation and Physical Deployment via RL"
title_zh: Humanoid-R0：通过强化学习连接文本到动作生成与物理部署
authors: "Zifeng Zhuang, Ting Wang, Binghong Zou, Xinxin Luo, Jianfei Ma, Huaicheng Zhou, Jinxin Liu, Donglin Wang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=agohD5ewsR"
tags: ["query:humanoid-rl"]
score: 8.0
evidence: 通过强化学习微调动作生成以实现可物理部署的人形机器人控制
tldr: 针对生成式动作可作为人形控制数据来源、但下游物理部署对平滑性、骨骼合理性与关键帧一致性要求严苛的问题，本文提出Humanoid-R0。该方法量化这些动作质量指标并转化为强化学习奖励函数，对文本到动作生成模型进行微调，使其输出满足物理可执行性要求。实验表明该框架能够衔接动作生成与真实人形机器人部署，缓解仿真多样性不足与示范采集昂贵的问题。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 生成动作可补充人形控制数据，但下游部署对动作质量与物理可行性要求严苛。
method: 量化平滑性、骨骼合理性与关键帧一致性指标，转为奖励函数并用RL微调动作生成模型。
result: 微调后的生成动作可满足物理部署要求，衔接动作生成与人形机器人控制。
conclusion: 强化学习微调可让生成式动作成为人形机器人控制的有效数据来源。
---

## Abstract
Motion generation models aim to create diverse and realistic motions from inputs such as text or keyframes, with applications in gaming, animation, and 3D content creation. Recently, generated motions have emerged as a viable supplement to reinforcement learning and teleoperation for humanoid control, overcoming the limitations of simulation diversity and bypassing the need for expensive demonstration collection. However, these downstream applications impose stringent requirements on motion quality—specifically, smoothness, skeletal plausibility, and keyframe consistency. To ensure generated motions meet these criteria, we quantify these metrics and convert them into reward functions for RL fine-tuning. Specifically, we fine-tune the motion generation component of HumanoidVLA using GRPO, resulting in Humanoid-R0, a model whose outputs are well-suited for robot control. Our approach is rigorously validated through extensive metric evaluations, simulation rendering, and real-world deployment, demonstrating significant improvements in motion smoothness, plausibility, and consistency. Notably, Humanoid-R0 enables stable execution of challenging sequences of consecutive commands on a real G1 robot, showcasing its enhanced capability for long-horizon task completion.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
通过强化学习微调动作生成以实现可物理部署的人形机器人控制。

### 2. 核心内容
针对生成式动作可作为人形控制数据来源、但下游物理部署对平滑性、骨骼合理性与关键帧一致性要求严苛的问题，本文提出Humanoid-R0。该方法量化这些动作质量指标并转化为强化学习奖励函数，对文本到动作生成模型进行微调，使其输出满足物理可执行性要求。实验表明该框架能够衔接动作生成与真实人形机器人部署，缓解仿真多样性不足与示范采集昂贵的问题。

### 3. 对应检索需求
reinforcement learning methods for controlling embodied agents and humanoid robots。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=agohD5ewsR](https://openreview.net/forum?id=agohD5ewsR)
