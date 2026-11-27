---
title: Abstracting Robot Manipulation Skills via Mixture-of-Experts Diffusion Policies
title_zh: 通过专家混合扩散策略抽象机器人操作技能
authors: "Ce Hao, Xuanran Zhai, Yaohua Liu, Harold Soh"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=VSWjHIveqZ"
tags: ["query:humanoid-rl"]
score: 6.0
evidence: 面向多任务操作策略的结构化技能基
tldr: 扩散策略在机器人操作中表现良好，但扩展到多任务场景时受模型规模与示范成本限制。本文提出技能专家混合策略SMP，学习紧凑的正交技能基，并用粘性路由在每步从少量相关专家中组合动作。方法配合变分训练目标与自适应专家激活，实现无需超大骨干的快速采样。在仿真与真实双臂平台的多任务与迁移任务中，SMP取得更高成功率。该工作为结构化技能表示的操作策略提供了高效方案。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 扩散策略扩展到多任务操作时受模型规模与示范成本限制。
method: 提出技能专家混合扩散策略，学习正交技能基并用粘性路由组合动作。
result: 在仿真与真实双臂平台的多任务和迁移任务中取得更高成功率。
conclusion: 该工作以结构化技能基实现高效多任务机器人操作策略学习。
---

## Abstract
Diffusion-based policies have recently shown strong results in robot manipulation, but their extension to multi-task scenarios is hindered by the high cost of scaling model size and demonstrations. We introduce Skill Mixture-of-Experts Policy (SMP), a diffusion-based mixture-of-experts policy that learns a compact orthogonal skill basis and uses sticky routing to compose actions from a small, task-relevant subset of experts at each step. A variational training objective supports this design, and adaptive expert activation at inference yields fast sampling without oversized backbones. We validate SMP in simulation and on a real dual-arm platform with multi-task learning and transfer learning tasks, where SMP achieves higher success rates and markedly lower inference cost than large diffusion baselines. These results indicate a practical path toward scalable, transferable multi-task manipulation: learn reusable skills once, activate only what is needed, and adapt quickly when tasks change.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向多任务操作策略的结构化技能基。

### 2. 核心内容
扩散策略在机器人操作中表现良好，但扩展到多任务场景时受模型规模与示范成本限制。本文提出技能专家混合策略SMP，学习紧凑的正交技能基，并用粘性路由在每步从少量相关专家中组合动作。方法配合变分训练目标与自适应专家激活，实现无需超大骨干的快速采样。在仿真与真实双臂平台的多任务与迁移任务中，SMP取得更高成功率。该工作为结构化技能表示的操作策略提供了高效方案。

### 3. 对应检索需求
robotic manipulation policies that leverage structured representations and reinforcement learning。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=VSWjHIveqZ](https://openreview.net/forum?id=VSWjHIveqZ)
