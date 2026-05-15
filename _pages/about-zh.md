---
permalink: /zh/
title: ""
excerpt: ""
author_profile: true
lang: zh
---

{% if site.google_scholar_stats_use_cdn %}
{% assign gsDataBaseUrl = "https://cdn.jsdelivr.net/gh/" | append: site.repository | append: "@" %}
{% else %}
{% assign gsDataBaseUrl = "https://raw.githubusercontent.com/" | append: site.repository | append: "/" %}
{% endif %}
{% assign url = gsDataBaseUrl | append: "google-scholar-stats/gs_data_shieldsio.json" %}

<span class='anchor' id='about-me'></span>

# 📖 教育经历

<div class="logo-row">
  <div class="logo-row__logo"><img src="{{ '/images/logos/hust.png' | relative_url }}" alt="华中科技大学"></div>
  <div class="logo-row__body">
    <h4>华中科技大学 &mdash; 武汉</h4>
    <p><em>2019 年 9 月 - 2025 年 12 月（在读）</em>，控制科学与工程博士，人工智能与自动化学院。</p>
    <p>研究方向：博弈论、强化学习、大语言模型。</p>
  </div>
</div>



# 📝 学术论文

1. [Preference-CFR Beyond Nash Equilibrium for Better Game Strategies. (ICML 2025)](https://arxiv.org/abs/2411.01217) 提出偏好反事实遗憾最小化算法（Pref-CFR），通过引入偏好与脆弱性参数实现多样化的纳什均衡求解，可在不损失策略强度的前提下定制不同风格的策略，并在德州扑克中展示了不同的打法风格。
2. [Accelerating Nash Equilibrium Convergence in Monte Carlo Settings Through Counterfactual Value Based Fictitious Play (NeurIPS 2024).](https://arxiv.org/abs/2309.03084) 提出基于反事实值的蒙特卡洛虚拟对弈算法（MCCFVFP），在德州扑克等大规模复杂博弈中相比传统 MCCFR 收敛速度提升 20–50%。
3. [Real-Time Weighted Fictitious Play: Converging to Equilibrium at the Speed of $O(T^{-1})$ in Games.](https://arxiv.org/abs/2402.12164) 提出实时加权虚拟对弈算法（RTWFP），在两人零和博弈中实现 $O(T^{-1})$ 的收敛速度，并扩展到相关均衡及连续时间 FP，在可扩展性与速度上均优于现有算法。
4. [ELO-Rated Sequence Rewards: Advancing Reinforcement Learning Models.](https://arxiv.org/abs/2409.03301) 提出基于 ELO 评级的序列奖励方法（ERRL），使用序数偏好与 ELO 评分替代传统数值奖励，在 Atari 等长程强化学习任务中取得领先性能。



# 💻 项目经历

### 基于博弈论的大语言模型微调（2025 年 3 月 ~ 至今）
探索使用博弈论方法突破大模型训练中的数据瓶颈，通过自博弈（self-play）生成高质量训练数据，推动大模型微调脱离对静态数据集的依赖。研究方向包括：多智能体自博弈、遗憾最小化、基于均衡的奖励塑形，希望让大模型在不依赖更多人工标注的前提下持续自我进化。

### 字节跳动 Seed &mdash; 游戏 NPC 强化学习项目（2021 年 7 月 ~ 2022 年 3 月）
这是我科研生涯中最具塑造意义的一段工业项目经历。我作为强化学习方向的主要实现者加入字节跳动朝夕光年（后归入字节跳动 Seed），负责为 AAA 项目《航海王：燃烧意志》研发陪玩型 AI NPC，目标是让 NPC 不再是单一最优策略，而是能够以多种近似真人的风格与玩家协同作战。

我在分布式 PPO/IMPALA 训练框架之上，自主设计并实现了**风格演化模块**，将离线人类偏好数据、线上行为统计与奖励分解结合在一起，使我们能够显式权衡进攻、防守、辅助、探索等不同维度的行为偏好。为了在让风格可分辨的同时保持策略强度，我引入了基于种群训练（Population Based Training）的多风格协同训练，配合多样性辅助奖励、跨风格头的 KL 约束以及从脚本机器人到镜像自博弈的渐进课程。我同时重构了数据流水线、评测体系与线上 A/B 工具链，使得这一套方法不仅是研究原型，而是真正可被运营接管上线。

最终上线的陪玩 NPC 在核心战斗指标上较此前规则系统提升 **80–120%**，多个风格变体达到上线水平，整套方法论也被沉淀为团队后续 NPC 项目的内部模板。该工作还合作发表了一篇人机交互方向的论文。这段经历让我系统性地走完了"算法设计—工程落地—产品上线"的完整链路，对我后续做研究的思路影响很深。

### vivo &mdash; 基于强化学习的 Stable Diffusion 模型微调（2025 年 2 月 ~ 2025 年 4 月）
负责使用强化学习对 Stable Diffusion 进行微调，设计了融合美学评分、文本相关性、多样性与人类反馈的奖励模型。初步结果显示生成图像在质量与对齐性上均有显著提升，正持续优化奖励设计与分布式训练规模。

### 分子 AI Lab &mdash; 德州扑克 AI 研发（2023 年 9 月 ~ 2024 年 1 月）
参与构建对标 Pluribus 的扑克 AI 系统。负责实现并调优 MCCFR 及其变种算法、优化计算性能，并开发策略存储与可视化工具，在两人对战中达到职业玩家水平。

### 华润集团 &mdash; 土地竞拍策略优化（2021 年 2 月 ~ 2022 年 6 月）
基于虚拟对弈（Fictitious Play）建模竞争对手策略，开发了用于大额土地竞拍的报价算法。在多次实拍中验证，报价精度提升 3–4 倍，中标概率提升约 5%，该算法后被采用为大额交易的标准工具。
