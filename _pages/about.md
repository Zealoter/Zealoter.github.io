---
permalink: /
title: ""
excerpt: ""
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

{% if site.google_scholar_stats_use_cdn %}
{% assign gsDataBaseUrl = "https://cdn.jsdelivr.net/gh/" | append: site.repository | append: "@" %}
{% else %}
{% assign gsDataBaseUrl = "https://raw.githubusercontent.com/" | append: site.repository | append: "/" %}
{% endif %}
{% assign url = gsDataBaseUrl | append: "google-scholar-stats/gs_data_shieldsio.json" %}

<span class='anchor' id='about-me'></span>

[//]: # (My name is Ju Qi. I'm from Huazhong University of Science and Technology, and my research areas are game theory and reinforcement learning.)

[//]: # (My research interest includes neural machine translation and computer vision. I have published more than 100 papers at the top international AI conferences with total <a href='https://scholar.google.com/citations?user=DhtAFkwAAAAJ'>google scholar citations <strong><span id='total_cit'>260000+</span></strong></a> &#40;You can also use google scholar badge <a href='https://scholar.google.com/citations?user=DhtAFkwAAAAJ'><img src="https://img.shields.io/endpoint?url={{ url | url_encode }}&logo=Google%20Scholar&labelColor=f6f6f6&color=9cf&style=flat&label=citations"></a>&#41;.)


[//]: # (# 🔥 News)

[//]: # (- *2022.02*: &nbsp;🎉🎉 Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus ornare aliquet ipsum, ac tempus justo dapibus sit amet. )

[//]: # (- *2022.02*: &nbsp;🎉🎉 Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus ornare aliquet ipsum, ac tempus justo dapibus sit amet. )

# 📖 Educations

<div class="logo-row">
  <div class="logo-row__logo"><img src="{{ '/images/logos/hust.png' | relative_url }}" alt="HUST"></div>
  <div class="logo-row__body">
    <h4>Huazhong University of Science and Technology &mdash; Wuhan, China</h4>
    <p><em>Sep. 2019 - Jun. 2026</em>, Ph.D. in Control Science and Engineering, School of Artificial Intelligence and Automation, advised by Prof. Yunfeng Luo.</p>
    <p>Research areas: Large Language Model, Reinforcement Learning, Game Theory.</p>
  </div>
</div>



# 📝 Publications 

1. [Preference-CFR Beyond Nash Equilibrium for Better Game Strategies. (ICML 2025)](https://arxiv.org/abs/2411.01217) Proposes the Preference Counterfactual Regret Minimization (Pref-CFR) algorithm to achieve diverse Nash equilibria, enabling customizable strategies by incorporating preference and vulnerability parameters. Demonstrates distinct play styles in Texas Hold’em without sacrificing strategic strength.
2. [Accelerating Nash Equilibrium Convergence in Monte Carlo Settings Through Counterfactual Value Based Fictitious Play (NeurIPS 2024).](https://arxiv.org/abs/2309.03084) Introduces the Monte Carlo Counterfactual Value-Based Fictitious Play (MCCFVFP) algorithm for large-scale games, achieving 20–50\% faster convergence than standard MCCFR in complex settings like Texas Hold’em.
3. [Real-Time Weighted Fictitious Play: Converging to Equilibrium at the Speed of $O(T^{-1})$ in Games.](https://arxiv.org/abs/2402.12164) Presents the Real-Time Weighted Fictitious Play (RTWFP) algorithm with $O(T^{-1})$ convergence in two-player zero-sum games, extending to correlated equilibrium and continuous-time FP. Outperforms existing algorithms in scalability and speed.
4. [ELO-Rated Sequence Rewards: Advancing Reinforcement Learning Models.](https://arxiv.org/abs/2409.03301) Proposes ELO-Rated Sequence Rewards (ERRL), which uses ordinal preferences and ELO ratings to replace numerical rewards, achieving superior performance in long-term RL tasks like Atari benchmarks.

[//]: # (<div class='paper-box'><div class='paper-box-image'><div><div class="badge">CVPR 2016</div><img src='images/500x300.png' alt="sym" width="100%"></div></div>)

[//]: # (<div class='paper-box-text' markdown="1">)

[//]: # ()
[//]: # ([Deep Residual Learning for Image Recognition]&#40;https://openaccess.thecvf.com/content_cvpr_2016/papers/He_Deep_Residual_Learning_CVPR_2016_paper.pdf&#41;)

[//]: # ()
[//]: # (**Kaiming He**, Xiangyu Zhang, Shaoqing Ren, Jian Sun)

[//]: # ()
[//]: # ([**Project**]&#40;https://scholar.google.com/citations?view_op=view_citation&hl=zh-CN&user=DhtAFkwAAAAJ&citation_for_view=DhtAFkwAAAAJ:ALROH1vI_8AC&#41; <strong><span class='show_paper_citations' data='DhtAFkwAAAAJ:ALROH1vI_8AC'></span></strong>)

[//]: # (- Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus ornare aliquet ipsum, ac tempus justo dapibus sit amet. )

[//]: # (</div>)

[//]: # (</div>)

[//]: # ()
[//]: # (- [Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus ornare aliquet ipsum, ac tempus justo dapibus sit amet]&#40;https://github.com&#41;, A, B, C, **CVPR 2020**)

[//]: # (# 🎖 Honors and Awards)

[//]: # (- *2021.10* Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus ornare aliquet ipsum, ac tempus justo dapibus sit amet. )

[//]: # (- *2021.09* Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus ornare aliquet ipsum, ac tempus justo dapibus sit amet. )



[//]: # (# 💬 Invited Talks)

[//]: # (- *2021.06*, Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus ornare aliquet ipsum, ac tempus justo dapibus sit amet. )

[//]: # (- *2021.03*, Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus ornare aliquet ipsum, ac tempus justo dapibus sit amet.  \| [\[video\]]&#40;https://github.com/&#41;)

# 🧑‍💼 Work Experiences

### ByteDance Seed &mdash; Doubao Post-Training (Jul. 2026 ~ Now)
Working on the post-training of Doubao large language models at ByteDance Seed. Focused on alignment and capability enhancement through supervised fine-tuning, RLHF / RLAIF, and reasoning-oriented reward modeling, with the goal of pushing Doubao's instruction following, reasoning and tool-use abilities further.

# 💻 Internship Experiences

<div class="logo-row">
  <div class="logo-row__logo"><img src="{{ '/images/logos/ByteDance.png' | relative_url }}" alt="ByteDance Seed"></div>
  <div class="logo-row__body">
    <h3>ByteDance Seed &mdash; LLM Post-training Based on Games (Jun. 2025 ~ Oct. 2025)</h3>
    <p><em>Individual Contributor.</em></p>
    <ul>
      <li><strong>Project Goal:</strong> integrate game-theoretic problems into LLM post-training to enhance LLM capabilities.</li>
      <li><strong>Project Results:</strong> delivered game-oriented LLM evaluation &amp; training frameworks; trained an LLM Texas Hold'em AI that outperformed GPT-o3, Grok-4, etc., with improved instruction following.</li>
      <li><strong>Personal Work:</strong> proposed a novel algorithm with an "LLM Reflection" mechanism that outperforms traditional RL methods in game scenarios; built the game-oriented LLM evaluation framework (integrated into the team's system) and a training framework based on Verl.</li>
    </ul>
  </div>
</div>

<div class="logo-row">
  <div class="logo-row__logo"><img src="{{ '/images/logos/Vivo.png' | relative_url }}" alt="vivo"></div>
  <div class="logo-row__body">
    <h3>vivo &mdash; SD Model Fine-Tuning via Reinforcement Learning (Feb. 2025 ~ Apr. 2025)</h3>
    <ul>
      <li><strong>Project Goal:</strong> fine-tune Stable Diffusion with reinforcement learning to improve generation quality and prompt alignment.</li>
      <li><strong>Project Results:</strong> early results show clear improvements in image quality, textual relevance and human preference alignment; ongoing work on reward design and distributed training scale-up.</li>
      <li><strong>Personal Work:</strong> designed a composite reward model combining aesthetics, textual relevance, diversity and human feedback; tuned the RL training pipeline for SD.</li>
    </ul>
  </div>
</div>

### Fen AI Lab &mdash; Texas Hold'em AI (Sep. 2023 ~ Jan. 2024)
*Project member, team of four.*

- **Project Goal:** create an AI that matches the performance of Pluribus, a renowned Texas Hold'em AI.
- **Project Results:** the final AI reached the level of professional players in two-player Texas Hold'em; the multi-player version is still under development.
- **Personal Work:** contributed to key algorithms (MCCFR, MCCFR pruning), built foundational components such as strategy storage and result visualization, and handled algorithm parameter tuning and testing.

<div class="logo-row">
  <div class="logo-row__logo"><img src="{{ '/images/logos/ByteDance.png' | relative_url }}" alt="ByteDance Nuverse"></div>
  <div class="logo-row__body">
    <h3>ByteDance Nuverse &mdash; Reinforcement Learning Internship (Jul. 2021 ~ Mar. 2022)</h3>
    <p><em>Main implementer, team of two.</em></p>
    <ul>
      <li><strong>Project Goal:</strong> design multi-style AI companion NPCs for the game <em>One Piece: Burning Blood</em>.</li>
      <li><strong>Project Results:</strong> added a style evolution module on top of the previous AI training framework, leading to an 80–120% improvement in key indicators and clear style differentiation in play; several AIs reached deployable quality.</li>
      <li><strong>Personal Work:</strong> served as the main executor of the project. Under my advisor's guidance, I implemented the multi-style AI algorithm and explored the integration of human preferences into reinforcement learning, which culminated in a research paper summarizing the findings and potential applications.</li>
    </ul>
  </div>
</div>

### China Resources Group &mdash; Land Auction (Feb. 2021 ~ Jun. 2021)
*Project leader, team of six.*

- **Project Goal:** design a bidding strategy for China Resources Group in the "first/last" land auction.
- **Project Results:** the strategy was approved by China Resources Land Group and deployed in dozens of land auctions (each over $100M). The algorithm outperformed the group's expert approach, boosting bid accuracy 3–4× and winning probability by ~5%, and was adopted as their standard land auction strategy.
- **Personal Work:** built a simulator of the "first/last" land auction from historical data and applied the Fictitious Play algorithm to develop strategies. Participated in three real auctions involving a total bidding scale of $1B, and refined the model based on real-world outcomes.