---
title: "Keep On Going: Learning Robust Humanoid Motion Skills via Selective Adversarial Training"
title_zh: 坚持下去：通过选择性对抗训练学习鲁棒人形运动技能
authors: "Yang Zhang, Zhanxiang Cao, Buqing Nie, Haoyang Li, Zhong Jiangwei, Qiao Sun, Xiaoyi Hu, Xiaokang Yang, Yue Gao"
date: 2026
publication_date: 2026
publication_date_precision: year
publication_date_source: conference year only; exact release date unverified
publication_date_kind: unknown
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38949/42911"
tags: ["query:humanoid-rl"]
score: 7.0
evidence: 选择性对抗训练提升人形机器人强化学习全身运动技能鲁棒性
tldr: 人形机器人需长时间可靠执行多样全身体技能，但强化学习运动策略在噪声、扰动与长时间运行下容易失稳。作者提出选择性对抗训练SA2RT，在攻击预算约束下学习识别并稀疏扰动最脆弱的状态与动作，通过非零和交替优化不断强化策略。实验验证该训练能持续提升运动策略对最强攻击与真实扰动的鲁棒性。该工作为真实人形机器人长时程鲁棒运动控制提供了有效的对抗训练思路。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 人形机器人需长时间执行多样全身体技能，但强化学习运动策略在噪声与扰动下易失稳。
method: 提出选择性对抗训练SA2RT，在攻击预算约束下稀疏扰动最脆弱状态与动作，交替优化增强策略鲁棒性。
result: 实验验证该对抗训练可持续强化策略，使其抵御最强攻击并提升长时程运动稳定性。
conclusion: 为真实人形机器人长时程鲁棒运动控制提供了有效的对抗训练思路。
---

## Abstract
Humanoid robots are expected to operate reliably over long horizons while executing versatile whole-body skills. Yet Reinforcement Learning (RL) motion policies typically lose stability under prolonged operation, sensor/actuator noise, and real world disturbances. In this work, we propose a Selective Adversarial Attack for Robust Training (SA2RT) to enhance the robustness of motion skills. The adversary is learned to identify and sparsely perturb the most vulnerable states and actions under an attack-budget constraint, thereby exposing true weakness without inducing conservative overfitting. The resulting non-zero sum, alternating optimization continually strengthens the motion policy against the strongest discovered attacks. We validate our approach on the Unitree G1 humanoid robot across perceptive locomotion and whole-body control tasks. Experimental results show that adversarially trained policies improve the terrain traversal success rate by 40%, reduce the trajectory tracking error by 32%, and maintain long horizon mobility and tracking performance. Together, these results demonstrate that selective adversarial attacks are an effective driver for learning robust, long horizon humanoid motion skills.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究背景**：人形机器人需要在长时程内稳定执行多样化全身运动技能，但基于强化学习（RL）的运动策略在真实部署中容易受到传感器噪声、执行器误差、环境变化和外部扰动影响。
- **核心问题**：仿真到现实存在分布偏移，RL 神经控制器对扰动敏感，导致人形机器人在复杂环境中长时间运行时失稳、跌倒或跟踪误差累积。
- **现有方法局限**：
  - 域随机化（DR）能提升一般鲁棒性，但无法针对策略的具体脆弱状态施加有效扰动。
  - 正则化方法（如 Lipschitz 约束、对称性约束）需要在探索能力与鲁棒约束之间权衡。
  - 残差模型依赖真实数据，实施效率较低。
  - 持续对抗攻击（PAP）虽能暴露脆弱性，但全时段攻击会造成状态分布偏移，诱发策略过度保守和鲁棒过拟合。
- **论文整体含义**：提出选择性对抗训练框架 SA2RT，通过“稀疏但精准”的对抗攻击识别并修复运动策略的真实脆弱点，从而提升人形机器人长时程运动与跟踪鲁棒性。

## 2. 方法论

- **核心思想**：同时学习运动策略 \(\pi_m\) 和攻击策略 \(\pi_{adv}\)。攻击策略在有限攻击预算下选择最脆弱的时间步，对状态和动作施加扰动；运动策略则在对抗样本上训练以抵抗这些攻击。部署时只使用运动策略，不需要攻击策略。
- **联合状态-动作攻击空间**：
  - 定义状态扰动集合 \(B_s=\{s+\delta_s\}\) 和动作扰动集合 \(B_a=\{a+\delta_a\}\)，满足 \(\|\delta_s\|\le \epsilon_s\)、\(\|\delta_a\|\le \epsilon_a\)。
  - 攻击动作空间为运动策略状态空间与动作空间的联合空间，即 \(\hat A=S\times A\)，用于同时模拟观测误差与执行偏差的级联影响。
- **选择性攻击策略 SAP**：
  - 与每个时间步都攻击的 PAP 不同，SAP 引入二值变量 \(b_t\in\{0,1\}\)，表示第 \(t\) 步是否攻击，并约束攻击总步数 \(\sum_t b_t\le N_a\)。
  - 优化目标是在攻击预算内最大化攻击收益，同时选择最脆弱的状态进行稀疏扰动。
  - 通过拉格朗日乘子 \(\lambda\) 将硬预算约束转化为软惩罚：
    \[
    \max_{b,\pi_{adv}} \mathbb{E}\left[\sum_t \hat R(s_t,a_t)\right]-\lambda\sum_t b_t
    \]
  - SAP 在扩展 MDP 中训练，其动作空间为 \(\{0,1\}\times\hat A\)，奖励为 \(\hat R-\lambda b\)，折扣因子设为 \(\gamma'=1\)。
- **非零和对抗训练**：
  - 不采用简单零和博弈，而是让攻击策略最大化自身攻击收益并压低运动策略价值：
    \[
    J(\theta_{adv})=\max_{\theta_{adv}}\left(V^{adv}_\pi(s)-V^m_\pi(s)\right)
    \]
  - 使用类似 PPO 的裁剪目标，并同时考虑攻击优势 \(A^{adv}_t\) 与运动策略优势 \(A^m_t\)，以提升优化单调性和训练稳定性。
  - 攻击策略与运动策略分别使用价值网络估计价值函数。
- **交替训练流程**：
  - 固定运动策略，更新攻击策略 \(N_{adv}\) 次，使其发现运动策略弱点。
  - 固定攻击策略，更新运动策略 \(N_m\) 次，使其适应并抵抗已发现的攻击。
  - 重复 \(N_{iter}\) 轮，实现在线鲁棒对抗训练。

## 3. 实验设计

- **机器人平台**：Unitree G1 人形机器人。
- **任务场景**：
  - **感知运动控制 PL**：平坦地面、斜坡、楼梯、离散地形等，评估速度跟踪、角速度跟踪和动态稳定性。
  - **全身控制 WBC**：全身轨迹跟踪，包括简单行走和动态舞蹈轨迹；真实实验中跟踪 120 秒舞蹈动作。
- **真实复杂地形**：斜坡、楼梯、碎石、沙地、草地；每种地形 5 组、每组 10 次试验。
- **对比方法**：
  - **CE**：干净环境训练，不使用域随机化和对抗攻击。
  - **DR**：使用域随机化训练。
  - **PAP**：使用持续攻击策略的鲁棒对抗训练。
  - **SAP**：论文提出的选择性攻击策略鲁棒对抗训练。
- **评价指标**：
  - 线速度误差 \(E_{vel}\)、角速度误差 \(E_{ang}\)。
  - 重力投影分量 \(E_g\)，用于评估动态稳定性。
  - 关键点位置误差 MPKPE，分上下身。
  - 关节位置误差 MPJPE，分上下身。
  - 复杂地形和轨迹跟踪成功率 \(R_{sr}\)。
- **Benchmark 性质**：论文未使用公开标准数据集或公开 benchmark，而是基于仿真环境和真实 Unitree G1 机器人自建评测任务。公平性方面，论文说明 DR 与 SAP 在训练中使用一致的扰动空间和阈值。

## 4. 资源与算力

- 论文提取文本中**未明确给出** GPU 型号、GPU 数量、训练总时长、仿真环境步数或总样本量等算力信息。
- 仅能确认实验平台为 **Unitree G1 人形机器人**，并包含仿真训练与真实机器人部署实验。
- 由于附录未包含在给定文本中，无法进一步确认是否在附录中报告了训练资源细节。

## 5. 实验数量与充分性

- **实验组数概览**：
  - 对抗扰动有效性实验：比较 DR 环境与 SAP 环境下 CE、DR、SAP 策略的成功率。
  - PL 鲁棒性实验：在干净环境和 DR 环境中比较 PL-DR 与 PL-SAP 的速度、角速度和稳定性指标。
  - WBC 鲁棒性实验：在干净环境和 DR 环境中比较 WBC-DR 与 WBC-SAP 的轨迹跟踪误差。
  - 消融实验：比较 PAP 与 SAP 在扰动等级 \(L_p\in\{1,2,3,4\}\) 下的归一化奖励和低扰动环境性能。
  - SAP 行为分析：不同任务下的攻击比例、从平地到楼梯过渡阶段的攻击序列。
  - 超参数分析：分析 \(\lambda\) 对攻击比例和运动性能的影响。
  - 真实机器人实验：5 类复杂地形穿越，每类地形 5 组×10 次；120 秒动态舞蹈轨迹跟踪。
- **充分性评价**：
  - 实验覆盖仿真与真实机器人、两类任务、多个基线、消融和超参数分析，整体较充分。
  - 真实地形实验有多次重复，表格中给出均值与标准差，具有一定统计意识。
  - 但缺少与 Lipschitz 正则化、对称性正则化、残差模型等方法的直接对比；真实实验仅限单一机器人型号和有限任务；未明确报告随机种子数量、置信区间计算方式和训练资源，复现性信息不足。

## 6. 主要结论与发现

- **选择性对抗攻击比域随机化更能暴露策略脆弱性**：在 SAP 攻击环境下，CE 和 DR 策略成功率均降至 0，而 SAP 训练策略仍保持约 95.7% 成功率。
- **SA2RT 提升感知运动鲁棒性**：PL-SAP 在干净和 DR 环境下的速度误差、角速度误差和重力投影误差均优于 PL-DR。
- **SA2RT 提升全身控制跟踪性能**：WBC-SAP 在所有评估指标上优于 WBC-DR，尤其在速度跟踪方面表现更明显。
- **PAP 与 SAP 的消融表明选择性攻击更优**：PAP 攻击更强但全时段攻击导致状态分布偏移和过度保守；SAP 只攻击脆弱状态，在鲁棒性与任务性能之间取得更好平衡。
- **SAP 能学习任务难度相关的攻击行为**：任务越难，攻击比例越高；在平地到楼梯的过渡阶段，SAP 能选择性攻击关键脆弱阶段并诱导跌倒。
- **真实机器人验证有效**：复杂地形穿越成功率显著提升，论文报告提升约 40%；120 秒舞蹈轨迹跟踪中，WBC-DR 在 65 秒左右失稳终止，WBC-SAP 将跟踪误差降低约 32% 并完成全程。

## 7. 优点

- **问题定位清晰**：针对人形机器人长时程运动中的鲁棒性问题，指出 DR 无法针对性暴露脆弱点、PAP 易导致保守过拟合的关键矛盾。
- **方法设计有针对性**：SAP 通过攻击预算和稀疏攻击选择最脆弱状态，避免全时段攻击造成的分布偏移。
- **攻击空间设计合理**：联合状态和动作空间扰动，能够覆盖观测误差与执行误差的级联影响。
- **优化框架较完整**：采用非零和博弈与交替训练，并给出带裁剪的单调优化目标，兼顾攻击强度与训练稳定性。
- **实验验证较全面**：包含仿真指标、消融、超参数分析、真实复杂地形和真实长时程舞蹈跟踪。
- **部署友好**：真实部署不需要攻击策略，仅使用鲁棒运动策略，具备实际应用可行性。
- **可解释性较好**：通过攻击比例、过渡阶段攻击序列和 \(\lambda\) 分析，展示了 SAP 的选择性攻击行为。

## 8. 不足与局限

- **基准与数据覆盖有限**：未使用公开 benchmark 或标准数据集，评测任务为自建场景，跨论文可比性有限。
- **真实实验规模仍有限**：仅使用 Unitree G1 一种机器人；真实地形实验虽重复多次，但任务类别和舞蹈轨迹数量有限。
- **基线对比不够全面**：主要对比 CE、DR、PAP、SAP，未直接比较 Lipschitz 正则化、对称性正则化、残差模型等已有鲁棒性方法。
- **超参数敏感性**：\(\lambda\) 对攻击比例和最终性能影响明显，需要调参；论文显示性能随 \(\lambda\) 先升后降。
- **算力与复现信息不足**：未报告 GPU 型号、数量、训练时长、随机种子数量等，影响复现和成本评估。
- **攻击模型仍有边界假设**：扰动受范数约束，真实世界扰动可能具有结构性、时变性和环境交互性；论文也将环境交互攻击列为未来工作。
- **安全与保守性权衡仍需进一步研究**：对抗训练可能带来策略保守化风险，虽然 SAP 缓解了 PAP 的问题，但最优攻击预算与策略敏捷性的权衡仍未完全解决。

（完）
