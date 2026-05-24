---
title: "From AlphaGo to *Longzhong Dui*: High-Quality Reasoning Under Limited Information"
date: 2026-05-24
layout: post
author: Ju Qi
lang: en
excerpt: "AlphaGo can crush human grandmasters on a closed board, yet it cannot produce a *Longzhong Dui*-style open strategic analysis. This post compares MCTS with human decision-making and argues that the real gap is not 'more compute', but a fundamentally different way of thinking."
---

> **TL;DR.** The ceiling of MCTS is the ceiling of *statistical intelligence*. The reason AlphaGo cannot reproduce Zhuge Liang's *Longzhong Dui* is not a compute gap, but a missing stack of human-style cognitive abilities: dynamic abstraction, meaningful macro-actions, asymmetric reasoning, causal opponent modeling, and dynamic value trade-offs.

## Introduction: A Paradox Worth Thinking About

In 2016, AlphaGo defeated Lee Sedol, giving many people their first visceral sense of what AI can do on complex decision tasks. The state space of Go is enormous and its branching is brutal, yet AlphaGo combined deep neural networks with Monte Carlo Tree Search (MCTS) — fusing policy priors, value evaluation and search — and broke through in a domain long considered to depend on human intuition.

But once you broaden the lens from Go to real-world strategy, a deep paradox appears: **AlphaGo can run millions of simulations on a board with crystal-clear rules and fully observable state, yet it struggles with open-ended strategic reasoning of the kind found in *Longzhong Dui* (隆中对).**

When Zhuge Liang proposed his "Three Kingdoms" plan in Longzhong, he had no complete information, no reliable real-time intelligence, and no way to enumerate every historical path over the next several decades. He was facing a highly uncertain, adversarial, multi-agent, long-horizon system: Cao Cao, Sun Quan, Liu Bei, Jingzhou, Yizhou, gentry families, public sentiment, geography, military, diplomacy — all entangled, where any local change could ripple through the whole structure.

From the perspective of modern cognitive science and decision theory, the value of *Longzhong Dui* is not just that it was a brilliant historical judgment. More importantly, it is a textbook demonstration of high-level human reasoning: **under limited information, limited compute, and almost no opportunity for trial-and-error, capturing the core structure of a complex situation through abstraction, filtering, modeling and focused reasoning.**

This is exactly where MCTS hits a wall on real-world problems. The hard part is not "adding a few more evaluation metrics", but **knowing, in each situation, which level of abstraction, which evaluation scale, and which search strategy to use.** In other words, the deep flaw of MCTS is not that it "doesn't compute enough", but that **its mode of thinking is fundamentally different from a human's.**

---

## 1. The Core Capability and Intrinsic Limits of MCTS

MCTS is a search method that makes decisions through sampling and statistical estimation. Its workflow has four steps:

1. **Selection** — start from the root and pick a branch using existing value estimates and visit counts.
2. **Expansion** — once you reach an under-explored node, expand it.
3. **Simulation** — estimate the outcome of that branch via simulation.
4. **Backpropagation** — push the result back up the path to update the values of all visited nodes.

Its main strength is generality: as long as you can define states, actions and a terminal reward, MCTS can incrementally approach a good solution in a huge decision space. AlphaGo's success owes a great deal to plugging neural-network priors and value functions into MCTS, turning the search from a blind random walk into one guided by high-quality prior knowledge.

But this also exposes its fundamental limits. MCTS is, at its core, **a bottom-up statistical machine**:

- It starts from concrete atomic states and atomic actions and aggregates value upward; it **can never escape the predefined state and action space**.
- It only cares about *what* is happening — it estimates state value via massive sampling — but it **does not understand *why* a state is valuable**.
- All its meta-decisions — exploration constants, levels of abstraction, evaluation metrics, stopping criteria — must be **set by humans in advance** and cannot be adjusted autonomously.

When applied to a closed system like Go — clear rules, full information, fixed time — MCTS's strengths shine. But the moment you point it at real strategic decisions, it runs into structural difficulties: **the real world has no predefined states and actions, no clear terminal reward, and no infinite repeated simulations.**

---

## 2. *Longzhong Dui* Is High-Compression-Ratio Human-Style Reasoning

If we treat *Longzhong Dui* as a decision problem, it is far harder than any board game:

- **Incomplete information** — Zhuge Liang could not know the true state of every army, supply line, or local power.
- **Huge action space** — military operations, diplomatic alliances, territorial choices, talent organization, internal governance.
- **Long horizon** — not a few moves to a winner, but a decade or several decades of strategic evolution.

Naive enumeration of all possible paths collapses immediately under those conditions. **What actually works is not exhaustive search, but modeling.** Zhuge Liang did not sample paths; he built a structured model of the world.

### Extreme state abstraction

*Longzhong Dui* does not break the empire down into every city, every army, every clan. It compresses the situation into a few key structures:

- Cao Cao controls the north and holds political legitimacy.
- Sun Quan holds Jiangdong with regional stability.
- Jingzhou is the connector between north–south and east–west.
- Yizhou offers strategic depth and resources.
- Liu Bei needs to build an independent base.

This is representation learning at an extreme compression ratio: **keep the variables that drive the long-term landscape, discard short-term noise.**

### Meaningful action abstraction

Zhuge Liang did not discuss "how many troops to send to which city on which day". He discussed *"ally with Wu against Cao"*, *"take Jingzhou first"*, *"then take Yizhou"*, *"wait for the world to change"*.

These are **macro-actions** — high-level strategic units composed of many low-level operations. They are not arbitrary action bundles, but coherent wholes carrying internal logic and strategic intent.

### Asymmetric allocation of compute

*Longzhong Dui* does not reason equally about every branch. It pours almost all of its thinking into two key nodes — *taking Jing-Yi* and *allying with Wu against Cao* — and **prunes** low-value branches like "submit to Cao" or "depend on Sun" outright.

This is the hallmark of a strong human decision-maker: **don't enumerate more, compress more accurately; don't search uniformly, know where it is worth digging.**

---

## 3. Six Algorithmic Properties of Human Decision-Making

If we translate Zhuge Liang's reasoning into algorithmic language, six core properties emerge — **each of which is missing from current MCTS**.

### 3.1 High-compression, dynamic state abstraction

Zhuge Liang reduces a near-infinite-dimensional empire into five core players and a few key strategic regions. The abstraction is not static but **dynamic** — he can zoom out to "the empire splits in three" when discussing the macro picture, and zoom in to "Guan Yu is arrogant by nature" when discussing concrete issues.

MCTS's state abstractions are typically fixed: too coarse and it loses key features, too fine and the tree explodes. **Goal-driven dynamic abstraction** remains very hard for current algorithms.

### 3.2 Meaning-based macro-action space

The core decisions in *Longzhong Dui* are not atomic actions but high-level units like "ally with Wu against Cao" or "take Jingzhou first". These macro-actions are not hand-coded; they emerge naturally from historical experience and causal logic.

In MCTS, macro-actions usually have to be designed by humans. **Automatically discovering meaningful macro-actions** — and handling the uncertainty inside them — is still an open problem.

### 3.3 Asymmetric allocation of cognitive resources

Zhuge Liang did not split his thinking time evenly across all strategies. He concentrated almost his entire reasoning budget on a few key nodes and pruned low-value branches outright.

This allocation is **not statistical, but intuitive and causal** — MCTS cannot accurately estimate the *information gain* of a node, i.e. how much new understanding thinking about it will yield.

### 3.4 Distributional, not point-wise, value evaluation

Zhuge Liang did not predict the outcome of any specific battle. He evaluated the **long-term distribution of outcomes** under different strategic paths: occupying Jing-Yi is slow but yields a stable base and strategic depth; confronting Cao Cao directly may give short-term gains but carries enormous downside risk.

Vanilla MCTS only estimates the expected value of a state and **completely ignores variance and risk**. In real decisions, an action with high mean but huge variance is often worse than one with slightly lower mean but more robust outcomes.

### 3.5 Causal opponent modeling under partial information

Stuck in Longzhong, Zhuge Liang's observation channel was full of noise and delay. Yet from limited historical data he built an extremely accurate world model and opponent model — judging that Cao "cannot be challenged head-on" and Sun "can be allied with but not absorbed", thereby locating the Nash equilibrium of this multi-agent system.

**MCTS opponent modeling is statistical; human opponent modeling is causal** — we don't just know what an opponent did, we understand *why* they did it.

### 3.6 Multi-dimensional dynamic value trade-offs

Zhuge Liang's decision balanced **geography, politics, public sentiment, resources and time** simultaneously, and the relative weights changed over time: when weak, prioritize survival and a base; once stable, prioritize expansion and initiative; when external conditions shift, recalibrate the risk appetite.

This **dynamic re-weighting** is exactly what humans do well and what algorithms struggle with.

---

## 4. The Real Difficulty: Coupling Between Metrics

It is easy to list valuable indicators when discussing decisions:

> mean value / variance / confidence interval / visit counts / policy prior / exploration difficulty / state uncertainty / opponent-response sensitivity / sub-tree complexity / risk lower bound / abstraction level / macro-action quality …

The hard part is not "naming these indicators". It is **knowing *when* to trust *which* one**. This is the **metric-coupling problem**, and it is the deepest gap between human decision-making and MCTS.

| Indicator | One reading | Another reading |
|---|---|---|
| High variance | Big upside, worth more exploration | Highly unstable, not worth more compute |
| High mean | High-quality action | Under-sampled, temporarily over-estimated |
| Low visit count | Has been overlooked | Genuinely worthless strategically |
| Macro-actions | Reduce search complexity | May hide critical failure modes |
| State abstraction | Improve efficiency | May wrongly merge situations that differ |

Stuffing all of these into a single formula does not necessarily make the algorithm stronger — it often makes it more brittle. Each indicator has its applicable conditions, and they conflict with each other.

What MCTS lacks is a **higher-level meta-decision capability**:

- For this node, do I look at the mean or the variance?
- Should I expand exploration or converge to verification?
- Should I refine further or raise the abstraction level?
- Should I chase the upper bound or protect the lower bound?
- Should I trust the policy prior or doubt it and re-search?

Strong human players have exactly this capability: **we do not score every metric column-by-column; we switch judgment criteria as the situation evolves.**

---

## 5. The Essence of Human Decision-Making: Three Things MCTS Will Never Replicate

The gap between MCTS and human decision-making is not a compute gap; it is a **mode-of-being gap**. AlphaGo Zero can surpass humans by self-play from scratch, but it can never produce *Longzhong Dui* from scratch.

### 5.1 Humans set their own goals; they aren't handed a win-loss function

Every MCTS-based AI shares one premise: a predefined, quantifiable objective. In Go it is "win the game"; in video games it is "maximize score"; in recommender systems it is "maximize CTR".

Human goals are never single, never given a priori, and certainly not a simple binary win/lose. Zhuge Liang's goal was not "unify China" — it was *"restore the Han and return to the old capital"*, a goal that bundles **political ideal, moral aspiration, personal ambition, and historical responsibility**.

More importantly, the value of a human decision is not determined solely by its outcome. Zhuge Liang ultimately failed to unify China, yet he is still revered as the embodiment of wisdom and loyalty.

MCTS only understands win and lose. It does not know what an *ideal* is, what *responsibility* is, or what *dignity* is.

### 5.2 Human decisions are built on millennia of collective experience and embodied practice

*Longzhong Dui* did not appear out of thin air. It is Zhuge Liang's distillation of centuries of historical experience since the Spring-and-Autumn period, of his deep understanding of Chinese geography, politics, military, and human nature, and of his **ten years of reading, thinking and observing in Longzhong**.

Human knowledge is not isolated; it is **collective wisdom passed down across generations**. We stand on our predecessors' shoulders, inheriting their experience, lessons, ideas and culture.

Today's AI is essentially "from scratch". Even large models only learn statistical regularities of language from massive text — they have never experienced war, never felt the weight of politics, never tasted human nature in the flesh. Their "knowledge" is second-hand, surface-level, ungrounded.

That is why pure tabula-rasa reinforcement learning is only practical in games: **in the real world you do not get that many do-overs.**

### 5.3 Human abstraction is meaning-based, not statistics-based

This is the deepest, most stubborn gap.

- **MCTS abstraction is based on statistical similarity** — it merges states that *look* similar.
- **Human abstraction is based on meaning** — we merge things that share the same essence, the same function, the same causal role.

Zhuge Liang reduces the empire to "Cao Cao, Sun Quan, Liu Bei" not because they look alike, but because they represent **three distinct political forces and strategic directions**. He treats "ally with Wu against Cao" as a single macro-action not because these moves co-occur often, but because **they jointly serve one strategic goal**.

MCTS will never understand what "Cao Cao" stands for, what "ally with Wu against Cao" means, or why "the empire splits in three" is a sensible strategy. It only sees correlations in the data, not the causal structure beneath.

---

## Conclusion: True Intelligence Is Knowing *How* to Think

Back to the original paradox: **why can AlphaGo crush top human Go players, yet fail at open-ended *Longzhong Dui*-style strategy?**

Not because AlphaGo is weak, but because Go and real strategy are two different kinds of problems:

| Dimension | Go | Real-world strategy |
|---|---|---|
| Rules | Clear | Fuzzy |
| Goal | Single | Multi-dimensional |
| Information | Fully observable | Incomplete |
| Feedback | Instant | Delayed |
| Trial-and-error | Repeatable simulations | Not repeatable |

AlphaGo represents one very successful form of intelligence: **statistical intelligence** — surpassing humans inside closed systems via massive compute and statistical methods.

*Longzhong Dui* represents another: **cognitive intelligence** — forming long-horizon strategic judgment in open systems via abstraction, causal reasoning, and meta-decision.

What makes a strong human decision-maker is not infinite compute. It is the ability, under limited information and limited compute, to **build the right abstraction quickly, identify the key variables, characterize the nature of uncertainty, and concentrate reasoning on what matters most**.

> **The ceiling of MCTS is the ceiling of statistical intelligence. True intelligence is not just computing the answer — it is knowing how to think. Until AI masters that, human decision-making remains a ceiling that machines cannot easily break through.**
