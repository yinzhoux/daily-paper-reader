---
title: "ManipLVM-R1: Reinforcement Learning for Reasoning in Embodied Manipulation with Large Vision-Language Models"
title_zh: ManipLVM-R1：面向具身操作推理的强化学习
authors: "Zirui Song, Guangxian Ouyang, Mingzhe Li, Yuheng Ji, Chenxi Wang, Zixiang Xu, Zeyu Zhang, Xiaoqing Zhang, Qian Jiang, Fengxian Ji, Zhenhao Chen, Zhongzhi Li, Xiuying Chen"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38922/42884"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 面向具身操作的大视觉语言模型强化学习推理
tldr: 针对大视觉语言模型在机器人操作中依赖昂贵人工标注、域外泛化不足的问题，论文提出ManipLVM-R1强化学习框架，用可验证奖励替代传统监督。该方法直接以任务对齐结果优化模型，增强物理推理与泛化能力，并降低对标注数据的依赖。工作表明强化学习可提升具身操作中视觉语言模型的适应性与推理表现，为机器人操作策略学习提供了新路径。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有基于大视觉语言模型的机器人操作依赖昂贵标注，域外泛化能力不足。
method: 提出ManipLVM-R1，用可验证奖励强化学习替代监督，直接优化任务对齐结果。
result: 摘要称该方法提升泛化与物理推理并减少标注依赖，具体实验数值未给出。
conclusion: 为具身操作中利用强化学习提升视觉语言模型适应性提供了框架。
---

## Abstract
Large Vision-Language Models (LVLMs) have recently advanced robotic manipulation by leveraging vision for scene perception and language for instruction following.
However, existing methods rely heavily on costly human-annotated training datasets, which limits their generalization and causes them to struggle in out-of-domain (OOD) scenarios, reducing real-world adaptability. To address these challenges, we propose ManipLVM-R1, a novel reinforcement learning framework that replaces traditional supervision with Reinforcement Learning using Verifiable Rewards (RLVR). By directly optimizing for task-aligned outcomes, our method enhances generalization and physical reasoning while removing the dependence on costly annotations. Specifically, we design two rule-based reward functions targeting key robotic manipulation subtasks: an Affordance Perception Reward to enhance localization of interaction regions, and a Trajectory Match Reward to ensure the physical plausibility of action paths. These rewards provide immediate feedback and impose spatial-logical constraints, encouraging the model to go beyond shallow pattern matching and instead learn deeper, more systematic reasoning about physical interactions. Experimental results show that ManipLVM-R1 achieves substantial performance gains across multiple manipulation tasks, using only 50% of the training data while achieving strong generalization to OOD scenarios. We further analyze the benefits of our reward design and its impact on task success and efficiency.

---

## 论文详细总结（自动生成）

# ManipLVM-R1 论文结构化总结

## 1. 核心问题与研究动机

- **背景**：大视觉语言模型（LVLM）已被用于机器人操作，依靠视觉做场景感知、语言做指令跟随，但多数工作集中在高层规划、动作序列化或视觉推理，对底层决策与物理动力学关注不足。
- **核心痛点一：标注依赖**。以 RoboBrain 为代表的路线通过"专家演示 + 语言模型生成思维链（CoT）"做监督微调（SFT），效果虽好但需要大量昂贵的人工/合成标注，且对未见场景泛化差。
- **核心痛点二：RLVR 迁移困难**。可验证奖励强化学习（RLVR）在数学、编程等可自动校验领域已获成功，但直接搬到机器人操作面临两个障碍：(a) 奖励稀疏、延迟；(b) 传统标量反馈缺乏空间-逻辑结构，无法有效引导视动学习，模型容易停留在浅层模式匹配。
- **整体含义**：论文试图用"结构化可验证奖励"替代"昂贵人工标注"，让 LVLM 在具身操作中学会更系统、更具物理落地性的推理，并提升域外（OOD）适应性。

## 2. 方法论

### 核心思想
- 提出 **ManipLVM-R1**：一个基于 RLVR 的框架，把整体操作任务**解耦为两个子任务**——可供性感知（affordance perception）与轨迹预测（trajectory prediction），分别训练独立模型，以获得更聚焦的学习信号与更好的物理接地。
- 用任务对齐的**规则化奖励**直接优化结果，无需 CoT 标注。

### 关键技术细节
- **策略采样**：给定图像编码 x 与指令 q，当前策略 π_θ 采样 G 条不同回复 {o₁,…,o_G}，每条用对应奖励函数打分。
- **可供性感知奖励**：
  - `R_spatial = R_format + R_aff`
  - `R_format`：要求输出结构为 `<think>…</think>` + `<answer>…</answer>`，answer 内含预测框坐标；合规得 1，否则 0。
  - `R_aff = IoU(b*, b̂)`，即预测框与真值框的交并比，鼓励空间精确、语义接地的定位。
- **轨迹匹配奖励**：
  - 模型输出 2D 坐标序列 T̂={p̂₁,…,p̂_N}（图像坐标系，左上角为原点），与真值 T* 比较。
  - `R_trajectory = R_format + R_path + R_end`
  - `R_format`：除标签结构外，额外约束预测点数量在 3–10 之间，保证简洁与可解释。
  - `R_path = R_DFD + R_HD + R_RMSE`：分别由离散 Fréchet 距离（整体形状与时间对齐）、Hausdorff 距离（最大逐点偏差）、RMSE（平均逐点误差）归一化到 [0,1] 后聚合。动机是纠正行为克隆类方法"只重终点、忽略路径质量"的缺陷。
  - `R_end = exp(−k‖p̂_N − p*_M‖₂)`：终点欧氏距离的指数衰减奖励，k 为衰减系数。
- **策略更新（GRPO 式）**：
  - 组内归一化计算优势：`A_i = (r_i − mean({r₁…r_G})) / std({r₁…r_G})`。
  - 提升高奖励回复的似然、抑制低奖励回复，并用与参考模型 π_ref 的 KL 散度约束训练稳定性；总目标为 `max E[R(q,o) − β·KL(π_θ‖π_ref)]`。

## 3. 实验设计

- **In-Domain 数据集**：ShareRobot（源自 Open X-Embodiment），含 100 万+ 规划 QA 对、6.5k 张稠密可供性标注图像、6.8k 帧轨迹标注，覆盖 102 个真实场景、12 种机器人本体。**关键设定：所有 SFT 基线用全量训练集，ManipLVM-R1 只用 50%。**
- **OOD 数据集**：
  - 可供性：UMD Part Affordance，选取 grasp / cut / pound / scoop 四类，均衡采样 1200 张测试图。
  - 轨迹：VAIT 验证集 500 例（源自 Open X-Embodiment），作者做了人工可视化校验与标注修正以去除噪声。
- **评价指标**：
  - 可供性：任务成功率（IoU > 50% 记为成功）+ 平均 IoU。
  - 轨迹：成功率（终点落在真值 20 像素内）+ DFD、HD、RMSE 及其均值。
- **对比方法**：
  - 开源零样本/少样本：Phi-4-multimodal-Instruct、Gemma-3-4B/12B/27B-it、Qwen2.5-VL-3B/7B/32B-Instruct、LLARVA、VILA1.5-13B。
  - 全监督微调：LLaVA-1.6-7B、InternVL2-2B、Qwen2.5-VL-3B-Instruct(SFT)、RoboBrain-7B（同为可供性+轨迹任务、基于大规模合成 CoT 微调，是最强对照）。

## 4. 资源与算力

- **论文正文（含摘要、方法、实验、结论）未提及任何算力信息**：没有 GPU 型号、数量、训练时长、采样数 G、batch size、学习率等超参细节。
- 仅能推断基座为 Qwen2.5-VL-3B（由命名 ManipLVM-R1-3B 及图 1 对比项可知），但训练开销无法评估，这对复现与成本对比构成明显信息缺口。

## 5. 实验数量与充分性

- **规模**：核心为两组主实验（In-Domain 表 1、OOD 表 2），共 14 个基线 + 1 个自研模型；另有图 1 的数据量-性能曲线（50% 数据对比）与图 3 的定性案例分析（含成功"aha moment"与失败案例）。
- **充分性评价**：
  - 优点：ID/OOD 双设定、覆盖 4 类可供性语义 + 轨迹多指标、同时对比开源与全监督两条基线线，且 RoboBrain-7B 是强同任务对照，比较对象选择较为客观；自研模型只用 50% 数据，属于"劣势条件对比"，公平性尚可。
  - 不足：**正文中没有奖励组件的消融表**（虽然摘要/结论声称"分析了奖励设计的收益"，但提取文本中未见量化消融）；未报告多随机种子的均值/方差或置信区间；只训练并评测了 3B 一个规模，缺少规模缩放研究；未与"用 50% 数据训练的 SFT 基线"做严格等数据量对照（50% 只对自研模型生效，反向削弱了"样本效率"论断的严密性）；失败案例仅定性展示，未做错误类型的定量统计。

## 6. 主要结论与发现

- **ID 结果**：ManipLVM-R1-3B 可供性 IoU 达 **31.0**（RoboBrain-7B 仅 11.79，Qwen2.5-VL-32B 仅 7.40），成功率 0.21；轨迹平均误差 **110.87**，成功率 0.28。相对最强监督基线，IoU 提升约 **144%**，轨迹精度提升约 **12.5%**。
- **OOD 结果**：可供性成功率 0.24、Grasp-IoU 34.65（四类中最高）、其余子类 23.5–28.3；VAIT 轨迹平均误差 **131.99** 为全场最低，优于 Qwen2.5-VL-32B-Instruct 与 RoboBrain-7B。
- **核心发现**：结构化、可验证的规则奖励能够在不依赖 CoT 标注的前提下激发潜在的空间推理与目标对齐能力；出现无显式思维链监督的"aha moment"式多步推理（如自主推断需匹配形状与颜色再定位插槽）。
- **局限发现**：失败主要源于常识缺口（把"钥匙孔"而非"门把手"当作交互点）与空间误感知（夹爪相对灶台位置判断错误），且模型缺乏自验证机制，推理期误差会累积。

## 7. 优点

- **范式上有价值**：把 RLVR 从数学/代码迁移到具身操作，明确论证了"奖励需要空间-逻辑结构"这一设计原则，而非简单套用标量奖励。
- **奖励设计细致且有物理含义**：可供性用 IoU 直接对齐交互区域；轨迹同时约束形状（DFD）、最坏偏差（HD）、平均误差（RMSE）与终点精度，弥补行为克隆"只顾终点"的通病。
- **样本效率与泛化兼顾**：仅用 50% 数据即超越全量监督的 7B 模型，OOD 上仍领先，论点与实验相互支撑。
- **评测工程较扎实**：OOD 的 VAIT 子集做了人工清洗与标注修正，避免噪声标签污染结论；指标定义（IoU>50%、20 像素终点阈值）清晰可复现。
- **定性分析坦诚**：既展示成功推理链，也公开失败案例并归因，可信度较高。

## 8. 不足与局限

- **绝对性能仍偏低**：成功率仅 21%–28%，距实际部署差距明显；IoU 31.0 虽为相对最优但绝对水平有限。
- **"操作"闭环缺失**：轨迹仅为图像空间 2D 坐标序列，未接入真实机器人执行或 3D/深度信息，所谓"task success"实为离线几何指标，与真实操作成功率之间存在鸿沟。
- **奖励依赖真值**：R_aff 与 R_path/R_end 均需 ground-truth 框与轨迹，奖励并非真正"无监督"，只是把标注成本从 CoT 转移到几何标注；对无标注新任务的可扩展性未被验证。
- **公式与表述不一致**：R_path 文字称"加权聚合"，公式却写作三项直接相加；归一化方式、权重、衰减系数 k 的具体取值均未给出，复现困难。
- **实验覆盖不足**：缺奖励消融、缺多规模对比、缺种子方差、缺与等数据量 SFT 的严格对照；OOD 只覆盖 4 类可供性与 1 个轨迹子集。
- **风险面未讨论**：格式奖励与内容奖励相加可能诱发"刷格式分"的奖励黑客行为；KL 约束强度 β 的敏感性未分析；模型缺乏自验证，常识型错误（门把手/钥匙孔）说明具身常识接地仍是瓶颈。
- **算力信息完全缺失**，不利于成本评估与工业界复用判断。

（完）
