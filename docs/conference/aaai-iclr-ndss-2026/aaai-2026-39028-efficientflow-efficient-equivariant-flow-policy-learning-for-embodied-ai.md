---
title: "EfficientFlow: Efficient Equivariant Flow Policy Learning for Embodied AI"
title_zh: EfficientFlow：面向具身智能的高效等变流策略学习
authors: "Jianlei  Chang, Ruofeng Mei, Wei Ke, Xiangyu Xu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39028/42990"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 面向具身智能控制的等变流策略学习与数据效率
tldr: 针对生成式视觉运动策略在具身智能任务中依赖大量示范且推理采样慢的问题，论文提出EfficientFlow，将等变性引入流匹配策略学习，并证明在高斯先验与等变速度网络下动作分布保持等变。该框架同时改善数据效率、泛化能力与动作生成速度，使流策略更适合多样具身控制任务，为结构化先验融入机器人策略学习提供了新途径。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有生成式具身策略数据效率低、推理采样慢，难以满足多样控制任务需求。
method: 提出EfficientFlow，将等变性融入流匹配，并理论证明动作分布的等变保持性质。
result: 摘要指出该方法可提升泛化并显著改善数据与采样效率，具体实验数值未完整给出。
conclusion: 为具身AI中高效、可泛化的结构化生成式策略学习提供了统一框架。
---

## Abstract
Generative modeling has recently shown remarkable promise for visuomotor policy learning, enabling flexible and expressive control across diverse embodied AI tasks. However, existing generative policies often struggle with data inefficiency, requiring large-scale demonstrations, and sampling inefficiency, incurring slow action generation during inference. We introduce EfficientFlow, a unified framework for efficient embodied AI with flow-based policy learning. To enhance data efficiency, we bring equivariance into flow matching. We theoretically prove that when using an isotropic Gaussian prior and an equivariant velocity prediction network, the resulting action distribution remains equivariant, leading to improved generalization and substantially reduced data demands. To accelerate sampling, we propose a novel acceleration regularization strategy. As direct computation of acceleration is intractable for marginal flow trajectories, we derive a novel surrogate loss that enables stable and scalable training using only conditional trajectories. Across a wide range of robotic manipulation benchmarks, the proposed algorithm achieves competitive or superior performance under limited data while offering dramatically faster inference. These results highlight EfficientFlow as a powerful and efficient paradigm for high-performance embodied AI.

---

## 论文详细总结（自动生成）

# EfficientFlow 论文中文总结

## 1. 核心问题与整体含义

- **研究背景**：生成式模型在视觉运动策略学习中表现出较强表达能力，扩散策略等方法能学习复杂动作分布，但存在两个关键瓶颈：
  - **数据效率低**：通常需要大量专家示范；
  - **采样效率低**：扩散模型推理时需数百步迭代去噪，难以满足实时机器人控制。
- **已有工作的不足**：EquiDiff 将等变性引入扩散策略以提升数据效率，但仍基于 DDPM 多步去噪，推理速度慢；流匹配虽更快更稳定，但如何把等变性有效融入流策略、并进一步加速少步采样，尚缺系统方案。
- **论文目标**：提出 **EfficientFlow**，统一“等变学习”和“流匹配生成式策略”，同时改善数据效率、泛化能力与推理速度，为具身智能提供高效策略学习框架。

## 2. 方法论

### 核心思想

- 将 **等变性** 引入 **Flow Matching** 策略：当观测发生群变换（如平面旋转）时，生成的动作分布也应相应变换。
- 通过等变速度场网络和 isotropic Gaussian 先验，使流匹配诱导的条件动作分布保持等变，从而获得更强归纳偏置、更少数据需求和更好泛化。
- 引入 **加速度正则化**，惩罚生成轨迹的二阶时间导数，使流轨迹更平滑、低曲率，从而支持更少 NFE 的快速采样。

### 关键技术细节

- **等变流策略与 Theorem 1**：
  - 设群 \(G\) 同时作用于观测空间和动作空间；
  - 若先验 \(p_0\) 各向同性，即 \(p_0(gx)=p_0(x)\)，且速度网络满足  
    \[
    u_\theta(t,gx|go)=g\,u_\theta(t,x|o)
    \]
  - 则流 ODE 诱导的条件分布满足  
    \[
    X_t|O=go \overset{d}{=} g(X_t|O=o),\quad t\in[0,1]
    \]
  - 当 \(t=1\) 时即得到动作分布等变性。论文强调：**不要求训练数据中的专家策略本身等变**，这与 EquiDiff 的强假设不同。
- **动作表示与网络设计**：
  - 关注平面旋转群 \(SO(2)\) 及其有限循环子群 \(C_u\)；
  - 动作向量为 10 维：6D 连续旋转表示、3D 平移、1D 夹爪宽度；
  - 旋转部分对应 \(\rho_1^3\)，平移的 \(x,y\) 对应 \(\rho_1\)、\(z\) 对应 \(\rho_0\)，夹爪宽度对应 \(\rho_0\)；
  - 使用 escnn 构建等变观测编码器、等变动作编码器/解码器及核心等变网络，整体满足 \(C_u\) 对称性。
- **加速度正则与 FABO**：
  - 训练目标为条件流匹配数据项加加速度惩罚：
    \[
    \mathbb{E}\|u_\theta(t,x_t)-u(t,x_t|x_1)\|_2^2
    +\lambda\mathbb{E}\left\|\frac{d^2x_t}{dt^2}\right\|_2^2
    \]
  - 采用时间相关权重 \(\lambda(t)=(1-t)^2\)，早期更强调平滑，后期更强调精度；
  - 真实边际轨迹的加速度不可直接计算，因此提出 **Flow Acceleration Upper Bound, FABO** 替代目标：从同一条件轨迹采样 \(t\) 与 \(t+\Delta t\) 的点，最小化
    \[
    \mathbb{E}\|u_\theta(t,\tilde{x}_t)-u_\theta(t+\Delta t,\tilde{x}_{t+\Delta t})\|_2^2
    \]
    论文称当 \(\Delta t\) 较小时，该量是真实加速度惩罚的上界代理。
- **时序一致性策略**：
  - 推理时从高斯噪声并行采样 \(m\) 条候选动作轨迹；
  - 选择与上一段已预测轨迹在重叠区间欧氏距离最小的轨迹执行；
  - 每隔 10 个预测周期随机选择一条候选轨迹，以保留多模态探索能力；
  - 批处理并行，额外推理开销较小。

## 3. 实验设计

- **Benchmark**：MimicGen 中的 **12 个机器人操作任务**，覆盖不同难度、时间跨度和物体布局。
- **输入与设置**：
  - 使用 agent-view 与 wrist-mounted 相机的 RGB 图像；
  - 所有策略采用绝对位姿控制；
  - MimicGen 的 agent view 并非正交视角，作者认为这更接近真实非理想视角，也更严格地检验泛化。
- **数据规模**：分别使用 **100、200、1000 条示范**训练。
- **对比方法**：
  - **EquiDiff**：等变扩散策略；
  - **ACT**；
  - **DP-C**：CNN 版 Diffusion Policy；
  - **DP-T**：Transformer 版 Diffusion Policy；
  - **DP3**：基于 3D 点云的扩散策略。
- **评估指标**：任务成功率、推理时间、达到最终最高成功率 50% 所需训练 epoch、消融实验平均成功率。
- **EfficientFlow 设置**：测试 1、3、5 NFE；基线按其原始配置运行或引用。

## 4. 资源与算力

- 论文正文和提供的文本中 **未明确报告** GPU 型号、GPU 数量、训练总时长、能耗或参数量等算力信息。
- 仅报告了推理运行时延，例如 1-NFE 平均 12.22 ms、3-NFE 22.59 ms、5-NFE 34.45 ms，以及单步推理最高约 81.8 Hz。
- 因此无法从论文中判断训练算力规模和可复现成本，这是一个信息缺口。

## 5. 实验数量与充分性

- **实验组数较多**：
  - 主实验覆盖 **12 个任务 × 3 种数据规模 × 多个基线方法**；
  - EfficientFlow 额外比较 1/3/5 NFE；
  - 报告了平均成功率与推理时间；
  - 额外分析学习效率，即达到 50% 最终最高成功率所需 epoch；
  - 消融实验在 12 个任务、100 条示范下比较 5 个变体：完整模型、NoAcc、NonEqui、EquiCFM、EquiMF。
- **充分性**：
  - 任务数量多，覆盖操作难度和数据规模变化；
  - 消融能较清晰地区分“等变性”和“加速度正则”的贡献；
  - 与多种生成式策略和 ACT 对比，并报告 3 个随机种子平均结果。
- **公平性与客观性**：
  - RGB 基线使用与 EfficientFlow 相同输入，控制变量较好；
  - 但部分基线结果直接引用自 EquiDiff 原文，未完全独立复现；
  - DP3 使用点云输入，与 RGB 方法输入模态不同；
  - 不同方法 NFE 配置不同，推理速度比较需注意架构差异；
  - 主要在仿真 benchmark 上验证，真实机器人泛化仍未覆盖。

## 6. 主要结论与发现

- **数据效率**：在 100 条示范下，EfficientFlow 在 12 个任务中 **7 个优于 EquiDiff**；其余 5 个任务中，除 Nut Assembly D0 外差距在 5 个百分点以内。200 条示范时达到 DP-C 使用 1000 条示范成功率的 **98.4%**。
- **采样效率**：1-NFE 平均推理时间 **12.22 ms**，相对 EquiDiff 约 **56.1× 加速**；5-NFE 仍约 **19.9× 加速**，单步推理可达约 **81.8 Hz**。
- **平均成功率**：Table 2 中，EfficientFlow 在 100/200/1000 示范下，1-NFE 平均成功率为 52.61/66.18/75.25，3-NFE 为 53.49/69.33/81.36，5-NFE 为 54.18/70.26/81.99；EquiDiff 100-NFE 为 53.77/68.59/79.69。
- **学习效率**：EfficientFlow 和 NoAcc 达到 50% 最终最高成功率所需 epoch 明显少于 EquiDiff；Hammer Cleanup D1 中仅需 EquiDiff 约五分之一 epoch。
- **消融结论**：完整模型平均成功率 **52.6**，NoAcc 39.3，NonEqui 37.7，EquiCFM 40.4，EquiMF 46.3。等变结构和加速度正则均有独立贡献且互补；在等变架构下，EfficientFlow 的加速度正则优于 Consistency Flow Matching 和 MeanFlow 变体。

## 7. 优点

- **理论贡献清晰**：证明各向同性高斯先验与等变速度网络可使流匹配动作分布保持等变，且不要求专家策略等变，假设更弱。
- **方法统一**：将等变归纳偏置与流匹配结合，同时处理数据效率和采样效率。
- **FABO 设计实用**：避免直接计算不可得的边际轨迹加速度，仅用条件轨迹构造可训练上界代理。
- **推理速度突出**：少步甚至单步生成即可达到有竞争力成功率，适合实时机器人控制。
- **实验覆盖较广**：12 个 MimicGen 任务、3 种数据规模、多种强基线、运行时延和学习效率分析。
- **消融较系统**：分别验证等变性和加速度正则，并与 Consistency Flow Matching、MeanFlow 等高效流变体比较。
- **工程细节完整**：动作表示、等变网络、时序重叠、候选轨迹选择和周期重置均有说明。

## 8. 不足与局限

- **算力信息缺失**：未报告 GPU 型号、数量、训练时长等，影响复现和成本评估。
- **仿真为主**：仅在 MimicGen 仿真 benchmark 上验证，缺少真实机器人实验；真实场景中的遮挡、噪声、动态环境和相机标定误差可能削弱等变优势。
- **对称性覆盖有限**：主要研究 \(SO(2)\)/有限循环子群 \(C_u\) 的平面旋转等变，未充分覆盖 SE(3)、尺度、物体对称性等更复杂对称结构。
- **超参与敏感性分析不足**：加速度权重 \(\lambda(t)\)、\(\Delta t\)、群阶 \(u\)、候选轨迹数 \(m\)、周期重置频率等缺少系统敏感性实验。
- **基线复现公平性**：部分基线结果直接引用 EquiDiff 原文，未完全独立重跑；不同方法输入模态和 NFE 配置存在差异。
- **理论证明位置**：Theorem 1 和 FABO 的严格证明主要在补充材料，正文以直观解释为主。
- **失败案例分析不足**：未深入分析 Nut Assembly D0 等表现较弱任务的原因，也缺少长时序鲁棒性和多模态行为保持的定量评估。
- **应用限制**：依赖 escnn 等等变网络库，实际部署需已知并匹配任务对称性；若真实环境对称性不成立，等变约束可能带来偏差。

（完）
