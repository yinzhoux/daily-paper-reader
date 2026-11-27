---
title: Learning Object-Centric Motion Priors from Human for Robotic Dexterous Manipulation
title_zh: 从人类学习物体中心运动先验用于机器人灵巧操作
authors: "Zhengdong Hong, Guofeng Zhang"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38892/42854"
tags: ["query:humanoid-rl"]
score: 8.0
evidence: 从人类示范学习物体中心运动先验并结合强化学习奖励
tldr: 多指灵巧手操作物体时维度高、动力学复杂，依赖人工奖励工程。作者利用人-物交互数据集学习整体预测未来手-物状态，而非单纯模仿人类示范。预测的物体未来状态可作为通用奖励项驱动强化学习，减少任务特定奖励设计。在三项仿真与真实操作任务上，该方法优于现有最优方法，显示出更好的跨任务泛化能力。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 多指灵巧手操作多样物体维度高、动力学复杂，且依赖任务特定奖励工程。
method: 利用人-物交互数据学习整体预测未来手-物状态，并将预测的物体状态作为强化学习通用奖励。
result: 在三项仿真与真实操作任务上优于现有最优方法，泛化性更强。
conclusion: 说明物体中心运动先验可减少奖励工程并提升灵巧操作策略的泛化。
---

## Abstract
Manipulating diverse objects with multi-fingered dexterous hands is challenging due to the high dimensionality and complex dynamics. Human-Object Interaction (HOI) datasets provide rich knowledge about task information and embodied interactions. Instead of solely imitating the human demonstrations, our method learns to holistically predict future hand-object states by leveraging these datasets. The predicted future states of the object can serve as a general-purpose reward term for reinforcement learning, reducing reliance on task-specific reward engineering and enhancing generalization across tasks. We conduct extensive experiments on three manipulation tasks in simulation and the real world. Our approach outperforms existing SOTA methods in both success rate and generalizability on novel objects. Furthermore, we validate the cross-embodiment compatibility of our methods by successfully deploying the skills on different robot hands.

---

## 论文详细总结（自动生成）

# 论文总结：从人类学习物体中心运动先验用于机器人灵巧操作

## 1. 核心问题与整体含义

- **研究动机**：多指灵巧手操作多样物体面临高维动作空间和复杂接触动力学。传统基于模型的轨迹优化依赖精确动力学模型；无模型强化学习样本效率低且需要大量任务特定奖励工程；从机器人数据做模仿学习又受限于大规模数据采集成本。
- **核心观察**：人类在操作物体时不仅模仿动作，还会潜意识预测物体未来状态。人-物交互（HOI）数据集包含丰富的 3D 手-物交互知识，可作为任务级先验。
- **整体含义**：论文不局限于直接模仿人类示范，而是从 HOI 数据中学习整体预测未来手-物状态，并将预测的物体未来状态作为强化学习的通用奖励项，减少任务特定奖励设计，提升对新物体、新位姿和新机器人手的泛化能力。

## 2. 方法论

### 2.1 总体流程

- 从真实机器人-物体初始配置中提取观测，包括任务设置、物体点云/位姿和机器人本体感知。
- 将观测输入 **HOI 运动预测器**，自回归生成未来手-物参考轨迹。
- 对预测的人手运动进行 **人到机器人手的重定向**，得到机器人参考轨迹。
- 使用 **轨迹引导的强化学习** 训练状态型技能策略。
- 通过系统辨识和域随机化实现 **零样本 Sim-to-Real** 部署到真实机器人。

### 2.2 HOI 运动预测器

- 使用 **Dex-YCB** 和 **ARCTIC** 数据集，均提供每个时间步的 6DoF 手-物位姿：手用 MANO 表示，物体用四元数和平移表示。
- 对物体网格做最远点采样（FPS），取 100 个点，经 **PointNet** 提取物体形状特征。
- 使用 **6 层 GPT-2 Transformer** 自回归预测未来手-物状态。输入历史手-物状态与 PointNet 特征，输出下一时刻手-物状态，并迭代预测至序列长度。
- 监督损失为：
  \[
  L(s^h_t,s^o_t)=\sum_t \alpha\|s^h_t-\hat s^h_t\|^2+\beta\|s^o_t-\hat s^o_t\|^2
  \]
  实验中 \(n=10,\alpha=1,\beta=2\)，物体项权重更大以补偿其维度占比低。
- 统一模型处理单/双手数据：ARCTIC 双手直接输入，Dex-YCB 通过零填充对齐维度。
- 真实机器人推理时，将机器人手视为人手的子集，修改 FrankMocap 的优化目标，用机器人正运动学得到的 3D 关节位置做 3D 对齐，并自适应调整 MANO 形状参数以适配不同尺寸机器人手。

### 2.3 人到机器人手重定向

- 采用基于优化的重定向，最小化机器人指尖与人类指尖距离，并加入时间平滑项：
  \[
  L_{\text{retarget}}(q_t)=\sum_{i=1}^5\|x^i_t-f_i(q_t)\|^2+\beta\|q_t-q_{t-1}\|^2
  \]
  约束关节范围 \(q_l\le q_t\le q_u\)，使用 NLopt 求解。

### 2.4 轨迹引导强化学习

- 将任务建模为 MDP；状态包括机器人关节位置和物体 6D 位姿，动作包括末端执行器增量位姿和手部关节增量；用 PPO 训练。
- 奖励由四部分组成：
  \[
  R=\lambda_1R_f+\lambda_2R_o+\lambda_3R_{\text{contact}}+\lambda_4R_{\text{success}}
  \]
  - \(R_f\)：机器人跟随参考手部关节位置和末端位姿。
  - \(R_o\)：物体跟随预测物体状态的通用奖励，包含平移和四元数旋转距离：
    \[
    R_o=e^{-\alpha_4\|T^o_t-\hat T^o_t\|^2}+e^{-\alpha_5\|\log(\hat q^{o-1}_t\otimes q^o_t)\|^2}
    \]
  - \(R_{\text{contact}}\)：鼓励拇指和至少一根其他手指接触物体。
  - \(R_{\text{success}}\)：任务成功奖励；障碍任务中增加碰撞大惩罚。
- 训练时随机化物体初始位置 \(\pm5\) cm、绕 z 轴旋转 \(\pm30^\circ\)。

### 2.5 Sim-to-Real

- 通过系统辨识调整仿真机器人 PID 参数和关节力矩限制，减小控制差距。
- 使用域随机化：观测噪声、摩擦、物体尺度、重量随机化，提高真实世界鲁棒性。
- 论文强调无需真实机器人微调，实现零样本迁移。

## 3. 实验设计

### 3.1 数据集与场景

- **仿真**：SAPIEN3 + OpenAI-Gymnasium，GPU 并行训练与渲染。
- **真实平台**：双臂 xArm-7，搭配 PSYONIC Ability hand、ROBOTERA XHand1 或 Inspire robot hand；RealSense D435i 相机；FoundationPose 做 6DoF 物体位姿跟踪；Easy-Hec++ 做手眼标定。
- **数据来源**：Dex-YCB、ARCTIC；额外使用非 Dex-YCB 的 YCB 物体、日常物体和 3D 打印障碍物。

### 3.2 任务与成功标准

- **YCB 物体抓取**：抓起目标物体并提升至初始高度以上 10 cm。
- **铰接物体操作**：铰接物体沿轴旋转超过 30°。
- **带障碍抓取**：机械臂和灵巧手在抓取全过程中不得碰撞障碍物，否则失败。
- **跨本体测试**：替换右侧机器人手，重新执行重定向和 RL，使用相同奖励项和参数。

### 3.3 对比方法

- YCB 抓取：ViviDex、AdaDexGrasp、ManipTrans、HOP、PPO w/o following。
- 铰接物体：Obj-Dex、ManipTrans、PPO w/o following。
- 带障碍抓取：ViviDex、AdaDexGrasp、ManipTrans、HOP、PPO w/o following。
- 消融：去掉物体跟随奖励 \(R_o\)、去掉接触奖励 \(R_{\text{contact}}\)。

## 4. 资源与算力

- 仿真训练使用 **单张 NVIDIA RTX 4090 GPU（24GB）** 和 **i7-14700K CPU**，运行 **1024 个并行环境**，平均约 **10000 steps/s**。
- 每个 PPO 策略训练 **1M steps**；仿真实验用 **5 个随机种子**，每个策略评估 **100 次试验**；真实实验重复 **20 次**。
- 论文未明确报告总 GPU 数量、总训练小时数、总算力消耗或能耗。

## 5. 实验数量与充分性

- 实验覆盖 **3 个主要操作任务**：YCB 抓取、铰接物体操作、带障碍抓取；并包含 **跨 3 种机器人手** 的跨本体测试和奖励消融。
- 数据划分较丰富：Dex-YCB 已见物体、非 Dex-YCB 未见物体、新初始位姿、ARCTIC 物体与日常物体、DexYCB 与 3D 打印障碍物。
- 仿真采用 5 seeds × 100 trials，真实实验 20 次重复，整体实验量较充分，且同时报告仿真与真实结果，客观性较好。
- 公平性方面：跨本体测试使用相同奖励项和参数；对未见配置，部分基线使用数据集中已有参考轨迹；障碍任务用 cuRobo 过滤参考轨迹碰撞帧。但真实实验仅 20 次重复，未报告置信区间或显著性检验；基线复现与调参细节有限，个别表格汇总值与分项均值存在轻微不一致（如 Tab.7 中 PPO w/o foll.），建议进一步核对。

## 6. 主要结论与发现

- 所提方法在三个任务上均优于现有 SOTA：
  - YCB 抓取仿真平均成功率 **0.84**，真实平均 **0.77**，优于 ViviDex、AdaDexGrasp、ManipTrans、HOP 和 PPO w/o following。
  - 铰接物体操作仿真平均 **0.66**、真实平均 **0.53**，显著优于 Obj-Dex 和 ManipTrans；对日常物体优势更明显。
  - 带障碍抓取仿真平均 **0.66**、真实平均 **0.63**，整体优于或接近最强基线，但优势幅度较小。
- 跨本体测试中，三种机器人手在多个任务上保持约 **52%–77%** 的成功率，说明方法具有跨本体兼容性。
- 消融表明：去掉物体跟随奖励 \(R_o\) 会显著降低样本效率；去掉接触奖励 \(R_{\text{contact}}\) 会导致训练不稳定和成功率下降。物体跟随奖励是稳定高效策略学习的关键。

## 7. 优点

- **通用奖励设计**：用预测物体未来状态替代任务特定奖励，减少奖励工程，提升跨任务泛化。
- **整体手-物建模**：不是单纯模仿人手轨迹，而是学习手-物联合未来状态，更符合操作任务本质。
- **统一预测器**：一个模型适配 Dex-YCB 和 ARCTIC，兼容单/双手数据。
- **零样本 Sim-to-Real**：结合系统辨识和域随机化，无需真实机器人微调即可部署。
- **跨本体验证**：在多种灵巧手上验证，增强实际应用潜力。
- **实验较扎实**：仿真与真实结合，包含未见物体、新位姿、障碍和消融，结果具有较强说服力。

## 8. 不足与局限

- **依赖 HOI 数据与标注**：需要高质量 3D 手-物位姿、物体网格和 6DoF 位姿估计；对数据集中未覆盖的物体类别和复杂形状泛化仍受限。
- **物体与任务范围有限**：主要验证刚体和铰接物体，未涉及可变形物体、软体、长时程多阶段任务或开放世界任意物体。
- **自回归预测误差**：长序列预测可能累积误差；预测器性能和参考轨迹质量直接影响 RL 效果。
- **重定向与本体差距**：虽然跨本体有效，但重定向仍需针对机器人手优化，不同手尺寸和关节限制可能带来额外误差。
- **奖励权重需手工调参**：虽减少任务特定奖励，但 \(R_o\)、接触奖励和成功奖励权重仍依赖人工设定。
- **真实实验规模有限**：每个真实设置重复 20 次，缺少置信区间和统计显著性分析；失败模式分析不足。
- **感知依赖**：真实部署依赖 FoundationPose 跟踪和已知物体网格/点云；遮挡、位姿估计误差可能影响性能。
- **报告细节**：未给出总训练时长和总算力；个别表格汇总值需核对。

（完）
