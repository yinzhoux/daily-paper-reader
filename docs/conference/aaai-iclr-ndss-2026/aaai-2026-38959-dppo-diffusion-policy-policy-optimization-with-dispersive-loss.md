---
title: "D²PPO: Diffusion Policy Policy Optimization with Dispersive Loss"
title_zh: 带分散损失的扩散策略策略优化
authors: "Guowei Zou, Weibing Li, Hejun Wu, Yukun Qian, Yuhang Wang, Haitao Wang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38959/42921"
tags: ["query:humanoid-rl"]
score: 8.0
evidence: 结合强化学习优化的扩散操作策略，用分散损失防止表示坍缩
tldr: 针对扩散策略在机器人操作中出现的表示坍缩问题，即语义相近的观测被映射为难以区分的特征，本文提出D2PPO。该方法引入分散损失正则，将批次内所有隐藏表示视为负样本对，迫使网络学习更具判别性的观测表示，并结合策略优化进行训练。实验表明该方法能更好处理复杂操作中的细微关键变化，说明结构化、判别性的表示学习对提升操作策略性能具有重要作用。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 扩散策略在复杂机器人操作中存在表示坍缩，语义相近观测难以区分，影响精细操作。
method: 提出D2PPO，用分散损失将批内隐藏表示互为负样本，学习判别性表示并联合策略优化。
result: 实验表明该方法缓解表示坍缩，提升了对细微关键变化的操作能力。
conclusion: 判别性表示正则可显著增强扩散操作策略的鲁棒性与表达能力。
---

## Abstract
Diffusion policies excel at robotic manipulation by naturally modeling multimodal action distributions in high-dimensional spaces. Nevertheless, diffusion policies suffer from diffusion representation collapse: semantically similar observations are mapped to indistinguishable features, ultimately impairing their ability to handle subtle but critical variations required for complex robotic manipulation. To address this problem, we propose D²PPO (Diffusion Policy Policy Optimization with Dispersive Loss). D²PPO introduces dispersive loss regularization that combats representation collapse by treating all hidden representations within each batch as negative pairs. D²PPO compels the network to learn discriminative representations of similar observations, thereby enabling the policy to identify subtle yet crucial differences necessary for precise manipulation. In evaluation, we find that early-layer regularization benefits simple tasks, while late-layer regularization sharply enhances performance on complex manipulation tasks. On RoboMimic benchmarks, D²PPO achieves an average improvement of 22.7% in pre-training and 26.1% after fine-tuning, setting new SOTA results. In comparison with SOTA, the results of real-world experiments on a Franka Emika Panda robot show the excitingly high success rate of our method. The superiority of our method is especially evident in complex tasks.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：扩散策略（Diffusion Policy）虽能建模高维、多模态动作分布，但在复杂机器人操作中常出现 **扩散表示坍缩（diffusion representation collapse）**：语义相近但任务含义不同的观测被编码为几乎不可区分的特征，导致策略对细微但关键的变化不敏感，进而生成错误动作。
- **背景与动机**：
  - 标准扩散策略主要依赖重构/去噪损失，只优化噪声预测精度，忽视中间特征表示的判别性与多样性。
  - 在抓取、孔轴装配、多物体搬运等任务中，观测差异很小但所需动作可能完全不同；表示坍缩会直接造成任务失败。
  - 传统对比学习可增强特征判别性，但通常依赖正负样本对、额外预训练、辅助模型或外部数据，不完全适合扩散策略训练。
- **整体含义**：论文将复杂操作失败归因于表示质量问题，提出用轻量的“分散损失”正则化扩散策略的中间表示，并结合策略梯度微调，形成两阶段训练框架 D²PPO。

## 2. 方法论：核心思想、关键技术细节与流程

- **核心思想**：
  - 采用“**无正样本对的对比损失**”思想：从 InfoNCE 中去掉正样本对齐项，仅保留使批内表示相互分散的项。
  - 将同一批次内所有隐藏表示互为负样本，迫使网络学习更具判别性的特征，避免相似观测被映射到同一特征簇。
- **两阶段训练框架**：
  1. **分散损失预训练**：在标准扩散损失上加入分散损失正则，增强表示多样性。
  2. **PPO/策略梯度微调**：以增强后的扩散策略为初始化，通过策略梯度优化任务回报。
- **预训练目标**：
  - 总损失为 `L_pre-train = L_diff + λ L_disp`。
  - `L_diff` 保证去噪/噪声预测准确；`L_disp` 鼓励批内特征分散；`λ` 控制正则强度。
  - 分散损失在多个去噪时间步上平均计算，并施加于 MLP 去噪网络的选定中间层。
- **三种分散损失变体**：
  - **InfoNCE-L2**：以平方 L2 距离衡量表示差异，鼓励几何空间分散。
  - **InfoNCE-Cosine**：以余弦不相似度衡量方向差异，具有尺度不变性。
  - **Hinge**：对距离小于 margin 的表示对进行惩罚，直接控制最小分散距离。
- **微调阶段**：
  - 扩散策略的动作概率涉及完整去噪链，无法像普通策略一样直接获得 `π(a|s)`。
  - 使用链式法则将策略梯度分解到各去噪步的条件概率上，并采用重要性采样只计算部分去噪步，以降低计算成本。
  - 使用步条件优势估计进行策略梯度更新，同时尽量保留预训练得到的表示结构。
- **方法特点**：不引入额外模型参数、不依赖额外预训练阶段或外部数据，具有即插即用性质。

## 3. 实验设计：数据集/场景、Benchmark 与对比方法

- **仿真 Benchmark**：RoboMimic 四个代表性操作任务：
  - **Lift**：基础物体抓取，最简单。
  - **Can**：圆柱物体抓取，中等难度。
  - **Square**：精确孔轴装配，高难度。
  - **Transport**：多物体协调搬运，最高难度。
- **任务难度定义**：基于平均执行步数并进行对数归一化，形成难度层级。
- **预训练实验**：
  - 对比基线 DPPO 与五种分散损失配置：InfoNCE-L2 Early/Mid/Late、InfoNCE-Cosine Early、Hinge Early。
  - 分析不同网络层施加分散损失对任务性能的影响。
- **微调实验**：
  - 在四个任务上比较 D²PPO 与 DPPO、Gaussian 策略及多种已有方法。
  - 表 2 对比方法包括 LSTM-GMM、IBC、BET、DiffusionPolicy-C、DiffusionPolicy-T、DPPO、MTIL（10-step/Full History）等。
- **真实机器人实验**：
  - 在 Franka Emika Panda 机器人上部署 D²PPO。
  - 每个任务进行 100 次试验，并与基线方法比较；重点展示 Square 和 Transport 等复杂任务。
- **消融实验**：
  - 在 Square 任务上分析分散损失系数 `λ` 的影响。
  - 通过热图分析不同层、不同分散损失变体在各任务上的适用性。

## 4. 资源与算力

- **论文给定文本未明确说明**使用的 GPU 型号、GPU 数量、训练时长、总计算量或参数量规模。
- 因此无法从文中判断：
  - 预训练与微调的实际算力成本；
  - 方法相对基线的训练效率；
  - 真实机器人实验的部署计算资源。
- 这会影响对方法可复现性和实际部署成本的完整评估。

## 5. 实验数量与充分性

- **实验规模大致包括**：
  - 四个 RoboMimic 任务上的预训练实验；
  - 五种分散损失变体与层位置的组合分析；
  - 四个任务上的策略梯度微调实验；
  - 表 2 中约九种方法的成功率对比；
  - Square 任务上的 `λ` 消融；
  - 四个真实机器人任务，每任务 100 次试验，约 400 次真实试验。
- **充分性优点**：
  - 覆盖了从简单到复杂的四类操作任务；
  - 同时包含预训练、微调、消融和真机验证；
  - 使用成功率、平均值、中位数、标准差和排名等指标，结果呈现较完整；
  - 真实机器人每任务 100 次试验，统计上比少量演示更有说服力。
- **局限**：
  - `λ` 消融仅在 Square 任务上进行，超参数敏感性分析不够全面；
  - 层位置与分散损失变体的选择呈现任务相关性，但缺少系统的跨任务联合消融；
  - 未明确说明随机种子数量、误差条计算方式和统计显著性检验；
  - 表 2 中部分基线可能引用已有结果，论文未详细说明所有基线的训练预算、调参协议和数据条件，因此跨方法比较的完全公平性仍需谨慎看待；
  - 真实实验每任务 100 次较充分，但环境随机化、初始条件分布和失败模式统计细节有限。

## 6. 主要结论与发现

- **表示坍缩是复杂操作失败的重要根因**：相似观测被编码为不可区分特征，导致策略无法做出上下文敏感的动作选择。
- **分散损失能有效缓解表示坍缩**：加入分散正则后，特征分布更分散、更具判别性，学习曲线收敛更快且最终成功率更高。
- **层位置与任务复杂度相关**：
  - 简单任务更适合在早期层施加正则；
  - 复杂任务从后期层正则中获益更明显。
- **任务越复杂，表示质量越关键**：论文报告任务难度与最大改进率呈强正相关（R²=0.92）。
- **性能提升显著**：
  - 预训练阶段平均提升约 **22.7%**；
  - 微调后平均提升约 **26.1%**；
  - 表 2 中 D²PPO 平均成功率 **0.94**，中位数 **0.95**，排名第一；
  - Transport 从 DPPO 的 0.60 提升到 0.87，Square 从 0.83 提升到 0.89。
- **真实机器人验证有效**：Transport 任务成功率从 Gaussian 的 0% 到 DPPO 的 45%，再到 D²PPO 的 70%；Square 任务中无分散损失的 DPPO 在最终放置阶段失败。
- **超参数需平衡**：Square 上 `λ=0.5` 表现最佳，过低正则不足，过高可能干扰任务相关学习。

## 7. 优点

- **问题识别有价值**：明确将扩散策略在复杂操作中的失败归因于中间表示坍缩，而非仅归因于动作生成或策略优化。
- **方法轻量且实用**：分散损失不需要额外参数、额外预训练或外部数据，可直接集成到现有扩散策略中。
- **训练框架清晰**：预训练增强表示、微调优化回报的两阶段设计逻辑合理，兼顾生成建模能力与任务目标。
- **实验链路完整**：从仿真预训练、微调对比到真实机器人部署，验证层次较完整。
- **复杂任务提升突出**：在 Square、Transport 等高难度任务上改进明显，说明方法针对了真实瓶颈。
- **对层位置和损失变体进行了探索**：提供了早期层/后期层与任务复杂度关系的经验性结论，对后续应用有参考价值。
- **真实机器人每任务 100 次试验**：相比仅展示少量成功案例，统计可靠性更好。

## 8. 不足与局限

- **算力与训练成本未报告**：缺少 GPU 型号、数量、训练时长等信息，难以评估实际开销和可复现性。
- **表示坍缩诊断偏定性**：主要依赖聚类可视化和性能曲线，缺少更系统的定量表示质量指标或跨数据集诊断。
- **实验覆盖有限**：
  - 仅覆盖 RoboMimic 四个操作任务和 Franka 真机，未验证其他机器人形态、视觉域或更广泛操作场景；
  - 未与 REPA 等其他表示正则方法进行直接实验比较。
- **超参数与层选择需任务相关调参**：不同任务适合不同层和变体，实际应用中可能需要额外搜索；`λ` 在 Square 上呈非单调关系，说明敏感性存在。
- **公平性细节不足**：与 SOTA 的比较中，部分基线结果来源、训练预算和调参协议未充分说明，跨方法公平性不能完全确认。
- **真实实验细节有限**：每任务 100 次试验较好，但环境随机化、初始状态分布、失败类型统计和安全性分析未展开。
- **应用限制**：方法仍依赖扩散策略和策略梯度微调，在线交互成本与真实部署风险需要进一步评估；表示分散正则过强时可能破坏任务相关结构。

（完）
