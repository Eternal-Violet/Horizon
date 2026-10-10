---
layout: default
title: "Horizon Summary: 2026-10-10 (ZH)"
date: 2026-10-10
lang: zh
---

> 从 27 条内容中筛选出 6 条重要资讯。

---

**科技新闻**
1. [Cloudflare 收购 Deno，Deno runtime 一年后停更](#item-tech-news-1) ⭐️ 9.0/10
2. [AI 智能体能否进行开放式科学发现？Station 环境研究报告](#item-tech-news-2) ⭐️ 7.0/10
3. [Oxide Computer 完成 4.45 亿美元 D 轮融资](#item-tech-news-3) ⭐️ 6.0/10
4. [Carrier-Explode：开源解码 iPhone 等主流手机运营商设置](#item-tech-news-4) ⭐️ 6.0/10
5. [密码学家 Matthew Green 警告 AI 可能颠覆公钥加密标准](#item-tech-news-5) ⭐️ 6.0/10
6. [Talus: a 23M-parameter diffusion model for game terrain, evaluated against a real-vs-real noise floor, running in the browser on WebGPU \[P\]](#item-tech-news-6) ⭐️ 6.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [Cloudflare 收购 Deno，Deno runtime 一年后停更](https://simonwillison.net/2026/Oct/9/deno-is-joining-cloudflare/) ⭐️ 9.0/10

Cloudflare 正式收购 Deno 项目，计划基于 Deno 团队今年 8 月开源的 celld（Cloudflare Workers 中 Durable Objects 模式的开源实现），把 workerd 自托管打造为使用 Workers 编程模型构建和运行应用的一等支持方式。Cloudflare 承诺将继续维护 Deno runtime 一年，按月发布包含错误修复和安全更新的版本；一年后将停止 Deno runtime 的开发，但代码保持开源，欢迎社区继续接手。Deno 与 Node.js 的创始人 Ryan Dahl 在 Hacker News 上表示这是双方共同决定，他解释 Deno 已被 Node 兼容性的引力井所吞噬、重复实现 Node 意义有限，本人将转向 celld 这类仅依赖对象存储进行协调与持久化的新服务器抽象。

rss · Simon Willison · 10月9日 22:48

**「背景」** Deno 是 Node.js 作者 Ryan Dahl 于 2018 年首次发布、2020 年推出 1.0 版的 JavaScript/TypeScript 运行时，强调安全权限模型与 Web 标准；Cloudflare 则运营着自有的 workerd 运行时来支撑其 Workers 平台，其 Durable Objects 提供了基于对象存储进行有状态协调的能力。2026 年 8 月，Deno 团队开源了 celld，作为 Durable Objects 模式的开源实现,为此次收购所设想的技术整合奠定了基础。

**「影响」** 依赖 Deno runtime 构建应用的开发者拥有约一年的窗口期来规划迁移或评估社区维护分支。Deno 标志性的细粒度权限模型允许精确指定允许访问的文件、目录与网络主机，而 Node.js 自 v22.13.0 起虽已声明权限模型稳定，但目前仅支持网络整体开关、尚不支持按主机粒度放行——迁移到其他运行时可能失去这一沙箱安全特性。

**「社区讨论」** 多位长期用户对 Deno runtime 即将停摆表达惋惜，有评论者认为 Deno 转向 npm 兼容性优先后逐渐背离了 Ryan Dahl 当初从第一性原理重建 Node 的愿景，也有评论将这一事件置于近期一连串开发者工具被大型公司收购或吸纳的趋势中（评论中列举的包括 Cursor 被 SpaceX 收购、Astral/uv 归 OpenAI、Bun 被 Anthropic 收购、Astro.js 与 VoidZero 归入 Cloudflare、NuxtLabs 归 Vercel、Hugging Face 归 NVIDIA 等）。

**标签**: `#acquisition`, `#javascript-runtime`, `#cloudflare`, `#open-source`, `#serverless`

---

<a id="item-tech-news-2"></a>
### [AI 智能体能否进行开放式科学发现？Station 环境研究报告](https://www.reddit.com/r/MachineLearning/comments/1x1lbrm/261008927_can_ai_agents_make_openended_scientific/) ⭐️ 7.0/10

一篇 arXiv 论文（编号 2610.08927）研究了 AI 智能体在 Station 开放世界环境中进行开放式科学发现的能力。研究人员提出两种新机制：Supervisor 机制与周期性的 Meta Reflection，用于在缺乏中间指标时维持探索动力。实验以三篇 ICLR 口头报告论文的研究问题构建任务，在禁用网络访问且不提供论文结果的条件下，让智能体尝试还原论文中的发现，按细分判定标准衡量重新发现率。结果显示 Station 智能体平均重新发现了 62.7% 的判定标准，而 Codex Multiagent-v2 基线仅为 15.4%，AI Scientist-v2 介于 14.4% 至 20.6% 之间。消融与行为分析表明，两种机制共同加入可提升研究覆盖度与连续性。

reddit · r/MachineLearning · /u/progenitor414 · 10月9日 13:26

**「Station 环境与开放式科学发现背景」** Station 是一个开放世界多智能体环境，其中多个智能体共同模拟一个科学发现生态系统，可自主提出假设、执行实验并迭代研究方向。此前，AI 系统在给定明确评价指标的科学发现任务（如材料筛选、蛋白质设计、定理证明）上已取得快速进展，但能否在缺乏预定义指标的开放式研究中自主推进仍不清楚。该论文正是针对这一缺口，通过让智能体接触三篇 ICLR oral 论文的研究问题但隐藏其结果，并以原论文中拆分的独立发现标准作为对照，量化智能体的&quot;再发现率&quot;。

**「影响」** 该论文为 AI 智能体在开放式科学发现任务上的评估提供了一种以已发表论文作为真值的方法论；研究者额外在两个没有对应论文的任务上进行测试，发现智能体做出的部分发现与知识截止日期之后人类研究者报告的结果高度吻合，但论文衡量的是「重新发现」而非全新发现，且结果来自单一环境与三篇特定 ICLR 论文，使用者需注意其适用范围。

**标签**: `#AI agents`, `#scientific discovery`, `#autonomous research`, `#benchmarks`, `#LLM evaluation`

---

<a id="item-tech-news-3"></a>
### [Oxide Computer 完成 4.45 亿美元 D 轮融资](https://oxide.computer/blog/our-445m-series-d) ⭐️ 6.0/10

Oxide Computer 在其官方博客宣布完成 4.45 亿美元的 D 轮融资。该公司专注于提供本地化（on-premises）云计算硬件与软件的一体化方案，此轮融资也是其迄今规模最大的一次。该消息在 Hacker News 上引发广泛关注，但原始博客内容未在本次数据中提供。

hackernews · ahlCVA · 10月9日 13:12 · [社区讨论](https://news.ycombinator.com/item?id=50020014)

**「背景」** Oxide Computer 是一家专注于本地部署\(on-premises\)云硬件与软件集成方案的公司，由 Eclipse Ventures 自公司成立七年来持续支持。本轮 4.45 亿美元 D 轮融资由 Eclipse 领投，规模较此前的 Series C 翻倍以上，SEC Form D 文件已披露相关细节。

**「股权融资选择引发供应链策略疑问」** 评论者 arpinum 对 Oxide 选择 4.45 亿美元股权融资而非贸易融资表示意外，认为尽管公司出于客户订单可能取消的风险厌恶而偏好股权，但引入新股东本身也是另一种形式的风险。该评论者推测 Oxide 此次大额融资可能与锁定 AMD 等供应商超出当前订单积压范围的长期承诺有关。结合 Oxide 此前的 Series C 曾获 2 亿美元用于机架级云计算硬件扩张，本次更大规模的融资延续了其重资产路径，但具体的供应商承诺与资金用途安排仍是公司未公开披露的关键信息，关注 Oxide 硬件供应链稳定性的客户与生态合作伙伴需要留意后续官方披露。

**「社区讨论要点」** Hacker News 用户的讨论主要集中在公司运营层面：一位申请者反馈其招聘流程耗时漫长且数月后才收到拒信；有用户欣赏公司博客中&quot;像交税一样兴奋&quot;的照片说明，认为沟通风格出色；财务方面，有熟悉国际贸易融资的评论者建议公司考虑债务融资而非增发股权，以降低订单流失带来的风险。另有用户希望公司在社交媒体上减少对 AI 卖点的过度强调。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://aiweekly.co/alerts/oxide-computer-discloses-445m-funding-round-in-sec-form-d">Oxide Computer discloses $ 445 M funding round in SEC... | AI Weekly</a></li>
<li><a href="https://oxide.computer/blog/our-445m-series-d">Our $ 445 M Series D | Oxide Computer Company</a></li>
<li><a href="https://trustpost.org/oxide-computer-series-c-funding-data-center-2026/">Oxide Computer Series C: $200M Funds Rack-Scale Cloud ...</a></li>

</ul>
</details>

**标签**: `#funding`, `#infrastructure`, `#hardware`, `#on-premises-cloud`, `#systems`

---

<a id="item-tech-news-4"></a>
### [Carrier-Explode：开源解码 iPhone 等主流手机运营商设置](https://carrierexplode.com/) ⭐️ 6.0/10

开发者 simplyalec 在 Hacker News 上发布了开源工具 Carrier-Explode，持续抓取并解码 iPhone、Google Pixel 和 Samsung Galaxy 等主流机型的运营商配置文件（carrier settings）。该工具附带常见基带配置项的解码器与说明，已在 AT&amp;T iPhone 18 Pro Max&quot;锁机&quot;事件的调查中发挥实际作用，使外界得以确认 AT&amp;T 在该事件中禁用了 5G SA（独立组网）模式，以规避可能导致硬件损坏的 bug。作者承认仍有大量校验工作要做，但工具已被爱好者团体视为填补运营商配置解析空缺的实用项目。

hackernews · simplyalec · 10月9日 18:10 · [社区讨论](https://news.ycombinator.com/item?id=50024499)

**「运营商配置与 AT&amp;T iPhone 18 Pro Max 锁机事件」** 运营商配置（carrier bundle）是运营商向手机推送的配置文件，可在不更新系统固件的前提下控制网络模式、热点权限、5G 选项等终端行为，其内容通常只能以加密形式获得，普通用户和研究者难以解读。近期 AT&amp;T 网络上发生的大规模 iPhone 18 Pro Max 锁机事件，让这类解码工具获得实际用武之地：外部分析显示，AT&amp;T 与苹果通过更新运营商配置禁用了 5G 独立组网（5G Standalone）模式以缓解问题，但双方均未就此发布解释性声明。这一事件既说明了运营商配置对终端行为的实质影响，也是 Carrier-Explode 在爱好者社区中被引用和验证的关键背景。

**「实际影响」** 工具表明运营商可通过 OTA 配置下发在用户不知情的情况下启用或禁用手机功能（如 5G SA、热点共享），对关注设备自主权的用户和移动安全研究者具有直接参考价值；遇到手机功能被运营商限制的用户，可访问 carrierexplode.com 比对自己设备的运营商配置项以核实设置来源。

**「社区讨论」** 有评论指出该工具已被用于追踪 AT&amp;T iPhone 18 Pro Max 锁机事件，并揭示 AT&amp;T 临时禁用 5G SA 模式是为了回避疑似硬件损坏的 bug，但 Apple 与 AT&amp;T 均未公开说明此问题，仅通过更换设备处理。同时多位用户对运营商可单方面通过配置禁用&quot;个人热点&quot;等&quot;反用户&quot;行为表达不满，并提出希望将相关数据回馈至 GNOME 的 mobile-broadband-provider-info 数据库。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://tidbits.com/2026/10/06/iphone-18-pro-max-att-users-update-to-ios-27-0-1-and-new-carrier-settings/">iPhone 18 Pro Max AT &amp; T Users: Update to iOS 27.0.1 and... - TidBITS</a></li>
<li><a href="https://forums.macrumors.com/threads/at-t-and-apple-just-took-steps-toward-fixing-iphone-18-pro-max-issue.2490977/">AT &amp; T and Apple Just Took Steps Toward Fixing iPhone 18 Pro Max ...</a></li>
<li><a href="https://news.ycombinator.com/item?id=50024499">Show HN: Carrier -Explode: iPhone , Pixel and Galaxy carrier settings ...</a></li>

</ul>
</details>

**标签**: `#mobile`, `#reverse-engineering`, `#open-source`, `#baseband`, `#networking`

---

<a id="item-tech-news-5"></a>
### [密码学家 Matthew Green 警告 AI 可能颠覆公钥加密标准](https://simonwillison.net/2026/Oct/9/matthew-green/) ⭐️ 6.0/10

密码学家 Matthew Green 在社交媒体上发文，提出两种尾部风险情景：1% 的概率我们身处&quot;Minicrypt&quot;世界（即公钥加密根本不可能存在的假想情形），以及 15% 的概率我们对现有公钥加密算法功能性地失去信心。他给出的核心论点是，AI 产生密码学&quot;惊喜&quot;的速率与人类——即便借助最好的 AI 协助——替换标准的速率，存在数量级上的差距，因此这类冲击只能靠提前准备来应对。

rss · Simon Willison · 10月9日 15:02

**「背景：Minicrypt 概念」** &quot;Minicrypt&quot; 出自 Russell Impagliazzo 提出的计算复杂性&quot;五世界&quot;假说之一，用于指代公钥加密不可能存在的假想情形。Simon Willison 在转载这条推文时补充了这一术语来源，以帮助读者理解 Green 所说的&quot;最坏情况&quot;所指。

**「对从业者的影响」** 对于依赖公钥加密的系统维护者、协议设计者与标准制定机构而言，Green 的提示暗示算法迁移（如后量子密码学）应在冲击到来之前提前部署与演练，而不是等到某次算法&quot;惊喜&quot;事件发生后再追赶标准更新周期。

**标签**: `#cryptography`, `#AI`, `#security`, `#standards`, `#analysis`

---

<a id="item-tech-news-6"></a>
### [Talus: a 23M-parameter diffusion model for game terrain, evaluated against a real-vs-real noise floor, running in the browser on WebGPU \[P\]](https://www.reddit.com/r/MachineLearning/comments/1x1v71p/talus_a_23mparameter_diffusion_model_for_game/) ⭐️ 6.0/10

A browser-deployable 23M-parameter diffusion model for game terrain heightmaps with property-conditioned generation and a clever &\#x27;real-vs-real&\#x27; noise floor evaluation methodology.

reddit · r/MachineLearning · /u/Old\_Cow\_6636 · 10月9日 19:52

**标签**: `#diffusion-models`, `#generative-ai`, `#procedural-generation`, `#WebGPU`, `#evaluation-methodology`

---