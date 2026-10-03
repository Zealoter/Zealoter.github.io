---
title: "If We Ask a Team of AIs to Prove Mathematical Theorems, What Kind of ‘Company’ Should We Build?"
date: 2026-08-25
layout: post
author: Ju Qi
lang: en
translation_key: ai-mathematical-proof-organization
excerpt: "When many AI agents work together on a mathematical problem, generating ideas is no longer the only scarce capability: organization, verification, communication, and human oversight become essential. This article sketches an AI mathematics institute built around claims, proofs, counterexamples, and review."
---

(This article grew out of my recent reading about AI tackling mathematical proofs. I had previously thought that the next step for agents might require improvement through self-play. Now, however, it seems possible that we could skip that step and organize agents directly using human management principles and company structures. This article emerged from my discussions with Codex.)

Suppose you have 16, 128, or even several thousand highly capable AI agents, tasked with solving an important mathematical problem.

The most natural approach might be to let every agent attempt a proof independently, collect their answers, and select the one that looks best.

But this approach is unlikely to deliver 16 or 128 times the intelligence. It is more likely to produce many duplicate conjectures, reasoning contaminated by other agents' ideas, untraceable chat logs, and a proof that every agent considers correct even though it conceals the same shared flaw.

As the number of agents grows, what becomes scarce is no longer the ability to generate yet another idea, but the ability to answer these questions:

- How do we break an unsolved problem into intermediate problems that can be investigated?
- How do we preserve the independence of different research directions?
- How do we determine whether an intermediate result actually holds?
- How do we prevent incorrect results from contaminating the entire system?
- How do we combine scattered correct results into a complete proof?
- When should humans intervene?

At this point, the problem extends beyond multi-agent reasoning and begins to resemble organizational design.

What we need to build is not a giant group chat, but an AI company dedicated to producing mathematical knowledge—or, more precisely, an **organizational system for AI mathematical proof**.

## 1. The Product Is Not an Answer, but a Verifiable Mathematical Object

The basic objects in ordinary office software are messages, documents, tasks, and meetings. In an AI mathematical proof system, the basic objects should instead be:

- Claims
- Proofs
- Counterexamples
- Proof obligations
- Dependencies
- Reviews
- Research decisions

For example, an agent cannot simply report:

> I have found that sparsification may preserve a certain parity structure in END-OF-LINE. This direction seems promising.

It must submit an object that other agents can challenge:

```text
Claim ID: CLAIM-0042
Precise statement: Transformation S preserves endpoint parity under conditions A and B
Definitions used: DEF-0011, DEF-0018
Lemma dependencies: CLAIM-0027
Current proof: PROOF-0042-v2
Unresolved issue: The bit-complexity bound in Step 7
Suggested challenge: Construct a minimal counterexample involving a non-injective mapping
```

This rule may look like a formatting requirement, but it changes the nature of the entire organization.

Agents no longer collaborate by deciding whose argument sounds more convincing. They collaborate through mathematical objects that can be traced, challenged, reproduced, and combined.

Chat is part of the work process; claims are organizational assets.

## 2. A 16-Agent Mathematics Institute

There is no need to begin with 128 agents. A more reasonable starting point is a minimal institute of 16 agents, used to test whether the organizational system itself works.

The division of labor could look like this:

| Role | Number of agents | Responsibilities |
| --- | ---: | --- |
| Independent researchers | 8 | Pursue four research directions and propose conjectures and proofs |
| Adversarial reviewers | 4 | Find counterexamples, check missing steps, and independently reproduce results without seeing the original reasoning |
| Formalization researcher | 1 | Encode key definitions and lemmas in systems such as Lean or Coq |
| Scientific editor | 1 | Maintain consistent notation, proof structure, and research drafts |
| Scheduling agent | 1 | Allocate tasks, reassign agents from stalled directions, and resolve shared blockers |
| Knowledge curator | 1 | Maintain the literature, claim graph, and relationships between versions |

The scheduling agent is the only administrator in the strict sense. The knowledge curator and scientific editor must also understand mathematics; proposing new theorems is simply not their primary objective.

The eight researchers can come from different model families. Some may excel at long contexts and overall structure, some may suit inexpensive parallel exploration, and others may be stronger at formalization code. Model diversity is part of scientific reliability, not merely a procurement strategy.

If all agents come from the same model, they are likely to share knowledge gaps, reasoning habits, and reward preferences. Ten highly correlated judgments do not amount to ten independent pieces of evidence.

## 3. An Organization Combining a University, a Market, and a Court

This organization cannot operate solely like a company or solely like a school. It is closer to a combination of three institutions.

### 1. The University: Protect Diverse Exploration

At the beginning of a project, several teams investigate the same problem independently. They can access shared definitions and published literature, but cannot yet see other teams' conjectures.

This prevents all agents from converging prematurely on the first seemingly plausible direction.

The system could even deliberately establish different schools of thought:

- One team studies only combinatorial structures.
- One team starts from topology and fixed points.
- One team studies circuit, query, or proof complexity.
- One team focuses on designing algorithms that challenge the intuition that the problem must be hard.

The algorithm team is especially important. An organization aiming to prove lower bounds can easily interpret every experimental observation as evidence of hardness if nobody seriously searches for algorithms.

### 2. The Market: Allocate Resources According to Evidence

Agents do not belong permanently to a research direction. They receive a time-limited allocation.

At the end of a research cycle, each direction is assigned a status based on its outputs:

- Green: It has produced new, independently verified lemmas and continues to receive resources.
- Yellow: It has made progress, but unverified assumptions are accumulating; expansion stops while the work undergoes adversarial review.
- Gray: It has produced no checkable output for several consecutive cycles and is temporarily frozen.
- Red: A counterexample has refuted a core claim, and downstream use must stop immediately.

Resources must be allocated according to evidence, not an agent's confidence.

An agent that writes polished reports should not receive more resources than one that finds a crucial counterexample but describes it plainly.

### 3. The Court: The Proposer of a Proof Cannot Also Be Its Judge

Every important result must pass three independent procedures:

1. Adversarial review: specifically search for counterexamples, quantifier errors, and hidden assumptions.
2. Blind reconstruction: prove the formal statement from scratch without reading the original chat.
3. Formal checking: submit the most important definitions and derivations to a proof assistant.

Majority voting is not appropriate here.

Twelve agents agreeing that a proof is correct cannot make an incorrect step correct. A mathematical organization ultimately relies on reconstructible chains of proof, not consensus.

## 4. Twelve Basic Rules for an AI Mathematical Proof System

If I were writing a charter for this institute, I would start with the following twelve rules.

### Rule 1: Claims Take Priority over Chat

Any result worth relying on across teams must become a versioned claim. Chat logs cannot serve as mathematical justification.

### Rule 2: Proposers Cannot Approve Their Own Results

A research agent may submit a proof, but it cannot mark the result as established.

### Rule 3: Consensus Is Not Proof

The number of agents, a model's reputation, and confidence scores cannot replace step-by-step verification.

### Rule 4: Independent Thinking Comes Before Communication

For important problems, agents using different models or different contexts should make independent attempts before exchanging results. Communicating too early undermines cognitive diversity.

### Rule 5: Failed Results Are Also Organizational Assets

Counterexamples, failed reductions, unsuccessful methods, and known barriers must be preserved. Later agents should be able to look up why a direction failed last time.

### Rule 6: Invalidations Must Propagate Downstream Automatically

When a claim is refuted, every proof depending on it must automatically be marked for review. Those proofs must not continue circulating with their previous status.

### Rule 7: Every Direction Has a Time Limit and Exit Conditions

There is no indefinite instruction to continue investigating. A research direction must specify its next falsifiable target in advance, along with the outcome that would justify stopping.

### Rule 8: Proof Debt Must Be Visible

The system continuously tracks unverified lemmas, hidden assumptions, failed reproductions, and circular dependencies. A longer proof is not necessarily closer to completion; it may simply have accumulated more debt.

### Rule 9: Different Models Play Different Epistemic Roles

A model good at generating ideas may not be a good reviewer; a model good at sustained writing may not be good at finding minimal counterexamples. Roles should be adjusted dynamically based on internal testing, not fixed permanently according to vendors' claims.

### Rule 10: Humans Supervise Exceptions, Not Every Step

Routine task allocation, claim creation, and independent review can run automatically. Changing the overarching goal, substantially increasing the budget, declaring the main theorem established, and publishing externally require human approval.

### Rule 11: Every Important Operation Must Be Replayable

Who changed a statement and when, which lemma was refuted, and which direction was suspended must all be recorded in an event log that cannot be overwritten.

### Rule 12: The Paper Is Not the Source of Truth

A paper is a narrative organization of verified claims. A writing agent must not quietly alter mathematical statements to make the prose flow better.

## 5. How Should Agents Communicate?

Unrestricted conversations among 16 agents might still be manageable. At 128 agents, communication relationships can quickly spiral out of control.

Cross-team communication should therefore be organized around objects, not group chats.

```text
A discussion about CLAIM-0042
An intermediate research request associated with NEED-0017
A proof dispute associated with REVIEW-0021
A work handoff associated with TASK-0108
```

Each agent subscribes only to:

- The claims it is currently investigating
- Its direct upstream dependencies
- Its direct downstream users
- A small number of research topics adjacent to its own direction

The system also needs to detect problematic communication patterns automatically:

- Has one agent become a bottleneck for all information?
- Has a group of agents formed a closed circle that validates only its own members' work?
- Does all verification come from the same model family?
- Are large numbers of tokens being spent explaining the same claim repeatedly?
- Is any team still citing an obsolete version that has already been invalidated?

Ideally, humans see a live proof-dependency graph and a list of exceptions, rather than tens of thousands of messages.

## 6. Where Do New Intermediate Problems Get Their Researchers?

Mathematical research cannot be fully decomposed into tasks at the outset. The most important intermediate lemmas often emerge during the research itself.

Any agent may submit an intermediate research request, but it must clearly state:

```text
What needs to be proved or refuted?
Which main claim does it block?
Which verified results does it depend on?
What output would count as completion?
If the attempt fails, what would that rule out?
```

The scheduling system first sends a small, flexible team to conduct a brief preliminary investigation. If the request blocks several research directions supported by strong evidence, agents are reassigned from stalled directions to form a temporary project.

Once the intermediate problem is resolved, the temporary project is dissolved immediately. It must not keep finding new reasons to exist merely because a team has already been formed.

This is exactly the same as a common problem in real companies: organizations can gradually shift from existing to carry out tasks to inventing tasks to sustain themselves. AI organizations must also guard against departments perpetuating themselves.

## 7. What Is the Human Role?

Humans should not read every agent's reasoning every day or approve every task allocation. Otherwise, they become the slowest component in the entire system.

Humans are better suited to four responsibilities:

1. Define the overarching research objective and boundaries that must not be crossed.
2. Decide budgets, model providers, and major resource adjustments.
3. Resolve epistemic disputes that two independent verification systems cannot settle.
4. Approve the announcement of the main theorem and its external publication.

The human dashboard needs to emphasize only items such as:

```text
A core claim may have a counterexample
Two model families have reached opposing review conclusions
The cost of one research direction is growing abnormally
Many downstream results depend on an unverified lemma
A candidate theorem has passed two independent reconstructions
```

The human is not an inspector on an assembly line, but the institute's director, institutional designer, and final publisher.

## 8. How Do We Measure Whether This AI Company Is Making Progress?

We should not use metrics such as:

- How many tokens were generated
- How many tasks were created
- How many agent meetings were held
- How many conjectures were proposed
- How many agents agreed

More meaningful metrics include:

- The number of independently verified claims produced per unit of cost
- The success rate of independent reproduction for key claims
- The average time from proposing a claim to discovering a counterexample
- Whether proof debt is increasing or decreasing
- The proportion of total resources spent on duplicate research
- The rate of effective cross-review between different model families
- How much reusable information failed directions leave behind

For a genuinely difficult mathematical problem, a month without a complete proof does not mean the organization has failed. But if a month produces only a mass of conversation, with no verifiable lemmas, counterexamples, or map of barriers, then the organization has failed.

## 9. How Would This System Work in the Case of PPAD?

Strictly speaking, PPAD is a complexity class, not a proposition that can be directly proved. We could make the overarching objective more specific by studying the relationship between FP and PPAD, or by proving that a new problem is PPAD-complete.

The system first divides the objective into several independent research programs:

- The graph structure and circuit representation of END-OF-LINE
- Approaches based on Brouwer, Sperner, and combinatorial topology
- Lower bounds in query, circuit, and proof complexity
- New reductions and new complete problems
- Polynomial-time algorithms for special structures

Suppose the topology team proposes a claim: a certain discretization preserves the parity structure of endpoints.

The system does not immediately insert it into the main proof. Instead, the following sequence takes place:

```text
The topology team submits a claim
→ The counterexample team searches for a minimal failing instance
→ Another model reconstructs the proof without seeing the original reasoning
→ The formalization agent makes the definitions and quantifiers precise
→ Once verified, the claim enters the shared claim graph
→ Only then may downstream reduction teams use it
```

If a counterexample is discovered later, the system automatically flags all downstream proofs and recommends resource reallocations. Humans can see which directions the failure affects and whether it leaves any weaker versions that still hold.

That is a mathematical research system, rather than a group of agents taking turns generating answers.

## 10. What May Matter Most Is the Study of Machine Organizations

We are accustomed to understanding AI capability in terms of individual models: how many questions they can answer correctly, how much code they can write, and how complex a task they can complete.

But once we can call on many models at low cost, system capability increasingly depends on something else:

> How are these intelligences organized?

The same model, placed in different institutional structures, may produce entirely different outcomes.

An organization that rewards only producing proofs as quickly as possible will mass-produce elegant-looking but incorrect proofs. An organization that requires independent challenges, preserves failures, and tracks dependencies may move more slowly, but it may actually accumulate knowledge.

Competition in AI research may therefore involve more than who has the strongest model. It may also depend on:

- Who has better procedures for decomposing research tasks
- Who has more reliable mechanisms for review across models
- Who can turn failed results into lasting assets
- Who can focus human attention on the most important disputes
- Who can compress thousands of local reasoning steps into a trustworthy chain of knowledge

Sixty smart agents do not automatically form a smarter whole, just as sixty mathematicians do not automatically form a first-rate research institute.

Models provide intelligence; organizations determine whether that intelligence ultimately produces noise or knowledge.
