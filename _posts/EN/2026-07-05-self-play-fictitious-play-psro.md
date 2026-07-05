---
title: "From Self-Play to PSRO: Why Fictitious Play Still Matters for Understanding Multi-Agent Training"
date: 2026-07-05
layout: post
author: Ju Qi
lang: en
excerpt: "Self-Play is not a single algorithm, but a training loop centered on opponent distributions. This post connects Fictitious Play, Double Oracle, and PSRO through one unified question: how should an agent face its own history?"
---

Self-Play is often presented as a success story in multi-agent reinforcement learning and computational game theory: AlphaGo became stronger through self-play, poker agents approached equilibrium through self-play, and AlphaStar used league training to obtain robust strategies.

But if we understand Self-Play merely as "letting an agent play against itself," we miss the central issue.

The real question is not simply "playing against oneself," but:

$$
\text{current policy should train against whom?}
$$

Should the current policy train against its latest version? Against a historical average? Against a mixture over historical policies? Against specially trained exploiters?

This is exactly where Fictitious Play and PSRO enter the picture. They are not separate from Self-Play; rather, they are systematic answers to the central question of opponent distributions in Self-Play.

A rough mental map is:

$$
\text{Naive Self-Play}
\subset
\text{Fictitious Play style learning}
\subset
\text{Population-based / PSRO style learning}.
$$

This is not meant as a strict set-theoretic inclusion. It is an evolution of ideas: from the current policy, to historical averages, to policy populations.

This post treats Self-Play not as a single algorithm, but as a training loop composed of several questions: how history is stored, how opponents are sampled, how responses are trained, and how the final strategy is represented. From this perspective, the roles of Fictitious Play and PSRO become much clearer.

## 1. Self-Play Is Not an Algorithm, but a Training Loop

Consider a finite game:

$$
G = \langle N,\{\Sigma_i\}_{i\in N},\{u_i\}_{i\in N}\rangle.
$$

Here $N$ is the set of players, $\Sigma_i$ is the strategy space of player $i$, and $u_i(\sigma_i,\sigma_{-i})$ is player $i$'s payoff under strategy profile $\sigma=(\sigma_i,\sigma_{-i})$.

At a very abstract level, Self-Play can be written as:

$$
\pi_i^{t+1}
\approx
\operatorname{Oracle}_i(\mu_{-i}^t),
$$

where $\mu_{-i}^t$ is the opponent distribution used to train player $i$ at iteration $t$, and $\operatorname{Oracle}_i$ is some response-learning procedure: an exact best response, an approximate best response, an RL trainer, an MCTS-enhanced policy improvement operator, and so on.

If the oracle is a best response, then:

$$
\operatorname{BR}_i(\mu_{-i})
\in
\arg\max_{\pi_i\in\Sigma_i}
\mathbb{E}_{\pi_{-i}\sim \mu_{-i}}
\left[
 u_i(\pi_i,\pi_{-i})
\right].
$$

This shows that the real design problem in Self-Play is not the slogan "play against yourself," but four concrete choices:

1. Memory: which historical policies should be stored?
2. Opponent distribution: how should $\mu^t$ be constructed from history?
3. Response oracle: how should $\operatorname{Oracle}(\mu^t)$ be trained?
4. Output strategy: should we deploy the latest policy, an average policy, or a mixture over policies?

Naive Self-Play is only the simplest special case:

$$
\mu_{-i}^t = \delta_{\pi_{-i}^{t}},
$$

meaning that the agent only trains against the opponent's current version.

This works well in many perfect-information games, especially when search, value functions, and policy improvement form a stable loop. But in general games, especially imperfect-information or strongly non-transitive games, it can easily enter a best-response cycle.

Rock-paper-scissors is the smallest example:

$$
R \rightarrow P \rightarrow S \rightarrow R.
$$

The example is elementary, but the issue is not. If the training target is always the current opponent, learning may simply chase local weaknesses instead of forming a stable long-run strategy.

## 2. Fictitious Play: The Classical Historical-Average Mechanism in Self-Play

Fictitious Play was introduced by Brown in 1951. Its core assumption is simple:

**Each player assumes that opponents play according to their historical average strategies, and then best-responds to that historical average.**

Suppose player $i$ has produced strategies $\sigma_i^1,\ldots,\sigma_i^t$ in the first $t$ iterations. The empirical average strategy is:

$$
\bar{\sigma}_i^t
=
\frac{1}{t}\sum_{k=1}^{t}\sigma_i^k.
$$

At iteration $t+1$, player $i$ computes a best response to the opponents' average strategies:

$$
\sigma_i^{t+1}
\in
\operatorname{BR}_i(\bar{\sigma}_{-i}^{t})
=
\arg\max_{\sigma_i}
 u_i(\sigma_i,\bar{\sigma}_{-i}^{t}).
$$

Then the average strategy is updated:

$$
\bar{\sigma}_i^{t+1}
=
\frac{t}{t+1}\bar{\sigma}_i^t
+
\frac{1}{t+1}\sigma_i^{t+1}.
$$

In a more general step-size form:

$$
\bar{\sigma}_i^{t+1}
=
(1-\alpha_{t+1})\bar{\sigma}_i^t
+
\alpha_{t+1}
\operatorname{BR}_i(\bar{\sigma}_{-i}^{t}).
$$

The original FP corresponds to $\alpha_{t+1}=1/(t+1)$.

The key point is not averaging for its own sake. The key is that FP changes the opponent distribution used in Self-Play:

$$
\mu_{-i}^t = \bar{\sigma}_{-i}^t.
$$

Naive Self-Play trains against the latest opponent. Fictitious Play trains against the historical-average opponent.

That is the crucial step. Training no longer only reacts to short-term weaknesses of the current strategy; it responds to a long-run empirical distribution.

In two-player zero-sum games, classical results show that the average strategies of FP converge to Nash equilibrium. In more general games, FP does not always converge, but it remains a fundamental template for understanding modern population-based self-play methods.

## 3. Why FP Is Closer to Equilibrium Learning Than Naive Self-Play

A typical abstraction of Naive Self-Play is:

$$
\sigma^{t+1}
\approx
\operatorname{BR}(\sigma^t).
$$

If the game has strong non-transitive structure, this dynamic may cycle.

FP instead has the form:

$$
\sigma^{t+1}
\approx
\operatorname{BR}(\bar{\sigma}^t),
\qquad
\bar{\sigma}^{t+1}
=
\operatorname{Average}(\bar{\sigma}^t,\sigma^{t+1}).
$$

Here $\bar{\sigma}^t$ plays the role of an empirical belief. Players do not assume that opponents will use only their latest policies; they assume opponent behavior is generated by the historical empirical distribution.

From an online-learning perspective, this turns "best-responding to the current opponent" into "tracking a response to an empirical distribution." From a game-theoretic perspective, it moves the update closer to the equilibrium idea of belief consistency plus optimal response.

This is the core value of FP:

$$
\text{stability comes from averaging the opponent, not from trusting the latest policy.}
$$

Of course, averaging has costs. FP may converge slowly, and computing a best response at each iteration can be expensive. Much of the modern literature can be viewed as modifying this template: approximate the best response, compress the history, or lift averaging from the action space to the policy space.

## 4. Theoretical Guarantees Often Stop at CCE, and That Is Often Enough

There is an important caveat: outside special settings such as two-player zero-sum games and potential games, Fictitious Play, PSRO, and many self-play variants usually cannot casually promise that they learn a Nash equilibrium.

A more realistic interpretation is that they often learn stability at the level of an empirical distribution. A typical target is the coarse correlated equilibrium (CCE).

Let $\rho$ be a distribution over joint strategy profiles. If for every player $i$ and every fixed deviation $\pi_i'$ we have:

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

then $\rho$ is a CCE.

Intuitively, if the training process outputs a distribution over joint policies, no single player can improve its expected payoff by committing in advance to a fixed alternative policy.

CCE is weaker than NE. Usually:

$$
\text{NE} \subseteq \text{CE} \subseteq \text{CCE}.
$$

But weaker does not mean useless. In large-scale multi-agent training, what we often need is not an analytically exact single-point NE, but a stable policy distribution that cannot be easily broken by simple unilateral deviations.

In two-player zero-sum settings, CCE aligns with the minimax value in terms of payoff. In more complex general-sum or multiplayer settings, CCE is often sufficient for training and evaluation. Many engineering systems deploy a population, league, or meta-policy rather than a single pure strategy anyway.

So a more realistic expectation for FP/PSRO-style methods is:

$$
\text{not necessarily exact NE, but a useful stable distribution.}
$$

This perspective also explains why PSRO and league training can work well in practice even when their theoretical guarantees do not always reach exact NE.

## 5. GWFP: Why Approximate Oracles Still Fit the FP Framework

In real systems, exact best responses are rarely available. A response policy trained by deep RL is usually only an approximate oracle, with sampling noise and function-approximation error.

This motivates Generalized Weakened Fictitious Play (GWFP), which writes FP in a looser form:

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

Here:

$b^{\epsilon_t}$ is an $\epsilon_t$-best response rather than an exact best response.

$M_{t+1}$ is a noise term, such as sampling error, value-estimation error, or training error.

$\alpha_t$ is the step size.

Typical convergence conditions include:

$$
\alpha_t\rightarrow 0,
\qquad
\sum_{t=1}^{\infty}\alpha_t=\infty,
\qquad
\epsilon_t\rightarrow 0,
$$

with the noise controlled in a weighted sense.

This framework matters because it explains why modern deep self-play can still be viewed as an approximate FP process: as long as the RL oracle improves, noise does not dominate the update, and averaging remains stable, the training process preserves the structure of FP.

This is the theoretical bridge from classical FP to NFSP, PSRO, and league training.

## 6. In Extensive-Form Games, Averaging Is Not So Simple

The previous notation is closer to normal-form games. In imperfect-information extensive-form games, a strategy is not merely a simple vector; it is a behavioral strategy defined over information sets:

$$
\sigma_i(I,a), \quad I\in\mathcal{I}_i,\ a\in A(I).
$$

Here $I$ is an information set of player $i$, and $A(I)$ is the set of actions available at that information set.

In extensive-form games, average strategies usually cannot be computed by simple pointwise averaging. One must account for the player's own reach probability. A common form is:

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

$\pi_i^{\sigma^t}(I)$ denotes the contribution of player $i$'s own actions to reaching information set $I$ under strategy $\sigma^t$.

The meaning of this reach-weighted average is that information sets more frequently reached under the player's own strategy receive more weight in the average strategy.

Extensive-Form Fictitious Play (XFP) can be understood as extending FP to extensive-form games: it maintains average behavioral strategies and computes best responses to those averages.

The problem is that a full best response may require traversing the game tree, which is infeasible in large imperfect-information games such as poker.

This leads to sampling, function approximation, policy networks, and average-policy networks. Neural Fictitious Self-Play (NFSP), for example, maintains two kinds of policies:

$$
\pi^{BR} \approx \operatorname{BR}(\bar{\pi}),
\qquad
\bar{\pi}\approx \text{average of historical best responses}.
$$

Training uses an anticipatory mixture:

$$
\pi^{mix}
=
\eta \pi^{BR}
+
(1-\eta)\bar{\pi}.
$$

Here $\eta$ controls the mixture between the current best-response policy and the historical-average policy.

This is the shadow of FP in deep learning: one network learns the response, and another learns the average.

## 7. Double Oracle: Solve a Restricted Game, Then Add Best Responses

Before PSRO, Double Oracle is the smoother concept to understand.

The starting point of Double Oracle is simple: the full strategy space is too large, so instead of solving the original game directly, begin with a small restricted strategy set and solve only the restricted game.

At iteration $t$, each player maintains a restricted strategy set:

$$
\Pi_i^t
=
\{\pi_i^1,\pi_i^2,\ldots,\pi_i^{K_i}\}.
$$

These policies induce a restricted game, often called a meta-game:

$$
M_i^t(k_1,\ldots,k_n)
=
 u_i(\pi_1^{k_1},\ldots,\pi_n^{k_n}).
$$

In two-player zero-sum games, the meta-game is a payoff matrix:

$$
M^t_{kl}
=
 u_1(\pi_1^k,\pi_2^l).
$$

Double Oracle first solves for an equilibrium in this restricted game:

$$
x^t
\in
\operatorname{Equilibrium}(M^t).
$$

Then it returns to the full strategy space and computes each player's best response to $x_{-i}^t$:

$$
\pi_i^{BR}
\in
\arg\max_{\pi_i}
\mathbb{E}_{\pi_{-i}\sim x_{-i}^t}
\left[
 u_i(\pi_i,\pi_{-i})
\right].
$$

If $\pi_i^{BR}$ is already in $\Pi_i^t$, then the restricted-game solution is not broken by any new response from the full strategy space, and the algorithm can stop.

If it is not in the set, add it:

$$
\Pi_i^{t+1}
=
\Pi_i^t
\cup
\{\pi_i^{BR}\}.
$$

Then rebuild the restricted game, solve it again, and compute new best responses.

The structure of Double Oracle is:

$$
\text{restricted game}
\rightarrow
\text{equilibrium in restricted game}
\rightarrow
\text{best response in full game}
\rightarrow
\text{expand restricted game}.
$$

If the strategy space is finite, the meta-game is solved exactly, and exact best responses are available, Double Oracle can expand the restricted game and eventually find an equilibrium of the original game.

But in deep multi-agent tasks, all three exact objects are usually too expensive:

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

This is where PSRO appears.

## 8. PSRO: Deep-Learning Double Oracle and Policy-Space FP

PSRO stands for Policy Space Response Oracles. It can be understood as a deep-learning version of Double Oracle, and also as a policy-space generalization of FP.

In PSRO, elements in the strategy pool are usually learned policies, such as neural network policies, rather than exact tabular strategies. The pool is still written as:

$$
\Pi_i^t
=
\{\pi_i^1,\pi_i^2,\ldots,\pi_i^{K_i}\}.
$$

Because payoffs in real environments are hard to compute analytically, the meta-game matrix is usually estimated through rollouts:

$$
\hat{M}_{kl}
=
\frac{1}{m}
\sum_{r=1}^{m}
R^{(r)}(\pi_1^k,\pi_2^l).
$$

Next, a meta-solver produces a meta-strategy on the estimated meta-game:

$$
x^t
=
\operatorname{MetaSolver}(\hat{M}^t).
$$

If the meta-solver is a Nash solver, $x^t$ is a meta-Nash distribution over the policy pool. If it is Uniform, AlphaRank, replicator dynamics, or another rule, it gives another weighting over historical policies.

Then an RL oracle trains a new response policy:

$$
\pi_i^{new}
\approx
\arg\max_{\pi_i}
\mathbb{E}_{\pi_{-i}\sim x_{-i}^t}
\left[
 u_i(\pi_i,\pi_{-i})
\right].
$$

Finally, add it to the policy pool:

$$
\Pi_i^{t+1}
=
\Pi_i^t
\cup
\{\pi_i^{new}\}.
$$

This is the main loop of PSRO.

Its correspondence with FP is straightforward:

| Dimension | Fictitious Play | PSRO |
| --- | --- | --- |
| Basic object | action / behavioral strategy | full policy |
| Memory | historical strategy average | policy pool |
| Opponent distribution | empirical average strategy | meta-strategy |
| Response | best response | oracle policy |
| Output | average policy | mixture over population |

So we can say:

$$
\text{PSRO is fictitious-play-like learning in policy space.}
$$

If FP performs historical averaging in the original strategy space, PSRO performs a policy-space version of this idea through a meta-strategy over the policy pool.

This is the shift from $\bar{\sigma}$ to $x\in\Delta(\Pi)$.

PSRO can scale to larger and more complex environments, but it also introduces three sources of error:

1. payoff estimation error;
2. meta-solver error;
3. oracle approximation error.

When $m$ is too small, noise can mislead the meta-strategy. As the policy pool grows, matrix evaluation becomes more expensive. If every iteration requires completing the payoff matrix, the cost usually grows at least quadratically in the number of policies.

This is one of the most common engineering bottlenecks in PSRO:

$$
|\Pi| \uparrow
\quad\Rightarrow\quad
\text{payoff evaluation cost} \uparrow.
$$

## 9. A Compact Comparison

| Method | Opponent distribution $\mu^t$ | Memory | Response target | Strength | Typical issue |
| --- | --- | --- | --- | --- | --- |
| Naive Self-Play | $\delta_{\pi^t}$ | latest policy | beat current version | simple and cheap | cycling, overfitting to current opponent |
| Fictitious Play | historical average $\bar{\sigma}^t$ | full historical average | best response to empirical belief | stable, clear equilibrium interpretation | slow convergence, expensive BR |
| NFSP/XFP | average behavioral strategy | average-policy network / behavioral strategy | approximate FP | scalable to deep settings | difficult average-policy learning |
| PSRO | meta-strategy $x^t\in\Delta(\Pi)$ | policy pool | oracle against population mixture | handles non-transitivity and diversity | payoff matrix and oracle costs |
| League Training | manually / automatically constructed opponent distribution | main policies, historical policies, exploiters | robust practical performance | engineering effectiveness | theory depends on specific mechanism |

The core variable in the table is always the same:

$$
\mu^t.
$$

That is, the opponent distribution used at the current training iteration.

If a self-play paper does not explain where $\mu^t$ comes from, it has not explained the most important training design choice.

## 10. A Unified View

We can write these methods in one form:

$$
\pi_i^{t+1}
\approx
\arg\max_{\pi_i}
\mathbb{E}_{\pi_{-i}\sim \mu_{-i}^t}
\left[
 u_i(\pi_i,\pi_{-i})
\right],
$$

and the difference lies in $\mu_{-i}^t$:

$$
\mu_{-i}^t
=
\begin{cases}
\delta_{\pi_{-i}^t}, & \text{Naive Self-Play},\\
\bar{\sigma}_{-i}^t, & \text{Fictitious Play},\\
x_{-i}^t\in\Delta(\Pi_{-i}^t), & \text{PSRO}.
\end{cases}
$$

This set of equations is almost the entire point of the post.

Self-Play is the outer training loop.

Fictitious Play adds historical-average beliefs to that loop.

PSRO lifts historical averaging from strategies themselves to a meta-distribution over a policy population.

Therefore, much of modern multi-agent training is fundamentally about answering:

$$
\text{How should we construct } \mu^t?
$$

## 11. Conclusion: FP Is Old, but Its Question Is Not

Fictitious Play is an old algorithm, but the question it asks is not old.

In today's deep multi-agent systems, we repeatedly face the same dilemma:

Training the latest policy is easy; training a policy that is stable under a long-run distribution is hard.

Beating the current opponent is easy; being stable against history and population is hard.

Obtaining one strong policy is easy; obtaining a strong and diverse policy ecosystem is hard.

From this perspective, Self-Play, Fictitious Play, and PSRO form three layers of the same line of thought:

$$
\text{current opponent}
\rightarrow
\text{historical average}
\rightarrow
\text{population-level meta-strategy}.
$$

Self-Play provides training data.

Fictitious Play provides the stabilizing principle of historical averaging.

PSRO provides a population-level representation in policy space.

What truly matters is not the terminology itself, but the shared question behind these methods:

**In multi-agent learning, how should an agent face its own history?**
