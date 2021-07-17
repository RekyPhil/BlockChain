1、比特币用到了密码学中的两个内容：一个是哈希函数，另一个是签名。哈希函数具有collision resistance、hiding、puzzle friendly这三个特点。

2、对称加密是用一个密钥，非对称加密是用一对（public key,private key）,用的是接收者的公钥私钥，公钥公布，私钥自己进行解密。公钥私钥的用来签名的。签名用私钥，验证这是我发起的需要用到公钥，

#### 2021.6.28

3、区块包括：block header(它内部有:version、hash of previous block header、merkle root hash、target、nonce) 只有区块头可以用指针连接

​                         block body(它内部有：)

4、轻节点（light node）只保存block header的信息，一般来说，轻节点无法独立验证交易的合法性（例如double spending）。系统中大多数节点是轻节点，全节点（full node）的个数并不是很多。轻节点没有参与区块链的构成和维护，轻节点只是利用区块链信息做一些查询之类的。

5、账本内容需要取得分布式的共识(distributed consensus),简单例子就是分布式的哈希表。

6、FLP impossiblity result ：在一个异步的系里（网络传输没有上限，这叫做异步系统(asynchronous)），网络时延没有上限，即使只有一个成员是有问题的（faulty）那么也不可能取得共识。

The FLP impossibility result for asynchronous deterministic consensus. In a fully asynchronous message-passing distributed system, in which at least one process may have a crash failure, it has been proven in the famous FLP impossibility result that a deterministic algorithm for achieving consensus is impossible.

7、CAP theorem:CAP(C是指consistency，A是指availability，P是指partition tolerance 三个我们想要的性质）该理论是指任何一个分布式系统这三个性质当中最多只能满足两个，不可能三个性质全满足。例如Paxous就满足consistency

In [theoretical computer science](https://en.wikipedia.org/wiki/Theoretical_computer_science), the **CAP theorem**, also named **Brewer's theorem** after computer scientist [Eric Brewer](https://en.wikipedia.org/wiki/Eric_Brewer_(scientist)), states that it is impossible for a [distributed data store](https://en.wikipedia.org/wiki/Distributed_data_store) to simultaneously provide [more than two out of the following three](https://en.wikipedia.org/wiki/Trilemma) guarantees:[[1\]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-Gilbert_Lynch-1)[[2\]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-2)[[3\]](https://en.wikipedia.org/wiki/CAP_theorem#cite_note-3)

- *[Consistency](https://en.wikipedia.org/wiki/Consistency_model)*: Every read receives the most recent write or an error
- *[Availability](https://en.wikipedia.org/wiki/Availability)*: Every request receives a (non-error) response, without the guarantee that it contains the most recent write
- *[Partition tolerance](https://en.wikipedia.org/wiki/Network_partitioning)*: The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes

8、Consensus in BitCoin     H（block header)≤target  

9、coinbase transaction 是比特币系统当中发行新的比特币的唯一方法。其他所有的交易都是讲比特币从一个账户转移到另一个账户。刚开始每个新的区块可以产生50BTC（出块奖励），协议规定每新增21万个区块之后奖励减半。比特币总量2100万。

10、区块链的投票机制的根据算力进行的，是占比不同的。这是可以防范女巫攻击（sybil attack）的。创建账户再多也是不影响算力的。

11、比特币是transaction-based ledger 

12、UTXO:unspend transaction output 

13、出块奖励是第一中奖励机制，transaction fee是另一种奖励机制。

14、每十分钟产生一个新的区块，大约四年会产生21万个区块，也就是每四年出块奖励会减半。

15、Bitcoin is secured by mining.对于一个去中心化的，没有mambership控制的系统来说，挖矿提供了一种凭借算力投票的有效手段。只要大部分算力掌握在诚实的节点手里，系统的安全性就能够得到保障。所以挖矿看似无意义，但对于整个系统的安全性是至关重要的。

16、交易第一次写入区块的时候称one confirmation  ,比特币确认需要6个confirmation的，即6个十分钟，区块链是不可篡改的账本（irrevocabe ledger),越长越不容易篡改。最长合法链。one confirmation这个区块产生之前是zero confirmation.

17、比特币协议中规定：每个区块的大小是有限制的，最多不能超过1兆字节。

18、selfish mining 正常情况下，挖到区块立马发布，而selfish mining是挖到区块先藏着，成为分叉攻击的一种手段；它还可以减少竞争，当别人挖到第一个时，我直接发布前两个，这样别人挖到的那个就作废了，奖励就都是我的，但是这样做依旧存在风险，可能我没有挖到第二个时就已经有人挖到同层次的第一个了，这样就有可能是我挖到的作废。

19、比特币工作原理：比特币工作在应用层（application layer)，他的底层是一个P2POverlay Network

​     application layer：Bitcoin Block chain 

​     network layer: P2P Overlay Network

比特币的P2P网络是非常简单的，所有节点都是对等的。它没有super node和master node。想要加入必须知道一个种子节点（seednode）它会告诉你它知道的网络中的其他节点。节点之间是通过TCP来通信的。这样有利于穿透防火墙，离开就直接离开，别的节点没有听到你的消息，过一段时间就会把你删掉。比特币设计原理是简单而不是高效。simple,robust,but not efficient.

20、消息传播在网络中采取flooding的模式，第一次接受转发，第二次不转发。

21、比特币系统中每个节点维护一个等待上链的交易的集合。

#### 2021.6.29

22、比特币中每隔2016个区块调整一次目标域值（target）大约每两个星期调整一下。调整目标阈值方法：target=target*actual time / expected time

注释：actual time是time spent mining the last 2016 blocks，  expected time 是理论产生2016个区块的时间（14周），上次产生2016个区块时间长则需要降低产生区块的难度，即增大目标阈值，公式后边的分式大于一时目标阈值就变大了，反之亦然。但是分式比值范围是（1/4，4） 

23、全节点：一直在线；在本地硬盘上维护完整的区块信息；在内存里维护UTXO集合，以便快速检验交易的正确性；监听比特币网络上的交易信息，验证每个交易的合法性；决定哪些交易会被打包到区块里；监听别的矿工挖出来的区块，验证其合法性；挖矿（决定沿着哪条链挖下去；当出现等长的分叉的时候，选择哪一个分叉）

24、轻节点：不是一直在线；不用保存整个区块链，只要保存每个区块的区块头；不用保存全部交易，只要保存与自己相关的交易；无法验证大多数交易的合法性，只能检验与自己相关的交易的合法性；无法检测网上发布的区块的正确性；可以验证挖矿的难度；只能检测哪个是最长链，不知道哪个是最长合法链。

#### 2021.6.30

25、挖矿设备：CPU 到GPU,GPU是为了通用并行计算而设计的，用来挖矿的时候仍然有部分部件闲置，比如说用于浮点数运算的部件，比特币的运算只是用到了整数的运算。现在更多用ASIC芯片挖矿，ASIC专用集成电路（Application Specific Integrated Circuit),这是专门为了比特币挖矿设计的芯片。

26、一个芯片只能为一个加密货币去挖矿，除非两种货币的mining puzzle一致可以通用，所以某些新发货币就会采用某种已有货币的mining puzzle，这种现象称为merge mining 。芯片研发周期较长，比特币的芯片研发用了一年时间。

27、input script 要给出一些签名（数目不定）及一段序列化的redeemScript .验证分如下两步：（1) 验证序列化的redeemScript 是否与output script中的哈希值匹配？（2）反序列化并执行redeemScript ,验证input script 中给出的签名是否正确？

28、redeem Script 的形式：P2PK形式；P2PKH形式；多重签名形式。

29、fork。一种是差不多时间产生两个区块。它们都可以继续产生，这种称为state fork。forking attack就属于state fork，它还叫做deliberate fork 。

另一种是因协议升级修改产生的分叉，大家用的协议不同而导致的，这种叫做protocol fork 根据对协议修改的内容的不同，分为hard fork 和 soft fork。

30、hard fork 最常见的就是block size limit,只要协议不更新，小节点就不会消失。

#### 2021.7.1

31、soft fork，如果我们对比特币协议加一些限制，加上限制之后原本合法的交易或者区块在新的协议中变得不合法了，这将引起soft fork。soft fork是临时性的

soft fork就是一个陪跑的，无法决定前进路线。

32、实际中出现软分叉的情况:一个情况就是给某些目前协议中没有规定的余语赋予他们一些新的规则，例如coinbase。

33、比特币历史上著名的软分叉是P2SH（pay to script hash)

34、问题汇总

问题一：给某人转账，但对方未连接在bitcoin网络上会出现什么情况？

这时候不需要接收者在线，转账交易不过是在区块链上记录一下把我账户上的bitcoin转到对方账户上，对方是否连入bitcoin网络是没有影响的

问题二:假设某个全节点收到了某个转账交易，有没有可能转账交易中接受者的收款地址是这个节点从来没听说过的？

这是可能的，bitcoin账户在创建的时候是不需要通知其他人，自己产生一个公私钥对就可以了，第一次收到钱以后其他节点才会知道这个收钱地址的存在。

问题三：如果账户私钥丢失，该怎么办？

那就没了，就直接没了！！！去中心化的数字货币一般都无法像现实中那样申诉。加密货币的交易所是需要身份证明的，我把bitcoin保存在交易所其实私钥实在交易所的，交易所又是中心化的，我在交易所是有一套账户的，该账户密码丢失没事，哎，就是没事！

交易所、数字钱包等是缺乏监管的，曾经出现过交易所被黑的情况，著名的Mt.Gox ,这曾经是世界上最大的比特币交易所，交易量占全球交易量的70%，这门头沟在日本····在日本，懂我意思没有。相比之下冷钱包和硬件钱包是相对安全的。

问题四：如果私钥泄露了怎么办出现一些可疑的交易该怎么办？

把钱转到安全账户，越快越好！！！

问题五：如果转账写错地址怎么办？

没有办法取消已经发布的交易，就跟充错话费一样，不知道对方是谁，往回要有可能要的回，也有可能要不回来还挨一顿骂。

问题六：是否存在头结果的情况，换句话说，你怎么知道是谁最先找到这个结果的？

发布的区块里有一个coinbase tx,里面有一个地址，是挖到这个的矿工的地址，想偷别人成果就必须修改地址，但是改了地址就改变了挖到的结果的根哈希值，也就不能在用了。每个矿工挖到的这个lance是和他的收款地址绑定在一起的。

问题七;交易费怎么算？

total inputs- total outputs=交易费，交易费给谁不需要提前知道，哪个矿工挖到矿了就可以自行计算所得交易费。

35、破坏比特币的匿名性方式一：虽然每个人可以产生多个公私钥对（多个账户），交易也可以有多个输入多个输出，但是钱包软件进行交易的方式相对固定，每次交易也会产生一个找零账户（例如输入是4和5 ，输出是6和3，那么4 5 3对应的就是同一个人的账户），即交易是可以让个人拥有的多个账户产生某些联系的。

36、破坏比特币的匿名性方式二：这个地址账户跟创建人在现实社会中的真实身份也可能产生关联。

虚拟货币bitcoin跟实体世界发生联系的时候就有可能泄露身份，资金转入和转出就是最明显的例子。

37、零知识证明（ Zero-Knowledge Proof）：一方（证明者）向另一方（验证者）证明一个称述是正确的，而无需透漏除该陈述是正确的外的任何信息。 Zero-Knowledge Proof的数学基础是同态隐藏，其特点有三个：一是输入不同，输出也不同，即不存在碰撞；二是给定加密函数值，很难反推出原输入值，即不可逆性，类似与哈希函数的hiding property ；三是对加密之后的函数值进行某些代数运算，等价于对这些输入进行相应的代数运算后在加密（同态加法；同态乘法；扩展多项式）

同态加法：加密值的和=和的加密

同态乘法：加密值的积=积的加密

扩展多项式由以上两个扩展得到。

38、盲签方法

39、零币和零钞专门为匿名性设计的货币，其在协议层就融合了匿名化处理，其匿名属性来自密码学保证。

零币（zerocoin)系统中存在基础币和零币，通过基础币和零币的来回转换，消除旧地址和新地址的关联性，其原理类似于混币服务

零钞（zerocash)系统使用zk-SNARKs协议，不依赖一种基础币，区块链中只记录交易第额存在性和矿工用来检验正常运行所需要关键属性的证明。区块链上既不显示交易地址也不显示交易金额，所有交易通过零知识验证的方式进行。干坏事专用币？

但是在与现实进行交互的时候依旧可能暴漏信息。

40、问题：指针一般在本地可用，在非本地就不适应了，那哈希指针是怎样做到在网络中传输并且可用的？

所谓哈希指针并非指针，实际系统中用的时候只有哈希，没有指针。或者可以理解为哈希值就是指针。哈希指针的性质保证了整个区块链的内容是不可篡改的。

41、区块恋，这种截断私钥的做法会减低账户的安全性，私钥256位。对于多个人的共享账户，不要用截断私钥的方法，可以选择多重签名（MULTISIG)。多重签名还具有其他灵活性，比如任意n个私钥中只要给出m个就可以打开账户。

42、UTXO里面的死钱对矿工是不友好的，很普遍。

43、为什么bitcoin系统能够绕过分布式共识中的那些不可能结论？

严格的说，bitcoin并没有取得真正意义下的共识，因为取得的共识随时都有可能被推翻，比如出现了分叉攻击

#### 知识改变命运，但是对知识的一知半解有可能使你的命运变得更差。

44、bitcoin的稀缺性：一是早期挖矿难度低很容易就挖到。二是早期出块奖励比较大

