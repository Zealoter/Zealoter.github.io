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

My name is Ju Qi. I'm from Huazhong University of Science and Technology, and my research areas are game theory and reinforcement learning.

[//]: # (My research interest includes neural machine translation and computer vision. I have published more than 100 papers at the top international AI conferences with total <a href='https://scholar.google.com/citations?user=DhtAFkwAAAAJ'>google scholar citations <strong><span id='total_cit'>260000+</span></strong></a> &#40;You can also use google scholar badge <a href='https://scholar.google.com/citations?user=DhtAFkwAAAAJ'><img src="https://img.shields.io/endpoint?url={{ url | url_encode }}&logo=Google%20Scholar&labelColor=f6f6f6&color=9cf&style=flat&label=citations"></a>&#41;.)


[//]: # (# 🔥 News)

[//]: # (- *2022.02*: &nbsp;🎉🎉 Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus ornare aliquet ipsum, ac tempus justo dapibus sit amet. )

[//]: # (- *2022.02*: &nbsp;🎉🎉 Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus ornare aliquet ipsum, ac tempus justo dapibus sit amet. )

# 📖 Educations
- *Sep. 2019 - Dec. 2025 (now)*, Huazhong University of Science and Technology. Wuhan, China. Ph.D. in Control Science and Engineering.



# 📝 Publications 

1. [Accelerating Nash Equilibrium Convergence in Monte Carlo Settings Through Counterfactual Value Based Fictitious Play (NeurIPS 2024).](https://arxiv.org/abs/2309.03084) Introduces the Monte Carlo Counterfactual Value-Based Fictitious Play (MCCFVFP) algorithm for large-scale games, achieving 20–50\% faster convergence than standard MCCFR in complex settings like Texas Hold’em.
2. [Preference-CFR Beyond Nash Equilibrium for Better Game Strategies.](https://arxiv.org/abs/2411.01217) Proposes the Preference Counterfactual Regret Minimization (Pref-CFR) algorithm to achieve diverse Nash equilibria, enabling customizable strategies by incorporating preference and vulnerability parameters. Demonstrates distinct play styles in Texas Hold’em without sacrificing strategic strength.
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

# 💻 Experiences
### Reinforcement Learning Fine-tuning of Generative Models at Vivo (Feb. 2025 ~ Now)
I have been working on fine-tuning a Stable Diffusion (SD) model using reinforcement learning to enhance its alignment with user preferences for image generation. The project focuses on designing a reward model that evaluates output quality based on aesthetic metrics, textual relevance, and diversity, while integrating human feedback data into the training loop. Current work involves balancing generation creativity with computational efficiency and mitigating reward hacking risks. Though the project remains in its iterative phase without finalized results, the framework has shown preliminary improvements in qualitative evaluations. Development is ongoing to refine reward mechanisms and scale the training process across distributed systems.

### Texas Hold'em AI Development at Fen AI Lab (Sep. 2023 ~ Jan. 2024)
As a project member in a four-person team at Fen AI Lab (Remote) from September 2023 to January 2024, I contributed to developing a Texas Hold'em AI aimed at rivaling the performance of Pluribus, a renowned poker AI. The project focused on implementing key algorithms such as Monte Carlo Counterfactual Regret Minimization (MCCFR) and its pruned variants, alongside building foundational components including strategy storage systems and real-time outcome visualization tools. My responsibilities included algorithm parameter tuning, testing, and optimizing computational efficiency. The resulting AI achieved professional-level performance in two-player scenarios, with ongoing development for multiplayer environments. My work directly supported the AI’s strategic decision-making framework, aligning it with project milestones.
 
### Reinforcement Learning for Game NPCs at ByteDance Nuverse (Jul. 2021 ~ Mar. 2022)
During my role as the main implementer in a two-person team at ByteDance Nuverse from July 2021 to March 2022, I designed multi-style AI companion NPCs for the game One Piece: Burning Blood. This involved enhancing an existing reinforcement learning framework by integrating a style evolution module to diversify AI behavior. I spearheaded the implementation of a multi-style algorithm, incorporating human preference data into the training process to create distinct playstyles. The upgraded framework improved key performance metrics by 80–120%, with certain AI models achieving production-ready quality. My contributions were documented in a research paper exploring human-AI interaction in reinforcement learning, highlighting practical applications for game development.

### Land Auction Strategy Optimization at China Resources Group (Feb. 2021 ~ Jun. 2022)
Leading a six-member team at China Resources Group from February to June 2021, I developed a data-driven bidding strategy for high-stakes "first/last" land auctions. By analyzing historical auction data, I constructed a simulation environment and applied the Fictitious Play algorithm to model competitor behavior and optimize bidding decisions. The strategy was tested in three live auctions totaling $1 billion in bids, with iterative refinements based on real-world outcomes. The finalized model increased bid accuracy by 3–4 times and raised win probability by approximately 5%, generating an estimated $1 million in additional revenue per successful bid. Approved by China Resources Land Group’s review board, the algorithm became their standard tool for land auctions, deployed across dozens of transactions exceeding $100 million each. My hands-on involvement in both simulation design and live auction execution ensured alignment between theoretical models and operational requirements.