# 第1课 课后作业

# 第 1 课 练习

今天的练习大部分取自这个[ZK Topic Sampler](https://learn.0xparc.org/materials/circom/prereq-materials/topic-sampler/)。

## ZKP 三色演示

访问并试用[交互式演示](https://zkshanghai.xyz/interactive/graph.html )。 这是我们在课堂上学习的三色示例的程序化版本。

- 回答页面底部的练习 1。

交互式零知识三色问题演示 原文
这是针对三色图的零知识证明协议的交互式演示。 零知识证明可以让验证者相信一个事实的真实性（即，一个图仅三色），而无需揭示图的具体颜色。

此应用程序允许您以验证者的身份玩游戏。 该应用程序（证明者）为您提供了一个图形，其颜色对您来说是隐藏的，并且您可以选择一条边，验证器将显示其颜色。 选择一个图并尝试点击一些边。

您可能会注意到游戏的不同轮次之间颜色会发生变化； 尽管证明者一旦为您提供选择就不允许改变主意，但允许混合选择之间的颜色。 事实上，如果没有，您可以对整个着色进行逆向工程（使其不是零知识证明）您可以通过按 揭露 按钮检查应用程序是否违背其承诺 . （既然这告诉你真正的颜色是什么，这显然不是零知识协议的一部分！）

一旦厌倦了手动单击边，您可以选择 自动 来加快速度。 当你进行了更多轮的协议时，证明者由于幸运而说谎（图不是三色）概率在下降，这也反映在置信度指标中。

练习 1： 目前，您只能选择相邻的节点对进行检查。 如果您可以选择任意节点对来检查，证明仍然是零知识吗？
A: It's not. Because it may violate the Soundness properties of ZKP, if the prover provides the wrong answer, he may not be caught.


练习 2： 当前用于置信度的方程是 1-(1/E)^n，其中 E 是图中的边，n 是运行试验的次数。 这是正确的等式吗？ 为什么没有先验？。
A: it is not the correct equation. The correct equation is $1-(1-\frac{1}{E})^n. The confidence here is how likely we are to believe that Prover knows the coloring scheme.

Prior probability (prior probability): refers to the probability that can be obtained before the experiment or sampling based on previous experience and analysis (refer to <Basic Series> 1: Prior Probability & Posterior Probability). Before interacting with the Prover, we have nothing to learn about the probabilities of the coloring schemes, no additional information, and thus no priors.

## 可选 - DLOG 的 ZKP

用离散对数实现非交互零知识证明！ 为此，您需要阅读并理解 [本讲义](https://people.eecs.berkeley.edu/~jfc/cs174/lecs/lec24/lec24.pdf) 的第一部分，因为 以及 [Fiat-Shamir 启发式](https://en.wikipedia.org/wiki/Fiat%E2%80%93Shamir_heuristic)。

具体来说，您应该实施：

- 函数 dlogProof(x, g, p) 返回 (1) 残差 y，计算方法为 g^x (mod p) 和 (2) 可以证明您知道 x 是 y 的离散对数的证据 pf。
- 函数 verify(y, g, p, pf) 如果 pf 是有效的证据，则计算结果为真，否则为假。如果证明者确实知道有效 x，则证明者应该只能以不可忽略的概率计算有效证明。

如果您需要帮助，可以在[此处](https://github.com/gubsheep/zk-beginner)找到带有注释的 Javascript 参考实现。 这个练习可能需要你几个小时。

对于额外的挑战，也可以尝试实施非交互式 ZKP 来证明 3 色！

```
code: lecture1-homework-code.py
```

## zkmessage.xyz

在 [zkmessage](https://zkmessage.xyz) 上创建一个帐户并发布消息，这是一个由 zkSNARK 支持的匿名留言板。
- 解释为什么你需要生成并保存一个“秘密值” 。
A: We will use the "secret" value to claim a ZKMessage public key and generate group signatures.


- 用白话写出 ZK 中正在证明的陈述。
A: I know some private key that represents the author of the post belongs to a group of people listed in the group-signed message. Here is a signature that I know such a private key, without telling you what the acture private key is.

- 从不同的浏览器或计算机登录到相同的 zkmessage 帐户。 解释为什么 zkmessage 不能像大多数社交应用程序一样，只使用简单的“用户名/密码” 。
A: In that way, we have to give the control of our account to the central server, thus they delete our account or messgages. But if we use the private key to login, we can control our account. If the server censors our messages or signatures, we can swap out the server for a decentralized data layer.

如果您好奇，我们在[此处](https://0xparc.org/blog/zk-group-sigs)更深入地探讨了 zkmessage 的构建。