---
title: Towards Affordance-Aware Robotic Dexterous Grasping with Human-like Priors
title_zh: 面向可供性感知的类人先验机器人灵巧抓取
authors: "Haoyu Zhao, Linghao Zhuang, Xingyue Zhao, Cheng Zeng, Haoran Xu, Yuming Jiang, Jun Cen, Kexiang Wang, Jiayan Guo, Siteng Huang, Xin Li, Deli Zhao, Hua Zou"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38313/42275"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 模仿人手运动先验并结合残差学习实现可供性感知灵巧抓取
tldr: 针对以往灵巧抓取方法只关注低层抓取稳定性、忽视可供性定位与类人姿态的问题，论文提出AffordDex两阶段框架，先在大规模人手运动数据上预训练轨迹模仿器获得自然运动先验，再训练残差模块适配可供性。实验表明该策略在多样物体上兼顾抓取稳定性、可供性定位与类人姿态，下游操作表现更佳，为通用灵巧抓取提供了新范式。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 以往灵巧抓取方法只关注低层抓取稳定性，忽视可供性定位与类人姿态，限制了下游操作能力。
method: 提出AffordDex两阶段框架，先在大规模人手运动数据上预训练轨迹模仿器获得自然运动先验，再训练残差模块适配可供性。
result: 实验表明该策略在多样物体上兼顾抓取稳定性、可供性定位与类人姿态，下游操作表现更佳。
conclusion: 该工作将运动先验与物体可供性结合，为通用灵巧抓取与操作提供了新范式。
---

## Abstract
A dexterous hand capable of generalizable grasping objects is fundamental for the development of general-purpose embodied AI. However, previous methods focus narrowly on low-level grasp stability metrics, neglecting affordance-aware positioning and human-like poses which are crucial for downstream manipulation.  To address these limitations, we propose AffordDex, a novel framework with two-stage training that learns a universal grasping policy with an inherent understanding of both motion priors and object affordances.  In the first stage, a trajectory imitator is pre-trained on a large corpus of human hand motions to instill a strong prior for natural movement. In the second stage, a residual module is trained to adapt these general human-like motions to specific object instances. This refinement is critically guided by two components: our Negative Affordance-aware Segmentation (NAA) module, which identifies functionally inappropriate contact regions, and a privileged teacher-student distillation process that ensures the final vision-based policy is highly successful. Extensive experiments demonstrate that AffordDex not only achieves universal dexterous grasping but also remains remarkably human-like in posture and functionally appropriate in contact location. As a result, AffordDex significantly outperforms state-of-the-art baselines across seen objects, unseen instances, and even entirely novel categories.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究背景**：灵巧手是实现通用具身智能的重要基础，但高自由度带来的控制难度使传统规划方法难以适用，近年来主流转向强化学习与模仿学习。
- **核心问题**：已有灵巧抓取方法多聚焦“抓得稳、抬得起”等低层稳定性指标，忽视了两类对下游操作至关重要的因素：
  - **可供性感知的接触位置**：例如应抓刀柄而非刀刃；
  - **类人抓取姿态与运动**：自然、可预测的动作更利于后续操作和人机协作。
- **整体含义**：论文主张抓取不应只是几何稳定，还应满足功能正确性与类人运动先验。为此提出 **AffordDex**，将“人手运动先验”和“负可供性约束”结合，学习可泛化的灵巧抓取策略。

## 2. 方法论

- **核心思想**：采用两阶段训练，将“自然性”和“功能正确性”解耦后再协同：
  - 第一阶段学习人手运动先验，使策略落在自然动作流形上；
  - 第二阶段用残差学习适配具体物体，并由负可供性模块约束“不能碰哪里”。
- **第一阶段：人手轨迹模仿**
  - 在大规模人手运动数据上预训练基础策略 \(\pi_H\)。
  - 状态包括机器人状态 \(R_t\)、物体状态 \(O_t\)、物体点云 \(P_t\)。
  - 奖励由手指模仿奖励与平滑奖励组成：手指关键点与 MANO 手对应关键点距离越小奖励越高；平滑奖励惩罚过大关节速度与力矩。
- **第二阶段：负可供性感知分割（NAA）**
  - 对原始网格进行程序化纹理生成，再从六个主方向渲染多视图图像。
  - 用 GPT-4V 生成物体的“负可供性”描述，即不应接触的区域，如刀刃。
  - 用 SAM 在稠密网格点上生成候选掩码，经 NMS 去重；再用 CLIP 计算每个掩码图像与文本描述的相似度，选择最匹配掩码。
  - 将掩码投影回 3D 点云，得到负可供性点集 \(N_t\)。该过程为离线一次性处理，约 160 秒/物体。
- **第二阶段：可供性感知残差学习**
  - 冻结 \(\pi_H\)，训练状态-based 教师策略 \(\pi_T\)，输入 \(R_t,O_t,P_t,N_t\)，通过 PPO 学习残差动作。
  - 最终动作：\(a_t=\pi_H(S_t^T)+\pi_T(S_t^T)\)。
  - 奖励形式：\(r_T=-r_d-r_g+r_s-r_n\)，其中 \(r_d\) 鼓励手接近物体，\(r_g\) 鼓励物体到达目标，\(r_s\) 为成功奖励，\(r_n\) 惩罚手接近负可供性区域。
  - 再用 DAgger 将教师蒸馏为视觉学生策略 \(\pi_S\)，学生仅使用 \(R_t,P_t,N_t\)，以缩小仿真特权信息与真实视觉输入之间的差距。

## 3. 实验设计

- **仿真平台**：IsaacGym，使用 Shadow Hand，24 个主动自由度（腕部 6 个、手指 18 个）。
- **数据集 / 场景**：
  - **UniDexGrasp**：3165 个物体、133 类；评估 seen objects、seen categories 下的 unseen objects、unseen categories。文中还出现“3200 seen objects”的表述，与 3165 存在轻微不一致。
  - **OakInk2**：约 2200 条右手操作序列用于预训练 \(\pi_H\)，并用于跨数据集泛化评估。
- **Benchmark 指标**：
  - **Succ**：200 步内将物体送达目标即成功。
  - **HLS**：用 Gemini 2.5 Pro 分析抓取视频序列，评估动作类人程度。
  - **AS**：基于 100 个负可供性采样点评估接触功能正确性；表中标为“↓”，但正文描述为“指尖远离负可供性点则加分”，存在指标方向与文字表述不一致。
- **对比方法**：PPO、DAPG、GSL、ILAD、UniDexGrasp、UniDexGrasp++、DexGrasp Anything。
- **实验设置**：state-based 与 vision-based 两种输入；覆盖 seen object、unseen object、unseen category、OakInk2；并包含定性对比与消融实验。

## 4. 资源与算力

- 文中明确提到：
  - 训练时在 **NVIDIA RTX 4090 GPU** 上并行模拟 **4096 个环境**。
  - NAA 模块在 **RTX 4090** 上约 **160 秒/物体**。
- **未明确说明**：GPU 总数、总训练时长、总 GPU 小时、存储与能耗等。因此无法准确评估完整训练成本。

## 5. 实验数量与充分性

- **实验组数概览**：
  - 主实验覆盖 UniDexGrasp 与 OakInk2 两个数据集；
  - 包含 state-based 与 vision-based 两类策略；
  - 覆盖 seen object、unseen object、unseen category 三类泛化；
  - 对比 7 类基线方法；
  - 消融 HTI、NAA、Teacher-student Distillation 三个核心组件；
  - 额外验证将 HTI 与 NAA 迁移到 UniDexGrasp++ 的增益；
  - 提供多组定性可视化。
- **充分性**：在仿真环境下，实验覆盖面较广，主实验、消融和迁移实验相互支撑，能较好说明各模块作用。
- **客观性与公平性风险**：
  - HLS 由 Gemini 2.5 Pro 自动评分，带有模型主观偏差；
  - AS 的指标定义与表格箭头方向不一致，可能影响解读；
  - DexGrasp Anything 只生成静态抓取姿态，HLS 不适用，比较维度不完全一致；
  - 缺少真实机器人实验与失败案例分析。

## 6. 主要结论与发现

- AffordDex 在 seen objects、unseen instances、unseen categories 以及 OakInk2 上均取得更高的抓取成功率，优于 UniDexGrasp、UniDexGrasp++ 等基线。
- 人手轨迹模仿显著提升抓取成功率和类人程度；去掉 HTI 后策略虽可能抓稳，但动作不自然。
- NAA 能有效引导策略避开刀刃等功能上不合适的区域，显著改善可供性评分。
- 教师-学生蒸馏对视觉策略尤为关键，缺少特权信息指导时视觉策略成功率明显下降。
- HTI 与 NAA 也可迁移到其他 RL 抓取方法（如 UniDexGrasp++），说明模块具有一定通用性。

## 7. 优点

- **问题切入有价值**：从“抓稳”推进到“抓得自然、抓得功能正确”，更贴近下游操作需求。
- **方法解耦清晰**：人手先验负责自然性，负可供性负责功能约束，残差学习负责物体适配。
- **负可供性建模巧妙**：将分割转化为“SAM 候选掩码 + CLIP 分类选择”，规避 MLLM 细粒度定位弱的问题。
- **训练流程完整**：状态教师 + 视觉学生蒸馏，兼顾仿真性能与视觉策略可部署性。
- **实验较系统**：多数据集、多泛化划分、多基线、消融与迁移实验结合，结论有较好支撑。

## 8. 不足与局限

- **仅仿真验证**：未展示真实机器人部署，存在仿真到现实差距。
- **依赖外部大模型**：NAA 依赖 GPT-4V、SAM、CLIP 与程序化纹理，错误会级联；六视图渲染也可能遗漏复杂凹面区域。
- **离线成本较高**：约 160 秒/物体，虽为一次性处理，但大规模物体库上成本不可忽视。
- **指标存在歧义**：AS 的文字定义与表格方向不一致；HLS 依赖 Gemini 自动评分，主观性和可复现性有限。
- **实验覆盖有限**：仅 Shadow Hand、右手数据；未系统评估不同手型、双臂、真实传感器噪声与动态下游任务。
- **负可供性较粗粒度**：主要告诉策略“不能碰哪里”，对“应如何为特定任务抓取”的正向任务可供性建模仍不足。
- **资源报告不完整**：缺少总 GPU 数、训练时长和完整计算预算。

（完）
