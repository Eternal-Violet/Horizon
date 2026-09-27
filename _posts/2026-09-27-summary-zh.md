---
layout: default
title: "Horizon Summary: 2026-09-27 (ZH)"
date: 2026-09-27
lang: zh
---

> 从 14 条内容中筛选出 3 条重要资讯。

---

**科技新闻**
1. [DeepSeek 发表论文描述 DSec 弹性计算系统](#item-tech-news-1) ⭐️ 7.0/10
2. [Reladraw：兼顾声明式语法与手动布局的图表语言](#item-tech-news-2) ⭐️ 6.0/10
3. [从零用 NumPy 实现带 GUI 的 MLP 教学可视化工具](#item-tech-news-3) ⭐️ 6.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [DeepSeek 发表论文描述 DSec 弹性计算系统](https://arxiv.org/abs/2609.22978) ⭐️ 7.0/10

...

hackernews · shenli3514 · 9月26日 18:22 · [社区讨论](https://news.ycombinator.com/item?id=49859112)

**「背景：智能体训练中的沙箱隔离与多级执行后端」** 在 AI 智能体训练中，沙箱用于隔离模型生成的代码与底层系统，使工具调用或外部程序能够安全执行。常见的隔离级别从开销极低的函数调用（FnCall）、进程级容器，到硬件虚拟化的 microVM 与完整虚拟机（full-VM）依次递增，安全边界与性能开销各异，不同任务对隔离强度的需求并不相同。DeepSeek 在 DSec 论文中将这些后端统一在同一 SDK 之下，使训练框架可按任务风险弹性选择执行粒度，这正是理解其后续规模指标的必要前提。

**「社区讨论」** ...

<details><summary>参考链接</summary>
<ul>
<li><a href="https://arxiv.org/abs/2609.22978">[2609.22978] DeepSeek Elastic Compute (DSec): A Sandbox ...</a></li>
<li><a href="https://technode.com/2026/09/23/deepseek-dsec-agent-training-sandbox-infrastructure/">DeepSeek details DSec sandbox infrastructure for agent training</a></li>

</ul>
</details>

**标签**: `#AI infrastructure`, `#distributed systems`, `#DeepSeek`, `#sandboxing`, `#elastic computing`

---

<a id="item-tech-news-2"></a>
### [Reladraw：兼顾声明式语法与手动布局的图表语言](https://github.com/reladraw/reladraw) ⭐️ 6.0/10

Reladraw 是一款开源图表语言，通过在声明式语法中加入相对位置指令（如 left of、right of），让作者既能以文本方式描述图表，又能控制节点的相对布局。项目在 GitHub 上发布，提供浏览器内 Playground、npm 安装方式，以及一个可被 Claude 等 AI 代理加载的技能包，明确面向人类作者与 AI 代理两类用户。它定位于 Mermaid、Graphviz 这类自动布局语言与 Draw.io 这类 GUI 工具之间，试图兼顾文本可编程性与手动布局控制。

hackernews · jpwalsh234 · 9月26日 17:10 · [社区讨论](https://news.ycombinator.com/item?id=49858513)

**「背景」** 此前的图表工具大致分为两类：一类是 Mermaid、Graphviz 等声明式语言，从文本描述自动生成布局，作者无法干预节点位置；另一类是 Draw.io 等 GUI 编辑器，可精确控制布局，但依赖手动操作，对程序化或代理驱动的场景效率较低。Reladraw 在声明式语法之上引入相对位置原语，试图填补这两类工具之间的空白。

**「影响」** 对开发者和 AI 代理使用者而言，Reladraw 提供了一种既可被代理读写、又允许作者保留布局控制权的文本格式，可能降低程序化生成或修改结构化图表的摩擦。但早期用户反馈也指出存在边缘情况缺陷，例如将一条边写为 from: left to: right 时未按预期渲染为曲线箭头，工具尚处于可用但仍需打磨的阶段。

**「社区讨论」** 多数评论者认同 Mermaid 自动布局与 Draw.io 手动 GUI 之间存在真实缺口，尤其在代理驱动的工作流中价值明显；有人建议将拓扑结构（箭头、分组）与布局指令解耦，并支持 C4 模型风格。还有测试者报告了具体 bug：一条从 left 指向 right 的边未被渲染为曲线，提示当前实现在边路由上仍有粗糙之处。

**标签**: `#diagramming`, `#open-source`, `#developer-tools`, `#ai-agents`, `#notation`

---

<a id="item-tech-news-3"></a>
### [从零用 NumPy 实现带 GUI 的 MLP 教学可视化工具](https://www.reddit.com/r/MachineLearning/comments/1wqy1qd/p_a_small_mlp_from_scratch_in_numpy_with_a_gui_to/) ⭐️ 6.0/10

用户 dev-luigi 在 GitHub 开源了一个纯 NumPy 实现的 MLP 教学工具 neural-network-digits，附带交互式 GUI。该项目不使用自动微分框架，手动实现反向传播，并提供带动量的 SGD、L2 正则化、Dropout、余弦衰减以及 4 种激活函数，在 MNIST 全量数据集上可达约 98.5% 准确率。训练过程中实时展示每 mini-batch 与 epoch 损失、各层梯度范数及失活神经元比例、当前权重分布与初始化分布的对比、首层感受野，并附带用 NumPy 实现的逐层 PCA/t-SNE 可视化（含错误预测到混淆数字簇的连线）、噪声与旋转鲁棒性曲线、置信阈值-覆盖率分析，以及一个可对单神经元进行消融/重缩放、对整网进行剪枝、给权重加噪或调整 Softmax 温度并立即更新测试准确率的实验面板。

reddit · r/MachineLearning · /u/No-Brain-1655 · 9月26日 18:38

**「背景」** 该项目把自己定位为 ML 教学辅助工具，明确面向高中到入门 ML 课程的学生、自学者以及需要在课堂上展示神经网络工作原理的教师。它与常见 PyTorch/TensorFlow 教程的区别在于：完全从零构建一个可交互的小型 MLP，并把训练过程内部状态（梯度、权重分布、感受野、逐层表征）通过 GUI 暴露出来，让用户能直观看到学习动态，而非只看到最终准确率。

**「影响」** 对于希望把 MLP 内部机制讲清楚的教学者与自学者，该工具提供了一个无需 PyTorch 即可上手、且能在课堂上演示的实验台：学生可以在神经元消融实验中亲手关掉某个隐藏单元或缩放其权重、或调整 Softmax 温度，并立即在前端看到测试准确率变化，从而把抽象的正则化与鲁棒性概念落到具体可观察的现象上。

**标签**: `#machine-learning`, `#education`, `#visualization`, `#neural-networks`, `#python`

---