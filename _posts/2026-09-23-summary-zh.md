---
layout: default
title: "Horizon Summary: 2026-09-23 (ZH)"
date: 2026-09-23
lang: zh
---

> 从 30 条内容中筛选出 11 条重要资讯。

---

**科技新闻**
1. [Anthropic 发布 Claude Opus 5.5，大幅下调各类型 token 价格](#item-tech-news-1) ⭐️ 9.0/10
2. [WordPress 7.1.2 修复路径遍历漏洞，可致条件性远程代码执行](#item-tech-news-2) ⭐️ 8.0/10
3. [Pentagon says overreliance on AI contributed to missile strike on Iran school](#item-tech-news-3) ⭐️ 8.0/10
4. [Claude Opus 5.5 与 GPT-6 Sol/Luna 同日发布，价格战升级](#item-tech-news-4) ⭐️ 8.0/10
5. [Claude Code v2.1.280 引入 Claude Opus 5.5](#item-tech-news-5) ⭐️ 7.0/10
6. [&\#x27;We hacked the FBI:&\#x27; Hackers say they have data on all FBI employees](#item-tech-news-6) ⭐️ 7.0/10
7. [Trail of Bits 发布 SAML 深度技术批判,指出其 XML 级设计缺陷](#item-tech-news-7) ⭐️ 7.0/10
8. [Artificial Analysis 发布 Claude Opus 5.5 多档推理基准与成本对比](#item-tech-news-8) ⭐️ 7.0/10
9. [GPT-6 改进提示缓存机制以降低延迟与成本](#item-tech-news-9) ⭐️ 7.0/10
10. [Complex KDA：理解并增强 Kimi Delta Attention 的表达能力](#item-tech-news-10) ⭐️ 7.0/10
11. [AI 协助破解一封 2005 年以来未解的 Enigma 历史电报](#item-tech-news-11) ⭐️ 6.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [Anthropic 发布 Claude Opus 5.5，大幅下调各类型 token 价格](https://www.anthropic.com/claude-opus-5-5) ⭐️ 9.0/10

Anthropic 于 2026 年 9 月 22 日发布 Claude Opus 5.5，作为此前商业表现领先的 Opus 5 的继任者。新版本对四类 token 价格进行了显著下调：缓存读取从每百万 tokens $0.50 降至 $0.20（降幅约 60%），输入 token 从 $5 降至 $4，输出 token 从 $25 降至 $20，缓存写入从 $6.25 降至 $5。此外，Anthropic 强调 Opus 5.5 在沟通风格上更为自然，重要信息前置，便于在长会话中作为协作伙伴使用。这是 Anthropic 在上周提出&quot;pacing the frontier&quot;（放缓前沿节奏）表态后的首个模型发布。

hackernews · km144 · 9月22日 16:29 · [社区讨论](https://news.ycombinator.com/item?id=49803892)

**「背景」** Claude Opus 5 是 Anthropic 此前最高规格的商用模型系列，评论引用 OpenRouter 排行榜数据指出，Opus 5 是该平台上按支出计排名最高的模型，并可能是当时全球支出最大的大语言模型，这为 Opus 5.5 的定价与定位提供了商业基线。在本次发布前不久，Anthropic 曾公开呼吁行业&quot;pacing the frontier&quot;，因此 5.5 的发布节奏与定价策略被外界与其表态对照审视。

**「影响」** 对依赖 Opus 系列处理高 token 消耗工作负载（如长上下文检索与缓存写入密集的 Agent 流程）的开发者而言，缓存读取费用下降约 60% 直接降低大批量调用成本；按当前差价估算，同样调用量的 token 支出可降至原先的 40%–80%，但具体节省幅度取决于调用中各类 token 的占比。

**「社区讨论」** 评论区出现明显分歧：部分用户对降价表示欢迎，并认可沟通风格的改进；但也有用户尖锐指出，Anthropic 在博客开篇即引用&quot;pacing the frontier&quot;表态，而具体降价幅度恰恰说明其并未放慢竞争节奏，认为这两者存在叙事矛盾。还有用户反映已转向 DeepSeek v4.1 等更便宜的替代方案，理由是后者在常规编码与页面改版任务中表现稳定。

**标签**: `#AI`, `#LLM`, `#Anthropic`, `#Claude`, `#pricing`

---

<a id="item-tech-news-2"></a>
### [WordPress 7.1.2 修复路径遍历漏洞，可致条件性远程代码执行](https://github.com/WordPress/wordpress-develop/security/advisories/GHSA-7hp8-65ch-5whp) ⭐️ 8.0/10

WordPress 发布 7.1.2 安全更新，修复一处未经身份验证即可利用的路径遍历漏洞。漏洞位于 \`locate\_template\(\)\` 函数，未对模板名做目录遍历限制，攻击者可借此实现条件性远程代码执行。官方 GitHub 安全公告（GHSA-7hp8-65ch-5whp）确认修复已向下游回溯至 4.7 分支，覆盖仍在使用旧版分支的站点。

hackernews · vntok · 9月22日 16:33 · [社区讨论](https://news.ycombinator.com/item?id=49803959)

**「locate\_template\(\) 与路径穿越」** WordPress 的 \`locate\_template\(\)\`（定义于 \`wp-includes/template.php\`）会根据页面 slug 在活动主题、父主题与 \`wp-includes\` 目录中查找对应的模板文件。路径穿越指利用未规范化的 \`../\` 等序列，让文件解析结果落到预期目录之外；GHSA-7hp8-65ch-5whp 的根因在于 \`get\_page\_template\(\)\` 拼接出的候选路径未经过 \`validate\_file\(\)\` 校验，使模板解析可能被引导至可被加载的 PHP 文件，间接达成代码执行。

**「社区讨论」** 讨论者普遍认为官方将补丁回溯至 4.7 分支值得肯定，但也指出约三分之一的 WordPress 站点并未运行最新的 7.x 分支，仍面临暴露风险。vntok 指出，受影响函数的官方文档页面上 9 年前就已有评论警告 \`locate\_template\(\)\` 不防御目录遍历攻击，提示该问题长期被忽视；另有用户表示已因此类安全问题将站点迁移至静态生成方案以减少攻击面。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://github.com/vulpecuna/CVE-2026-87902">vulpecuna/CVE-2026-87902: Unauthenticated RCE on Wordpress ...</a></li>
<li><a href="https://github.com/WordPress/wordpress-develop/security/advisories/GHSA-7hp8-65ch-5whp">Unauthenticated path traversal in page- template resolution leading...</a></li>

</ul>
</details>

**标签**: `#security`, `#wordpress`, `#vulnerability`, `#web-development`, `#cve`

---

<a id="item-tech-news-3"></a>
### [Pentagon says overreliance on AI contributed to missile strike on Iran school](https://www.bloomberg.com/graphics/2026-iran-school-attack/) ⭐️ 8.0/10

Pentagon report finds that overreliance on the Maven AI targeting system—fed outdated facility data—contributed to a U.S. missile strike on an Iranian school, raising urgent questions about automation bias and human oversight in military AI.

hackernews · devonnull · 9月22日 19:03 · [社区讨论](https://news.ycombinator.com/item?id=49806430)

**标签**: `#ai-safety`, `#military-ai`, `#automation-bias`, `#policy`, `#ml-deployment`

---

<a id="item-tech-news-4"></a>
### [Claude Opus 5.5 与 GPT-6 Sol/Luna 同日发布，价格战升级](https://simonwillison.net/2026/Sep/22/opus-and-sol-and-luna/) ⭐️ 8.0/10

2026 年 9 月 22 日，Anthropic 发布 Claude Opus 5.5，约一小时后 OpenAI 发布 GPT-6 Sol 和 GPT-6 Luna。GPT-6 Luna 输入价为 $0.10/M、输出 $0.50/M，GPT-6 Sol 为 $2/M 输入、$10/M 输出，均较 GPT-5.6 同名版本降价一半；考虑到 GPT-5.6 还将在 11 月上调 25%，GPT-6 系列的相对降幅更大。Claude Opus 5.5 输入 $4/M、输出 $20/M，较前代 5.x 降价 20%，缓存读取价格下降 60%，对长上下文 agent 调用成本影响显著。Simon Willison 在&quot;鹈鹕骑自行车&quot;SVG 测试中发现，Opus 5.5 在 max 思考档位下因过度推理撞上 128,000 token 输出上限而未返回结果，两次失败各耗约 $2.56、耗时近 20 分钟，作者质疑该档位实际可用性。

rss · Simon Willison · 9月22日 23:46

**「背景」** OpenAI 的 GPT-5.6 系列是该公司的上一代前沿模型，包含 Sol（高性能档）、Terra（中间档）和 Luna（性价比路线）三个分支，其中 GPT-5.6 Luna 已因性能与低价兼具而成为开发者构建应用时的常用选择；GPT-5.6 目前采用促销定价，并已宣布将于 11 月再上调 25%。Anthropic 的 Claude Opus 5.0 及此前的 4.5、4.6、4.7、4.8 版本长期维持 $5/$25 的每百万 token 输入/输出定价，更高层的 Claude Fable 系列则定价更高，而 xAI Grok 4.7 与小米 MiMo v2.6 Flash/Pro 也已在发布前一天刚刚推出。

**「成本与可用性的双重影响」** 对开发者和采购方而言，最直接的两项具体后果是：其一，Claude Opus 5.5 的 max 思考档位存在已记录的失败模式——在 Simon Willison 的 SVG 鹈鹕生成测试中，模型因推理过程输出达到 128,000 token 上限而未能返回最终结果，两次尝试每次消耗约 $2.56 并耗时近 20 分钟，意味着将 Opus 5.5 部署在 max 档位处理长链推理或复杂生成任务时存在已观察到的可用性问题，使用方在选型时需将这一档位视为不可靠路径而非默认高线；其二，价格层面的连锁反应迫使采购侧立即重新评估——Anthropic 在 Opus 5.5 降价 20% 并将缓存读取价下调 60% 后，OpenAI 立即以 GPT-6 Sol/Luna 给出较 GPT-5.6 优惠价再降 50% 的回应，使 GPT-6 Luna（$0.10/$0.50）成为仅次于 GPT-5 Nano 的极低定价模型，叠加 GPT-5.6 系列将于 11 月涨价 25%，继续停留在 GPT-5.6 系列上的应用迁移到 GPT-6 系列具有明确的成本驱动收益，且 Opus 5.5 缓存价下调对长上下文 agent 会话（90% 以上输入按缓存价计费）有具体节省。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://fortune.com/2026/09/22/what-ai-slowdown-openai-anthropic-release-dueling-moreaffordable-models-as-ai-price-wars-heat-up/">What slowdown? OpenAI, Anthropic release dueling models as AI price wars heat up | Fortune</a></li>
<li><a href="https://www.kucoin.com/news/flash/anthropic-and-openai-launch-new-ai-models-amid-price-cuts">Anthropic and OpenAI Launch New AI Models Amid Price Cuts | KuCoin</a></li>

</ul>
</details>

**标签**: `#AI models`, `#LLM pricing`, `#Anthropic`, `#OpenAI`, `#industry news`

---

<a id="item-tech-news-5"></a>
### [Claude Code v2.1.280 引入 Claude Opus 5.5](https://github.com/anthropics/claude-code/releases/tag/v2.1.280) ⭐️ 7.0/10

Claude Code v2.1.280 将 Claude Opus 5.5（\`claude-opus-5-5\`）设为新的默认 Opus 模型，提供 1M 上下文窗口，定价为输入/输出 $4/$20 每百万 token，缓存读取 $0.20 每百万 token。本次更新还新增了环境变量 \`CLAUDE\_CODE\_MAX\_MCP\_DESCRIPTION\_LENGTH\`，用于修改每个 MCP 会话中工具描述和服务器说明默认 2,048 字符的上限；并在 \`hook\_execution\_complete\` OpenTelemetry 事件中加入钩子输出大小与已保存的超限输出数量。此外还修复了自动模式反复重试或反复拒绝的安全检查问题、对称链接路径写入校验问题、多次按 Ctrl+C/Ctrl+D 关闭对话框而非退出程序、Windows 终端提示行错位等多处缺陷。

github · ashwin-ant · 9月22日 16:38

**「背景」** Claude Code 是 Anthropic 推出的命令行 AI 编程工具，Opus 系列为其面向复杂任务的高端模型线。本次发布的 v2.1.280 由 Anthropic 官方在 GitHub 发布，属于常规迭代版本号下的功能更新。

**「影响」** 对 Claude Code 的用户与开发者：默认模型升级到支持 1M 上下文的 Opus 5.5，并在缓存读取侧提供 $0.20/百万 token 的较低费率，长会话或需要引用大量代码、文档的工作流在缓存命中时可显著降低调用成本；同时新增的 MCP 描述长度配置项允许部署方按需放宽工具描述上限，便于接入描述冗长的第三方 MCP 服务。

**标签**: `#AI`, `#developer-tools`, `#Claude`, `#release-notes`, `#MCP`

---

<a id="item-tech-news-6"></a>
### [&\#x27;We hacked the FBI:&\#x27; Hackers say they have data on all FBI employees](https://www.404media.co/we-hacked-the-fbi-hackers-say-they-have-data-on-all-fbi-employees/) ⭐️ 7.0/10

Hacker group ShinyHunters claims responsibility for breaching the FBI and obtaining data on all employees, raising serious questions about federal data security practices.

hackernews · spenvo · 9月22日 17:46 · [社区讨论](https://news.ycombinator.com/item?id=49805278)

**标签**: `#cybersecurity`, `#data-breach`, `#government-it`, `#infosec`, `#incident-response`

---

<a id="item-tech-news-7"></a>
### [Trail of Bits 发布 SAML 深度技术批判,指出其 XML 级设计缺陷](https://blog.trailofbits.com/2026/09/21/saml-a-fractal-of-bad-design/) ⭐️ 7.0/10

Trail of Bits 发布了一篇题为《SAML: A fractal of bad design》的技术分析文章,详细论证 SAML 协议反复出现安全漏洞的根源在于 XML 层级的根本性设计选择。文章串联了 XML Signature Wrapping\(XSW\)、XML 签名验证缺陷等多类已知漏洞,认为 SAML 的问题并非孤立的实现缺陷,而是嵌套式的结构性问题。该文章在 Hacker News 上获得 147 分、85 条评论,引发针对 SSO 协议设计权衡的实质性技术讨论。

hackernews · aray07 · 9月22日 18:57 · [社区讨论](https://news.ycombinator.com/item?id=49806335)

**「什么是 SAML 及其设计背景」** SAML（Security Assertion Markup Language，安全断言标记语言）是面向企业级单点登录（SSO）的标准协议，由 OASIS 标准化已超过二十年，目前仍是身份联邦（Identity Federation）场景中部署最广泛的技术之一。与更侧重 API 与现代 Web 应用的 OIDC（OpenID Connect）不同，SAML 完全基于 XML 构建，依靠 XML Signature（xmlsig）对认证断言（Assertion）进行签名和完整性保护，并通过浏览器重定向在身份提供商（IdP）与服务提供商（SP）之间交换带签名的 XML 文档。这种基于文档和标记语言的协议结构虽然能满足复杂的企业联合身份需求，但其校验逻辑——尤其是 xmlsig 默认对多种校验方式的支持和签名范围判定——历史上反复成为安全研究中漏洞的高发区域，构成了 Trail of Bits 文章批评 SAML 设计的具体技术语境。

**「影响」** 对需要实现或审计企业 SSO / 身份系统的开发者与安全工程师而言,文章整理了一份聚焦 XML 协议层攻击面的具体清单,可在选型与代码审查时作为参考依据;但社区共识是 SAML 的主要替代品 OIDC 同样存在独立的安全问题,从 SAML 迁移到 OIDC 并不能简单地视为安全性提升。

**「社区讨论」** 社区讨论集中于两点:其一,bawolff 给出历史案例,指出曾有主流 C 语言 XML 签名实现在校验签名时,会同时回退使用攻击者可控文档中的密码进行 HMAC 校验,甚至回退到 Web PKI 校验,导致攻击者用自己域名的 TLS 私钥即可签出合法 SAML 文档;其二,tehnoslow 与 cameronh90 就 OIDC 是否更优展开争论——前者认为文章未对 OIDC 做同等深度比较,JWT 算法混淆、\`none\` 算法攻击、受众校验缺失以及 JOSE 库缺陷同样普遍,后者则认为 SAML 仍具备 OIDC 缺失的 IdP-initiated flow 等企业级特性,OIDC 是一组规范支持参差不齐的星座,迁移不能视为简单的安全升级。

**标签**: `#security`, `#authentication`, `#saml`, `#identity`, `#web-standards`

---

<a id="item-tech-news-8"></a>
### [Artificial Analysis 发布 Claude Opus 5.5 多档推理基准与成本对比](https://artificialanalysis.ai/models/claude-opus-5-5) ⭐️ 7.0/10

Artificial Analysis 发布了对 Anthropic Claude Opus 5.5 在多个推理强度（max、xhigh、medium）下的基准测试页面。测试显示在相同高强度推理档位下，Claude Opus 5.5 的每任务成本约为前代 Opus 5 的一半；但在 max 档位上，有用户反馈模型在复杂生成任务中因 128,000 token 推理预算耗尽而未能完成输出。

hackernews · theanonymousone · 9月22日 16:51 · [社区讨论](https://news.ycombinator.com/item?id=49804316)

**「评测背景与对照对象」** Artificial Analysis 是第三方独立的大语言模型评测平台，长期对各厂商前沿模型在智能水平、推理能力与单任务成本等维度进行横向打分。此次评测针对 Anthropic 于 2026 年 9 月发布的旗舰模型 Claude Opus 5.5，并以同厂商上一代模型 Claude Opus 5 作为成本与能力的对照基准，分析 Opus 5.5 在 medium、max、xhigh 三档推理力度下的表现差异。

**「影响」** 对使用 Anthropic API 的开发者而言，Opus 5.5 在高强度推理档位上的成本下降（hglaser 称相比 Opus 5 同档位约减半）可降低单位任务开销；但 max 档位在多步推理任务中存在 128k token 上限耗尽的风险（simonw 报告生成 SVG 任务两次因此失败），选用 max 档位时需评估任务长度与推理预算的匹配。

**「社区讨论」** 评论围绕三个方向展开：simonw 指出 max 档位的 128k token 预算在 SVG 类生成任务中两次耗尽，导致任务失败；breckenedge 提出模型上线后性能可能回撤的担忧，提到其内部基准发现 Sol 的表现已退至 Luna 水平；cmiles8 则认为前沿闭源模型相对开源权重模型仅有轻微优势但价格高出约 100 倍，质疑闭源实验室长期商业模式的可持续性。

**标签**: `#claude`, `#anthropic`, `#model-benchmarks`, `#llm-pricing`, `#frontier-models`

---

<a id="item-tech-news-9"></a>
### [GPT-6 改进提示缓存机制以降低延迟与成本](https://openai.com/index/better-prompt-caching-for-gpt-6) ⭐️ 7.0/10

OpenAI 在 2026 年 9 月 22 日发布的博客中宣布，GPT-6 对提示缓存（prompt caching）机制进行了多项改进，主要包括更高的缓存命中率、新的诊断工具、显式缓存断点（explicit breakpoints），以及面向开发者的控制选项。官方称这些改进旨在减少推理延迟并降低 API 调用成本。该来源为 OpenAI 官方博客的摘要，文中未给出具体的命中率提升数字或定价变化。

rss · OpenAI Blog · 9月22日 21:00

**「背景」** 提示缓存（prompt caching）是 LLM API 中的一种常见优化机制：服务端将已处理过的提示前缀结果暂存复用，以降低重复请求的延迟与 token 成本。2026 年 9 月 22 日，OpenAI 发布了 GPT-6 系列模型（含 Sol、Luna 等变体），并对提示缓存机制进行了升级，本文即为 OpenAI 关于该升级的官方说明。

**「影响」** 对在生产环境中运行 LLM 应用的开发者而言，更高的缓存命中率与显式断点意味着可减少对重复提示前缀的重复计算，从而降低响应延迟与 token 成本；但 OpenAI 在该摘要中未量化命中率提升幅度，也未说明与此前 GPT-5 缓存行为的兼容性差异，建议开发者查阅完整 API 文档或进行实测后再据此调整缓存策略。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.digitalapplied.com/blog/gpt-6-sol-luna-launch-pricing-benchmarks-2026">GPT - 6 Sol and Luna: API Prices, Benchmarks and Trade-offs</a></li>
<li><a href="https://kingy.ai/blog/gpt-6-sol-luna-specs-benchmarks-pricing-comparison/">GPT - 6 Sol and GPT - 6 Luna: Specs, Benchmarks, Pricing... - Kingy AI</a></li>

</ul>
</details>

**标签**: `#AI`, `#LLM`, `#OpenAI`, `#Performance`, `#Developer Tools`

---

<a id="item-tech-news-10"></a>
### [Complex KDA：理解并增强 Kimi Delta Attention 的表达能力](https://www.reddit.com/r/MachineLearning/comments/1wn5uv9/understanding_and_enhancing_kimi_delta_attention_r/) ⭐️ 7.0/10

一篇论文系统分析了 Gated Deltanet（GDN）与 Kimi Delta Attention（KDA）在表达能力上的差异，并提出扩展方案 Complex KDA（CKDA）。论文证明 KDA 的完整对角门控在对角元素取值扩展至 \[-1, 1\]、delta 规则学习率扩展至 \[0, 2\] 时，可作为反射矩阵在单步内完成二维旋转；CKDA 因此能够表达任意正交的对角加秩一矩阵，并跟踪对称群 S3、S4 与 A5，但无法覆盖 S5。实验部分显示 CKDA 可学习 S3 与 S4，在音频续写任务上取得有希望的结果，并在语言建模上与标准 KDA 训练稳定、表现相当。

reddit · r/MachineLearning · /u/Yossarian\_1234 · 9月22日 10:34

**「背景」** Kimi Delta Attention \(KDA\) 是一种线性注意力变体，与 Gated Deltanet \(GDN\) 的关键区别在于其采用了完整的对角门控。该研究指出，KDA 的对角门控在理论上可充当反射矩阵，但默认的门控值域与 delta 规则学习率限制了 2D 旋转等表达能力，因此需要将门控范围扩展至 \[-1,1\]、学习率扩展至 \[0,2\]，才能形成所提出的 Complex KDA \(CKDA\)。

**「影响」** 对研究线性注意力机制的研究者而言，CKDA 提供了一个有理论支撑且经验验证的 KDA 变体，在不牺牲语言建模训练稳定性的前提下拓宽了可表达的变换范围；但当前证据为论文作者自报，尚无独立复现。

**标签**: `#linear-attention`, `#expressivity-theory`, `#kimi-delta-attention`, `#language-modeling`, `#audio-modeling`

---

<a id="item-tech-news-11"></a>
### [AI 协助破解一封 2005 年以来未解的 Enigma 历史电报](https://www.cryptocellar.org/bgac/the-mvueh-break.html) ⭐️ 6.0/10

据 CryptoCellar BGAC 挑战页面报道，一位研究者借助 OpenAI 的 GPT-6 &quot;Astra&quot; 构建 Python 与 C++ Enigma 模拟器，再通过暴力搜索参数，解开了一封自 2005 年起悬而未决的二战 Enigma 密文。解密得到的明文被还原为一段含义普通的军事电报，大意为&quot;请告知行军路线，我位于 Rosenow……立即回电，Waschbusch&quot;。

hackernews · sohkamyung · 9月22日 13:52 · [社区讨论](https://news.ycombinator.com/item?id=49801324)

**「Enigma 密码机与这条报文的背景」** Enigma 是二战期间纳粹德国使用的机电转子密码机，其密钥空间庞大，曾被认为几乎无法破解。这条 1941 年的无线电报文自 2005 年起作为公开挑战的一部分长期未能被破译，原因包括它未与当日其他报文共用日常密钥、原始转录存在错误，以及转子在第 72 个字母处发生罕见的转动而干扰了常规的 crib 攻击方法。GPT-6 Astra 是 OpenAI 于 2026 年 9 月发布的语言模型，在本事件中由开发者引导其构建 Enigma 模拟器并执行密钥穷举搜索。

**「实际意义」** 该案例展示了 AI 生成模拟代码在处理单个历史密文时的实际作用，而非通用的密码学突破。社区指出该密文之所以长期未解，是因为其密钥与当日其他通信不同、转录存在错误、左转子第 72 位发生罕见翻转，绕开了标准 crib 攻击；公开来源未能确认报道中的工作量、自主性以及与更广泛 Enigma 项目的差异。

**「社区讨论」** 多位评论者指出标题夸大了 AI 的自主性——Astra 的核心工作是生成 Enigma 模拟器代码，而非独立完成密码分析。有用户报告 Gemini 3.8 Flash 在约 45 分钟内即独立完成了类似的解密尝试，这削弱了&quot;突破性&quot;的说法；也有人质疑生成的模拟器代码有多少是新颖的、有多少只是已知实现。该密文明文为普通军事行军路线请求，既无情报价值，也不代表 Enigma 在整体上被攻破。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/GPT-6_Astra">GPT - 6 Astra - Wikipedia</a></li>
<li><a href="https://beincrypto.com/gpt-6-astra-enigma-message-break/">OpenAI &#x27;s GPT - 6 Astra Cracked a Nazi Enigma Message in 10 Hours...</a></li>

</ul>
</details>

**标签**: `#cryptography`, `#AI-applications`, `#enigma`, `#historical-ciphers`, `#AI-assisted-coding`

---