---
title: Efficient Reinforcement Learning by Guiding World Models with Non-Curated Data
title_zh: 利用非精选数据引导世界模型的高效强化学习
authors: "Yi Zhao, Aidan Scannell, Wenshuai Zhao, Yuxin Hou, Tianyu Cui, Le Chen, Dieter Büchler, Arno Solin, Juho Kannala, Joni Pajarinen"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://openreview.net/pdf?id=oBXfPyi47m"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 利用世界模型引导强化学习以提升样本效率
tldr: 针对离线数据提升在线强化学习样本效率时朴素微调失效的问题，本文扩展可用数据池，利用无奖励、混合质量且跨多种本体的非精选数据。作者诊断出离线与在线数据分布偏移是失败主因，提出经验回放与执行引导两项技术来有效利用离线数据训练世界模型。实验表明这些改进显著加速了在线强化学习训练，为低成本数据驱动的样本高效学习提供了可行方案。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 离线数据可提升在线强化学习样本效率，但朴素微调因分布偏移在多任务上失效。
method: 利用无奖励、混合质量、跨本体的非精选数据训练世界模型，并引入经验回放与执行引导。
result: 两项技术缓解了分布偏移，显著加速了在线强化学习训练。
conclusion: 世界模型引导结合非精选数据是实现样本高效强化学习的有效途径。
---

## Abstract
Leveraging offline data is a promising way to improve the sample efficiency of online reinforcement learning (RL).
This paper expands the pool of usable data for offline-to-online RL by leveraging abundant non-curated data that is reward-free, of mixed quality, and collected across multiple embodiments. Although learning a world model appears promising for utilizing such data, we find that naive fine-tuning fails to accelerate RL training on many tasks. Through careful investigation, we attribute this failure to the distributional shift between offline and online data during fine-tuning. To address this issue and effectively use the offline data, we propose two techniques: i) experience rehearsal and ii) execution guidance. With these modifications, the non-curated offline data substantially improves RL's sample efficiency. Under limited sample budgets, our method achieves nearly twice the aggregate score of learning-from-scratch baselines across 72 visuomotor tasks spanning 6 embodiments. On challenging tasks such as locomotion and robotic manipulation, it outperforms prior methods that utilize offline data by a decent margin.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
利用世界模型引导强化学习以提升样本效率。

### 2. 核心内容
针对离线数据提升在线强化学习样本效率时朴素微调失效的问题，本文扩展可用数据池，利用无奖励、混合质量且跨多种本体的非精选数据。作者诊断出离线与在线数据分布偏移是失败主因，提出经验回放与执行引导两项技术来有效利用离线数据训练世界模型。实验表明这些改进显著加速了在线强化学习训练，为低成本数据驱动的样本高效学习提供了可行方案。

### 3. 对应检索需求
Find methods that use structured world models to improve sample efficiency in robotic reinforcement learning.

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=oBXfPyi47m](https://openreview.net/forum?id=oBXfPyi47m)
