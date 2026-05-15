---
title: "From Self-Play to AGI: A Plausible Path and Six Unresolved Fundamental Problems"
date: 2026-05-15
layout: post
author: Ju Qi
lang: en
excerpt: "Self-Play has driven breakthroughs in closed environments, but the leap toward AGI requires far more than scaling. This post outlines six interlocking problems that any self-play system must solve to truly grow like a learner."
---

> **TL;DR.** Self-Play is one plausible road to AGI, but "playing against itself + more compute" is a misreading. The real bottleneck is whether the system can *organize* its own learning. This post unpacks six tightly-coupled problems that define this challenge.

## Abstract

Over the past decade, Self-Play has achieved breakthrough progress in well-defined closed environments such as Go and poker, sparking widespread debate about whether it can become a training paradigm for Artificial General Intelligence (AGI).

This paper argues that while Self-Play may indeed be one of the important paths toward AGI, equating it simply to *"playing against itself"* and expecting AGI to emerge through scaling is a fundamental misunderstanding. The real bottleneck lies not in individual technologies, but in **building a complete system capable of autonomously organizing learning like humans**.

This paper systematically outlines six core problems that must be solved for Self-Play to evolve toward AGI:

1. Automatic task abstraction and decomposition
2. Local feedback acquisition and transfer
3. Autonomous curriculum discovery
4. Cost-effective rollout and fine-grained credit assignment
5. Sustainable experience accumulation
6. Prevention of goal drift and self-deception

These six problems form a tightly coupled dependency chain that collectively defines *"how a system can grow like a genuine learner."*

**Keywords:** Self-Play; Artificial General Intelligence; Autonomous Learning; Curriculum Discovery; Continual Learning; Alignment Problem.

---

## Introduction

Since AlphaGo defeated Lee Sedol in 2016, Self-Play has emerged as one of the most remarkable technologies in artificial intelligence. From Go to Mahjong, from StarCraft to Texas Hold'em, system after system has reached or even surpassed top human levels by continuously playing against itself in closed environments. These astonishing achievements naturally raise a fundamental question:

> Given how powerful Self-Play is in these tasks, can it be further extended to become a training paradigm for more general intelligence?

Two extreme views have formed in academia and industry. One argues that Self-Play only works in *"toy worlds"* and is too far removed from the complex, dynamic real world. The other claims that with sufficient computing power and larger models, Self-Play will naturally extend to all tasks. **This paper argues that neither view is accurate.**

The true power of Self-Play lies not in *"playing chess against oneself,"* but in providing a mechanism that can continuously generate training signals and improve itself without relying entirely on human annotation. However, the leap from superhuman performance on single tasks to general intelligence requires not an order-of-magnitude increase in computing power, but a *fundamental transformation in how training is organized*. The world that AGI faces is not a single game, but a mixture of thousands of tasks, goals, and scenarios with no unified rules or final scores.

Therefore, if Self-Play is to truly lead toward AGI, it must evolve from a **single-environment optimizer** into a **multi-task, self-organizing, and sustainably accumulating learning system**. This paper systematically elaborates on the six core problems that must be addressed during this evolution, analyzes their interdependencies, and explores their deeper implications for the nature of intelligence.

---

## 1. The Essence of the Problem: From "Can We Self-Play?" to "Can We Organize Learning?"

When people talk about Self-Play, they often envision a traditional picture: given a well-defined task, define win/loss rules, let the model play against itself repeatedly, and update parameters based on final outcomes. **But if our goal is AGI, this imagination is far too narrow.**

Complex tasks in the real world often lack both clear final rewards and unique correct answers. More importantly, humans do not learn by *"end-to-end consumption of final results."* Human learning more closely resembles this iterative cycle:

1. When facing a complex problem, first grasp the **main contradictions** while ignoring trivial details.
2. Decompose complex goals into a small number of **key subproblems**.
3. Determine which capabilities need improvement most urgently and establish **learning priorities**.
4. Obtain feedback and correct errors through **local practice**.
5. Finally **integrate** these local capabilities into a complete problem-solving ability.

This means that what truly deserves research is not "whether the model can play many games against itself," but: *whether the model can autonomously discover problems, organize curricula, correct errors locally, accumulate knowledge over time, and avoid drifting off course in the process.*

Without these capabilities, so-called Self-Play is at best repetitive training that fails to produce genuine capability growth. With them, it may gradually approximate a more general learning mechanism.

---

## 2. Six Core Problems for Self-Play Toward AGI

Below, we formalize the above framework into six core problems. In our view, these constitute the real bottlenecks on the path to AGI via Self-Play, and **none have been thoroughly resolved**.

### 2.1 Automatic Task Abstraction and Decomposition

> *Can we stably grasp core contradictions?*

The first problem is not "can we decompose tasks," but: **can the model extract the core contradictions from complex problems rather than getting bogged down in trivial details?**

Task decomposition sounds like a natural process, but without the constraint of *"prioritizing the critical over the trivial,"* models easily fall into two extremes: either over-decomposing into a vast number of low-value checklists, or missing the point entirely and wasting enormous computing power on irrelevant local optimizations. This is precisely a common flaw in many current large language models: they appear diligent, listing numerous items and producing extensive analyses, yet fail to accurately identify the truly important key contradictions, and even *"go down rabbit holes"* on secondary issues.

A good Self-Play system must first possess the ability to **compress complex tasks into a small number of the most critical, worth-learning subproblems** rather than mechanically chopping large problems into pieces. The emphasis here is not on "how complete the decomposition is," but on **"how accurate the abstraction is."** If this first step fails, all subsequent local feedback, training scheduling, and long-term accumulation will be built on a flawed foundation.

### 2.2 Local Feedback Acquisition

> *Can we form clear, transferable intermediate evaluations?*

Once key subproblems have been abstracted, can the system obtain stable, dense feedback on these subproblems?

Traditional Self-Play typically relies on terminal rewards: win or lose, correct or incorrect. But in the complex tasks that AGI faces, final outcomes are often ambiguous, sparse, and delayed, making direct end-to-end learning ineffective. Therefore, the key is no longer to design a perfect validator for every large task, but to enable the model to obtain feedback **at the level of key subproblems**.

For example:

- When **creating a presentation**, feedback should focus not just on whether the final result is "good," but on whether the content organization is clearer, the hierarchy is more distinct, and the key points are more prominent.
- When **writing an article**, feedback should address whether the argument is focused, the reasoning is coherent, and the structure is logical.

These evaluations may not be entirely objective, but they are **closer, denser, and more conducive to attribution than terminal rewards**.

An important insight here is that we should not place the entire burden of *"designing cross-domain transferable evaluators"* on human manual engineering. Instead, we should have confidence in the generalization capabilities of large models. Once tasks are abstracted into sufficiently simple, critical, and structurally clear subproblems, many local feedback mechanisms naturally become sharable across tasks. In other words, **transfer is more likely to result from "correctly abstracting the problem" than from pre-designing all transfer rules for the model.**

### 2.3 Autonomous Curriculum Discovery

> *Can we arrange reasonable learning sequences and priorities?*

Given thousands of tasks, can the system autonomously discover an appropriate learning order?

When discussing Self-Play, many people assume tasks are already given and training is just a matter of continuous sampling and playing. But the real challenge lies in: given 10,000 tasks—

- Which one should be learned first?
- Which tasks are most worth investing computing power in right now?
- Which are foundational capabilities that should be prioritized?
- Which tasks, while appearing difficult, would be a waste of time to practice at the current stage?
- Which tasks have already been sufficiently mastered and require no further rollouts?

This is not a simple sampling problem, but a **curriculum discovery problem**. A truly powerful Self-Play system must not only be able to learn, but also be able to plan how to learn. It must possess some form of *"learning scheduling intelligence"*: determining the most important training directions under limited budgets, and automatically establishing sequences and priorities.

Without this layer, so-called multi-task Self-Play easily degenerates into brute-force uniform drilling: practicing each task a little, but never forming a genuine path of capability growth. The effectiveness of human learning, to a large extent, stems precisely from the fact that we do not distribute our energy evenly, but continuously adjust our focus.

### 2.4 Large-Scale Rollout and Fine-Grained Credit Assignment

> *Can we learn effectively at affordable cost?*

Even if the above three conditions are met, can the training system actually execute these learning processes at an affordable cost?

A practical bottleneck of Self-Play is its **extremely high rollout cost**. Long trajectories, multi-round reasoning, reflection and revision, tool use, and branching attempts all rapidly drive up sampling costs. Moreover, rewards in complex tasks are localized and delayed, which raises another problem: even after generating trajectories, can the system accurately determine which steps led to improvements and which caused failures?

Two problems are inextricably linked here:

1. Whether **large-scale rollout** can be done cheaply.
2. Whether **credit** can be finely assigned back to critical steps and decisions.

If rollout is too expensive, the system cannot evolve sustainably. If credit assignment is too coarse, the system may appear to be training but will not learn anything genuinely useful. This layer determines whether the high-level learning organization described earlier can be translated into executable training processes.

### 2.5 Sustainable Experience Accumulation

> *Can we absorb new knowledge without catastrophic forgetting?*

Can the model learn new things without erasing old capabilities?

This is actually a classic challenge faced by all continual learning systems. If Self-Play is to be a long-term path toward AGI, it cannot be a matter of *"knowing it this round, forgetting it the next."* Otherwise, the system may appear to be training continuously, but in reality is just constantly rewriting its cache with no genuine accumulation of capability.

A system capable of long-term Self-Play must possess some **stable mechanism for experience consolidation**. It must be able to integrate newly learned strategies, abstractions, and techniques into its existing capability structure rather than constantly overwriting local regions. Otherwise, as multi-task learning progresses, interference between tasks will become increasingly severe, and the system may fall into a vicious cycle of *"forgetting earlier skills as it learns new ones."* This also demonstrates that the key to AGI is not just larger model capacity, but **stronger long-term memory and continual learning mechanisms**.

### 2.6 Goal Alignment

> *Can we prevent goal drift and self-deception in long-term Self-Play?*

Can the system avoid gradually drifting away from the goals humans actually care about during long-term self-play?

This is a **highly dangerous yet easily overlooked** issue. A system that can stably decompose tasks, obtain local feedback, arrange curricula, rollout cheaply, and remember continuously may still learn the wrong things. It may learn to please its local evaluators, exploit loopholes in task decomposition, and game seemingly reasonable metrics, ultimately forming a stable but incorrect self-reinforcing loop.

Therefore, "not forgetting" is insufficient; the system must also "not drift off course." What it remembers must not only be extensive but also **correct**. The goals it optimizes must not only be stable but also **genuinely aligned with the capability improvements humans desire**. This is the fundamental problem that all long-term Self-Play approaches must confront. Otherwise, *the better the system becomes at learning, the better it may become at deceiving itself.*

---

## 3. The Chain Dependency of the Six Problems

It is crucial to emphasize that these six problems are **not a loose checklist**. They exhibit clear chain dependencies, forming a complete closed loop of a learning system:

| Stage | Role | Question |
|---|---|---|
| 1. Starting Point | Abstraction | Grasp core contradictions and abstract key problems |
| 2. Foundation | Feedback | Establish effective local feedback mechanisms |
| 3. Scheduling | Curriculum | Decide what to learn first / where to practice more |
| 4. Execution | Training System | Translate decisions into scalable rollouts and updates |
| 5. Accumulation | Memory | Stably integrate new capabilities into existing knowledge |
| 6. Alignment | Direction | Ensure the process does not deviate from human goals |

From this perspective, **Self-Play toward AGI is never as simple as "playing more games."** It is a complete learning systems engineering problem. The absence of any single link will render the entire system ineffective.

---

## 4. Why These Problems Remain Unresolved

Some may ask: these problems sound so natural, why haven't they been truly solved yet? The answer is that each is not merely an engineering challenge, but **touches on deeper questions about the nature of intelligence itself**.

- The problem of **task abstraction** touches on the cognitive core of *"what constitutes a key contradiction."*
- The problem of **local feedback** touches on *"what kinds of intermediate progress are learnable."*
- The problem of **curriculum discovery** touches on *"what order capability growth should follow."*
- The problem of **rollout and credit assignment** touches on *"how to learn efficiently in long-horizon decision-making."*
- The problem of **continual memory** touches on *"how knowledge consolidates into stable structures."*
- The problem of **goal drift** touches on *"how systems can remain aligned with human goals during long-term self-optimization."*

In other words, these are not scattered training tricks, but collectively define at different levels *"how a system can grow like a genuine learner."* Solving them will require not only engineering breakthroughs but also a deeper understanding of intelligence itself.

---

## Conclusion

This paper does not claim that Self-Play is inherently equivalent to AGI, nor that simply scaling today's self-opposition by ten or a hundred times will naturally lead to AGI. However, we do believe that if we seriously ask *"how a system can continuously improve itself with minimal human supervision,"* Self-Play forces us to confront a set of the most fundamental questions:

- How does it discover **what is worth learning**?
- How does it **focus on what matters**?
- How does it obtain **local feedback**?
- How does it arrange its **learning sequence**?
- How does it train **cost-effectively**?
- How does it **accumulate** knowledge over time?
- How does it **avoid learning the wrong things** in the process?

If these problems are truly solved, Self-Play will likely no longer be just a training technique for specific games, but will evolve into a learning mechanism much closer to general intelligence.

Conversely, if these problems remain unsolved, no matter how large the models or how powerful the computing power, Self-Play will ultimately achieve only local successes and fail to truly advance toward AGI.

> **The key to AGI may not lie in making models play against themselves more frequently, but in teaching them how to be genuine learners: discovering priorities, organizing their own training, accumulating experience, and continuously correcting themselves.**
