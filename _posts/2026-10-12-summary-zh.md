---
layout: default
title: "Horizon Summary: 2026-10-12 (ZH)"
date: 2026-10-12
lang: zh
---

> 从 21 条内容中筛选出 7 条重要资讯。

---

**科技新闻**
1. [陶哲轩&quot;数学 2.0&quot;框架：AI 介入数学研究](#item-tech-news-1) ⭐️ 7.0/10
2. [Sliced Wasserstein 嵌入 + HNSW 实现 4.8 万幅画作配色 检索](#item-tech-news-2) ⭐️ 7.0/10
3. [The gap in shared understanding of LLM capability is widening](#item-tech-news-3) ⭐️ 6.0/10
4. [主张回避带远程证明 passkey 的博客文章引发争议](#item-tech-news-4) ⭐️ 6.0/10
5. [AI agent 用 5000 亿 tokens 反编译《使命召唤：现代战争 2》\(2009\)](#item-tech-news-5) ⭐️ 6.0/10
6. [浏览器内可视化小模型选词与注意力的开源工具 Attention Galaxy](#item-tech-news-6) ⭐️ 6.0/10
7. [I trained a 414k-parameter transformer to fly a boids flock, then tested whether the rules a probe can read are the ones it uses \[P\]](#item-tech-news-7) ⭐️ 6.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [陶哲轩&quot;数学 2.0&quot;框架：AI 介入数学研究](https://teorth.github.io/tao-web/slides/math-2-0-caltech-2026.pdf) ⭐️ 7.0/10

菲尔兹奖得主陶哲轩（Terence Tao）于 2026 年在加州理工学院以 PDF 幻灯片形式发表演讲，提出&quot;数学 2.0&quot;概念，将 AI/LLM 工具对数学研究的影响类比为一次范式转变。该框架主张 AI 不再仅是辅助工具，而是逐步融入问题求解与证明环节的新型研究伙伴。但需注意，此为幻灯片而非完整论文，且 AI 对前沿数学的真实贡献在社区中仍存争议。

hackernews · Anon84 · 10月11日 13:16 · [社区讨论](https://news.ycombinator.com/item?id=50043026)

**「背景」** 陶哲轩是 2006 年菲尔兹奖得主，长期被视为当代最具影响力的数学家之一。&quot;数学 1.0&quot;通常指人类数学家独立完成问题构思、证明撰写与同行评审的传统研究模式；&quot;数学 2.0&quot;则是陶哲轩对 LLM 等 AI 工具进入这一流程后所处新阶段的命名。Lean、Isabelle 等形式化证明助手以及 AI 定理搜索近年在数学领域的应用持续推进，本次演讲是对这一趋势的系统化框架总结。

**「影响」** 社区中多位数学家反馈 AI 在数日内解决了他们研究数年的开放问题，部分人因此需要重写已提交的科研经费申请，并形容得知问题被解决的感觉&quot;如同失去一位老友或恋人&quot;——表明 AI 工具已对在职数学家的工作分配、经费规划以及情感投入产生切实影响。

**「社区讨论」** 针对陶哲轩一张关于癌症药物的幻灯片，dekhn 与 squidmaster 提出反驳：许多已获临床使用的药物机制至今未被完全阐明（如全身麻醉），医生通常不会因不理解机制而拒绝有效疗法，这与&quot;必须先理解机制才能信任解药&quot;的预设相矛盾。thomasahle 则从软件工程角度补充，认为当前一代数学 AI 并未像良好贡献者那样为理论&quot;代码库&quot;添加最优雅的扩展。

**标签**: `#AI`, `#mathematics`, `#scientific-research`, `#LLMs`, `#paradigm-shift`

---

<a id="item-tech-news-2"></a>
### [Sliced Wasserstein 嵌入 + HNSW 实现 4.8 万幅画作配色 检索](https://www.reddit.com/r/MachineLearning/comments/1x39uu6/sliced_wasserstein_embeddings_hnsw_for/) ⭐️ 7.0/10

项目 &quot;Palette Atlas&quot; 将 48,695 幅公共领域画作量化为 128 个等权颜色后，在 OKLab 空间沿 Fibonacci 半球 8 个方向投影排序并取 16 个分位数，得到 128 维 Sliced Wasserstein 嵌入，其 L1 距离对真 EMD（Wasserstein-1）构成下界。结合从零实现的 HNSW 索引（M=16, efConstruction=200），ef=32 时 recall@10 达到 1.000，单次查询约 0.25 ms，相对暴力 EMD 的 14 ms 提速约 50 倍。240 查询上与精确 EMD 前 10 的重合率为 78%（L1）/69%（L2），距离开销仅 1.8%/3.4%，明显优于软色直方图 Hellinger（45%, 13.5%）和平均色（3%, 161%）。相比原 HNSW 论文，该实现把顶层 8 个入口节点替换为 k-means 地标，平均距离计算次数几乎不变（2,558 vs 2,556），且每个入口节点对应一个典型配色家族。

reddit · r/MachineLearning · /u/Potential-Barber8658 · 10月11日 14:39

**「背景」** Wasserstein-1（Earth Mover&\#x27;s Distance）衡量两个等权颜色分布间的最小传输成本，比直方图或均值方法更贴合“配色相似”的直觉，但成对计算成本高，难以直接用于最近邻检索。Sliced Wasserstein 通过沿若干随机或确定性方向做 1D 投影并对分位数排序取平均，把高维最优传输近似为若干 1D OT 的均值，常作为可微且高效的代理。HNSW（Hierarchical Navigable Small World）是当前主流的近似最近邻图索引，常在百万到亿级向量规模上实现亚毫秒级检索，其加速效果取决于数据内禀维度。

**「影响」** 对做最优传输、嵌入或近似最近邻的 ML 从业者，这套开源的量化 Sliced Wasserstein 嵌入 + from-scratch HNSW 提供了一个可直接复用的配色检索参考，并在 128 维、内禀维度约 11 的设定下量化了 HNSW 相对暴力搜索仍有效的原因；将顶层节点替换为 k-means 地标的改动也展示了在不增加距离计算次数的前提下提升入口代表性的可行做法。

**标签**: `#machine-learning`, `#optimal-transport`, `#nearest-neighbor-search`, `#computer-vision`, `#information-retrieval`

---

<a id="item-tech-news-3"></a>
### [The gap in shared understanding of LLM capability is widening](https://twitter.com/karpathy/status/2109361546505966046) ⭐️ 6.0/10

Discussion of a Karpathy observation about the widening perception gap between AI practitioners who see rapid capability gains and a broader public who experiences little tangible benefit.

hackernews · albertzeyer · 10月11日 20:20 · [社区讨论](https://news.ycombinator.com/item?id=50047422)

**标签**: `#AI`, `#LLMs`, `#Industry Commentary`, `#Software Engineering`, `#Public Perception`

---

<a id="item-tech-news-4"></a>
### [主张回避带远程证明 passkey 的博客文章引发争议](https://nonfunctional.substack.com/p/passkeys-are-a-trap-do-not-use-them) ⭐️ 6.0/10

...

hackernews · laurex · 10月11日 21:59 · [社区讨论](https://news.ycombinator.com/item?id=50048312)

**「背景」** ...

**「影响」** ...

**「社区讨论」** ...

**标签**: `#authentication`, `#passkeys`, `#security`, `#webauthn`, `#identity`

---

<a id="item-tech-news-5"></a>
### [AI agent 用 5000 亿 tokens 反编译《使命召唤：现代战争 2》\(2009\)](https://momo5502.com/posts/2026-10-09-game-decompilation/) ⭐️ 6.0/10

博客 momo5502.com 发布长文，详细记述了使用 AI agent 对 2009 年发售的《使命召唤：现代战争 2》二进制进行反编译的实验，整个过程消耗约 5000 亿 tokens。作者设定了与原二进制字节匹配的目标，要求 AI 精确控制编译器版本与优化选项等微调，才能让生成的汇编码与原二进制逐字节相同。基于版权顾虑（评论中提到&quot;corporate America was here to ruin our fun&quot;），作者此前两篇相关文章已被删除，本次实验的成果也无法公开发布。

hackernews · davikr · 10月11日 02:02 · [社区讨论](https://news.ycombinator.com/item?id=50039092)

**「背景」** 游戏反编译（decompilation）是指将已编译的二进制可执行文件逆向还原为可读源代码，长期由社区项目推动。社区常见的做法是追求 byte-matching——即重新编译后产出与原版逐字节一致的机器码；为此往往需要反复调整编译器版本、优化选项等细节，其难度和成本远高于仅要求行为一致的语义等价（semantic equivalence）方法。该作者此前曾在 Black Ops 3 上做过逆向工程工作（boiii 项目），本次实验可视为同一作者在更大规模、更复杂的商业作品上的延伸尝试。

**「成本与效率教训」** 该实验消耗 500B tokens 的核心原因是追求与原二进制字节一致的汇编输出，而非仅实现功能等价，这迫使智能体反复调整编译器版本、优化选项等细节。社区评论指出，采用多智能体协作（例如让一个智能体编写语义等价的 C 代码并附带测试用例，再交由测试框架验证）的方法可将成本降低数十到上百倍；此外，所选模型也被认为并非性价比最高的选择。另一个实际后果是，由于商标限制，反编译产物无法公开发布，进一步压缩了项目的实用价值。

**「社区讨论」** 评论普遍把高昂的成本归因于字节匹配这一&quot;荒谬的目标&quot;。aetherspawn 认为若改为追求语义等价（functional equivalence），token 消耗可能降低 10 到 100 倍；brandonpelfrey 进一步分享了自己的方案——由 agent A 为每个函数编写语义等价的 C 代码并附带测试用例，再提交给验证 harness。还有评论以碳排放类比指出，5000 亿 tokens 约相当于 15 次旧金山至伦敦往返的等效排放。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://web.archive.org/web/20230515211728/https://github.com/momo5502/boiii">GitHub - momo 5502 /boiii: An attempt at reverse engineering and...</a></li>
<li><a href="https://duskport.com/decomp/zeldaret-projects/">Every Zelda Decompilation Project, Ranked by Progress (2026)</a></li>

</ul>
</details>

**标签**: `#AI agents`, `#reverse engineering`, `#decompilation`, `#LLM costs`, `#code generation`

---

<a id="item-tech-news-6"></a>
### [浏览器内可视化小模型选词与注意力的开源工具 Attention Galaxy](https://www.reddit.com/r/MachineLearning/comments/1x3lgnz/i_built_a_browser_tool_to_visualize_how_a_small/) ⭐️ 6.0/10

开发者 talhatahir-10xe 开源了一款名为 Attention Galaxy 的浏览器端工具，完全在本地（基于 onnxruntime-web）运行量化后的 SmolLM2-135M（int8），无需服务器，可在手机端使用。输入提示词后，工具会逐 token 生成，并展示每一步的下一候选 token 概率分布，以及当前 token 对历史 token 的注意力连线（带权重标注），点击任一词语即可查看其注意力分布的排名。作者在开发过程中也遇到了典型的&quot;注意力陷阱（attention sink）&quot;现象，即早期 token 异常吸引大量注意力权重。仓库与演示地址已在原帖中给出。

reddit · r/MachineLearning · /u/Minute-Mountain2665 · 10月11日 22:30

**「背景」** 注意力可视化（如注意力权重热力图、注意力回滚）是教学中展示 Transformer 内部行为、帮助理解模型决策的常用手段。&quot;注意力陷阱（attention sink）&quot;指的是模型会不成比例地把注意力分配到序列开头的少数 token 上，即便这些 token 在语义上并不相关，这一现象在多个小型 Transformer 模型中被观察到，并非代码缺陷。SmolLM2-135M 来自 Hugging Face 的 SmolLM2 系列，主打可在端侧运行的小规模语言模型。

**「影响」** 对学习 Transformer 注意力机制的学生和教学者而言，这一可即时在浏览器中交互运行的小工具，提供了一个无需部署后端、即可观察真实模型行为的低门槛实验环境；想在自己项目中复用的开发者可直接参考其仓库，使用 onnxruntime-web 在 Web 上加载并量化运行小型 LLM 的方法。

**标签**: `#machine-learning`, `#attention-visualization`, `#browser-inference`, `#onnx-runtime-web`, `#education`

---

<a id="item-tech-news-7"></a>
### [I trained a 414k-parameter transformer to fly a boids flock, then tested whether the rules a probe can read are the ones it uses \[P\]](https://www.reddit.com/r/MachineLearning/comments/1x39jlu/i_trained_a_414kparameter_transformer_to_fly_a/) ⭐️ 6.0/10

A small transformer trained from scratch to predict boid movements learns emergent flocking rules that can be partially read out via linear probes, with specific rules depending on particular attention layers.

reddit · r/MachineLearning · /u/rage\_81 · 10月11日 14:25

**标签**: `#machine-learning`, `#transformers`, `#mechanistic-interpretability`, `#pytorch`, `#emergent-behavior`

---