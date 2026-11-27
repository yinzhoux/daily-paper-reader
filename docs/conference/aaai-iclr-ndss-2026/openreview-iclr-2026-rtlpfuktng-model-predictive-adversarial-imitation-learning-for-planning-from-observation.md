---
title: Model Predictive Adversarial Imitation Learning for Planning from Observation
title_zh: 面向观测规划的模型预测对抗模仿学习
authors: "Tyler Han, Yanda Bao, Bhaumik Mehta, Gabriel Guo, Sanghun Jung, Anubhav Vishwakarma, Emily Kang, Rosario Scalise, Jason Liren Zhou, Bryan Xu, Byron Boots"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=rTlPfuKTNg"
tags: ["query:humanoid-rl"]
score: 6.0
evidence: 结合模型预测规划的机器人对抗模仿学习
tldr: 针对机器人仅从观测示范中学习规划策略时，逆强化学习与模型预测控制分步进行的问题，论文提出基于规划的对抗模仿学习，同时学习奖励函数并通过经验改进规划智能体。该方法利用观测级示范统一奖励学习与规划部署，提升模仿的效率和可解释性。研究分析规划式模仿的优势，为机器人从示范中恢复意图并执行规划提供了新框架。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 传统从示范学习规划需先逆强化学习再模型预测控制，流程分离且效率有限。
method: 提出基于规划的对抗模仿学习，同时学习奖励并改进规划智能体。
result: 摘要指出该方法利用观测示范统一奖励学习与规划部署，具体实验结论未展开。
conclusion: 为机器人观测示范下的可解释规划式模仿学习提供了统一方法。
---

## Abstract
Humans can often perform a new task after observing a few demonstrations by inferring the underlying intent. For robots, recovering the intent of the demonstrator through a learned reward function can enable more efficient, interpretable, and robust imitation through planning. A common paradigm for learning how to plan-from-demonstration involves first solving for a reward via Inverse Reinforcement Learning (IRL) and then deploying it via Model Predictive Control (MPC). In this work, we unify these two procedures by introducing planning-based Adversarial Imitation Learning, which simultaneously learns a reward and improves a planning-based agent through experience while using observation-only demonstrations. We study advantages of planning-based AIL in generalization, interpretability, robustness, and sample efficiency through experiments in simulated control tasks and real-world navigation from few or single observation-only demonstration.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
结合模型预测规划的机器人对抗模仿学习。

### 2. 核心内容
针对机器人仅从观测示范中学习规划策略时，逆强化学习与模型预测控制分步进行的问题，论文提出基于规划的对抗模仿学习，同时学习奖励函数并通过经验改进规划智能体。该方法利用观测级示范统一奖励学习与规划部署，提升模仿的效率和可解释性。研究分析规划式模仿的优势，为机器人从示范中恢复意图并执行规划提供了新框架。

### 3. 对应检索需求
Find work combining object centric representation learning and imitation learning for robot manipulation.

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=rTlPfuKTNg](https://openreview.net/forum?id=rTlPfuKTNg)
