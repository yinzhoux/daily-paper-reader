---
title: "Rethinking Progression of Memory State in Robotic Manipulation: An Object-Centric Perspective"
title_zh: 重思机器人操作中的记忆状态演进：对象中心视角
authors: "Nhat Chung, Taisei Hanyu, Toan Nguyen, Huy Le, Frederick Bumgarner, Duy Minh Ho Nguyen, Khoa Vo, Kashu Yamazaki, Chase Rainwater, Tung Kieu, Anh Nguyen, Ngan Le"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37337/41299"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 面向具身操作智能体的对象中心表征与记忆
tldr: 针对非马尔可夫操作任务中关键决策线索藏在物体历史而非当前场景的问题，本文从对象中心视角重新审视机器人操作的记忆状态演进。作者构建了 LIBERO-Mem 任务套件，在对象级部分可观测条件下对视觉运动策略进行压力测试，涵盖短程与长程序列交互。研究揭示了缺乏持久对象记忆时策略会重复或遗漏动作，凸显对象中心表征与记忆对具身智能体的必要性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 在非马尔可夫操作中，关键线索存在于物体历史，缺乏持久对象记忆会使视觉运动策略失效。
method: 从对象中心视角构建 LIBERO-Mem 任务套件，在对象级部分可观测下压力测试操作策略。
result: 实验显示无持久对象记忆的策略会重复或遗漏动作，暴露了记忆建模的必要性。
conclusion: 对象中心表征与记忆是具身操作智能体应对复杂序列任务的关键。
---

## Abstract
As embodied agents operate in increasingly complex environments, the ability to perceive, track, and reason about individual object instances over time becomes essential, especially in tasks requiring sequenced interactions with visually similar objects. In non-Markovian settings, critical decision cues lie in object histories rather than the current scene. Without persistent memory of prior interactions (what was used, where it was placed, or how it changed), visuomotor policies may fail, repeat past actions, or overlook completed ones. To surface this challenge, we introduce LIBERO-Mem, a non-Markovian task suite for stress-testing robotic manipulation under object-level partial observability. It combines short- and long-horizon object tracking with temporally sequenced subgoals, requiring reasoning beyond the current frame. However, vision-language-action (VLA) models often struggle in such settings, with token scaling quickly becoming intractable even for tasks spanning just a few hundred frames. We propose Embodied-SlotSSM, a slot-centric VLA framework built for temporal scalability. It maintains spatio-temporally consistent slot identities and leverages them through two mechanisms: (1) slot-state-space modeling for reconstructing short-term history, and (2) a relational encoder to align the input tokens with action decoding. Together, these components enable temporally grounded, context-aware action prediction. Experiments show Embodied-SlotSSM's baseline performance on LIBERO-Mem and general tasks, offering a scalable solution for non-Markovian reasoning in object-centric policies.

---

## 论文详细总结（自动生成）

## 1. 核心问题与研究动机

- 论文关注**非马尔可夫机器人操作**中的**对象级记忆**问题：智能体需要在长时间交互中记住“某个物体是否被拿过、放在哪里、操作了几次、与其他物体的关系如何变化”。
- 在真实任务中，当前视觉观测往往不能唯一决定正确动作：两个时刻的画面可能几乎相同，但由于历史不同，正确动作不同。这被建模为**对象级 POMDP**，即部分可观测马尔可夫决策过程。
- 现有 VLA（视觉-语言-动作）模型大多采用**马尔可夫假设**，仅根据当前观测和语言指令预测动作，缺乏对对象历史的持久记忆，容易重复动作、遗漏已完成步骤或在视觉相似物体间混淆。
- 现有机器人 benchmark 多聚焦短时程或原子任务，已有记忆 benchmark 也较少系统测试**对象身份歧义、遮挡、关系顺序、重复操作**等对象级 POMDP 场景。
- 因此，论文提出两个核心贡献：
  - **LIBERO-Mem**：面向对象级部分可观测的非马尔可夫操作任务套件；
  - **Embodied-SlotSSM**：基于对象槽位与状态空间模型的记忆增强 VLA 框架。

## 2. 方法论

### 2.1 核心思想

- 用**对象中心槽位（slot）**表示场景中的离散实体，并为每个槽位维护跨时间的隐状态，从而在视觉相似或遮挡情况下仍能追踪对象身份与交互历史。
- 用**状态空间模型（SSM）**替代对完整历史稠密 token 的显式建模，以缓解长时程序列中 token 数量线性增长带来的计算与显存问题。
- 通过“短期历史重建 + 关系编码 + 动作解码”实现时序 grounded 的动作预测。

### 2.2 关键技术细节

- **问题形式化**：传统 VLA 假设  
  \(P(a_t|v_{1:t},l)=P(a_t|v_t,l)\)。  
  论文针对存在 \(v_{t1}\approx v_{t2}\) 但正确动作不同的非马尔可夫情形，要求策略依赖对象历史 \(H_t\) 而非当前帧。
- **Slot Attention 对象定位**：
  - 将视觉编码器输出的稠密特征绑定到 \(K=16\) 个对象槽 \(s_t=\{s_t^1,\dots,s_t^K\}\)。
  - 通过多头注意力与 GRU 迭代更新槽位，使槽位对应场景中的对象实体。
  - 时间 \(t=0\) 时随机初始化槽位；\(t>0\) 时用上一时刻最终槽位初始化，以保持对象身份跨时间一致。
- **时序对比损失**：
  - 对锚槽 \(s_t^i\)，将邻近帧中对应槽作为正样本，不同视频或不同位置的槽作为负样本，使用余弦相似度和温度系数 \(\tau=1\) 的对比损失增强时序一致性。
- **SlotSSM 状态空间建模**：
  - 对每个槽独立建模输入依赖的递推：
    \(h_t=A(e_t)h_{t-1}+B(e_t)e_t,\quad y_t=C(e_t)h_t\)。
  - \(A,B,C\) 设计为块对角形式，每个块仅由对应槽输入条件化，从而保持对象级模块化隐状态。
- **瞬态记忆与窗口重建**：
  - SlotSSM 不只预测下一帧，而是预测以当前时刻为中心、包含 \(p\) 帧过去和 \(q\) 帧未来的槽潜变量窗口。
  - 通过共享的 Past MLP 重建短期历史，使模型学习运动连续性、平滑噪声并增强非马尔可夫条件下的表示稳定性。
- **动作控制与关系编码**：
  - 在实验实现 **Naive E-SlotSSM** 中，由于长时程观测分块限制，额外输入 oracle 子目标 \(g_t\)（如“bowl 1 on plate 3”）。
  - Slot Fusion 融合当前槽 \(s_t\)、预测下一槽 \(\hat{s}_{t+1}\) 和 oracle 子目标，得到槽动态 \(d_t\)。
  - Relation Encoder 通过交叉注意力将槽动态与原始视觉特征对齐，生成 16 个关系 token。
  - 动作解码器（图中标注为 Frozen LLM Action Decoder）基于关系 token、槽动态和语言查询 \(l\) 预测动作，如 \(\Delta x,\Delta\theta,\Delta grasp\)。

## 3. 实验设计

- **实验环境**：全部在仿真中进行，基于 LIBERO 场景，固定布局并随机初始化物体位姿。
- **数据集 / Benchmark**：
  - **LIBERO-Goal**：用于评估一般马尔可夫操作任务，共 10 个任务。
  - **LIBERO-Mem**：论文提出的非马尔可夫对象级记忆 benchmark，共 10 个任务，覆盖四类记忆维度：
    - Object Motion（OM）：物体运动/放置状态记忆；
    - Object Sequence（OS）：重复操作次数记忆；
    - Object Relation（OR）：物体间关系与顺序记忆；
    - Object Occlusion（OO）：遮挡物体记忆。
  - 每个任务包含 200–700 帧，收集 120 条轨迹，其中 100 条训练、20 条验证；评估使用 \(N=20\) 个随机种子。
- **评价指标**：
  - LIBERO-Goal：任务成功率；
  - LIBERO-Mem：子目标完成率（subgoal completion），按总子目标完成比例计算。
- **对比方法**：
  - \(\pi_0\)（\(h=1\)，256 tokens）；
  - SlotVLA / OpenVLA + Slot Attention（\(h=1\)，16 tokens；\(h=8\)，128 tokens）；
  - Naive E-SlotSSM（32 tokens，使用 oracle 子目标）。
- **其他分析**：对任务 T1 进行槽注意力可视化，观察 gripper 与 bowl 槽位在抬升和放置过程中的一致性。

## 4. 资源与算力

- 论文**未明确报告**使用的 GPU 型号、GPU 数量、训练时长、模型参数量、显存占用或推理成本。
- 仅说明实验在仿真中完成，每个任务使用 \(N=20\) 个随机种子。
- 因此无法从论文中评估其训练/推理算力开销与可复现性。

## 5. 实验数量与充分性

- 实验覆盖 **2 个 benchmark、共 20 个任务**，每个任务 20 个种子；对比了 \(\pi_0\)、SlotVLA 的两种时程配置以及 Naive E-SlotSSM。
- 另有一组槽注意力定性可视化。
- **不足**：
  - 正文中**没有显式消融实验**，未单独分析 Slot Attention、SlotSSM、时序对比损失、窗口预测、Relation Encoder、oracle 子目标等各组件的贡献。
  - 未报告方差、置信区间或统计显著性；20 个种子的结果稳定性有限。
  - 对比公平性存在问题：Naive E-SlotSSM 使用 **oracle 子目标**，而基线没有；同时不同方法的 token 预算不同（16/32/128/256），因此性能提升不能完全归因于记忆架构。
  - 未在真实机器人上验证，也未与更多记忆增强 VLA 或长时程策略进行系统比较。
- 总体而言，实验能说明“现有反应式 VLA 在对象级 POMDP 下明显失效”，但**不足以充分证明各方法组件的必要性**，结论应视为初步 baseline。

## 6. 主要结论与发现

- 现有 VLA 模型在 LIBERO-Mem 上表现很差：\(\pi_0\) 和 SlotVLA 的平均子目标完成率仅约 5.0%，说明纯反应式策略难以处理对象级部分可观测任务。
- Naive E-SlotSSM 在 LIBERO-Mem 上取得最高平均子目标完成率 **14.8%**，在 T1、T3、T5、T9、T10 上有部分成功，表明槽位时序记忆对重复操作、遮挡和部分关系任务有帮助。
- 在 LIBERO-Goal 上，Naive E-SlotSSM 平均成功率 **83.0%**，高于 SlotVLA \(h=8\) 的 75.5% 和 SlotVLA \(h=1\) 的 32.0%，说明对象中心记忆设计在一般操作任务上也有收益。
- 槽位可视化显示模型能在抬升和放置过程中持续关注同一对象，表现出一定的对象永久性与跟踪能力。
- 但绝对性能仍然较低，T2、T4、T6、T7、T8 等任务为零成功，说明长时程重复、关系重排和复杂遮挡仍是开放挑战；作者也承认子目标 grounding 是关键瓶颈。

## 7. 优点

- **问题定义清晰且重要**：将机器人操作中的记忆问题明确为对象级 POMDP，而非简单的帧历史建模。
- **Benchmark 设计有针对性**：LIBERO-Mem 覆盖运动、序列、关系、遮挡四类对象记忆，并包含对象身份歧义、子目标标注和时序压力测试。
- **方法具有结构性和可扩展性**：Slot Attention 提供对象级离散表示，SlotSSM 以线性递推维护对象历史，避免全历史稠密 token 的线性膨胀。
- **时序一致性设计较完整**：上一时刻槽位初始化、时序对比损失、过去-未来窗口重建共同增强对象跟踪与短期动态

建模。
- **模块化设计便于扩展**：对象槽位与槽位级 SSM 隐状态将“对象身份—历史—动态”解耦，理论上可扩展到更多对象、更长时程以及多模态对象属性记忆。
- **Benchmark 与方法形成闭环**：LIBERO-Mem 的任务维度与 Embodied-SlotSSM 的对象级记忆机制相对应，便于后续研究者围绕对象运动、序列、关系和遮挡分别分析失败模式。
- **对“记忆”而非“帧堆叠”的强调具有方法论价值**：论文没有简单增加历史帧或 token 数，而是尝试用对象中心表示和递推状态压缩历史，这为长时程 VLA 的记忆设计提供了可讨论的结构性方案。

## 8. 局限与风险

- **真实世界有效性未知**：全部实验在仿真中完成，未涉及真实机器人中的感知噪声、标定误差、物体外观变化、动态遮挡和抓取失败恢复，因此方法的现实鲁棒性无法判断。
- **oracle 子目标削弱结论强度**：Naive E-SlotSSM 依赖 oracle 子目标输入，而基线方法没有同等信息；这使 LIBERO-Mem 上的性能提升不能完全归因于对象级记忆架构，也说明系统离端到端长时程自主决策仍有距离。
- **缺少组件消融**：Slot Attention、时序对比损失、SlotSSM、窗口重建、Relation Encoder、槽位继承初始化等设计均未单独验证，无法判断哪些模块真正贡献了性能，哪些可能只是增加复杂度。
- **绝对性能仍然很低**：LIBERO-Mem 上最高平均子目标完成率仅 14.8%，多数任务接近或等于零成功，说明论文展示的是“反应式 VLA 会失败”的现象，而非已经解决对象级 POMDP。
- **对比公平性有限**：不同方法的 token 预算、历史长度和辅助信息不一致；20 个随机种子虽提供一定重复性，但未报告方差、置信区间或显著性检验，结果稳定性与统计可信度不足。
- **任务与数据规模偏小**：LIBERO-Mem 仅 10 个任务，每任务 100 条训练轨迹，场景基于 LIBERO 固定布局；这对训练大型 VLA 或评估泛化能力而言规模有限，也可能放大特定任务设计的影响。
- **对象身份跟踪仍依赖较强假设**：槽位在 \(t>0\) 时用上一时刻槽位初始化，且槽数固定为 16；当对象数量变化、对象离开视野后重新进入、严重遮挡或外观高度相似时，槽位身份是否稳定仍缺少系统压力测试。
- **长时程记忆容量与遗忘机制未充分讨论**：SSM 隐状态虽然避免 token 线性增长，但固定容量隐状态在数百至数千帧后能否保留关键对象历史、如何处理无关历史干扰，论文没有给出定量分析。
- **评价指标较粗**：子目标完成率能反映部分进展，但不能区分“正确完成子目标”与“偶然满足子目标条件”，也未报告动作精度、重复操作次数、对象混淆率等更细粒度记忆指标。
- **缺少失败模式分析**：正文未系统统计失败原因是语言 grounding、槽位错配、历史遗忘、动作解码还是子目标预测错误，因此对后续改进的指导有限。

## 9. 启示与可改进方向

- **统一信息预算与公平基线**：后续工作应在相同 token 预算、相同历史长度、相同辅助信息条件下比较对象槽位记忆、历史帧拼接、循环 VLA、外部记忆库等方案，并将 oracle 子目标替换为学习得到的子目标预测器。
- **补足消融与统计报告**：至少应分别移除时序对比损失、窗口重建、槽位继承、SlotSSM 递推和 Relation Encoder，并报告多种子均值、方差和显著性检验。
- **强化对象重识别与生命周期管理**：可引入显式对象 ID、槽位新生/消亡机制、跨遮挡重识别损失和对象数量自适应机制，以处理对象离开视野后重新出现、遮挡和相似物体混淆。
- **将记忆与语言 grounding 更紧密结合**：论文作者已承认子目标 grounding 是瓶颈；未来可将对象历史与语言中的指代表达、任务进度状态联合建模，而不是仅将语言作为动作解码查询。
- **从仿真走向真实机器人**：需要在真实平台上评估感知噪声、抓取失败恢复、动态场景和长期运行中的记忆漂移，并报告推理延迟与显存开销。
- **扩展 benchmark 的难度与多样性**：可增加对象数量变化、不可逆操作、跨任务记忆复用、干扰物体、动态遮挡和更长时程任务，以更全面检验对象级 POMDP 能力。

## 10. 总体评价

- 论文提出了一个**重要且被现有 VLA 研究相对忽视的问题**：机器人操作中的对象级部分可观测性与长时程对象记忆，并通过 LIBERO-Mem 将对象运动、序列、关系和遮挡四类记忆需求显式化，具有较好的 benchmark 价值。
- 方法层面，Embodied-SlotSSM 将 Slot Attention 的对象中心表示与 SSM 的递推记忆结合，思路清晰、结构合理，为“用对象级状态压缩历史”提供了可复用的框架。
- 但当前实验证据仍属**初步验证**：LIBERO-Mem 绝对成功率很低，Naive E-SlotSSM 依赖 oracle 子目标，缺少消融、统计检验和真实机器人实验，因此尚不足以证明该架构已有效解决非马尔可夫操作问题。
- 更准确的定位是：论文指出了一个关键问题，给出了一个有潜力的结构性方案和有针对性 benchmark，但距离稳健、端到端、可实际部署的对象级记忆 VLA 仍有明显距离。

（完）
