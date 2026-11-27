---
title: Gentle Manipulation Policy Learning via Demonstrations from VLM Planned Atomic Skills
title_zh: 基于视觉语言模型规划原子技能示范的轻柔操作策略学习
authors: "Jiayu Zhou, Qiwei Wu, Jian Li, Zhe Chen, Xiaogang Xiong, Renjing Xu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38955/42917"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 结合结构化技能分解的强化学习操作策略
tldr: 长时程接触丰富操作任务通常需要大量真实数据与专家工程，成本高且难以扩展。本文提出结合分层语义分解、强化学习、视觉语言模型与知识蒸馏的框架，将复杂任务分解为原子技能并在仿真中训练带显式力约束的强化学习策略。视觉语言模型负责高层任务分解与技能规划并生成示范。该方法在防止物体损伤的精细操作中实现高效策略学习，提升了可扩展性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 长时程接触丰富操作任务依赖大量真实数据与专家工程，成本高难扩展。
method: 提出分层语义分解结合强化学习、视觉语言模型与知识蒸馏的框架，含显式力约束。
result: 方法在仿真中训练带力约束的原子技能策略，实现精细接触操作的策略学习。
conclusion: 该框架以结构化技能分解降低了操作策略学习的成本并提升可扩展性。
---

## Abstract
Autonomous execution of long-horizon, contact-rich manipulation tasks traditionally requires extensive real-world data and expert engineering, posing significant cost and scalability challenges. This paper proposes a novel framework integrating hierarchical semantic decomposition, reinforcement learning (RL), visual language models (VLMs), and knowledge distillation to overcome these limitations. Complex tasks are decomposed into atomic skills, with RL-trained policies for each primitive exclusively in simulation. Crucially, our RL formulation incorporates explicit force constraints to prevent object damage during delicate interactions. VLMs perform high-level task decomposition and skill planning, generating diverse expert demonstrations. These are distilled into a unified policy via Visual-Tactile Diffusion Policy for end-to-end execution. We conduct comprehensive ablation studies exploring different VLM-based task planners to identify optimal demonstration generation pipelines, and systematically compare imitation learning algorithms for skill distillation. Extensive simulation experiments and physical deployment validate that our approach achieves policy learning for long-horizon manipulation without costly human demonstrations, while the VLM-guided atomic skill framework enables scalable generalization to diverse tasks.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究动机**：长时程、接触丰富的机器人操作任务通常依赖大量真实世界示范数据和专家工程，数据采集成本高、可扩展性差；同时，传统视觉感知难以捕捉精细接触动力学，现有 VLM 数据生成方法又多忽略触觉与接触力信息。
- **核心问题**：如何在**不依赖昂贵人类示范**的情况下，为长时程、接触丰富且需要“轻柔操作”的任务生成高质量示范，并学习可部署的端到端操作策略。
- **整体含义**：论文提出一个“仿真强化学习原子技能 + VLM 高层规划组合 + 视觉触觉扩散策略蒸馏”的闭环框架，试图同时解决数据瓶颈、力安全约束、多模态感知和长时程任务组合扩展问题。

## 2. 方法论

- **核心思想**：将复杂长时程任务分解为可复用的原子技能；每个原子技能在仿真中通过带力约束奖励的强化学习训练；再由 VLM 根据语言指令和场景图像规划原子技能序列，自动生成专家示范；最后用视觉-触觉扩散策略将示范蒸馏为统一端到端策略。
- **接触力建模**：将接触力分解为法向力、剪切力和扭矩，并据此设计“抓取、旋转、移动、横向移动、水平拉取”等原子技能，使技能与真实交互中的力模式对应。
- **原子技能训练**：
  - 使用 SAC 算法，在 Isaac Gym 仿真中训练，利用最大熵鼓励策略随机性，双 Q 网络降低估值偏差。
  - 采用域随机化，扰动物体初始位姿、质量和摩擦系数。
  - 动作空间为末端相对笛卡尔命令 `{ax, ay, az, arx, ary, arz, ac}`，其中平移/旋转沿 TCP 轴，`ac` 控制平行夹爪开合。
  - 每个技能设计单阶段奖励，并加入力惩罚项。以抓取为例：
    `R_Grasp = T - tanh(D_e) + PCp + Hr + Cr + Fp + Sr`
    其中 `T` 为时间惩罚，`D_e` 为夹爪到物体距离，`PCp` 惩罚过早闭合，`Cr` 鼓励接触，`Hr` 奖励抬升高度，`Fp` 惩罚过大接触力，`Sr` 为成功奖励。
- **VASK 数据生成框架**：
  - VLM 作为顶层规划器，知识库包含操作背景、原子技能库及每个技能的接触力描述和系统提示。
  - 输入自然语言任务描述与 RGB 图像，VLM 将任务分解为原子技能序列，例如“打开抽屉并放入物体”可规划为 `["Horizontal Pull", "Grasp", "Move", "Open"]`。
  - 数据生成分四阶段：初始化环境、VLM 规划技能序列、机器人执行并采集点云与接触力反馈、筛选满足任务完成且接触力较低的轨迹。
- **VT-DP 知识蒸馏**：
  - 基于 DP3，融合视觉点云与触觉点云；裁剪全局点云仅保留夹爪和操作物体，视觉点云降采样至 256 点，触觉点云至 128 点，并分别编码以保留模态特征。
  - 使用 Transformer 噪声预测网络，参数量约 13.27M；训练 100 步去噪，推理 10 步去噪；策略使用 8 步 horizon，2 步观测预测 5 步未来动作。
  - 仅需约 50 条高质量示范即可蒸馏长时程轻柔操作策略。

## 3. 实验设计

- **仿真环境与机器人系统**：Isaac Gym 仿真；真实平台为 UR5 机械臂、两个 GelSight Mini 触觉传感器、平行夹爪和 Intel RealSense D415 RGB-D 相机；触觉仿真采用 TacSL 软接触模型。
- **Benchmark 任务**：四个长时程操作任务：
  - Object Stack（OS）：抓取随机方块并堆叠到平台。
  - Open and Place（OP）：打开盒子并将物体放入。
  - Cabinet and Place（CP）：打开抽屉并将物体放入。
  - Pour Ball（PB）：抓取装有球的杯子并将球倒入碗中。
- **数据与 benchmark**：构建带语言标签的小规模视觉-触觉 3D 点云数据集，并提出 VT-DP 作为多模态模仿学习训练 benchmark。
- **对比与消融**：
  - 不同 VLM 规划器：Doubao-pro、Doubao-lite、Qwen-max、Qwen2.5-7B/32B/72B，评估原子技能规划与技能切换准确率。
  - 技能消融：VLM 直接生成末端 waypoint 和夹爪二值命令，不使用原子技能库。
  - 力感知消融：奖励中是否加入显式力惩罚，比较长时程执行中的接触力分布。
  - 示范数据来源对比：VASK+VT-DP、VLM Planning、人类示范+VT-DP。
  - 输入模态对比：RGB/点云 × 有/无触觉，即 DP、DP3、VT-DP 等变体。
  - 真实世界定性部署：展示 OP、OS、PB 等任务执行过程。

## 4. 资源与算力

- 文中明确提到：VT-DP 推理在 **RTX 3060 GPU** 上以 **28 Hz** 运行；模型约 **13.27M 参数**；训练约 **800 epochs** 收敛；训练使用 100 步去噪，推理使用 10 步去噪。
- 未明确说明：训练使用的 GPU 型号与数量、总训练时长、总算力消耗、并行环境数量、仿真训练总步数等。
- 因此，论文对推理硬件有说明，但**训练算力报告不完整**，难以评估整体计算成本与可复现性。

## 5. 实验数量与充分性

- 大致实验规模：
  - 5 个原子技能的成功率统计，成功率约 0.89–0.98。
  - 6 种 VLM 规划器 × 4 个任务，共 24 组轨迹生成成功率评估。
  - 3 种方法（VASK+VT-DP、VLM Planning、Human data+VT-DP）× 4 个任务，比较成功率、成功路径长度和平均接触力。
  - 4 种输入模态 × 4 个任务，每个任务 30 次试验，共约 480 次策略评估。
  - 力感知消融：4 个任务 × 2 种策略 × 10 次试验的接触力分布比较。
  - 真实世界定性部署展示。
- **充分性**：消融维度较全面，覆盖规划器、技能库、力约束、数据来源和输入模态；表 4 明确每任务 30 次试验，并保证相同示范数量和数据生成模型，公平性较好。
- **不足**：真实世界仅定性展示，缺少成功率、接触力和试验次数统计；部分表格未报告每任务试验次数与置信区间；未做统计显著性检验；仅单一机器人平台、单一触觉传感器配置和四个仿真任务，跨物体、跨场景泛化验证有限；VLM 商业模型版本、提示细节和随机性控制未充分披露。

## 6. 主要结论与发现

- VASK+VT-DP 在四个仿真任务上的平均成功率约 **0.79**，显著优于 VLM 直接规划（约 0.375）和人类示范+VT-DP（约 0.41）。
- VASK+VT-DP 的成功路径长度更短，平均接触力更低；例如 OS 平均接触力约 0.322 N，而人类数据方法约 0.809 N，说明自动生成数据更平滑、更轻柔。
- 力感知奖励能持续降低并稳定长时程操作中的接触力，验证显式力约束对轻柔操作有效。
- VLM 规划器性能差异明显：Doubao-vision-pro 平均成功率约 0.713，表现最佳；Qwen2.5-7B 仅约 0.033，说明模型规模和指令跟随能力影响规划稳定性。
- 输入模态方面，视觉点云+触觉的 VT-DP 平均成功率约 0.79，优于仅视觉点云（约 0.58）和 RGB 方法（约 0.26–0.28），表明触觉对接触丰富任务关键。
- 真实机器人定性部署验证了数字孪生、点云对齐和触觉降采样流程的可行性。

## 7. 优点

- **数据生成闭环有创新性**：将 RL 原子技能、VLM 组合规划和扩散策略蒸馏结合，减少对人工示范的依赖。
- **显式力感知**：在奖励中加入力惩罚，并将接触力信息纳入技能库和示范筛选，直接面向“轻柔操作”和安全交互。
- **原子技能可组合、可扩展**：同一技能库可组合出不同序列长度的长时程任务，具备较好的任务扩展性。
- **多模态策略设计合理**：视觉点云提供空间几何，触觉点云提供接触细节，分别编码后融合，优于单模态基线。
- **示范效率高**：仅约 50 条高质量示范即可蒸馏策略，数据效率较高。
- **实验消融较系统**：覆盖 VLM 选择、技能库、力约束、数据来源和输入模态，结论相互支撑。
- **真实部署考虑工程细节**：使用数字孪生、坐标统一、模拟机械臂点云融合、颜色阈值裁剪和触觉对齐，提升 sim-to-real 可行性。

## 8. 不足与局限

- **真实世界验证不足**：仅定性展示，缺少真实任务成功率、接触力统计、失败模式和多次试验的定量评估。
- **力约束是软约束**：通过奖励惩罚鼓励低接触力，并非硬安全约束，不能从理论上保证绝不损伤物体。
- **仿真依赖较强**：原子技能训练依赖全状态可观测和 TacSL 触觉仿真，真实触觉点云需对齐与降采样，sim-to-real gap 仍存在。
- **VLM 引入额外开销与不稳定性**：论文承认 VLM 增加计算开销，且存在幻觉；最终需蒸馏来稳定策略，但 VLM 规划失败会直接影响示范质量。
- **实验覆盖有限**：仅四个仿真任务、单一 UR5 平台和特定触觉传感器；未系统评估新物体、新场景、新技能组合和更长序列的泛化。
- **公平性与可复现性风险**：人类示范质量受采集者影响，论文将其作为低质量数据解释，但未详细说明采集者数量和技能水平；商业 VLM 版本与提示细节披露有限。
- **算力报告不完整**：未给出训练 GPU 数量、总时长和仿真环境规模，影响成本评估与复现。
- **应用限制**：当前更适合结构化仿真任务和有限技能库场景；开放环境中物体多样性、遮挡、传感器噪声和长时程误差累积仍是挑战。

（完）
