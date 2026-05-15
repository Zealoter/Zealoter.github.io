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
- *Sep. 2019 - Dec. 2025 (now)*, Huazhong University of Science and Technology. Wuhan, China. Ph.D. in Control Science and Engineering.



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

# 💻 Experiences

### Fine-tuning LLM via Game Theory (Mar. 2025 ~ Now)
Exploring game-theoretic approaches to overcome data bottlenecks in LLM training. By enabling self-play to generate high-quality data, we aim to advance LLM fine-tuning beyond reliance on static datasets.


### SD Model Fine-Tuning via Reinforcement Learning at Vivo (Feb. 2025 ~ Apr. 2025)
Worked on fine-tuning Stable Diffusion with reinforcement learning. Designed a reward model combining aesthetics, textual relevance, diversity, and human feedback. Early results show improved image quality and alignment, with ongoing efforts to refine reward design and scale distributed training.

### Texas Hold'em AI Development at Fen AI Lab (Sep. 2023 ~ Jan. 2024)
Contributed to building a poker AI rivaling Pluribus. Implemented and tuned MCCFR and its variants, optimized computation, and developed strategy storage and visualization tools. Helped achieve professional-level play in 2-player games.
 
### Reinforcement Learning for Game NPCs at ByteDance Nuverse (Jul. 2021 ~ Mar. 2022)
During my role as the main implementer at ByteDance Nuverse from July 2021 to March 2022, I designed multi-style AI companion NPCs for the game One Piece: Burning Blood. Enhanced RL framework with a style evolution module, integrating human preference data to create diverse playstyles. Improved key performance metrics by 80–120%, with some models production-ready. Co-authored a paper on human–AI interaction.


### Land Auction Strategy Optimization at China Resources Group (Feb. 2021 ~ Jun. 2022)
Developed a bidding algorithm for high-stakes land auctions by applying Fictitious Play to model competitor strategies and optimize bids. Validated in multiple live auctions, the method improved bid accuracy by 3–4× and increased win probability by ~5%. The algorithm was subsequently adopted as the standard tool for large-scale transactions.