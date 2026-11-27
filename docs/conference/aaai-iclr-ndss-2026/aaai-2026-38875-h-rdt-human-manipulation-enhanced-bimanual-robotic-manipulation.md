---
title: "H-RDT: Human Manipulation Enhanced Bimanual Robotic Manipulation"
title_zh: H-RDT：以人类操作增强双臂机器人操作
authors: "Hongzhe Bi, Lingxuan Wu, Tianwei Lin, Hengkai Tan, Zhizhong Su, Hang Su, Jun Zhu"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38875/42837"
tags: ["query:humanoid-rl"]
score: 6.0
evidence: 利用人类数据先验的双臂操作模仿学习
tldr: 机器人操作模仿学习受限于高质量机器人示范数据的稀缺，跨本体数据又因形态与动作空间差异难以统一训练。本文提出H-RDT，利用带三维手部姿态标注的大规模第一人称人类操作视频，从中提取自然操作策略的行为先验来增强机器人操作能力。方法通过扩散Transformer将人类先验迁移到机器人双臂操作中。该工作缓解了机器人数据瓶颈，为跨本体模仿学习提供了新思路。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 机器人操作模仿学习面临大规模高质量示范数据稀缺的核心难题。
method: 提出H-RDT，用带三维手部姿态的人类操作视频作为行为先验增强双臂操作。
result: 方法借助人类数据先验缓解数据瓶颈，提升双臂操作模仿学习效果。
conclusion: 该工作为跨本体、数据高效的机器人操作学习提供了可行途径。
---

## Abstract
Imitation learning for robotic manipulation faces a fundamental challenge: the scarcity of large-scale, high-quality robot demonstration data. Recent robotic foundation models often pre-train on cross-embodiment robot datasets to increase data scale, while they face significant limitations as the diverse morphologies and action spaces across different robot embodiments make unified training challenging. In this paper, we present  H-RDT (Human to Robotics Diffusion Transformer), a novel approach that leverages human manipulation data to enhance robot manipulation capabilities. Our key insight is that large-scale egocentric human manipulation videos with paired 3D hand pose annotations provide rich behavioral priors that capture natural manipulation strategies and can benefit robotic policy learning. We introduce a two-stage training paradigm: (1) pre-training on large-scale egocentric human manipulation data, and (2) cross-embodiment fine-tuning on robot-specific data with modular action encoders and decoders. Built on a diffusion transformer architecture with 2B parameters, H-RDT uses flow matching to model complex action distributions. The modular design of action encoder and decoder components enables effective knowledge transfer from the unified human embodiment to diverse robot platforms through efficient fine-tuning. Extensive evaluations encompassing both simulation and real-world experiments, single-task and multitask scenarios, as well as few-shot learning and robustness assessments, demonstrate that H-RDT outperforms training from scratch and existing state-of-the-art methods, including π0 and RDT, achieving significant improvements of 13.9% and 40.5% over training from scratch in simulation and real-world experiments, respectively. The results validate our core hypothesis that human manipulation data can serve as a powerful foundation for learning bimanual robotic manipulation policies.

---

## 论文详细总结（自动生成）

# H-RDT 论文结构化总结

## 1. 核心问题与整体含义

- **研究动机**：机器人操作模仿学习高度依赖大规模、高质量机器人示范数据，但这类数据主要通过遥操作采集，成本高、设备复杂、操作者技能要求高，难以规模化。
- **现有路线局限**：当前机器人基础模型常采用跨本体机器人数据预训练，但不同机器人形态、末端执行器、动作空间差异大，统一训练困难；现有机器人数据集规模和数据质量也有限。
- **论文核心洞察**：大规模第一视角人类操作视频，若配有逐帧 3D 手部姿态标注，可提供丰富的操作行为先验，包括抓取方式、双手协调、物体可供性、任务分解等，可作为机器人策略学习的基础。
- **整体含义**：论文提出 H-RDT，试图把“人类操作数据”作为机器人双臂操作的可扩展数据源，通过统一人类动作表示和跨本体微调，将人类操作先验迁移到多种机器人平台，从而缓解机器人示范数据稀缺问题。

## 2. 方法论

### 2.1 核心思想

- 采用**两阶段训练范式**：
  1. **人类数据预训练**：在大规模第一视角人类操作数据上学习操作先验；
  2. **跨本体机器人微调**：通过模块化动作编码器/解码器，将预训练模型适配到不同机器人动作空间。
- 使用 **2B 参数扩散 Transformer** 作为策略骨干，并以 **Flow Matching** 建模复杂动作分布。
- 通过一个共享的 **48 维人类手部动作表示** 桥接人类与机器人本体差异。

### 2.2 问题形式化

- 策略 \(\pi_\theta\) 根据多模态观测生成未来动作序列：
  - 输入：RGB 视觉观测 \(o_t\)、机器人本体状态 \(s_t\)、语言指令 \(l\)；
  - 输出：未来 \(H\) 步动作序列 \(a_{t:t+H}\)。
- 目标是学习可泛化、可跨本体部署的操作策略。

### 2.3 人类动作表示设计

- 将人类双手操作表示为 **48 维向量**：
  - **双侧手腕位姿**：每只手位置 3 维 + 旋转 6 维，共 \(2 \times 9 = 18\) 维；
  - **双手指尖位置**：每手 5 指 × 3 维 × 2 手 = 30 维。
- 该表示与多数使用末端执行器位姿控制的机器人动作空间兼容，可视为其“超集”，便于知识蒸馏和跨本体迁移。
- 设计意图是显式编码抓取构型、方向约束、相对空间关系等可迁移操作特征。

### 2.4 两阶段训练流程

- **Stage 1：人类数据预训练**
  - 在 EgoDex 数据集上训练，使用 338K+ 轨迹、194 类操作任务；
  - 动作空间为 48 维人类手部表示；
  - 学习人类操作策略、物体交互和双手协调模式。
- **Stage 2：跨本体微调**
  - 迁移视觉编码器、语言编码器和 Transformer 骨干权重；
  - **重新初始化**状态适配器、动作适配器和动作解码器，以匹配目标机器人动作空间；
  - 例如双臂 7-DOF + 平行夹爪可对应 14 维机器人动作。
- 这种选择性迁移保留视觉-语义和操作先验，同时让模块化动作接口适配不同机器人形态。

### 2.5 Flow Matching 动作生成

- 不采用传统扩散目标，而使用 Flow Matching 学习从噪声到目标动作序列的连续向量场。
- 构造直线流路径：
  - \(a_\tau = \tau \cdot a^*_{t:t+H} + (1-\tau)z\)，其中 \(z \sim \mathcal{N}(0,I)\)，\(\tau \in [0,1]\)。
- 训练损失：
  - \(\mathcal{L}_{FM} = \mathbb{E}_{\tau,z,a^*,c}\left[\|v_\theta(a_\tau,\tau,c) - (z-a^*_{t:t+H})\|^2\right]\)。
- 条件信息 \(c=\{o_t,s_t,l\}\) 包括多视角 RGB、本体状态和语言指令。
- 推理时通过 ODE solver 积分学习到的向量场生成动作。

### 2.6 网络架构

- **视觉编码器**：DinoV2 + SigLIP，后接 MLP 适配器；
- **语言编码器**：T5-XXL，后接投影适配器；
- **模块化动作编码器**：状态和噪声动作分别经 MLP adapter 映射到 Transformer 维度；
- **Transformer 骨干**：LLaMA-3 风格，使用 RMSNorm、SwiGLU、自注意力处理状态/动作 token，图像和语言通过独立 cross-attention 注入，Flow time 通过 AdaLN 注入；
- **模块化动作解码器**：MLP 解码为目标机器人动作空间。
- 微调时动作编码器、状态适配器和动作解码器可针对每个目标本体重新训练。

## 3. 实验设计

### 3.1 仿真实验

- **Benchmark**：RoboTwin 2.0 双臂操作基准。
- **评估模式**：
  - Easy：干净桌面环境；
  - Hard：域随机化，包括 3cm 桌高变化、随机背景、光照变化、物体杂乱等。
- **机器人本体**：
  - Aloha-Agilex-1.0；
  - 双臂 Franka-Panda。
- **任务设置**：
  - 单任务：13 个代表性任务，每任务 50 条示范；
  - 多任务：45 个任务，约 2250 条域随机化示范，表中展示 10 个代表任务。
- **指标**：任务成功率。

### 3.2 真实世界实验

- **Aloha-Agilex-2.0 / 双臂 Piper**：
  - 任务 1：毛巾折叠，测试可变形物体操作；
  - 任务 2：杯子放到杯垫，测试根据物体位置选择左右手的空间推理能力；
  - 每任务 25 次试验，采用子任务分级评分和最终完整成功率。
- **双臂 ARX5 少样本实验**：
  - 113 个多样化 pick-and-place 任务；
  - 每任务仅 1–5 条示范；
  - 用于测试样本效率和人类先验价值。
- **双臂 UR5 + UMI**：
  - 使用 UMI 手持夹爪采集示范；
  - 任务为外卖袋双臂放置，分解为右手抓、右手放、左手抓、左手放四个子任务；
  - 每项评估 25 次试验。

### 3.3 对比方法

- **RDT**：Robotics Diffusion Transformer 基线；
- **π0**：当前先进视觉-语言-动作模型；
- **w/o human**：H-RDT 去掉人类数据预训练，即从机器人数据直接训练；
- 部分实验还对比“从零训练”设置。

### 3.4 评估维度

- 单任务与多任务性能；
- 跨本体泛化；
- 域随机化下的环境鲁棒性；
- 少样本学习与样本效率；
- 可变形物体操作和双手空间推理。

## 4. 资源与算力

- 论文提取文本中**未明确说明**使用的 GPU 型号、GPU 数量、训练总时长、预训练/微调算力消耗等关键资源信息。
- 文中仅提到：
  - 模型规模为 **2B 参数**；
  - 人类预训练数据为 EgoDex 的 **338K+ 轨迹、194 个任务**；
  - 使用 Flow Matching 和 ODE solver 进行训练/推理。
- 因此无法从论文中判断其实际训练成本、可复现性和算力门槛。**这是论文透明性方面的明显缺失。**

## 5. 实验数量与充分性

### 5.1 实验数量概览

- **仿真单任务**：13 个 RoboTwin 2.0 任务，Easy/Hard 两种模式；
- **仿真多任务**：45 个任务训练，展示 10 个代表任务结果；
- **跨本体仿真**：Aloha-Agilex-1.0 与 Franka-Panda 两个平台；
- **真实世界**：
  - Aloha-Agilex-2.0 上 2 个双臂任务，各 25 次试验；
  - ARX5 上 113 个少样本任务，但表中仅展示 5 个代表任务及平均；
  - UR5+UMI 上 1 个双臂任务，分解为 4 个子任务，各 25 次试验；
- **消融/控制实验**：主要通过“w/o human”验证人类预训练贡献。

### 5.2 充分性评价

- **优点**：
  - 覆盖仿真与真实、单任务与多任务、少样本、域随机化、多机器人本体；
  - 使用统一 benchmark 和强基线 RDT、π0；
  - “w/o human”控制变量较直接地验证人类数据预训练价值；
  - 真实任务包含可变形物体、双手协调和空间推理，任务类型较多样。
- **不足**：
  - 缺少对关键设计因素的细粒度消融，例如：
    - 48 维动作表示的必要性；
    - 手腕/指尖各维度贡献；
    - Flow Matching 与普通扩散的对比；
    - 模块化动作编码器/解码器设计；
    - 冻结策略、重初始化范围；
    - 人类预训练数据规模与任务多样性的 scaling 影响。
  - 部分实验只报告代表性子集：113 个 ARX5 任务仅列出 5 个任务结果；45 个多任务实验仅展示 10 个任务。
  - 未报告随机种子、方差、置信区间或统计显著性检验。
  - 真实世界每任务 25 次试验数量尚可，但总任务覆盖和统计功效仍有限。
  - 基线适配细节、超参数搜索和算力对齐情况未充分说明，公平性仍需谨慎解读。

## 6. 主要结论与发现

- **人类操作数据预训练有效**：H-RDT 在仿真和真实实验中均优于从零训练、RDT 和 π0。
- **总体提升**：
  - 摘要报告相对从零训练，仿真提升 **13.9%**，真实世界提升 **40.5%**。
- **真实双臂任务**：
  - 毛巾折叠：H-RDT 完整成功率 52%，RDT 40%，w/o human 0%；
  - 杯子到杯垫：H-RDT 64%，RDT 28%，w/o human 20%；
  - 两任务平均：H-RDT 58%，RDT 34%，w/o human 10%。
- **ARX5 少样本**：
  - 113 个任务、每任务 1–5 条示范下，H-RDT 平均 41.6%，RDT 16.0%，π0 31.2%，w/o human 17.6%。
  - 说明人类先验在数据稀缺场景下尤其有价值。
- **UR5+UMI 双臂任务**：
  - H-RDT 平均 58.0%，RDT 29.0%，π0 31.0%，w/o human 16.0%；
  - 抓取和放置子任务均有明显提升。
- **仿真单任务**：
  - Easy 平均 68.7%，Hard 平均 25.6%；
  - 相对 w/o human 在 Easy 和 Hard 均提升约 8.4%。
- **仿真多任务**：
  - H-RDT 平均 87.2%，RDT 28.8%，π0 48.4%，w/o human 67.2%；
  - 相对从零训练提升 20.0%，多任务场景下人类预训练收益更大。
- **跨本体泛化**：
  - Aloha-Agilex-1.0 上 87.2%，Franka-Panda 上 62.9%；
  - 说明模块化动作适配器支持不同机器人形态迁移。
- **总体发现**：人类操作先验能提供有效归纳偏置，提升样本效率、鲁棒性和多任务学习能力；模块化两阶段设计可实现从统一人类本体到多种机器人本体的迁移。

## 7. 优点

- **数据视角有新意**：利用带 3D 手部姿态的大规模第一视角人类视频，绕开昂贵机器人遥操作数据瓶颈。
- **动作表示设计合理**：48 维手腕位姿 + 指尖位置表示，兼顾末端位姿控制兼容性和双手灵巧操作信息。
- **两阶段训练解耦清晰**：人类预训练学习通用操作先验，机器人微调适配具体本体，避免直接混合异构机器人数据。
- **模块化跨本体适配**：动作编码器/解码器可按机器人动作空间重初始化，骨干和视觉-语言先验共享，工程上具有扩展性。
- **生成模型选择较先进**：2B Diffusion Transformer + Flow Matching，适合多模态条件和高维动作序列建模。
- **实验覆盖面较广**：仿真 + 真实、多平台、单/多任务、少样本、域随机化，验证维度较全面。
- **控制变量较直接**：设置“w/o human”对照，较清晰地支撑“人类数据预训练带来收益”的核心假设。
- **真实少样本结果有说服力**：在每任务 1–5 条示范的困难设置下明显优于 RDT 和 π0，体现实际应用潜力。

## 8. 不足与局限

- **算力与训练细节缺失**：未报告 GPU 型号、数量、训练时长、预训练/微调成本，影响复现和成本评估。
- **对人类数据标注依赖强**：方法依赖高质量逐帧 3D 手部姿态和语言标注；若目标领域缺乏此类数据，迁移能力未知。
- **动作表示覆盖有限**：48 维手腕+指尖表示主要面向双臂末端执行器式操作，可能不足以覆盖高自由度灵巧手、手内操作、力触觉、接触丰富任务或移动操作。
- **跨本体范围仍有限**：实验集中在桌面双臂机械臂，尚未验证移动机器人、人形机器人、不同自由度灵巧手等更广泛本体。
- **消融不够充分**：缺少对动作表示、Flow Matching、模块化 adapter、冻结/重初始化策略、预训练数据规模等关键设计的系统消融。
- **结果报告透明度不足**：113 个 ARX5 任务仅展示 5 个代表任务；45 个多任务仅展示 10 个；缺少方差、置信区间和失败案例分析。
- **基线公平性需谨慎**：π0、RDT 与 H-RDT 的模型规模、预训练数据、训练算力和调参预算可能不同；人类数据预训练带来的数据优势需要更严格控制才能完全归因于方法设计。
- **真实世界统计功效有限**：每任务 25 次试验、任务数量有限，且真实环境随机性大，结论仍需更大规模重复验证。
- **潜在数据偏差**：EgoDex 中的人类操作习惯、任务分布和物体类别会引入偏差；对分布外物体、场景和长期自主任务的安全性、鲁棒性尚未充分评估。
- **结论表述较强**：论文提出“人类操作数据可作为双臂机器人策略学习基础”，但现有实验仍主要集中在特定桌面操作和有限本体上，通用基础模型的结论需要更多跨领域验证。

（完）
