---
title: "DexMan: Learning Bimanual Dexterous Manipulation from Human and Generated Videos"
title_zh: DexMan：从人类视频与生成视频学习双臂灵巧操作
authors: "Jhen Hsieh, Kuan-Hsun Tu, Kuo-Han Hung, Tsung-Wei Ke"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=93LGsNwfMW"
tags: ["query:humanoid-rl"]
score: 8.0
evidence: 将人类视频示范转化为人形机器人双臂灵巧操作技能
tldr: 针对从人类视频学习人形机器人双臂灵巧操作通常依赖相机标定、深度传感器与三维物体资产等额外标注的问题，论文提出DexMan框架，直接从第三人称人类操作视频估计手物姿态，并利用接触式奖励训练人形机器人策略。实验在TACO基准上物体姿态估计取得最优并绝对提升0.08，仿真中学会双臂灵巧操作技能，降低了人形操作技能获取的标注门槛。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 从人类视频学习人形机器人双臂灵巧操作通常依赖相机标定、深度传感器与三维物体资产等额外标注。
method: 提出DexMan框架，直接从第三人称人类操作视频估计手物姿态，并利用接触式奖励训练人形机器人双臂灵巧操作策略。
result: 实验在TACO基准上物体姿态估计取得最优并绝对提升0.08，并在仿真中学会双臂灵巧操作技能。
conclusion: 该工作降低了从人类视频学习人形操作的标注门槛，推动了人形机器人的技能获取。
---

## Abstract
We present DexMan, an automated framework that converts human visual demonstrations into bimanual dexterous manipulation skills for humanoid robots in simulation. Operating directly on third-person videos of humans manipulating rigid objects, DexMan eliminates the need for camera calibration, depth sensors, scanned 3D object assets, or ground-truth hand and object motion annotations. Unlike prior approaches that consider only simplified floating hands, it directly controls a humanoid robot and leverages novel contact-based rewards to improve policy learning from noisy hand–object poses estimated from in-the-wild videos.

DexMan achieves state-of-the-art performance in object pose estimation on the TACO benchmark, with absolute gains of 0.08 and 0.12 in ADD-S and VSD. Meanwhile, its reinforcement learning policy surpasses previous methods by 19% in success rate on OakInk-v2. Furthermore, DexMan can generate skills from both real and synthetic videos, without the need for manual data collection and costly motion capture, and enabling the creation of large-scale, diverse datasets for training generalist dexterous manipulation. 

Video results are available at: https://dexman2026.github.io/

---

## 论文详细总结（自动生成）

### 1. 检索相关性
将人类视频示范转化为人形机器人双臂灵巧操作技能。

### 2. 核心内容
针对从人类视频学习人形机器人双臂灵巧操作通常依赖相机标定、深度传感器与三维物体资产等额外标注的问题，论文提出DexMan框架，直接从第三人称人类操作视频估计手物姿态，并利用接触式奖励训练人形机器人策略。实验在TACO基准上物体姿态估计取得最优并绝对提升0.08，仿真中学会双臂灵巧操作技能，降低了人形操作技能获取的标注门槛。

### 3. 对应检索需求
humanoid robots interacting with objects through whole-body control and manipulation。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=93LGsNwfMW](https://openreview.net/forum?id=93LGsNwfMW)
