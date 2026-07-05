---
title: "从 Self-Play 到 PSRO：Fictitious Play 为什么仍是理解多智能体训练的一条主线？"
date: 2026-07-05
layout: post
author: Ju Qi
lang: zh
excerpt: "Self-Play 不是一个单一算法，而是一类围绕对手分布构造的训练闭环。本文从 Fictitious Play、Double Oracle 到 PSRO，梳理多智能体训练中“智能体应该如何面对自己的历史”这一主线。"
---

在多智能体强化学习和计算博弈论里，Self-Play 经常被当成一个成功经验来讲：AlphaGo 通过自我博弈变强，扑克 AI 通过自我博弈逼近均衡，AlphaStar 通过联赛机制训练出鲁棒策略。

但如果只把 Self-Play 理解成“让智能体和自己打”，其实会漏掉最关键的问题。

真正重要的不是“自己打自己”，而是：

$$
\text{current policy should train against whom?}
$$

当前策略应该打谁？打自己的最新版本？打历史平均策略？打一组历史策略的混合分布？还是打专门训练出来的 exploiters？

这正是 Fictitious Play 和 PSRO 的位置。它们不是 Self-Play 之外的另一个世界，而是对 Self-Play 中“对手分布”这个核心问题的系统回答。

可以先给一个粗略判断：

$$
\text{Naive Self-Play}
\subset
\text{Fictitious Play style learning}
\subset
\text{Population-based / PSRO style learning}.
$$

当然，这不是严格的集合关系，而是一条思想演化线：从当前策略，到历史平均，再到策略群体。

本文不把 Self-Play 当作一个单一算法，而是把它拆成“历史如何保存、对手如何采样、响应如何训练、最终策略如何输出”这几个问题来看。这样再看 Fictitious Play 和 PSRO，它们的位置会清楚很多。

## 1. Self-Play 不是算法，而是一类训练闭环

考虑一个有限博弈：

$$
G = \langle N,\{\Sigma_i\}_{i\in N},\{u_i\}_{i\in N}\rangle.
$$

其中 $N$ 是玩家集合，$\Sigma_i$ 是玩家 $i$ 的策略空间，$u_i(\sigma_i,\sigma_{-i})$ 是玩家 $i$ 在策略组合 $\sigma=(\sigma_i,\sigma_{-i})$ 下的收益。

Self-Play 的最抽象形式可以写成：

$$
\pi_i^{t+1}
\approx
\operatorname{Oracle}_i(\mu_{-i}^t),
$$

其中 $\mu_{-i}^t$ 是第 $t$ 轮给玩家 $i$ 使用的“对手分布”，而 $\operatorname{Oracle}_i$ 是某种响应学习过程，例如精确最佳响应、近似最佳响应、RL 训练器、MCTS 增强策略改进器等。

如果 oracle 是最佳响应，则有：

$$
\operatorname{BR}_i(\mu_{-i})
\in
\arg\max_{\pi_i\in\Sigma_i}
\mathbb{E}_{\pi_{-i}\sim \mu_{-i}}
\left[
u_i(\pi_i,\pi_{-i})
\right].
$$

这说明 Self-Play 里真正需要设计的不是一句“自己和自己打”，而是以下四件事：

1. 记忆机制：保存哪些历史策略？
2. 对手分布：如何从历史中构造 $\mu^t$？
3. 响应 oracle：如何训练 $\operatorname{Oracle}(\mu^t)$？
4. 输出策略：最终使用最新策略、平均策略，还是策略混合？

Naive Self-Play 只是其中最简单的一种特例：

$$
\mu_{-i}^t = \delta_{\pi_{-i}^{t}},
$$

也就是只打对手的当前版本。

这个设定在很多完全信息游戏中很有效，尤其当搜索、价值函数、策略改进形成稳定闭环时。但在一般博弈，特别是不完全信息和非传递性强的博弈中，它很容易进入 best-response cycle。

石头剪刀布只是最小例子：

$$
R \rightarrow P \rightarrow S \rightarrow R.
$$

这个例子本身很基础，但它暴露的问题并不基础：如果训练目标总是当前对手，学习过程可能只是在追逐局部漏洞，而不是形成稳定的长期策略。

## 2. Fictitious Play：Self-Play 中最经典的历史平均机制

Fictitious Play 由 Brown 在 1951 年提出。它的核心假设是：

**每个玩家都认为对手会按照历史平均策略行动，然后对这个历史平均策略作最佳响应。**

设玩家 $i$ 在前 $t$ 轮产生的策略为 $\sigma_i^1,\ldots,\sigma_i^t$，经验平均策略为：

$$
\bar{\sigma}_i^t
=
\frac{1}{t}\sum_{k=1}^{t}\sigma_i^k.
$$

第 $t+1$ 轮，玩家 $i$ 计算对其他玩家历史平均策略的最佳响应：

$$
\sigma_i^{t+1}
\in
\operatorname{BR}_i(\bar{\sigma}_{-i}^{t})
=
\arg\max_{\sigma_i}
u_i(\sigma_i,\bar{\sigma}_{-i}^{t}).
$$

然后更新平均策略：

$$
\bar{\sigma}_i^{t+1}
=
\frac{t}{t+1}\bar{\sigma}_i^t
+
\frac{1}{t+1}\sigma_i^{t+1}.
$$

如果写成更一般的步长形式：

$$
\bar{\sigma}_i^{t+1}
=
(1-\alpha_{t+1})\bar{\sigma}_i^t
+
\alpha_{t+1}
\operatorname{BR}_i(\bar{\sigma}_{-i}^{t}).
$$

原始 FP 对应 $\alpha_{t+1}=1/(t+1)$。

这几行公式的重点不是“求平均”本身，而是它改变了 Self-Play 的对手分布：

$$
\mu_{-i}^t = \bar{\sigma}_{-i}^t.
$$

Naive Self-Play 打的是最新对手；Fictitious Play 打的是历史平均对手。

这一步非常关键。它使训练过程不再只对当前策略的漏洞做短期响应，而是对长期经验分布做响应。

在两人零和博弈中，经典结果表明 FP 的平均策略收敛到纳什均衡。在更一般的博弈中，FP 不总是收敛，但它仍然是理解许多现代 population-based self-play 方法的基本模板。

## 3. 为什么 FP 比 Naive Self-Play 更像“求均衡”？

Naive Self-Play 的典型更新可以抽象成：

$$
\sigma^{t+1}
\approx
\operatorname{BR}(\sigma^t).
$$

如果博弈存在强非传递结构，这个动力学可能长期绕圈。

FP 则是：

$$
\sigma^{t+1}
\approx
\operatorname{BR}(\bar{\sigma}^t),
\qquad
\bar{\sigma}^{t+1}
=
\operatorname{Average}(\bar{\sigma}^t,\sigma^{t+1}).
$$

这里 $\bar{\sigma}^t$ 扮演的是经验信念。玩家不是假设对手下一轮一定采用最新策略，而是假设对手的行为由历史经验分布生成。

从在线学习角度看，这相当于把“对当前对手的最优响应”变成“对经验分布的跟踪响应”。从博弈论角度看，它让策略更新更接近“信念一致性 + 最优响应”的均衡思想。

这就是 FP 的核心价值：

$$
\text{stability comes from averaging the opponent, not from trusting the latest policy.}
$$

当然，平均也会带来代价。FP 往往收敛慢，且每轮最佳响应可能很贵。现代方法基本都在围绕这两个问题做改造：如何近似最佳响应，如何压缩历史，如何把平均从动作空间推广到策略空间。

## 4. 理论上到 CCE，很多时候已经够用了

这里需要补一个容易被忽略的点：离开两人零和、势博弈等特殊条件后，Fictitious Play、PSRO 以及很多 self-play 变体，理论上通常不能轻易承诺“学到纳什均衡”。

更稳妥的理解是：它们很多时候学习到的是某种经验分布上的稳定性，典型目标可以落在粗相关均衡（Coarse Correlated Equilibrium, CCE）这一层。

设 $\rho$ 是联合策略空间上的一个分布。若对任意玩家 $i$ 和任意固定偏离策略 $\pi_i'$，都有：

$$
\mathbb{E}_{\pi\sim \rho}
\left[
u_i(\pi_i,\pi_{-i})
\right]
\geq
\mathbb{E}_{\pi\sim \rho}
\left[
u_i(\pi_i',\pi_{-i})
\right],
$$

则称 $\rho$ 是一个 CCE。

这句话的意思是：如果训练过程最终给出的是一个联合策略分布，那么任何单个玩家在开局前承诺换成某个固定策略，都不能提高自己的期望收益。

CCE 比 NE 弱。通常有：

$$
\text{NE} \subseteq \text{CE} \subseteq \text{CCE}.
$$

但“弱”不代表“没用”。在大规模多智能体训练里，很多时候我们真正需要的不是一个解析意义上精确的单点 NE，而是一个不容易被简单单边偏离打穿的稳定策略分布。

特别是在两人零和场景中，CCE 在收益意义上已经和 minimax value 对齐；在更复杂的 general-sum 或多人场景中，CCE 也常常足够支撑训练和评估。很多工程系统部署的本来也不是单一纯策略，而是 population、league 或 meta-policy。

所以，对 FP/PSRO 这类方法更现实的期待是：

$$
\text{not necessarily exact NE, but a useful stable distribution.}
$$

这个视角也解释了为什么 PSRO、league training 等方法在理论保证不总是强到 NE 的情况下，仍然能在实际任务中表现很好。

## 5. GWFP：为什么近似 oracle 也能放进 FP 框架？

实际系统里很少能算出精确最佳响应。深度 RL 训练出来的响应策略通常只是近似 oracle，而且还带有采样噪声和函数逼近误差。

这就引出 Generalized Weakened Fictitious Play, GWFP。它把 FP 写成更宽松的形式：

$$
\bar{\sigma}^{t+1}
=
(1-\alpha_{t+1})\bar{\sigma}^{t}
+
\alpha_{t+1}
\left(
b^{\epsilon_t}(\bar{\sigma}^{t})+M_{t+1}
\right).
$$

其中：

$b^{\epsilon_t}$ 是 $\epsilon_t$-best response，而不要求精确最佳响应。

$M_{t+1}$ 表示噪声项，例如采样误差、估值误差、训练误差。

$\alpha_t$ 是步长。

典型收敛条件包括：

$$
\alpha_t\rightarrow 0,
\qquad
\sum_{t=1}^{\infty}\alpha_t=\infty,
\qquad
\epsilon_t\rightarrow 0,
$$

以及噪声在加权意义下可控。

这个框架很重要，因为它解释了为什么现代深度 self-play 仍然可以被看成 FP 的近似版本：只要 RL oracle 逐渐变好、噪声不持续主导更新、平均机制稳定，训练过程就仍然保留 FP 的结构。

这也是从经典 FP 走向 NFSP、PSRO、league training 的理论桥梁。

## 6. 扩展式博弈里，平均策略没有那么简单

前面的写法更接近正规式博弈。到了不完全信息扩展式博弈，策略不再只是一个简单向量，而是定义在信息集上的行为策略：

$$
\sigma_i(I,a), \quad I\in\mathcal{I}_i,\ a\in A(I).
$$

这里 $I$ 是玩家 $i$ 的信息集，$A(I)$ 是在该信息集可选的动作集合。

扩展式博弈里的平均策略通常不能简单逐点平均，还需要考虑玩家自身到达信息集的概率。一个常见写法是：

$$
\bar{\sigma}_i^T(I,a)
=
\frac{
\sum_{t=1}^{T}
\pi_i^{\sigma^t}(I)\sigma_i^t(I,a)
}{
\sum_{t=1}^{T}
\pi_i^{\sigma^t}(I)
}.
$$

$\pi_i^{\sigma^t}(I)$ 表示在第 $t$ 轮策略下，玩家 $i$ 自己的行动导致到达信息集 $I$ 的概率贡献。

这个 reach-weighted average 的含义是：那些在玩家自身策略下更常到达的信息集，对平均策略贡献更大。

Extensive-Form Fictitious Play, XFP 可以理解为把 FP 推广到扩展式博弈：在行为策略空间中维护平均策略，并计算对平均策略的最佳响应。

问题在于，完整最佳响应需要遍历博弈树；在扑克这类大规模不完全信息博弈中，这通常不可承受。

于是后续方法会引入采样、函数逼近、策略网络或平均策略网络。例如 Neural Fictitious Self-Play, NFSP 的一个典型思想是同时维护两类策略：

$$
\pi^{BR} \approx \operatorname{BR}(\bar{\pi}),
\qquad
\bar{\pi}\approx \text{average of historical best responses}.
$$

训练时使用 anticipatory mixture：

$$
\pi^{mix}
=
\eta \pi^{BR}
+
(1-\eta)\bar{\pi}.
$$

其中 $\eta$ 控制当前最佳响应策略和历史平均策略之间的混合比例。

这就是深度学习语境下的 FP 影子：一个网络学响应，一个网络学平均。

## 7. Double Oracle：先在受限策略集里求，再把最佳响应加进来

理解 PSRO 之前，先看 Double Oracle 会顺很多。

Double Oracle 的出发点是：完整策略空间太大，直接求原博弈均衡很难；那就先从一个很小的受限策略集开始，只在这个小集合里求解。

设第 $t$ 轮每个玩家维护一个受限策略集：

$$
\Pi_i^t
=
\{\pi_i^1,\pi_i^2,\ldots,\pi_i^{K_i}\}.
$$

这些策略诱导出一个受限博弈，也常叫元博弈：

$$
M_i^t(k_1,\ldots,k_n)
=
u_i(\pi_1^{k_1},\ldots,\pi_n^{k_n}).
$$

两人零和时，元博弈就是一个 payoff matrix：

$$
M^t_{kl}
=
u_1(\pi_1^k,\pi_2^l).
$$

Double Oracle 先在这个受限博弈上求均衡：

$$
x^t
\in
\operatorname{Equilibrium}(M^t).
$$

然后回到原始策略空间，计算每个玩家对 $x_{-i}^t$ 的最佳响应：

$$
\pi_i^{BR}
\in
\arg\max_{\pi_i}
\mathbb{E}_{\pi_{-i}\sim x_{-i}^t}
\left[
u_i(\pi_i,\pi_{-i})
\right].
$$

如果 $\pi_i^{BR}$ 已经在 $\Pi_i^t$ 中，说明当前受限博弈的解已经没有被原始策略空间中的新响应打破，可以停止。

如果它不在策略集中，就把它加入：

$$
\Pi_i^{t+1}
=
\Pi_i^t
\cup
\{\pi_i^{BR}\}.
$$

然后重新构造受限博弈、重新求均衡、重新找最佳响应。

所以 Double Oracle 的结构非常清楚：

$$
\text{restricted game}
\rightarrow
\text{equilibrium in restricted game}
\rightarrow
\text{best response in full game}
\rightarrow
\text{expand restricted game}.
$$

如果策略空间有限、元博弈精确求解、最佳响应精确计算，Double Oracle 可以逐步扩展受限博弈并最终找到原博弈均衡。

但这三个“精确”在深度多智能体任务里基本都太贵：

$$
\text{exact strategy}
\rightarrow
\text{learned policy},
$$

$$
\text{exact payoff}
\rightarrow
\text{sampled payoff estimate},
$$

$$
\text{exact best response}
\rightarrow
\text{RL oracle}.
$$

PSRO 就是在这个位置出现的。

## 8. PSRO：把 Double Oracle 深度学习化，也把 FP 提升到策略空间

PSRO 全称 Policy Space Response Oracles。它可以看成 Double Oracle 的深度学习版本，也可以看成 FP 思想在策略空间中的推广。

在 PSRO 中，策略池里的元素通常不是表格策略，而是训练出来的 policy，例如神经网络策略。策略池仍然记为：

$$
\Pi_i^t
=
\{\pi_i^1,\pi_i^2,\ldots,\pi_i^{K_i}\}.
$$

由于真实环境里 payoff 很难解析计算，元博弈矩阵通常通过 rollout 估计：

$$
\hat{M}_{kl}
=
\frac{1}{m}
\sum_{r=1}^{m}
R^{(r)}(\pi_1^k,\pi_2^l).
$$

接下来，meta-solver 在估计得到的元博弈上产生元策略：

$$
x^t
=
\operatorname{MetaSolver}(\hat{M}^t).
$$

如果 meta-solver 是纳什求解器，那么 $x^t$ 就是策略池上的元纳什分布；如果是 Uniform、AlphaRank、replicator dynamics 或其他规则，它就会给出另一种历史策略权重。

然后用 RL oracle 训练新的响应策略：

$$
\pi_i^{new}
\approx
\arg\max_{\pi_i}
\mathbb{E}_{\pi_{-i}\sim x_{-i}^t}
\left[
u_i(\pi_i,\pi_{-i})
\right].
$$

最后加入策略池：

$$
\Pi_i^{t+1}
=
\Pi_i^t
\cup
\{\pi_i^{new}\}.
$$

这就是 PSRO 的主循环。

它和 FP 的对应关系非常清楚：

| 维度 | Fictitious Play | PSRO |
| --- | --- | --- |
| 基本对象 | 动作/行为策略 | 完整策略 |
| 历史记忆 | 历史策略平均 | 策略池 |
| 对手分布 | 经验平均策略 | 元策略 |
| 响应 | best response | oracle policy |
| 输出 | average policy | mixture over population |

所以可以说：

$$
\text{PSRO is fictitious-play-like learning in policy space.}
$$

如果 FP 的“历史平均”是在原始策略空间里做，那么 PSRO 的“历史平均”就是通过 meta-strategy 在策略池上做。

这就是从 $\bar{\sigma}$ 到 $x\in\Delta(\Pi)$ 的变化。

这使得 PSRO 可以用于更大、更复杂的环境，但也引入了三个误差源：

1. payoff estimation error；
2. meta-solver error；
3. oracle approximation error。

当 $m$ 不够大时，元策略可能会被噪声误导。策略池越大，矩阵估计成本越高；如果每轮都补全 payoff matrix，代价通常至少随策略数平方增长。

这也是 PSRO 工程上最常见的瓶颈之一：

$$
|\Pi| \uparrow
\quad\Rightarrow\quad
\text{payoff evaluation cost} \uparrow.
$$

## 9. Self-Play、FP、PSRO 的差别可以浓缩成一张表

| 方法 | 对手分布 $\mu^t$ | 记忆 | 响应目标 | 优点 | 典型问题 |
| --- | --- | --- | --- | --- | --- |
| Naive Self-Play | $\delta_{\pi^t}$ | 最新策略 | 打败当前版本 | 简单、便宜 | 循环、过拟合当前对手 |
| Fictitious Play | 历史平均 $\bar{\sigma}^t$ | 全历史平均 | 对经验信念最佳响应 | 稳定、均衡解释清晰 | 收敛慢、BR 代价高 |
| NFSP/XFP | 平均行为策略 | 平均策略网络/行为策略 | 近似 FP | 可扩展到深度设置 | 平均策略学习困难 |
| PSRO | 元策略 $x^t\in\Delta(\Pi)$ | 策略池 | 对 population mixture 的 oracle | 能处理非传递和策略多样性 | payoff matrix 与 oracle 成本高 |
| League Training | 手工/自动构造的对手分布 | 主策略、历史策略、exploiters | 鲁棒实战表现 | 工程有效 | 理论解释依赖具体机制 |

这张表里的核心变量始终是同一个：

$$
\mu^t.
$$

也就是当前训练轮的对手分布。

如果一篇 self-play 论文没有讲清楚 $\mu^t$ 是怎么来的，它就没有讲清楚最关键的训练设计。

## 10. 一个统一视角

可以把三类方法统一写成：

$$
\pi_i^{t+1}
\approx
\arg\max_{\pi_i}
\mathbb{E}_{\pi_{-i}\sim \mu_{-i}^t}
\left[
u_i(\pi_i,\pi_{-i})
\right],
$$

差别只在于 $\mu_{-i}^t$：

$$
\mu_{-i}^t
=
\begin{cases}
\delta_{\pi_{-i}^t}, & \text{Naive Self-Play},\\
\bar{\sigma}_{-i}^t, & \text{Fictitious Play},\\
x_{-i}^t\in\Delta(\Pi_{-i}^t), & \text{PSRO}.
\end{cases}
$$

这组公式几乎就是整篇文章的核心。

Self-Play 是外层训练闭环。

Fictitious Play 给这个闭环加入历史平均信念。

PSRO 把历史平均从策略本身推广到策略群体上的元分布。

所以现代多智能体训练中的很多设计，本质上都是在回答：

$$
\text{How should we construct } \mu^t?
$$

## 11. 结语：FP 旧，但它问的问题没有旧

Fictitious Play 是一个很老的算法，但它提出的问题并不老。

在今天的深度多智能体系统里，我们仍然不断遇到同一个困境：

训练最新策略很容易，训练在长期分布上稳定的策略很难。

打败当前对手很容易，面对历史和群体都稳定很难。

得到一个强策略很容易，得到一个强而多样的策略生态很难。

从这个角度看，Self-Play、Fictitious Play 和 PSRO 可以被看成同一条线上的三个层次：

$$
\text{current opponent}
\rightarrow
\text{historical average}
\rightarrow
\text{population-level meta-strategy}.
$$

Self-Play 提供训练数据。

Fictitious Play 提供历史平均的稳定化原则。

PSRO 提供策略空间中的群体化表达。

真正值得研究的，不是某个术语本身，而是它们共同指向的那个问题：

**在多智能体学习中，智能体应该如何面对自己的历史？**
