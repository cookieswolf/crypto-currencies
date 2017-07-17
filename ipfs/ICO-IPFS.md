ICO-IPFS(Filecoin)—下一代分布式网络协议
=====

![ipfs-logo](../logo/ipfs-logo.png)

项目介绍
----
* 星际文件系统（简称IPFS）是一个去中心化的、点对点的超媒体分发协议，是由 Protocol Labs 从2014年开始开发的开源项目。IPFS用基于内容寻址替代传统的域名寻址，用户不需要关心服务器的位置，不用考虑文件存储的名字和路径。将文件放到IPFS节点中，将会得到基于其内容计算出的唯一加密哈希值。哈希值直接反映文件的内容，哪怕只修改一比特，哈希值也会完全不同。当IPFS被请求一个文件哈希时，它会使用一个分布式哈希表找到文件所在的节点，取回文件并验证文件数据。

市场关注度（数据截止2017/6/29）
-----
* 推特：6187
* github：7717
* 官网全球排名：104823

代币介绍
-----
* IPFS团队准备把称作 Filecoin 的数字货币融入 IPFS，这个数字货币的首要用途是：奖励网络中成功存储数据的矿工。与比特币不同的是，比特币依靠算力工作量证明，而 Filecoin 的工作量证明还包括可恢复证明部分，这需要节点证明它们存储了某一个特定的文件。网络会通过奖励数字币的方式激励节点尽可能多的存储全网络的数据，货币可以在交易中流通，也可以兑换成其他的货币。

项目分析
-----

* IPFS提供了具有内容寻址的超链接和高吞吐量的内容寻址存储模型。这形成了广义的Merkle有向无环图。IPFS没有单点故障，节点不需要相互信任。分布式内容传递可以节省带宽，并防止HTTP所遇到的DDoS攻击。

* 用户可以将本地文件添加到IPFS文件系统，使其可供世界各地使用。文件通过唯一哈希值来进行标识。如果更改文件，哈希值将变得完全不同。
IPFS提供了一个友好的WEB访问接口，用户可以通过本机的 IPFS-HTTP 网关(http://localhost:5001/ipfs/) 或者公共的网关(http://ipfs.io/) 获取IPFS网络中的内容，也可以通过特定的浏览器或者插件通过ipfs:/or fs:/的方式直接获取内容。

* IPFS弥补了现有区块链系统在文件存储方面的短板，将IPFS的永久文件存储和区块链的不可篡改、时间戳证明特性结合，非常适合应用于保护版权、身份证明、来源证明等方面。

* HTTP存在的问题
 * HTTP低效且昂贵，HTTP一次只能从一个服务器获取文件。IPFS没有存储上的限制，大文件会被切分成小的分块，下载的时候可以从多个服务器同时获取。IPFS通过计算机网络分散存储数据，而不是由中央服务器存储数据。在视频分发领域可节省60%的带宽，IPFS让分发大文件变得可能且高效。
 * HTTP过度依赖主干网络，内容容易遭到审查和封锁，像美国国家安全局这样的组织，只需要在几个点上拦截通信来进行监视，对政府来说，阻止网站访问这些高度集中化的资源变得容易,让主干网络存在很多可靠性的问题。主干网络有时还会被损坏，或者出现路由表失控，其后果可能是非常严重。Internet骨干网并不健全，其很容易被攻击，同时一些重要的光纤线路被切断时服务很容易遭受影响。

* IPFS如何工作

 * IPFS从根本上改变了用户搜索的方式。通过IPFS，用户搜索的是内容。通过HTTP浏览器搜索文件的时候，首先找到服务器的位置（IP地址），然后使用路径名称在服务器上查找文件。按照这个设计，只有文件所有者可以判断这是否是用户要找的文件。此时，必须保证托管者不会通过移除文件或者关闭服务器而对文件做任何更改。

 * 当文件被添加到IPFS节点上，它得到一个新的名字。这个名字实际上是一个加密哈希，它是从文件内容中被计算出来。通过加密保证该哈希始终只表示该文件的内容。哪怕只在文件中修改一个比特的数据，哈希都会完全不同。

 * 当下一步向IPFS分布式网络询问哈希的时候，它通过使用一个分布式哈希表，可以快速（在一个拥有10,000,000个节点的网络中只需要20跳）地找到拥有数据的节点，从而检索该数据，并使用哈希验证这是否是正确的数据。

 * IPFS是通用的，并且存储限制很少。它服务的文件可大可小，对于一些大的文件，它会自动将其切割为一些小块，使IPFS节点不仅仅可以像HTTP一样从一台服务器上下载文件，而且可以从数百台服务器上进行同步下载。IPFS网络是一个细粒度的、不可靠的、分布式的、易联合的内容分发网络（Content Delivery Network , CDN）。对于所有数据类型都是很有用的，包括图像、视频流、分布式数据库、操作系统、blockchains等，而对于IPFS来说，最重要的是静态web网站。

 * IPFS文件也可以是特殊的IPFS目录对象，它允许用户使用人类可读的文件名，透明地链接到其他IPFS哈希。用户可以通过默认方式加载目录中的index.html，这也是标准的HTTP服务器采用的方式。使用目录对象，IPFS可允许用户采用完全相同的方式生成静态网站。将web网站添加到IPFS节点中只需要一个简单的命令：ipfs add -r yoursitedirectory。在此之后，用户可以从任何IPFS节点访问，而不需要链接到HTML上的任何哈希。

 * IPFS不需要每个节点存储所有发布到IPFS上的内容。相反，每个节点只存储自己想要的数据。如果每个节点托管一点数据，所有数据通过累积就提供了比任何集中式HTTP更多的空间、带宽和可用性。分布式网络将很快成为世界上最快、最可用、以及最大的数据存储。没有人有能力关闭所有的节点，所以数据永远不会丢失。

 * 从其他IPFS节点复制、存储web网站很容易。它只需要一条命令以及网站的哈希值：ipfs pin add -r QmcKi2ae3uGb1kBg1yBpsuwoVqfmcByNdMiZ2pukxyLWD8。IPFS负责剩下的所有工作。

 * IPFS哈希代表不可变的数据，这意味着它们是不能被更改的，否则会导致哈希值的变更。这是一件好事，因为它鼓励数据的持久性，但我们仍然需要一种方法来找到最新的IPFS哈希以表示你的网站。IPFS通过一种特殊的功能来实现，即IPNS。IPNS允许用户使用一个私有密钥来对IPFS哈希附加一个引用，使用一个公共密钥哈希（简称pubkeyhash）表示你的网站的最新版本。如果用户使用过比特币，可能会对此比较熟悉，一个比特币地址也是一个pubkeyhash。如果该链接不起作用，不用担心。能够通过更改pubkeyhash所指向的内容，而pubkeyhash却永远保持不变。这样，网站的更新问题就得到了解决。

 * IPFS/ IPNS哈希是一些很大的、难看的字符串，而且不容易记住。所以IPFS允许用户使用现有的域名系统（Domain Name System, DNS）来为IPFS/IPNS内容提供人类可读的链接。它允许用户通过在域名服务器上将哈希插入TXT记录来实现这一点（如果你方便使用一个命令行，运行如下命令：dig TXT ipfs.git.sexy）。

* 未来，IPFS已计划支持Namecoin，它理论上可以用来创建一个完全去中心化的、分布式的web，整个环境中不需要一个中心控制。没有ICANN，没有中央服务器，没有“权威”证书，也没有瓶颈。这听起来很疯狂。可现实的确疯狂。因为使用今天的技术这是完全可以实现的！

* 通过一个HTTP网关，IPFS可以实现从HTTP到IPFS的过度，浏览器可以完全实现IPFS之前，现在已经允许当前的web浏览器访问IPFS。用户很快就可以切换到IPFS，完成web网站的存储、分发和服务。

* 到目前为止，IPFS还处于实验阶段。当网站更新的时候，Neocities将每天发布一个哈希IPFS。这个哈希将指向该网站的最新版本，并通过IPFS HTTP网关可以访问。因为每次更新IPFS哈希都会变更，这也能够为所有网站提供一个存档历史记录。

* 从长期来看，如果一切顺利的话，Neocities希望使用IPFS存储所有的网站，并为每个网站发布IPNS键。这将让用户可以不依赖于Neocities而进行内容发布。如果构建得当，即使Neocities不存在了，用户仍然可以更新自己的网站。通过有效地去除网站对Neocities中央服务器的依赖，这种集中控制环境将被永久性打破。IPFS真正能够替代HTTP可能还需要一段时间，而且也有很多工作要做。
   
 |网站|链接|
 |----|----|
 |官网|https://ipfs.io/|
 |twitter|http://twitter.com/ipfsbot|
 |Github|https://github.com/ipfs/ipfs|
|IPFS文档|https://ipfs.io/docs/|

* 官方暂未公布ICO信息，关于ICO的详细方案，我们将继续跟踪。请大家继续关注小密圈：加密货币投资分析（ID：61818889）



