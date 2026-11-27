---
title: "DemoGrasp: Universal Dexterous Grasping from a Single Demonstration"
title_zh: DemoGrasp：从单条演示学习通用灵巧抓取
authors: "Haoqi Yuan, Ziye Huang, Ye Wang, Chuan Mao, Chaoyi Xu, Zongqing Lu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=Bf4FeuW0Mr"
tags: ["query:humanoid-rl"]
score: 6.0
evidence: 从单条演示学习灵巧抓取策略并进行动作适配
tldr: 针对多指灵巧手通用抓取中高维长时程探索困难、依赖复杂奖励与课程设计且易陷次优解的问题，论文提出DemoGrasp，从单条成功抓取演示出发，通过修改腕部位姿与手指关节角动作来迁移到新物体与新位姿。实验表明该方法无需复杂奖励设计即可在多样物体上实现通用灵巧抓取，性能优于强化学习基线，降低了演示驱动灵巧抓取的学习成本。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 多指灵巧手通用抓取依赖强化学习，但高维长时程探索需复杂奖励与课程设计，易陷入次优解。
method: 提出DemoGrasp，从单条成功抓取演示出发，通过编辑腕部位姿与手指关节角动作迁移到新物体与新位姿。
result: 实验表明该方法无需复杂奖励设计即可在多种物体上实现通用灵巧抓取，性能优于强化学习基线。
conclusion: 该工作展示了演示引导的动作编辑可作为高效替代方案，降低灵巧抓取的学习成本。
---

## Abstract
Universal grasping with multi-fingered dexterous hands is a fundamental challenge in robotic manipulation. While recent approaches successfully learn closed-loop grasping policies using reinforcement learning (RL), the inherent difficulty of high-dimensional, long-horizon exploration necessitates complex reward and curriculum design, often resulting in suboptimal solutions across diverse objects. We propose DemoGrasp, a simple yet effective method for learning universal dexterous grasping. We start from a single successful demonstration trajectory of grasping a specific object and adapt to novel objects and poses by editing the robot actions in this trajectory: changing the wrist pose determines where to grasp, and changing the hand joint angles determines how to grasp. We formulate this trajectory editing as a single-step Markov Decision Process (MDP) and use RL to optimize a universal policy across hundreds of objects in parallel in simulation, with a simple reward consisting of a binary success term and a robot–table collision penalty. In simulation, DemoGrasp achieves a 95% success rate on DexGraspNet objects using the Shadow Hand, outperforming previous state-of-the-art methods. It also shows strong transferability, achieving an average success rate of 84.6% across diverse dexterous hand embodiments on six unseen object datasets, while being trained on only 175 objects. Through vision-based imitation learning, our policy successfully grasps 110 unseen real-world objects, including small, thin items. It generalizes to spatial, background, and lighting changes, supports both RGB and depth inputs, and extends to language-guided grasping in cluttered scenes.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
从单条演示学习灵巧抓取策略并进行动作适配。

### 2. 核心内容
针对多指灵巧手通用抓取中高维长时程探索困难、依赖复杂奖励与课程设计且易陷次优解的问题，论文提出DemoGrasp，从单条成功抓取演示出发，通过修改腕部位姿与手指关节角动作来迁移到新物体与新位姿。实验表明该方法无需复杂奖励设计即可在多样物体上实现通用灵巧抓取，性能优于强化学习基线，降低了演示驱动灵巧抓取的学习成本。

### 3. 对应检索需求
Find work combining object centric representation learning and imitation learning for robot manipulation.

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=Bf4FeuW0Mr](https://openreview.net/forum?id=Bf4FeuW0Mr)
