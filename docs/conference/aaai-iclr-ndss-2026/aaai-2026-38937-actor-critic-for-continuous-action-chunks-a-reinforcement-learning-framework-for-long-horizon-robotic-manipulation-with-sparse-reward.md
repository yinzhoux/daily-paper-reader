---
title: "Actor-Critic for Continuous Action Chunks: A Reinforcement Learning Framework for Long-Horizon Robotic Manipulation with Sparse Reward"
title_zh: 连续动作块的演员-评论家：面向稀疏奖励长时程机器人操作的强化学习框架
authors: "Jiarui Yang, Bin Zhu, Jingjing Chen, Yu-Gang Jiang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38937/42899"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 面向稀疏奖励长时程机器人操作的强化学习框架
tldr: 针对现有强化学习在稀疏奖励长时程机器人操作任务中难以稳定高效学习连续动作序列的问题，论文提出AC3框架，通过分别面向actor与critic的稳定化机制直接学习高维连续动作块。实验表明该方法训练更稳定、数据效率更高，在稀疏奖励长时程操作任务上成功率优于基线，为长时程机器人操作提供了可复用的学习框架。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有强化学习方法在稀疏奖励的长时程机器人操作任务中难以稳定且高效地学习连续动作序列。
method: 提出AC3框架，通过面向actor与critic的稳定化机制，直接学习高维连续动作块以完成长时程操作。
result: 实验表明该方法在稀疏奖励的长时程操作任务中训练更稳定、数据效率更高，任务成功率优于基线。
conclusion: 该工作将动作分块与强化学习结合，为长时程机器人操作提供了稳定高效的学习框架。
---

## Abstract
Existing reinforcement learning (RL) methods struggle with long-horizon robotic manipulation tasks, particularly those involving sparse rewards. While action chunking is a promising paradigm for robotic manipulation, using RL to directly learn continuous action chunks in a stable and data-efficient manner remains a critical challenge. 
This paper introduces AC3 (Actor-Critic for Continuous Chunks), a novel RL framework that learns to generate high-dimensional, continuous action sequences. To make this learning process stable and data-efficient, AC3 incorporates targeted stabilization mechanisms for both the actor and the critic. First, to ensure reliable policy improvement, the actor is trained with an asymmetric update rule, learning exclusively from successful trajectories. Second, to enable effective value learning despite sparse rewards, the critic's update is stabilized using intra-chunk n-step returns and further enriched by a self-supervised module providing intrinsic rewards at anchor points aligned with each action chunk. We conducted extensive experiments on 25 tasks from the BiGym and RLBench benchmarks. 
Results show that by using only a few demonstrations and a simple model architecture, AC3 achieves superior success rates on most tasks, validating its effective design.

---

## 论文详细总结（自动生成）

# AC3 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **任务背景**：长时程机器人操作（如移动盘子、翻三明治、双手移动操作）要求智能体执行一长串连贯动作，状态-动作探索空间随任务长度急剧膨胀，且任一子任务失败即导致整体失败。
- **稀疏奖励困境**：这类任务通常只在任务完成时给出 1 的奖励，中间步骤没有任何引导信号，智能体难以判断哪些前置动作对最终成功关键，自主探索效率极低。
- **动作分块（action chunking）的价值与局限**：
  - 在模仿学习（IL）中非常成功，如 ACT、Diffusion Policy 用强生成模型一次预测整段连续动作序列；
  - 但 IL 性能受专家数据上界限制，存在分布漂移（distributional shift），遇到略微偏离专家轨迹的未见状态即失败（论文图 1(a)）。
- **把分块引入 RL 的难点**：
  - 块长增大使探索空间指数级膨胀，价值估计难处理，Q 值易爆炸、训练不稳定；
  - CQN-AS 通过离散化动作块库 + 分层离散 Q 学习规避该问题，但离散化牺牲精度与灵活性（图 1(b)）；
  - Q-Chunking 用复杂蒸馏流程生成连续块，但依赖大规模离线数据、计算开销大，不适合少样本、实时控制场景。
- **研究空白**：缺少一个能在连续动作域中**直接、稳定、数据高效**地学习动作块的 RL 框架。AC3 即为此提出，仅用少量专家示范 + 简单网络结构即可在线自我提升。

## 2. 方法论

### 2.1 问题建模
- 将任务建模为**连续块空间的半马尔可夫决策过程（SMDP）**：元组 (S, A, P, r, γ)。
  - S 为高维状态（RGB 视觉 + 机器人本体感知拼接）；
  - A 为定长连续动作块；
  - r ∈ {0,1} 稀疏奖励；
  - 给定 N 条专家示范 D_demo 作为小规模离线数据。
- 目标：最大化期望折扣回报。

### 2.2 核心思想
- 基于 **DDPG 风格 off-policy actor-critic** 改造：actor 直接输出连续动作块，critic 评估整块价值；并针对 actor 与 critic 分别设计**稳定化机制**，以在稀疏奖励、少示范条件下稳定训练。

### 2.3 关键技术细节
- **Actor（连续动作块策略）**：
  - 策略 π_θ(s_t) 直接输出 A_t = {a_t, …, a_{t+C−1}} ∈ R^{C×d_a}，实现时间抽象，缓解逐步决策的局部次优、提升执行连贯性；
  - 网络结构：简单 **MLP + GRU**（捕捉块内时序依赖、保证计算效率）；
  - 执行时逐时间步弹出单个动作，并用 ACT 的 **temporal ensembling** 平滑执行。
- **Critic（块内 n 步 Q 值估计）**：
  - Q_φ(s_t, A_t) 估计执行整块后的期望回报；
  - 直接用整块回报作目标噪声大、样本效率低、且无法为块内每个原始动作提供细粒度反馈，因此改用 **intra-chunk n-step TD 目标**：
    - 目标值 y_t = 前 n 步观测奖励的折扣和 + γ^n 乘以目标网络在 s_{t+n} 处对「下一状态策略输出 + 裁剪高斯探索噪声 ε」的估值；
    - 沿用 TD3 的**双目标 critic + clipped double-Q（取 min）** 抑制过估计；
    - critic 网络同样是 MLP + GRU。
- **Critic 更新**：最小化两个 critic 的 Q(s_t, A_t^exp) 与 y_t 的 MSE（式 3）。
- **Actor 更新（非对称更新规则）**：
  - 从回放池中筛选出**成功轨迹**构成 B_succ（含专家示范与在线成功 rollout）；
  - 损失 = λ_BC · BC 损失（‖π_θ(s_t) − A_t^exp‖²）+ λ_Q · Q 损失（−min_i Q_{φ_i}(s_t, π_θ(s_t))）；
  - 权重 λ_BC = 1.0，λ_Q = 0.1；
  - 关键点：策略梯度**只限制在成功轨迹定义的「可信区域」**内，因为稀疏奖励下 critic 对大部分状态空间估值极不准确，用全部数据（含失败）训练会导致策略退化甚至崩溃（图 8）。
- **自监督奖励塑形（锚点内在奖励）**：
  - 预训练**目标网络 G_ω**（与状态编码器同结构），用**对比学习 + Triplet Loss**：同轨迹时间邻近状态为正样本、不同轨迹或时间远离的状态为负样本，拉近正样本、推远负样本，间隔 m；
  - 定义当前状态到示范状态集合的最小平方隐空间距离 d(s_t) = min_{s_d} ‖G_ω(s_t) − G_ω(s_d)‖²；
  - **锚点机制**：每 K 步（实验中 K = C = 16）设一个锚点，只有当 t ≡ 0 (mod K) 且 d(s_t) < m 时给予内在奖励 a = 0.1，否则为 0；该设计与块级策略天然对齐，为整个动作块提供信号并鼓励块内随机探索；
  - 内在奖励需**小于任务成功奖励**，否则智能体会利用错误设定的内在奖励而放弃真实目标（图 7 显示等值或线性递增奖励导致 Q 值爆炸与策略失败）。

### 2.4 算法流程（Algorithm 1 文字描述）
1. 初始化双 critic、actor、目标网络，回放池以专家示范初始化；
2. 用 Triplet Loss 在示范上预训练目标网络 G_ω；
3. 在线循环：每 C 步用策略 + 裁剪噪声生成一个新动作块；逐步执行单个动作、获得奖励与新状态；非终止时用内在奖励替换/覆盖奖励；存入回放池；
4. 采样 mini-batch（含 s_t, A_t^exp, r_{t:t+n−1}, s_{t+n}）；
5. 计算 n 步目标 y_t，更新两个 critic，软更新目标网络（μ = 0.005）；
6. 用成功掩码 m_succ 计算 BC 损失与 Q 损失，加权更新 actor。

## 3. 实验设计

- **Benchmark 与场景**：
  - **BiGym**：双手移动操作基准，15 个任务，覆盖多子任务（如 saucepan to hob）与精细操作（如 move plate）；每任务仅用 **10 条人类示范**；RGB 84×84，来自头部 + 左右腕三个相机。
  - **RLBench**：桌面操作基准，10 个任务；每任务 **100 条示范**（与 CQN 相同采集方式）；RGB 84×84，来自前、腕、左右肩四个相机。
  - 两者均为**稀疏奖励**（仅成功给 1）。
- **对比方法**：
  1. **AC3**（本文）；
  2. **CQN-AS**：分层离散 Q 学习做动作块；
  3. **DrQ-v2**：逐步输出的 actor-critic 确定性策略（附加辅助 BC 损失以助收敛）；
  4. **Chunk-wise BC**：与 AC3 actor 同结构的纯离线块级模仿学习。
- **评测协议**：每任务训练 50k 步；每个 checkpoint 用 25 个 episode 统计成功率；3 个随机种子，报告均值与标准差；chunk-wise BC 取最后三个 checkpoint 的平均。
- **超参**：AdamW；actor/critic 学习率 1e-4，目标网络 1e-5；γ = 0.99；探索噪声 σ = 0.01、裁剪 c = 0.1；块长 C = 16；n = 4；锚点间隔 K = 16、margin m = 0.5、内在奖励 0.1。
- **消融实验**（主要在 BiGym 的 move plate 与 RLBench 的 open oven 两个代表性任务上）：
  - 动作块长度 C 的影响；
  - intra-chunk n-step 回报（n = 1/4/8/16）的影响；
  - 自监督奖励塑形设置（无塑形、线性递增、rint = 0.1、与成功奖励等值）；
  - actor 是否只用成功轨迹（非对称更新 vs 全数据更新）；
  - 模型复杂度与推理速度对比（参数量、单次推理毫秒数）。

## 4. 资源与算力

- 文中仅说明「所有实验在一张 **RTX 3090 GPU** 上完成」。
- **未明确给出**：GPU 数量（表述为单数，推测为 1 张）、总训练时长/GPU 小时、每任务训练 wall-clock 时间、3 个种子 × 25 个任务的总计算量、内存与存储开销。
- 网络规模方面提供了间接信息：actor 6.56M 参数、actor+critic 共 14.44M 可训练参数；推理 2.9 ms/块。
- 因此算力报告**不够充分**，无法据此评估方法的实际训练成本与可复现性门槛。

## 5. 实验数量与充分性

- **规模**：2 个 benchmark、共 **25 个任务**（BiGym 15 + RLBench 10），每个任务 3 个种子，每个 checkpoint 25 个 episode，训练 50k 步——覆盖面在同类工作中属较广。
- **消融**：约 4–5 组消融（块长、n 步、奖励塑形、actor 数据筛选、效率对比），但**基本只集中在 2 个任务**（move plate、open oven）上，泛化性证据有限；作者称补充材料有更详细分析。
- **公平性**：
  - 所有 RL 基线（DrQ-v2、CQN-AS）都加了辅助 BC 损失，AC3 也使用 BC 项，条件相对对等；
  - 与 chunk-wise BC 使用相同 actor 结构与相同示范数据，控制较好；
  - 但 **AC3 使用了额外信息**（成功轨迹筛选、预训练目标网络、锚点内在奖励），而部分基线未获得同等奖励塑形，存在一定「信息不对等」的比较偏差；
  - 未与论文明确提及的 **Q-Chunking** 做实验对比，也未与 ResiP、T-SAC 等块相关 RL 方法比较，基线选择偏保守。
- **客观性**：报告了 3 种子均值 ± 标准差，曲线完整；但成功率的统计噪声在 25 episode 下仍较大，且未报告显著性检验。
- 总体：**广度尚可、深度与公平性有待加强**，消融任务数偏少，缺少真实机器人验证。

## 6. 主要结论与发现

- **性能**：在 BiGym 大多数任务上 AC3 成功率最高，且能在 10k 步内快速提升，明显优于 chunk-wise BC；在 RLBench 上优于 BC 基线、与 CQN-AS 相近，但网络结构更简单；DrQ-v2 在多数任务上显著劣于 BC 基线，说明**块级预测对长时程稀疏奖励任务不可或缺**。
- **块长很关键**：高维动作空间任务（move plate）需要较长块（C = 16）保证双手动作连贯，C = 4 几乎完全失效；低自由度简单任务（open oven）过长块反而增加探索噪声，中等长度最优。
- **n 步选择需折中**：理论上 n = C 无偏，但实际会因探索噪声与 critic 无法细粒度指导块内动作而失败（move plate 上 n = 16 直接失效）；n = 4 或 8 是较好折中，n = 1 在高维任务中易 Q 值爆炸。
- **奖励塑形需谨慎**：rint = 0.1 的锚点塑形在复杂任务上收益显著且不损害简单任务；但若内在奖励等于成功奖励或随轨迹线性递增，会引发 Q 值爆炸与策略失败（智能体利用错误设定的奖励）。
- **非对称更新是稳定性的关键**：让 actor 学习全部经验（含失败）会导致策略显著退化甚至崩溃，原因是稀疏高维下 critic 对未见状态估值严重偏差，产生误导性梯度。
- **效率优势**：推理只用 actor（6.56M 参数），2.9 ms/块，比 CQN-AS（28.58M、9.5 ms）快 3 倍以上，可承受 temporal ensembling 的额外开销，适合高频/低延迟部署。

## 7. 优点

- **问题定位清晰**：准确指出「IL 受数据上界 + 分布漂移」「离散块损失精度」「蒸馏方案重且贵」三点空白，动机链条完整。
- **方法简洁实用**：仅用 MLP+GRU 而非 Transformer/扩散模型，却在 25 个任务上取得有竞争力的成功率，工程可落地性强。
- **两个稳定化机制针对性强且互为补充**：
  - 非对称 actor 更新把策略优化限制在价值函数可信区域，是稀疏奖励下的一个通用、低成本技巧；
  - intra-chunk n-step 回报在「宏观选块」与「微观块内微调」之间取得平衡，缓解 Q 值爆炸；
  - 锚点式内在奖励与块结构天然对齐，且用对比学习预训练目标网络，无需额外环境奖励工程。
- **数据高效**：BiGym 上仅 10 条示范即可在线自我提升并超越纯 BC，符合真实机器人数据稀缺的约束。
- **实验设计有对照意识**：为所有 RL 基线统一加辅助 BC 损失、与同结构 BC 对比，并系统消融块长、n 步、奖励形式。
- **效率分析到位**：给出参数量与推理延迟的量化对比，强调推理只用 actor 的实际部署优势。

## 8. 不足与局限

- **实验覆盖**：
  - 消融几乎只在 2 个任务（move plate、open oven）上做，结论外推性受限；
  - 全部为**仿真实验**（BiGym、RLBench），无真实机器人验证，sim-to-real 的鲁棒性未知；
  - 未与 Q-Chunking、ResiP、T-SAC 等最相关的块级 RL 工作对比，基线覆盖不全。
- **对示范的依赖**：方法仍需要专家示范（10/100 条）来初始化回放池、做 BC 正则、预训练目标网络；并非「无示范」的纯 RL，示范质量与数量对结果的影响未被系统研究。
- **超参敏感性**：内在奖励幅值、锚点间隔 K、margin m、n、块长 C 都需任务相关调参；论文自己展示了奖励设定不当会导致 Q 值爆炸，说明方法对奖励塑形的错误设定较脆弱，缺少自适应机制。
- **理论支撑不足**：SMDP 建模与非对称更新、锚点奖励的收敛性/最优性缺乏理论分析，主要靠经验证据。
- **算力与可复现性报告不完整**：只提到一张 RTX 3090，未给训练时长、总计算量，也未给完整超参与任务级配置（推到补充材料），复现成本不透明。
- **评价指标单一**：只报告成功率，缺少样本效率曲线（学习所需交互步数）、执行平滑度、动作精度、失败模式分析等；25 episode × 3 seed 的统计置信度有限，无显著性检验。
- **潜在偏差风险**：成功轨迹筛选（B_succ）在成功率低的初期可能样本极少，导致 actor 更新方差大；论文未讨论该冷启动问题及失败轨迹被完全弃用的信息浪费。
- **应用限制**：块长固定（C = 16）、需 temporal ensembling 平滑，对动态环境或需要高频反应式纠偏的任务可能不适应；推理虽快但仍需视觉编码，实时性依赖硬件。

（完）
