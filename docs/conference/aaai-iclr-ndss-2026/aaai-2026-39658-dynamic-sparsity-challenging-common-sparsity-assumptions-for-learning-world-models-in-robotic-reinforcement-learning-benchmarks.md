---
title: "Dynamic Sparsity: Challenging Common Sparsity Assumptions for Learning World Models in Robotic Reinforcement Learning Benchmarks"
title_zh: 动态稀疏性：质疑机器人强化学习基准中世界模型学习的常见稀疏假设
authors: "Muthukumar Pandaram, Jakob Hollenstein, David Drexel, Samuele Tosatto, Antonio Rodriguez-Sanchez, Justus Piater"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39658/43619"
tags: ["query:humanoid-rl"]
score: 8.0
evidence: 检验机器人强化学习世界模型中的稀疏结构先验与样本效率
tldr: 学习动力学模型即世界模型可提升强化学习样本效率，近期工作据此假设因果图稀疏并引入稀疏先验，但这些假设缺乏系统检验。作者分析MuJoCo Playground等机器人强化学习环境的真实动力学，考察因果稀疏与时间稀疏假设是否成立。结果显示常见稀疏性假设在真实动力学中并不普遍成立，从而挑战了依赖稀疏先验的世界模型学习做法。该工作为机器人强化学习中的结构化世界模型设计提供了实证依据与警示。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 世界模型常被假设具有稀疏因果图与时间稀疏性并据此引入先验，但这些假设缺乏系统检验。
method: 分析MuJoCo Playground等机器人强化学习基准环境的真实动力学，检验稀疏性假设是否成立。
result: 发现常见稀疏性假设在真实动力学中并不普遍成立，挑战了依赖稀疏先验的世界模型学习。
conclusion: 提醒研究者在机器人强化学习中谨慎使用稀疏结构先验，为世界模型设计提供实证依据。
---

## Abstract
The use of learned dynamics models, also known as world models, can improve the sample efficiency of reinforcement learning. Recent work suggests that the underlying causal graphs of such dynamics models are sparsely connected, with each of the future state variables depending only on a small subset of the current state variables, and that learning may therefore benefit from sparsity priors. Similarly, temporal sparsity, i.e. sparsely and abruptly changing local dynamics, has also been proposed as a useful inductive bias. In this work, we critically examine these assumptions by analyzing ground truth dynamics from a set of robotic reinforcement learning environments in the MuJoCo Playground benchmark suite, aiming to determine whether the proposed notions of state and temporal sparsity actually tend to hold in typical reinforcement learning tasks. We study (i) whether the causal graphs of environment dynamics are sparse, (ii) whether such sparsity is state-dependent, and (iii) whether local system dynamics change sparsely. Our results indicate that global sparsity is rare, but instead the tasks show local, state-dependent sparsity in their dynamics and this sparsity exhibits distinct structures, appearing in temporally localized clusters (e.g., during contact events) and affecting specific subsets of state dimensions. These findings challenge common sparsity prior assumptions in dynamics learning, emphasizing the need for grounded inductive biases that reflect the state-dependent sparsity structure of real-world dynamics.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究背景**：基于模型的强化学习（MBRL）通过学习世界模型/动力学模型提升样本效率，但稠密动力学模型容易学到虚假相关，导致泛化差、预测误差累积。
- **既有假设**：近期工作常假设真实动力学的因果图是**稀疏**的，即每个未来状态变量只依赖少量当前状态和动作；并进一步假设存在**时间稀疏性**，即局部动力学只在少数时刻突然切换。相关方法据此引入稀疏先验、因果结构学习或局部因果建模。
- **核心问题**：这些稀疏假设多在受控或合成环境中验证，尚不清楚它们是否适用于带接触、碰撞和动态交互的典型机器人强化学习基准。
- **整体含义**：论文不是提出新的世界模型算法，而是对“稀疏先验是否与真实动力学结构对齐”进行实证检验。作者利用 MuJoCo Playground 中真实仿真动力学的 Jacobian 分析，系统考察全局稀疏、状态依赖稀疏和时间稀疏，并检验普通 MLP 能否恢复真实稀疏结构。其意义在于提醒：稀疏先验若过强或形式错误，可能阻碍学习重要交互。

## 2. 方法论

- **核心思想**：将环境真实转移函数 \(s_{t+1}=\text{step}(s_t,a_t)\) 视为可微动力学，通过自动微分计算状态 Jacobian \(J_s=\partial \text{step}/\partial s_t\) 和动作 Jacobian \(J_a=\partial \text{step}/\partial a_t\)，用 Jacobian 中零元素的比例刻画局部因果依赖的稀疏性。
- **因果与 Jacobian 的关系**：
  - 若输出状态维度 \(j\) 不直接依赖输入维度 \(i\)，则对应偏导 \(\partial \text{step}_j/\partial x_i=0\)。
  - Jacobian 中某个元素在所有状态和动作下恒为零，是因果边缺失的**必要且充分条件**；在有限采样中只能检验必要条件，因此得到真实全局稀疏性的**上界**。
  - 稀疏度定义为 Jacobian 零元素数量除以总元素数量。
- **分析流程**：
  - 使用专家 PPO 策略收集轨迹，并注入 colored noise 以鼓励探索。
  - 利用 MJX 对仿真器 `step(s,a)` 自动微分，构建包含状态、动作、下一状态及状态/动作 Jacobian 的数据集。
  - 对每个环境统计：
    - 全局恒零 Jacobian 元素，回答 Q1；
    - Jacobian 元素在样本中零值比例、稀疏度直方图和 t-SNE 可视化，回答 Q2；
    - 零/非零稀疏状态持续时间的分布，回答 Q3；
    - 训练 MLP 近似 `step(s,a)`，比较预测误差和诱导稀疏度，回答 Q4。
- **MLP 恢复实验**：使用两层 ELU 激活、每层 512 单元的 MLP，以 MSE 预测下一状态；比较基线 MSE 与加入真实 Jacobian 监督的 MSE(J)、MAE(J)、仅对预测 Jacobian 施加 L1 正则的 L1(J)，以及只对真实零元素施加 MAE 的稀疏感知误差 SAE(J)。MLP Jacobian 绝对值小于 \(10^{-6}\) 视为零。

## 3. 实验设计

- **Benchmark**：MuJoCo Playground 中实现的 DeepMind Control Suite 连续控制任务，共 8 个环境：
  - BallInCup、CartpoleBalance、CheetahRun、ReacherHard、FingerSpin、FingerTurnEasy、WalkerRun、SwimmerSwimmer6。
- **数据来源**：使用 PPO 训练的专家策略产生随机策略 rollout，并加入 colored noise 探索；通过 MJX 自动微分获得真实状态和动作 Jacobian。
- **分析场景**：
  - Q1：统计 8 个环境中跨多个 rollout 恒为零的 Jacobian 元素，表 1 给出状态和动作 Jacobian 零元素计数及比例。
  - Q2：用稀疏度直方图、t-SNE 嵌入和接触事件示例分析状态依赖稀疏；重点展示 ReacherHard、FingerTurnEasy、FingerSpin 等。
  - Q3：展示 BallInCup、CheetahRun 等环境中稀疏度随时间变化，并统计所有环境中零/非零状态持续时长分布。
  - Q4：在 8 个环境数据上训练 MLP，比较 5 种损失配置：MSE、+MSE(J)、+MAE(J)、+L1(J)、+SAE(J)。
- **对比方法**：主要是 MLP 不同损失项之间的对比，并未与复杂世界模型架构、因果发现方法或稀疏 Transformer 等模型进行端到端比较。
- **评价指标**：全局零元素比例、Jacobian 稀疏度、稀疏持续时间、归一化下一状态 MSE、MLP Jacobian 相对稀疏度。

## 4. 资源与算力

- 论文**未明确报告** GPU 型号、数量、训练时长或总计算量。
- 仅在局限性中提到“由于计算预算原因”，实验只覆盖有限智能体和环境，架构探索也限于等宽 MLP。
- 因此无法从文中判断其算力规模，也无法复现其计算成本。

## 5. 实验数量与充分性

- **实验组数**：
  - 覆盖 8 个机器人连续控制环境；
  - 每个环境进行全局稀疏统计、稀疏度分布、时间持续性和 MLP 恢复分析；
  - Q4 包含 5 种损失配置，在 8 个环境上聚合比较；
  - 使用多个 rollout 和随机种子进行平均，但文中未明确给出轨迹数、种子数和样本总量。
- **充分性**：
  - 优点是对 8 个代表性 MuJoCo/DM Control 任务做了多角度实证，Q1–Q4 层层递进，能较好支撑“全局稀疏罕见、局部状态依赖稀疏存在、时间上成簇变化”的结论。
  - 不足是环境、智能体和数据分布仍有限；只分析状态空间，未分析像素观测；Q4 仅测试简单 MLP，未探索更强架构；未报告统计检验细节，作者也称部分差异“不显著”。
- **客观与公平性**：
  - 使用真实仿真器 Jacobian 作为 ground truth，较直接、客观；
  - MLP 不同损失在同一数据与架构下比较，较公平；
  - 但阈值选择（\(10^{-12}\)、\(10^{-6}\)）可能影响零元素判定；采样只能给出全局稀疏上界；专家策略 rollout 可能偏向任务相关状态，不能完全代表整个状态空间。

## 6. 主要结论与发现

- **全局稀疏性罕见**：多数环境没有大量恒零 Jacobian 元素；仅 CheetahRun、ReacherHard、WalkerRun、SwimmerSwimmer6 等出现少量全局零元素，状态 Jacobian 零元素比例约 5.25%–18.75%，动作 Jacobian 基本无恒零元素。
- **存在状态依赖的局部稀疏**：稀疏性随当前状态变化，常与接触事件相关。例如 FingerSpin/FingerTurnEasy 中，手指未接触物体时稀疏度较高，接触或推动物体时稀疏度降低。
- **稀疏模式呈离散、重复结构**：稀疏度直方图集中在少数取值，可能与是否接触地面、是否抓住物体、步态阶段等有关。
- **时间稀疏性存在**：稀疏状态往往持续多个时间步后突然切换，例如 BallInCup 中绳子松弛/绷紧、CheetahRun 中步态相位变化；持续时间分布可为时间稀疏正则化提供超参参考。
- **普通 MLP 难以恢复真实稀疏结构**：训练会提高 MLP Jacobian 稀疏度，但仍远低于真实目标；加入真实 Jacobian 损失能提高诱导稀疏度，却未充分恢复；MAE(J) 对预测略有帮助但不显著；L1(J) 提高稀疏度但损害预测；SAE(J) 可在不显著降低预测性能的情况下提高稀疏度，但仍与真实稀疏差距很大。
- **总体结论**：稀疏先验并非普遍适用；更有前景的方向是建模**状态依赖、时间局部化、接触/相位驱动的动态稀疏结构**，而非强制全局静态稀疏。

## 7. 优点

- **直接检验基础假设**：不同于仅提出新先验，论文用真实动力学 Jacobian 对稀疏假设做实证审查，问题清晰且有价值。
- **分析层次完整**：区分全局稀疏、状态依赖稀疏和时间稀疏，避免把“局部零元素”误判为“全局稀疏因果图”。
- **ground-truth 可微分析**：利用 MJX 自动微分获得真实 Jacobian，比仅分析学习模型更可靠。
- **负结果具有警示意义**：指出全局稀疏先验可能错配，MLP 难以自动恢复稀疏结构，对世界模型架构设计有直接启示。
- **提供可操作观察**：稀疏持续时间均值、接触相关稀疏模式等可为正则化强度或动态结构设计提供经验依据。
- **可复现性**：论文提供补充版本和代码链接，便于后续验证。

## 8. 不足与局限

- **环境与智能体覆盖有限**：仅 8 个 MuJoCo Playground/DM Control 任务，且只使用 PPO 专家策略的随机 rollout；更多环境、智能体和数据分布可能改变结论。
- **仅分析状态空间**：未分析像素或部分可观测观测空间；真实机器人中观测映射不可逆，结论不能直接推广到视觉世界模型。
- **全局稀疏只能给上界**：有限采样无法穷尽状态动作空间，Q1 的零元素统计是真实全局稀疏的上界而非精确值。
- **阈值敏感**：零元素判定依赖 \(10^{-12}\) 和 \(10^{-6}\) 阈值，可能影响稀疏度统计。
- **MLP 架构探索有限**：仅使用等宽两层 MLP，未与稀疏 Transformer、因果结构学习、变分稀疏门控等更强架构比较，不能断言所有学习方法都无法恢复稀疏。
- **统计严谨性不足**：未明确报告样本量、种子数、置信区间和显著性检验；作者也承认部分预测差异不显著。
- **算力信息缺失**：未报告 GPU 型号、数量和训练时长，影响复现与成本评估。
- **应用限制**：结论主要适用于仿真连续控制基准；真实机器人接触动力学、摩擦、柔顺性和感知噪声可能更复杂，需进一步验证。
- **个别展示可能存在不一致**：图 4 正文称 FingerSpin，图注写 FingerTurnEasy，读者需结合补充材料核对。

（完）
