---
title: Coordinated Humanoid Robot Locomotion with Symmetry Equivariant Reinforcement Learning Policy
title_zh: 基于对称等变强化学习策略的人形机器人协调运动
authors: "Buqing Nie, Yang Zhang, Rongjun Jin, Zhanxiang Cao, Huangxuan Lin, Xiaokang Yang, Yue Gao"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38918/42880"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 面向人形机器人协调运动的深度强化学习策略
tldr: 针对现有人形机器人深度强化学习方法忽视机器人形态对称性、导致动作不协调与性能次优的问题，论文提出对称等变策略SE-Policy，在actor中嵌入严格对称等变、在critic中嵌入对称不变且无需额外超参数。实验在速度跟踪任务上表明该策略产生时空协调的运动并取得更高任务性能，为强化学习控制人形机器人提供了有效思路。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有人形机器人深度强化学习方法忽视机器人形态对称性，导致动作不协调、性能次优。
method: 提出对称等变策略SE-Policy，在actor中嵌入严格对称等变、在critic中嵌入对称不变，无需额外超参数。
result: 实验在速度跟踪任务上表明该策略产生时空协调的运动，任务性能更高。
conclusion: 该工作将形态对称性引入强化学习策略结构，为人形机器人协调运动控制提供了有效思路。
---

## Abstract
The human nervous system exhibits bilateral symmetry, enabling coordinated and balanced movements. However, existing Deep Reinforcement Learning (DRL) methods for humanoid robots neglect morphological symmetry of the robot, leading to uncoordinated and suboptimal behaviors. Inspired by human motor control, we propose Symmetry Equivariant Policy (SE-Policy), a new DRL framework that embeds strict symmetry equivariance in the actor and symmetry invariance in the critic without additional hyperparameters. SE-Policy enforces consistent behaviors across symmetric observations, producing temporally and spatially coordinated motions with higher task performance. Extensive experiments on velocity tracking tasks, conducted in both simulation and real-world deployment with the Unitree G1 humanoid robot, demonstrate that SE-Policy improves tracking accuracy by up to 40% compared to state-of-the-art baselines, while achieving superior spatial-temporal coordination. These results demonstrate the effectiveness of SE-Policy and its broad applicability to humanoid robots.

---

## 论文详细总结（自动生成）

## 一、论文核心问题与整体含义

- **研究背景**：人形机器人具有天然的双侧形态对称性，人类运动控制也依赖双侧对称来实现协调与平衡。然而，现有基于深度强化学习（DRL）的人形机器人控制方法通常把策略视为黑箱，未显式利用机器人形态对称性。
- **核心问题**：传统 DRL 策略对对称等价的观测可能输出不一致、不对称的动作，导致左右关节运动风格不一致、步态不协调、轨迹偏移和任务性能次优。
- **整体含义**：论文希望将人形机器人形态对称性作为先验嵌入策略网络结构，使策略在对称观测下产生严格对称动作，从而获得更自然、更协调、更高精度的运动控制。
- **现有方法不足**：
  - 时间对称方法（如周期相位、CPG）主要改善步态周期性，约束较弱。
  - 数据增强和损失正则化只能诱导“软等变”，推理时仍可能被违反，且正则项可能引入额外超参数并干扰优化。
  - 严格等变方法多在经典控制或仿真任务中验证，在真实人形机器人上的有效性仍缺乏研究。

## 二、论文提出的方法论

### 1. 核心思想

- 提出 **Symmetry Equivariant Policy（SE-Policy）**：在 actor 中嵌入**严格对称等变**，在 critic 中嵌入**对称不变**，且不引入额外超参数。
- 基本假设：人形机器人结构具有反射对称性，因此对应 MDP 的转移概率和奖励函数在对称变换下保持不变，最优策略应满足对称等变性，最优价值函数应满足对称不变性。

### 2. 对称性建模

- 将机器人控制建模为 MDP：\(\mathcal{M}=\langle S,O,A,P,R,\gamma\rangle\)。
- 定义状态、观测和动作的对称变换函数分别为 \(F_s\)、\(F_o\)、\(F_a\)。
- 论文给出的关键性质包括：
  - 转移概率不变：\(P(F_s(s')\mid F_s(s),F_a(a))=P(s'\mid s,a)\)。
  - 奖励函数不变：\(R(F_s(s),F_a(a))=R(s,a)\)。
  - 最优 critic 不变：\(Q(F_s(s),F_a(a))=Q(s,a)\)，\(V(F_s(s))=V(s)\)。
  - 最优策略等变：\(\pi^*(F_s(s))=F_a(\pi^*(s))\)。
- 直观例子：机器人以左脚支撑、右脚悬空时，最优动作是放下右脚；对称状态下则应放下左脚。

### 3. 观测与动作空间

- 观测维度为 96，主要包括：
  - 基座角速度；
  - 投影重力；
  - 速度指令 \((c_x,c_y,c_\omega)\)；
  - 关节位置、关节速度；
  - 上一时刻动作；
  - 相位输入 \(\Phi=(\Phi_{\sin},\Phi_{\cos})\)；
  - 高度图 \(H\)，仅用于 critic。
- 动作空间为 27 维，表示 27 个关节的目标位置。
- 表 1 给出了各分量的反射对称变换规则，例如左右手臂/腿部关节互换并取负、速度指令的 \(y\) 和角速度分量取负、相位输入取负等。

### 4. 网络架构

- 整体架构受 DreamWaQ 启发，包括：
  - 历史编码器 \(f_{en}\)；
  - 观测解码器 \(f_{de}\)；
  - 策略网络 \(f_\pi\) 作为 actor；
  - 价值网络 \(V\) 作为 critic。
- actor 基于时间历史观测 \(o_{[t-h:t]}\) 编码潜变量 \(z\)，再结合当前观测 \(o_t\) 输出动作：\(a_t=f_\pi(o_t,z)\)。
- 历史编码器通过预测下一观测进行训练：
  \[
  \mathcal{L}_{AE}=\mathrm{MSE}(\hat{o},o_{t+1}),\quad \hat{o}=f_{de}(f_{en}(o_{[t-h:t]}))
  \]
- 为保证潜变量也参与对称等变，论文定义了潜变量 \(z\) 的对称变换 \(F_z\)：在偶数长度下，奇数索引与相邻偶数索引交换。
- 所有网络使用 Linear + ReLU 构造等变 MLP，参考 ESCNN 通过参数共享实现等变性。
- actor 输入和输出分别按观测对称变换和动作对称变换构造；critic 对输入观测和高度图的对称变换保持输出不变。

### 5. 训练框架

- 主体训练流程与 PPO 一致。
- critic 使用 MSE 损失：
  \[
  \mathcal{L}_V=\mathrm{MSE}(V(H_t,o_t),y)
  \]
  其中 \(y\) 为 reward-to-go。
- actor 使用自编码重建损失 \(\mathcal{L}_{AE}\) 与 PPO 损失：
  \[
  \mathcal{L}_{PPO}=\mathbb{E}_D[\min(\rho_\pi A(s,a),g(\rho_\pi)A(s,a))]
  \]
  其中 \(\rho_\pi=\pi(a\mid o,H)/\pi_{old}(a\mid o,H)\)，并使用裁剪操作限制更新幅度。
- 奖励包括速度跟踪、平衡维持和动作平滑/力矩约束等正则项。
- 训练中使用课程学习，逐步增加地形、任务指令和传感器噪声难度；同时使用域随机化以支持 sim-to-real。

## 三、实验设计

### 1. 实验平台与场景

- 机器人：**Unitree G1**，27 自由度人形机器人。
- 仿真环境：**NVIDIA Isaac Gym**。
- 任务：速度跟踪任务，机器人需跟踪随机速度指令。
- 仿真中速度指令范围：
  - \(|v_x|<0.8\,\mathrm{m/s}\)
  - \(|v_y|<0.8\,\mathrm{m/s}\)
  - \(|\omega|<0.5\,\mathrm{rad/s}\)
- 真实世界实验：通过 sim-to-real 部署到真实 G1，跟踪多个速度指令并保持不越界；还在草地、坡面、沙地、石块等非结构化地形上测试通过能力。

### 2. Benchmark 与对比方法

- 对比方法包括：
  1. **DreamWaQ**：当前先进的腿足机器人无模型 DRL 运动控制方法。
  2. **DreamWaQ-Regu**：在 DreamWaQ 中加入对称正则项：
     \[
     \mathcal{L}_{reg}=\left\|\pi(F_o(o_{[t-h:t]}))-F_a(\pi(o_{[t-h:t]}))\right\|^2
     \]
     用于惩罚双侧关节的不对称驱动。
  3. **SE-Policy（actor only）**：消融版本，将 SE-Policy 的 critic 替换为普通 MLP critic，用于研究 critic 对称不变性的作用。
- 所有方法保持相同超参数和环境，训练超过 5K 次迭代。

### 3. 评价指标

- **TE-Velocity / TE-V**：命令速度与实际速度向量的平均差异。
- **TE-Position / TE-P**：实际位置与期望位置误差。
- **TE-Orientation / TE-O**：实际朝向与期望方向的角度偏差。
- **Temporal Symmetry / Temp-S**：当前关节动作与后续半周期对应关节动作的差异，衡量时间周期对称性。
- **Spatial Symmetry / Spat-S**：策略输出与对称观测下对称动作之间的差异，直接衡量策略的对称等变性。
- 上述指标均为越低越好。

## 四、资源与算力

- 论文明确提到：所有方法训练超过 **5K iterations**，约 **4 小时**，使用 **NVIDIA RTX 4090 GPU**。
- 论文表述为 “NVIDIA RTX 4090 GPU devices”，但**未明确说明 GPU 数量**。
- 未给出总 GPU 小时、显存占用、并行环境数量等更细算力信息。
- 因此，算力信息部分可总结为：训练时长和 GPU 型号有说明，但 GPU 数量与总算力开销未明确披露。

## 五、实验数量与充分性

### 1. 实验类型

论文大致包含以下几类实验：

- **仿真定量对比实验**：DreamWaQ、DreamWaQ-Regu、SE-Policy、SE-Policy（actor only）在速度跟踪任务上的 TE-V、Temp-S、Spat-S 对比。
- **跟踪误差随时间变化实验**：TE-P 和 TE-O 随运动时间的变化曲线。
- **八方向轨迹可视化实验**：机器人从中心向八个方向运动，比较理想轨迹与实际轨迹。
- **足部运动可视化实验**：比较左右脚高度、步长、相位差和运动协调性。
- **消融实验**：SE-Policy（actor only）验证对称不变 critic 的必要性。
- **真实机器人实验**：sim-to-real 速度跟踪和越界测试。
- **真实地形实验**：草地、坡面、沙地、石块等非结构化地形通过性测试。

### 2. 充分性与公平性评价

- **优点**：
  - 同时覆盖仿真与真实机器人，增强了结论的可信度。
  - 包含与强基线 DreamWaQ 的对比，并加入 DreamWaQ-Regu 这一软对称约束基线。
  - 进行了 actor-only 消融，能够说明 critic 对称不变性的贡献。
  - 使用多个定量指标，既评估任务性能，也评估时空对称性。
  - 论文声称所有方法使用一致超参数和环境，公平性较好。
- **不足**：
  - 对比方法数量较少，主要是 DreamWaQ 系列，未与更多严格等变 RL 方法或其他人形机器人控制方法比较。
  - 真实世界实验以展示和定性验证为主，定量样本、试验次数和统计显著性未充分报告。
  - 表格中部分指标标准差较大，例如 DreamWaQ 的 TE-V 为 \(16.43\pm9.54\)，但未说明随机种子数量或置信区间构造方式。
  - 地形实验仅说明具备通过性，缺少与基线在真实地形上的系统定量对比。
  - 未报告不同随机种子下的稳定性、训练曲线方差等。

总体来看，实验设计覆盖了“仿真定量 + 消融 + 真机验证”，方向较完整；但在统计严谨性、基线多样性和真实环境定量评估方面仍不算非常充分。

## 六、主要结论与发现

- SE-Policy 能有效嵌入现有 DRL 框架，用于人形机器人速度跟踪控制。
- 在仿真中，SE-Policy 的 TE-V 为 **9.85 cm/s**：
  - 比 DreamWaQ 的 **16.43 cm/s** 低约 **40.0%**；
  - 比 DreamWaQ-Regu 的 **13.91 cm/s** 低约 **19.2%**。
- SE-Policy 的 Spat-S 为 **0.00**，说明其策略在结构上实现了严格的空间对称等变。
- SE-Policy 的 Temp-S 为 **7.86×10⁻² rad**，优于 DreamWaQ 的 **22.52×10⁻² rad** 和 DreamWaQ-Regu 的 **16.58×10⁻² rad**，表明时间周期协调性更好。
- SE-Policy（actor only）虽然优于 DreamWaQ，但 TE-V 和 Temp-S 均差于完整 SE-Policy，说明对称不变 critic 对训练等变策略是必要的。
- 轨迹可视化显示，SE-Policy 更贴近理想轨迹，并表现出关于 \(y=0\) 的镜像对称性；DreamWaQ-Regu 的软正则约束不足，轨迹仍可能偏移。
- 足部运动可视化显示，SE-Policy 的左右脚具有更一致的步幅、振幅和相位差，运动更协调。
- 真实机器人实验表明，SE-Policy 在速度、位置和朝向跟踪上优于基线，并能在草地、坡面、沙地、石块等常见非结构化地形上行走。

## 七、优点

- **方法层面**：
  - 将形态对称性以严格等变网络结构嵌入 actor，以不变性嵌入 critic，而不是依赖软正则或数据增强。
  - 不引入额外超参数，避免对称正则权重调参问题。
  - 同时考虑空间等变和时间周期性，观测中保留相位输入，评价中也区分 Spat-S 与 Temp-S。
  - 网络结构设计与 PPO/DreamWaQ 框架兼容，具有一定通用性。
- **实验层面**：
  - 同时进行仿真和真实 Unitree G1 部署，验证了 sim-to-real 可行性。
  - 加入 DreamWaQ-Regu 软约束基线和 actor-only 消融，能较清晰地说明“严格等变”和“critic 不变性”的作用。
  - 使用轨迹、足部高度等多种可视化手段解释性能差异。
  - 在真实非结构化地形上测试，增强了应用价值展示。

## 八、不足与局限

- **任务覆盖有限**：主要在速度跟踪任务上验证，未系统测试转向、复杂操作、抗扰动、跌倒恢复、上下楼梯等更复杂人形机器人任务。
- **机器人平台单一**：仅使用 Unitree G1，方法对其他自由度配置、质量分布或非严格对称机器人是否适用尚未验证。
- **对称性假设较强**：方法依赖机器人形态严格反射对称；实际机器人可能存在制造误差、负载不对称、关节磨损或传感器偏差，严格等变可能限制策略表达能力。
- **基线数量有限**：主要对比 DreamWaQ 系列，缺少与其他严格等变 RL、对称数据增强、CPG/相位方法或其他人形机器人控制框架的系统比较。
- **真实实验定量不足**：真机部分更多是展示性结果，未给出与仿真同等规模的统计指标、重复次数和误差分布。
- **统计报告不够充分**：未明确随机种子数量、训练方差、显著性检验；部分指标标准差较大，结论稳健性仍需更多统计支撑。
- **算力信息不完整**：只说明使用 RTX 4090 和约 4 小时训练，未说明 GPU 数量与总计算开销。
- **特权信息依赖**：critic 使用高度图作为特权信息，真实部署时 actor 不使用高度图，但训练与部署之间的信息不对称仍需进一步分析。
- **泛化边界未充分探讨**：对不同地形、速度范围、负载变化、外部扰动和长期运行的泛化能力缺少系统评估。

（完）
