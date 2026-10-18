---
permalink: /zh/
title: ""
excerpt: ""
author_profile: true
lang: zh
translation_key: home
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
    <p><em>2019 年 9 月 - 2026 年 6 月</em>，控制科学与工程博士，人工智能与自动化学院，师从罗云峰教授。</p>
    <p>研究方向：大语言模型、强化学习、博弈论。</p>
  </div>
</div>



# 🧑‍💼 工作经历

<div class="logo-row">
  <div class="logo-row__logo"><img src="{{ '/images/logos/ByteDance.png' | relative_url }}" alt="字节跳动 Seed"></div>
  <div class="logo-row__body">
    <h3>字节跳动 Seed &mdash; 豆包大模型后训练（2026 年 7 月 ~ 至今）</h3>
    <p>在字节跳动 Seed 团队从事豆包大模型的后训练工作。聚焦于通过 SFT、RLHF / RLAIF 以及面向推理的奖励建模等方法持续提升模型的对齐质量与综合能力，目标是进一步增强豆包在指令跟随、复杂推理与工具使用等方向上的表现。</p>
  </div>
</div>

# 📝 学术论文

1. [Preference-CFR Beyond Nash Equilibrium for Better Game Strategies. (ICML 2025)](https://arxiv.org/abs/2411.01217) 提出偏好反事实遗憾最小化算法（Pref-CFR），通过引入偏好与脆弱性参数实现多样化的纳什均衡求解，可在不损失策略强度的前提下定制不同风格的策略，并在德州扑克中展示了不同的打法风格。
2. [Accelerating Nash Equilibrium Convergence in Monte Carlo Settings Through Counterfactual Value Based Fictitious Play (NeurIPS 2024).](https://arxiv.org/abs/2309.03084) 提出基于反事实值的蒙特卡洛虚拟对弈算法（MCCFVFP），在德州扑克等大规模复杂博弈中相比传统 MCCFR 收敛速度提升 20–50%。
3. [Real-Time Weighted Fictitious Play: Converging to Equilibrium at the Speed of $O(T^{-1})$ in Games.](https://arxiv.org/abs/2402.12164) 提出实时加权虚拟对弈算法（RTWFP），在两人零和博弈中实现 $O(T^{-1})$ 的收敛速度，并扩展到相关均衡及连续时间 FP，在可扩展性与速度上均优于现有算法。
4. [ELO-Rated Sequence Rewards: Advancing Reinforcement Learning Models.](https://arxiv.org/abs/2409.03301) 提出基于 ELO 评级的序列奖励方法（ERRL），使用序数偏好与 ELO 评分替代传统数值奖励，在 Atari 等长程强化学习任务中取得领先性能。



# 💻 实习经历

<div class="logo-row">
  <div class="logo-row__logo"><img src="{{ '/images/logos/ByteDance.png' | relative_url }}" alt="字节跳动 Seed"></div>
  <div class="logo-row__body">
    <h3>字节跳动 Seed &mdash; 基于博弈的大模型后训练（2025 年 6 月 ~ 2025 年 10 月）</h3>
    <ul>
      <li><strong>项目目标：</strong>将博弈论问题引入大语言模型的后训练流程，提升 LLM 能力上限。</li>
      <li><strong>项目成果：</strong>交付了面向博弈场景的 LLM 评估框架与训练框架；训练出的德州扑克 LLM AI 在指令遵循能力提升的同时，整体表现优于 GPT-o3、Grok-4 等模型。</li>
      <li><strong>个人工作：</strong>提出了一种带有 "LLM Reflection" 机制的新算法，在博弈场景中优于传统强化学习方法；搭建了面向博弈的 LLM 评估框架（已集成进团队体系）以及基于 Verl 的训练框架。</li>
    </ul>
  </div>
</div>

<div class="logo-row">
  <div class="logo-row__logo"><img src="{{ '/images/logos/Vivo.png' | relative_url }}" alt="vivo"></div>
  <div class="logo-row__body">
    <h3>vivo &mdash; 基于强化学习的 Stable Diffusion 模型微调（2025 年 2 月 ~ 2025 年 4 月）</h3>
    <ul>
      <li><strong>项目目标：</strong>使用强化学习对 Stable Diffusion 进行微调，提升生成质量与提示词对齐效果。</li>
      <li><strong>项目成果：</strong>初步结果显示生成图像在质量、文本相关性以及与人类偏好的对齐上均有明显提升，正在持续优化奖励设计与扩大分布式训练规模。</li>
      <li><strong>个人工作：</strong>设计了融合美学评分、文本相关性、多样性与人类反馈的复合奖励模型，并调优了 SD 的强化学习训练链路。</li>
    </ul>
  </div>
</div>

### Fen AI &mdash; 德州扑克 AI（2023 年 9 月 ~ 2024 年 1 月）

- **项目目标：**打造一款对标 Pluribus（业内知名德州扑克 AI）水平的 AI。
- **项目成果：**最终 AI 在两人德州扑克中达到了职业玩家水平，多人德州扑克 AI 仍在持续开发中。
- **个人工作：**参与核心算法的研发（如 MCCFR、MCCFR pruning），搭建了策略存储与结果可视化等基础组件，并负责算法的参数调优与测试。

<div class="logo-row">
  <div class="logo-row__logo"><img src="{{ '/images/logos/ByteDance.png' | relative_url }}" alt="字节跳动朝夕光年"></div>
  <div class="logo-row__body">
    <h3>字节跳动朝夕光年 &mdash; 强化学习实习（2021 年 7 月 ~ 2022 年 3 月）</h3>
    <ul>
      <li><strong>项目目标：</strong>为游戏《航海王：燃烧意志》设计多风格 AI 陪玩 NPC。</li>
      <li><strong>项目成果：</strong>在原有 AI 训练框架之上加入风格演化模块，核心指标提升 80–120%，并在玩法风格上形成清晰区分，部分 AI 已达到可上线水平。</li>
      <li><strong>个人工作：</strong>作为该项目的主要执行者，在导师指导下实现了多风格 AI 算法，并探索了人类偏好与强化学习相融合的方法，最终沉淀为一篇总结研究发现与潜在应用的研究论文。</li>
    </ul>
  </div>
</div>

### 华润集团 &mdash; 土地竞拍（2021 年 2 月 ~ 2021 年 6 月）

- **项目目标：**为华润集团设计 "首/末" 类型土地竞拍中的报价策略。
- **项目成果：**该策略获华润置地集团认可，并在数十宗（每宗超 1 亿美元）的土地竞拍中部署。算法表现优于集团专家方案，报价精度提升 3–4 倍，中标概率提升约 5%，最终被采纳为集团标准土地竞拍策略。
- **个人工作：**基于历史竞拍数据搭建 "首/末" 类竞拍仿真环境，使用 Fictitious Play 算法开发竞价策略；亲历 3 次真实竞拍，总报价规模约 10 亿美元，并据此持续打磨模型。

# 📝 最新博客

{% assign zh_posts = site.posts | where_exp: "post", "post.path contains '_posts/CN/'" | sort: 'date' | reverse %}
{% if zh_posts.size > 0 %}
{% for post in zh_posts limit:2 %}
<div class="paper-box" style="margin-bottom: 24px;">
  <h3 style="margin: 0 0 6px 0;"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
  <p class="page__meta" style="margin: 0 0 8px 0;">{{ post.date | date: "%Y 年 %m 月 %d 日" }}</p>
  <div class="archive__item-excerpt">
    {{ post.excerpt | strip_html | truncate: 220 }}
  </div>
</div>
{% endfor %}

<p style="text-align: right;"><a href="{{ '/zh/blog/' | relative_url }}">查看全部博客 →</a></p>
{% else %}
<p>暂无博客内容，敬请期待。</p>
{% endif %}

# 🎮 兴趣爱好

下面这些爱好不只是「玩」：偶尔我也会为它们做点东西。最大的一次「跑偏」，是给一款从高中玩到现在的策略游戏做了中文版。

### 黑冰中文版 · Black ICE Chinese —— 钢铁雄心 3 黑冰 MOD 汉化整合

一个免费、非盈利的玩家项目：把 **Black ICE**（《钢铁雄心 3》体量最大的英文 MOD）和《钢铁雄心3 TFH 402 汉化第三版》整合成一个中文版，目标是「打开就是中文，能从头玩到尾」。

- **为什么做：** 高中、本科、研究生三个阶段我都在玩 HOI3，前后一千多个小时，最喜欢的始终是黑冰：补给是硬的，工业是真要算的，一个装甲军的编制能研究一下午。但我英语撑不住它的阅读量——玩三个小时，两个小时在查词。
- **做了什么：** 原版引擎只认 8 位字形，中文根本显示不出来。项目改了 `hoi3_tfh.exe`：把字形读取从 8 位扩到 16 位（42 处补丁点 + 8 KB 新增代码段），修掉一个必定触发的 `0xC0000005` 崩溃（一句 `mov cl,[edx+eax]` 覆盖了调用者的 `ecx`），并打开 4 GB 地址空间，避免后期大地图内存不足。
- **做到什么程度：** 本地化文本 80,195 / 83,751 条，覆盖率 **95.8%**；将领姓名、部队番号、内阁部长均 **100%**。武器型号和规格故意保留英文——中文玩家本来也读英文。还差少量战区司令部番号和一次完整通关测试。
- **顺带：** 这也是一个可以核对的人机协作样本：用了什么工具、花了多少时间、烧了多少 token，都写在仓库的 `ABOUT.md` 里。

[仓库 →](https://github.com/Zealoter/BlackICE-Chinese)

# 🌱 关于我

性格开朗乐观，喜欢迎接有挑战性的任务。生活中热爱**围棋**、**电子游戏**和**足球**。

- **围棋：**野狐围棋业余 7 段水平。
- **游戏：**长期挚爱《星际争霸 II》，曾经达到**国服（中国）大师段位**。
- **足球：**铁杆**多特蒙德**球迷，最喜欢的球员是**马尔科·罗伊斯（Marco Reus）**。

人生的一个巧合是：我喜欢的几乎所有东西——围棋、星际争霸、足球——都先后成为了 DeepMind 的研究对象。这个巧合也是我深信 AI 力量的原因之一。我的目标是基于大语言模型，通过 **强化学习、博弈论与多智能体系统** 的结合，在研究与产业落地两个维度推进 AGI 的前沿。
