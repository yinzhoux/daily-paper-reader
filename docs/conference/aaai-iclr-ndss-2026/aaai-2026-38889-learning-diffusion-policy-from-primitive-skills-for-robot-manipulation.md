---
title: Learning Diffusion Policy from Primitive Skills for Robot Manipulation
title_zh: 从原始技能学习扩散策略的机器人操作
authors: "Zhihao Gu, Ming Yang, Difan Zou, Dong Xu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38889/42851"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 使用离散结构化技能表征的技能条件扩散操作策略
tldr: 针对现有扩散策略依赖全局指令生成短期控制信号、易导致动作错位的问题，本文提出以原始技能为条件的 SDP 方法。作者将移动、开合夹爪等细粒度短程操作抽象为八种可复用原始技能，并用视觉语言模型提取离散表征来条件化动作规划。方法把可解释技能学习与条件动作规划结合，改善了操作动作生成的准确性与一致性，为结构化技能表征驱动的操作策略提供了范例。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有扩散策略依赖全局指令生成短期动作，易出现动作错位，缺乏细粒度技能引导。
method: 提出 SDP 技能条件扩散策略，将八种可复用原始技能与视觉语言模型离散表征结合。
result: 方法把可解释技能学习融入条件动作规划，提升了操作动作生成的准确性与一致性。
conclusion: 以结构化原始技能为接口可有效改进机器人操作扩散策略的动作生成。
---

## Abstract
Diffusion policies have recently shown great promise for generating actions in robotic manipulation. However, existing approaches often rely on global instructions to produce short-term control signals, which can result in misalignment in action generation. We conjecture that the primitive skills, referred to as fine-grained, short-horizon manipulations, such as "move up" and "open the gripper", provide a more intuitive and effective interface for robot learning. To bridge this gap, we propose SDP, a skill-conditioned diffusion policy that integrates interpretable skill learning with conditional action planning. SDP abstracts eight reusable primitive skills across tasks and employs a vision-language model to extract discrete representations from visual observations and language instructions. Based on the representations, a lightweight router network is designed to assign a desired primitive skill for each state, which helps construct a single-skill policy to generate skill-aligned actions. By decomposing complex tasks into a sequence of primitive skills and selecting a single-skill policy, the proposed SDP ensures skill-consistent behavior across diverse tasks.
Extensive experiments on two challenging simulation benchmarks and real-world robot deployments demonstrate that SDP consistently outperforms state-of-the-art methods, providing a new paradigm for skill-based robot learning with diffusion policies.

---

## 论文详细总结（自动生成）

# 论文结构化总结：Learning Diffusion Policy from Primitive Skills for Robot Manipulation（SDP）

## 1. 核心问题与研究动机

- **背景**：扩散策略（Diffusion Policy, DP）通过条件去噪生成动作序列，在机器人操作中表现优异；后续工作引入自然语言指令作为条件，扩展到多任务场景。
- **核心问题**：现有方法大多把**高层全局指令直接映射为短期动作**，指令粒度过粗、语义抽象，容易导致动作生成**歧义与错位（misalignment）**。例如机器人即将“闭合夹爪”时，全局指令“把柠檬放进锅里”无法提供明确的即时指导。
- **核心假设**：细粒度、短时程的**原始技能（primitive skills）**，如“向上移动”“打开夹爪”，是更直观、更有效的机器人学习接口。
- **整体含义**：论文提出 **SDP（Skill-conditioned Diffusion Policy）**，将可解释的技能学习与条件动作规划结合：先把复杂任务分解为原始技能序列，再为每个状态选择单一技能策略，从而生成与技能一致的动作，缓解指令与动作之间的粒度错位。

## 2. 方法论

### 2.1 核心思想
- 跨任务抽象出 **8 种可复用原始技能**：`roll`、`yaw`、`open the gripper`、`move up`、`translate`、`close the gripper`、`move down`、`rotate`。
- 用视觉语言模型（VLM）从视觉观测与语言指令中提取离散表征，再由轻量 **router 网络**为每个状态分配最合适的技能。
- 被选中的技能用于**参数化扩散策略中的 FFN 层**，构造“单技能扩散策略”，生成与技能对齐的动作。

### 2.2 关键技术细节

- **组合式提示集成（CPE）**
  - 设计统一文本模板：`"the robot arm is going to {skill}."`
  - 受 CLIP prompt ensemble 启发，对 8 个技能生成提示集成：`PEn = "the robot arm is going to {skill}." ⊗ P`
  - 经冻结的 CLIP 文本编码器与 MLP，得到技能提示嵌入 `p ∈ R^{8×C_img}`；文本可预计算并存储，提升推理效率。

- **视觉语言表征**
  - 静态相机与腕部相机图像经共享图像编码器得到视觉 token；高层指令经 tokenizer 与词嵌入得到文本 token。
  - 文本与视觉 token 拼接后送入 Transformer，得到视觉语言表征 `z_vl`。

- **原始技能选择（Router）**
  - 对 `z_vl` 的 token 维度做平均得 `z_avg`，经 MLP 输出 8 维 logits，再经 Softmax 与 top-1 得到技能分配向量 `R(z_vl) ∈ R^8`。
  - 技能嵌入为加权选择：`z = Σ_{i=1}^{8} R(z_vl)_i · p_i`。
  - 技能分配**无显式监督**，由下游动作生成损失端到端驱动。

- **状态先验注入**
  - 时间步与本体感觉由小 MLP 编码，经改进的 AdaLN 生成**跨层共享**的调制信号（相比逐层独立参数更省参数）。
  - 视觉语言 token 经线性层 + RMSNorm 后，通过每个 block 的 Cross-Attention 注入。

- **技能相关 FFN（LoRA 式）**
  - 在原始 FFN 之外增加由技能嵌入 `z` 经 MLP 生成的两个矩阵 `W1_z ∈ R^{C×16}`、`W2_z ∈ R^{16×C}`：
    `FFN(x) = W2_z(SwishGLU(W1_z x)) + FFN_ori(x)`
  - 可视为混合专家（MoE）变体：第一项为技能相关“专家”，第二项为共享“专家”。

- **训练目标**
  - 去噪分数匹配损失 `L_SM`，加正交正则：`L = L_SM + γ·L_Orth`，其中 `L_Orth = (1/64)Σ_iΣ_j Cos(p_i, p_j)`，`γ = 0.01`，用于降低技能提示嵌入间的余弦相似度。
  - 推理使用 DDIM，仅 **4 步去噪**。

## 3. 实验设计

### 3.1 仿真 Benchmark
- **CALVIN**
  - 4 个场景配置（A–D），34 个任务，24,000 条语言标注演示。
  - 采用 **ABCD→D** 与更具挑战的 **ABC→D**（零样本迁移到未见环境 D）。
  - 评测 1,000 条指令链，每条含 5 个连续任务；指标为 1–5 连续任务成功率与平均完成长度。
- **LIBERO**
  - 四个 suite：**Spatial / Object / Goal / Long**，各 10 个任务、每任务 50 条人类遥操作演示。

### 3.2 真实世界实验
- 6-DoF **Lebai** 机械臂，9 个任务，每任务采集 30 条轨迹，报告 20 次试验的平均成功率。
- **多任务学习**（6 个任务）：空间感知（放柠檬入锅、开微波炉放薯片）、工具使用（扫方块入簸箕、用勺子搅水）、语义理解（倒水、堆叠方块）。
- **视觉泛化**（3 个任务）：操作未见物体（苹果、香蕉）、含复杂干扰物的柠檬抓放。

### 3.3 对比方法
- CALVIN：DiffPolicy、RoboFlamingo、GR-1、MDT、MoDE、RT-1、OpenVLA、UniVLA、SkillDiffuser。
- LIBERO：DiffPolicy、Octo、MDT、OpenVLA、MaIL、UniActions、UniVLA。
- 真实世界：MoDE、OpenVLA。

### 3.4 实现设置
- 基于 **12-block Diffusion Transformer（DiT）**，在 **OpenX** 上预训练。
- 仿真：AdamW，学习率 `1e-4`，batch size 64，图像缩放至 224×224，40 epochs，3 个随机种子取平均。
- 真实世界：仅用静态相机，训练 200 epochs。

## 4. 资源与算力

- 文中明确提到：仿真任务在 **4 张 A100 GPU** 上微调 **40 epochs**。
- 真实世界实验训练 **200 epochs**，但**未说明 GPU 型号、数量与训练时长**。
- OpenX 预训练阶段的具体算力开销**未报告**。
- 总体而言，算力信息部分披露，真实世界与预训练部分不够完整。

## 5. 实验数量与充分性

- **实验规模**
  - 2 个仿真 benchmark（CALVIN 两种划分、LIBERO 四个 suite）。
  - 1 套真实机器人实验，共 9 个任务，覆盖多任务学习与视觉泛化。
  - 2 组消融：关键组件（Cross-Attention、先验注入、技能抽象、CPE）与技能条件化策略（加法、拼接、FiLM、式(4)）。
  - 1 组复杂度分析（参数量、FLOPs、推理时间）。
  - 1 组技能分配可视化分析。
- **充分性**
  - 覆盖仿真与真实、多任务与泛化、定量与定性分析，整体较为充分；消融在 CALVIN 与 LIBERO-Long 上均有报告。
  - 仿真结果基于 3 个种子，具有一定统计可靠性。
- **客观性与公平性**
  - 基线多为已发表 SOTA，MoDE 使用官方代码重实现（标注 †），比较相对公平。
  - 真实世界基线使用默认超参数微调，但仅报告 20 次试验的平均值，**未给出方差或多随机种子结果**。
  - 真实世界每任务仅 30 条演示，数据规模有限，可能影响结论稳健性。

## 6. 主要结论与发现

- **CALVIN**
  - ABCD→D：五连任务成功率 **86.5%**，平均完成长度 **4.67**，超越 MDT、MoDE 等。
  - ABC→D：五连任务成功率 **76.9%**，比 MoDE 高 **14.5%**，比 UniVLA 高 **20.4%**；平均长度从 3.80 提升至 **4.49**。
  - 仅用 4 步去噪即优于使用 10 步的扩散基线。
- **LIBERO**
  - 平均成功率 **96.9%**，比 MDT 高 13.4%，比 UniVLA 高 4.4%。
  - 是唯一在 **LIBERO-Long** 上超过 90%（93.8%）的策略。
- **真实世界**
  - 在多任务学习（空间感知、工具使用、语义理解）中一致优于 MoDE 与 OpenVLA，复杂任务优势明显。
  - 对未见物体苹果可较好泛化（形状与柠檬相似），但对香蕉等未见形状性能下降。
  - 对视觉干扰物较鲁棒：成功率仅从 75% 降至 65%，基线受干扰严重。
- **可解释性**
  - 尽管技能分配无显式监督，可视化显示分配技能与视觉观测行为良好对齐，能按时间顺序组合技能完成长程任务。
- **消融结论**
  - Cross-Attention 注入视觉语言信息贡献最大；先验注入、技能抽象、CPE 依次带来增益。
  - 技能条件化方式中，LoRA 式 FFN 参数化（式 4）优于加法、拼接与 FiLM。

## 7. 优点

- **问题切入清晰**：准确指出“全局指令—短期动作”粒度错位问题，并以细粒度技能作为中间接口，动机与方案一致。
- **技能设计可解释、可复用**：8 个原始技能跨任务共享，可组合完成复杂任务，便于人类理解与调试。
- **显式技能分配**：不同于 VQ 等隐式离散码本，Router 显式选择技能，透明度和可控性更强。
- **参数高效的条件化设计**：LoRA 式低秩 FFN 仅增加少量参数即可建立技能与动作的依赖；AdaLN 跨层共享调制信号减少参数。
- **统一模型多任务**：所有技能在单一模型中学习，而非为每个技能训练独立策略，更高效。
- **工程效率考虑**：CPE 提示可预计算缓存；仅 4 步去噪即可生成动作。
- **实验覆盖较全面**：两个挑战性仿真 benchmark + 真实机器人部署，兼顾多任务、长程与视觉泛化，并配有消融、复杂度与可视化分析。

## 8. 不足与局限

- **计算开销增加**：模型参数量 1017M（MoDE 为 780M），FLOPs 74.5G，推理时间 45.1ms（比 MoDE 多约 14.6ms），实时性受限场景需权衡。
- **技能集合手工固定**：仅 8 个预定义原始技能，可能不足以覆盖高灵巧、双臂、精细装配等更复杂操作；技能粒度与完备性缺乏系统性验证。
- **技能分配无显式监督**：Router 完全由动作损失驱动，分配错误可能难以诊断，且缺乏技能级标注或准确率评估。
- **真实世界实验规模有限**：每任务仅 30 条演示、20 次试验，未报告方差或多随机种子；任务种类与物体多样性仍有限。
- **泛化边界明显**：对未见形状（香蕉）性能下降，说明视觉泛化仍依赖与训练物体形状的相似性。
- **算力信息不完整**：真实世界训练与 OpenX 预训练的 GPU 数量、时长未说明，复现成本不易评估。
- **基准饱和风险**：LIBERO 上部分 suite 已接近 99%，进一步提升空间有限，区分度可能下降。
- **跨本体泛化未验证**：仅在单一 Lebai 机械臂与仿真环境验证，未讨论跨机器人本体或跨场景的迁移能力。
- **依赖外部预训练模型**：CLIP 文本编码器、Florence-2 词嵌入、OpenX 预训练等组件的贡献与耦合影响未单独分析。

（完）
