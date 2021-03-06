---
title: 「链节点 & 链读」波卡生态圆桌论坛 | 达尔文回顾
author: @DarwiniaNetwork
authorURL: http://twitter.com/DarwiniaNetwork
---

![](assets/2020-04-27-chainnode-ama.png)

链读与链节点、PolkaBase 联合主办名为「波卡能不能成为下一个以太坊生态」已于昨晚 19 点与大家见面！在长达 2 个半小时的视频直播中，中国优质波卡生态项目 Acala、Bifrost、Crust、Darwinia、Phala、MXC 极域返场，思考波卡生态目前的定位，预测未来生态的趋势。

大家一起来回顾下达尔文的问答吧！

<!--truncate-->

## Darwinia Network 达尔文网络

达尔文网络是基于 substrate 开发的去中心化的异构链的跨链转接桥网络。我们想解决的问题是，现在市场上的异构链的跨链方案不够去中心化，主要是基于托管的，无法避免道德信任风险以及对小微资产转移不友好。我们采用的是轻客户端的基于事实的一个方案，一种新颖的跨链验证 Chain Relay，使用了 MMR 区块链头承诺、乐观博弈机制、Relayer 激励模型等设计，可以实现仅需要提交对数数量的区块头及其衍生数据，也就是亚线性的性能。大大提高了效率和经济可用性。

有了高效 ChainRelay 加持，我们就可以安全构建双向桥，在两个异构链上双向对等搭建智能合约和相互的 ChainRelay，由智能合约控制资产锁定、赎回等操作，而验证则通过桥头堡达尔文 ChainRelay 实现。与其在每两个链之间搭建直连桥，重复制造轮子，可以通过搭建到达尔文中继链的桥来最容易的实现的“从任何地方来”到“任何地方去”的目标。

## Q&A

### 1、项目方简介

主持人好，各位嘉宾好，大家好，我是达尔文网络（Darwinia Network）联合创始人 Alex。

大概从 2012 年开始，我和另外一位 Co-Founder Denny 就已经开始接触和加入加密社区，Darwinia 现在的核心成员一部分都来自 Bitshares（比特股）团队，Bitshares 也是我们当时参与比较深的一个开源项目，Denny 还曾经是 Bitshares 1.0 的核心开发，当然我们一直保持开放心态，对整个加密生态和其他项目也有不同程度的关注和参与，例如 Ethereum, MakerDAO, NEO 等等。大概 2018 年的时候，我们成立了 Itering 新加坡公司(https://www.itering.io/)，现在是 Darwinia 开源软件的开发商，也是 Darwinia 的主要开发团队。

达尔文网络是基于 Substrate 开发的去中心化异构链跨链桥接网络，专注于建设未来资产互联网络，包括非标资产拍卖市场、稳定币跨链、资产交易兑换等领域。当前较多跨链方案为中心化或半去中心化，难以避免道德风险。基于轻客户端的 BTCRelay 项目却失败了，这是因为经典轻客户端是线性 relay 区块，也就是每一个块都要 relay，使得维护成本高昂，经济上不可为继。而达尔文 Chain Relay 是一种新颖的跨链验证 Relay，实现了超级轻客户端，使用了 Merkle Mountain Range（MMR）区块链头承诺，乐观博弈机制 Optimistic Verification Game，Relayer 激励模型等技术，可以实现仅需要提交对数数量的区块头及其衍生数据，也就是亚线性的性能。大大提高了效率和经济可用性。甚至可以实现按需 relay 块头并进行验证的能力。有了高效 ChainRelay 加持，我们就可以安全构建双向桥，在两个异构链上双向对等搭建智能合约和相互的 ChainRelay，由智能合约控制资产锁定、赎回等操作，而验证则通过桥头堡达尔文 ChainRelay 实现。与其在每两个链之间搭建直连桥，重复制造轮子，可以通过搭建到达尔文中继链的桥来最容易的实现的“从任何地方来”到“任何地方去”的目标。

而一旦达尔文成为波卡的平行链，则可直接打通波卡生态和外界的联系。

从 19 年开始，我们已经发布了三个版本的测试网络，最近我们上线了最后一版测试网 Crab，定位类似于 Kusama 网络之于 Polkadot。这个测试网络将会长久的运营，即使是主网上线之后也会保留，供开发者测试使用。另外 Darwinia 主网主要的功能已经开发完成，但还需要进行更多的安全审计和测试，此外，我们也在等待 Substrate 稳定下来，最终主网上线的时间应该会比 Polkadot 主网稍微晚一点。

### 2、谈谈对以太坊生态的看法？波卡生态目前发展情况？有可能超过吗？

同源性：Gavin 本身出自以太坊社区，黄皮书的作者，在以太坊社区有很搞的声望，所以从一定程度上来说是同源的。

目标：目标上来看，我觉得说法有不同，但是本质上也并没有太大的区别，以太坊想要实现一台世界计算机，波卡则更偏向 web3 的目标，都是想建造一个去中心化无需信任的世界。

官方力度：以太坊已经度过早期的强力推动期，相对官方背景的基金会以及其他机构相对来说推动力度减弱，基本就是大家自己寻找喜欢或者感兴趣的点，喜欢就去做的状态，也因为实际上已经摸索到了一些应用场景，从早些时候的 ICO，到后来的 dApp 游戏，再到现在的 Defi，主题很多，也容易吸引到开发者。波卡则还处于早期的阶段，所以官方驱动的力量比较大，从生态项目资助的各种 grant、到开发者培训项目、到社区运营方面的各种活动比较高频。

路径差异：智能合约 vs 链。智能合约开发比较快，容易上手，实现的应用相对比较简单一些，也受 EVM 的限制，更高级的功能是不太容易实现的。有点像早期的电脑，需要在几 K 的内存里搞事情，需要压榨系统的每一分能力；substrate 开发链则灵活度更大。受局限比较小。这套工具框架的逐渐成熟、以及各种功能的模块逐渐丰富多样起来，门槛也会变低。

开发者差异：智能合约开发者 Solidity vs Rust 开发者。比较灵动的 js 开发者和比较守规矩的开发者，动态脚本语言和静态编译语言的差别。

讨论超过不超过不重要，我觉得不是件有意义的事情，超过又如何不超过又如何，关注两个生态如何互惠互利，也包括其他的项目如何能够协作起来，一起推动整个行业的进步，这可能是更有意义的。

### 3、基础协议 or 终端 dApp，为波卡生态带来什么？为什么加入 Substrate Builders Program？

达尔文作为一个异构链桥接方案提供者，对波卡生态而言是一个强有力的补充。我们知道在波卡生态内，波卡本身作为中继链存在，其他项目已平行链方式接入波卡，并通过波卡实现生态内的互操作性。但这里有一个隐形的约束条件是大家共享波卡的验证人池，在这个基础上互操作性由波卡中继链提供支持。好比大家是一个国家的人，虽然说到是各自的方言，但是差别不大，所以沟通没啥问题。但是，对于外部的异构链，好像就是讲外语的，除了语言以外，文化背景都不一样的，跟他们沟通就不是波卡想要搞定的了。波卡实际上发过一个 RFP，也就是提出一个问题请项目团队来解决，它的原来思想是在波卡和每一个外部异构链之间搭一座桥，好比是一个翻译的角色，来解决这个问题。所以这个问题的本质是异构链之间的互操作性问题，达尔文就是来解决这个问题的。

我们目前的异构链跨链解决方案是基于轻客户端，我们认为比目前大部分项目采用的半去中心化的托管模式要更去中心化，无需信赖信托机构或者信托机构联盟。并且创新实现了超级轻节点，解决了原来轻节点维护成本太高导致经济不可为继的问题。并且达尔文作为一个桥中心，只需要从外部链搭建一座到达尔文的桥。就可以使每一个链接的链实现互联，而不需要两两之间都要建桥。达尔文针对这个应用改造自己的链，来高效实现这个能力。

所以，对波卡生态而言，每一个项目都可以通过达尔文获得这种能力，真正做到专注自己的业务，大家都需要的异构链跨链需求就我们来搞定了，不用每个人都重复早一次轮子。在此基础上，我们希望可以看到众多单链协议可以实现多链版本的升级。

加入 Substrate Buiders Program 的好处是显而易见的，达尔文是使用 substrate 这套工具开发基本框架的，所以加入这个 program 可以获得更多一手的技术支持，尤其可以和其他项目团队沟通，互相学习。这是非常重要的。

### 4、项目为什么选择 Substrate 技术？目前进展如何？项目在技术开发上遇到什么困难？

我们决定加入波卡生态，最早是因为有关注以太坊，所以对 Dr. Gavin Wood 和 Parity 做的工作也一直比较感兴趣。波卡的技术逻辑难懂，恐怕是因为太快切入细节，被庞大的体系给淹没了。其实如果理解了波卡诞生的使命，了解全貌后通过一条主线去贯穿理解各个部分那就显得一切都合情合理了。过去和 Dr. Gavin Wood 有过很多次交流，所以我想我大概能讲明白这个问题吧。

波卡诞生的初衷是想让各个链各司所职，专注自己的业务特点去设定各种参数，实现自己的个性，但是又能保持一定共性，使得安全性、互操作性能有保证，价值在链接可以自由流动。沿着这个思路下去，就有了让大家能够快速开发链的业务逻辑，不必重复发明轮子，把过往的经验抽象提炼出来变成一个比较容易使用的开发工具，开发者可以迅速搞定底层的各种功能，比如 p2p 协议，共识算法等等，而又可以通过各种功能模块或者叫组件库可以快速拼搭，按需使用。这样就可以有更多精力注重在自己要解决的业务功能上。这就是 substrate 这套工具组诞生的原因。而 Polkadot 本身则作为一个 relay chain 把这些应用链联系起来，让他们可以共享安全池，消息可以互通。

大画面看清楚了，剩下的就是细节问题的理解了。

我们也参与开发和使用过其他的一些区块链开源框架，例如 Bitshares 所使用的 Graphene 框架。相比之下，发现 substrate 这个框架的设计在很多方面是非常具有前瞻性的，包括模块化设计，运行时环境等等。Substrate 框架跟我们团队的匹配度很高，适合快速迭代的要求。我们的团队 Itering 一直致力于区块链应用的大规模落地，因此研究和开发的技术方案主要针对应用落地这个方向，包括跨链技术 Darwinia Relay，分布式秘钥管理服务 DKMS，链上随机数，NFT 可识别性等等，同时，区块链网络又是一个复杂的网络系统，需要有很坚强的底层支撑和安全保障，应对这个问题离不开广泛的开源社区帮助和强有力的合作伙伴。通过一年多的使用与学习，我们认为 Substrate 是非常有棒的一个区块链框架内核，有意思的是，我们的团队也被其主要实现语言 Rust 圈粉。

当然，过程中还是有一些挑战的，我想主要原因是 Substrate 这套工具本身就在快速演进中，所以要跟上节奏需要花费不少精力。我们积极参与社区讨论和建设，也加入了 Substrate Builders Program 和 Web3.0 Bootcamp，与 Parity 的开发者保持紧密沟通。我们开发的 Ruby 实现的 substrate 底层 codec 项目 scale 也获得了 web3 grant。我们通过这些方法来紧跟开发的节奏。

我们期待 Substrate 2.0 可以尽快稳定下来，可以早日投入生产环境，同时，作为开发者我也认同 It’ll be done when it’s done.

### 5、项目方如何合作共赢？预测：谁会获得第一批卡槽？

我来开个玩笑哈，我觉得大家都不用急，这个卡槽都会有。刚刚 Phala 的佟林调侃说 Kusama 是给穷团队，我觉得其实不是，在波卡上的槽位还早着呢。最开始肯定是在 Kusama 上开放槽位，而且它因为是测试网，数量和要求上都会宽松一点。

还有就是我们前一阵和 Web3 Foundation 和 Parity 沟通的时候，了解到波卡对 Kusama 的定位有一些变化，它不是一个随时抛弃的测试链，因为它已经被赋予了一定价值，他们甚至鼓励团队申请 Kusama 的卡槽，所以 Kusama 有点像一个 staging chain，你如果想去申请波卡的槽位，很有可能先去 Kusama 历练一次。但也不一定是这样的路径，有些团队可能就一直待在 Kusama 上，因为它也是有经济价值的，虽然没有波卡那么大，所以在它上面做点事也是很理所当然的。

至于以后第一批能拿到波卡槽位的，我觉得要符合几点，一个是它已经上线稳定一段时间了，经过了安全审计的，并为生态提供了公共价值的，还有就是有较多社区支持的，过早臆测也说不准，大家都有机会先在 Kusama 上玩一下。

## 专业评审团问题

### 问题一（PolkaBase yuanliang 提问）
**我们都知道波卡的最终生态，也就是目前波卡里程碑计划中所说的 2.0 阶段是成为一个 Nested Relaychain，也就是一个可分成的终极链。但其实说近不近说，远不远。中继链的分层，是为了无线可拓展可能性必须实现的功能。根据波卡官网的里程碑。波卡的 2.0 形态，会在预计 2021 年进行工程上的开发，但其实会在 2020 年底可能会开始概念上的验证以及研究跟证明，因此在大家的心目中波卡的分层中继和他的无限拓展性是怎么样的？**

会形成多中心多层级的拓补结构，会有多种垂直具有很强领域特性的子中继链产生，围绕着它各种垂直应用链互联，把业务领域的方方面面做到极致，并且通过上级 relaychain 与其他层级的应用链沟通。成为子级 relaychain 的成本会很低，发布一条应用链成本也会很低，有可能会出现阶段性的应用链甚至是即抛型的应用链。而一些联盟链或者私有链也会接入。

### 问题二（CT 中文 Cookie 提问）
**第二个是问下达尔文，你们最近做了很多 NFT 的内容，圈子里最近也有很多关于 NFT 的有趣尝试，你认为 NFT 会是一个新的赛道么？达尔文之后会在 NFT 上继续做什么样的尝试么？**

我们认为 NFT 是个巨大的市场，传统非标资产的总规模数倍于标准化产品。数字领域里，非标资产外延更被极大扩展，比如游戏道具、门票、巴菲特晚餐权利之类啦，这些东西以后都会在链上交易和流转。

我们现在看到的都是标准数字货币，但是我相信未来 nft 非标资产也会数倍于标准资产。达尔文很重视 NFT 的赛道，我们之前做一款游戏境外星球，来展示游戏中的道具如何转移，包括如何和其他游戏如何互动，在之后我们也计划做跨链 nft 交易所，好比 opensea 升级版，opensea 只能交易 ETH 上的游戏道具，我们想升级为一个跨链版本，支持多生态上的游戏道具，甚至继续拓展到游戏道具外的 NFT 资产，来作为演示一个单链版本的 nft 交易所如何进化到一个多链版本的。

### 问题三（链节点 beimo 提问）
**在今年的跨链赛道上，波卡无疑是受到很多期待的一个项目，可以问问项目方们，你们对波卡上线后的期待是怎样的？另外我们知道很多项目也在等待波卡上线后发力，可以分别说说你们在上线后最重要的一个任务或者目标么？**

波卡上线对市场或者生态来讲可以提振信心，短期里象征意义更大些。它的过程类似 kusama，是个渐进的过程，到大体功能比较完整，比如 parachain 开放，估计还需要几个月。所以，也不要期望一下子看到一座宏伟的建筑，能看到清晰的轮廓就很了不起了。对我们项目团队而言，一个更重要意义在于 substrate 工具组的稳定，这利于我们比较稳定地使用它，我相信各个项目团队都很头疼的是，目前经常要升级工具，而不少升级是破坏性的，这使得团队需要花费很多精力来处理这些升级造成的冲突。它的稳定可以使我们更专注业务逻辑模块的研发。
