#### 2021.7.2

1、以太坊（Ethereum)是区块链2.0，针对bitcoin中存在的一些问题进行了改进。比如说出块时间，bitcoin出块时间是十分钟，有人觉得时间太长了，影响了响应时间，所以以太坊中出块时间大幅度降低到十几秒，为了适应这种新的出块时间，以太坊还设计了一套基于GOSE协议的共识机制；第二个改变就是挖矿使用的mining  puzzle ，比特币的mining  puzzle是计算密集型的，比拼的是计算哈希值的算力，这样造成一个结果就是挖矿设备的专业化（CPU到GPU在到ASIC芯片）而以太坊设计的mining  puzzle就对内存要求比较高，叫做memory hard.这样设计在一定程度上就限制了ASIC芯片的使用（ASIC resistance）再比如用权益证明(proof of stake) 来代替工作量证明（POW:proof of work）.权益证明就是用类似股份投票的形式来决定下一个区块怎么产生。除此之外以太坊还增加了对智能合约的支持（smart contract）.

2、智能合约：智能合约是运行在区块链上的一段代码，代码的逻辑就定义了合约的内容。

3、bitcoin：decentralized currency

4、以太坊（Ethereum)：decentralized  contract

5、账户：bitcoin中使用的是基于交易的账本；Ethereum是基于账户的模型（account-based ledger),这种模型可以抵御double spending（付款人不诚实）.但是存在replay attack（收钱人不诚实）。

6、replay attack的解决方法可以加一个交易次数（nonce）

7、Ethereum有两类用户账号，一是externally owned account(外部账户)，另一类是smart contract account (合约账户)，合约账户不能主动发起一个交易，所有的交易只能由外部账户发起。

8、MPT（Merkle Patricia tree )，Ethereum用的是modified  Merkle Patricia tree

9、Merkle tree和binary tree的区别：把普通指针换成了哈希指针。

10、区块链和链表的区别是把普通指针换成了哈希指针。

11、状态数中保存的是（key ,value ).value账户状态怎么存储在状态数当中的呢？实际上它是要经过一个序列化的过程，用RLP 这个编码做序列化，之后在存储。

12、RLP:Recursive Length Profix是一种做序列化的方法，特点是简单。它只支持一种类型：nested array of bytes(字符数组)，可以嵌套。Ethereum中的整数、比较复杂的哈希表等等所有最后都要变成nested array of bytes。

13、交易树用来证明某个交易被打包到某个区块里了，向轻节点提供这样的 Merkle proof。收据树也是一样的。

14、Ethereum还支持更加复杂的操作，比如说查找过去十天内与某个智能合约相关的交易，查找方法：一种操作是把过去十天产生的所有区块全部扫描一遍，看看由哪些交易是和这个智能合约相关的，这种方法复杂度较高。另一种就是Ethereum引入了bloom filter这个数据结构，它可以支持比较高效的查找某个元素是否在一个比较大的集合里面。一般的简单bloom filter不支持删除操作。

15、Ethereum的运行过程可以看成交易驱动的状态机（transaction-driven state machine) 。这个状态机的状态就是所有账户的状态，就是状态树中包含的内容。交易就是每次发布交易区块里的那些交易，通过驱执行这些交易能够驱动系统从当前的状态转移到下一个状态。

16、bitcoin和Ethereum都是运行在应用层的共识协议。底层是一个P2P的overlay network.出块时间短可能导致临时性分叉多，成为常态。

17、orphan block(stale block)在Ethereum中叫做uncle block,它也有出块奖励，大约最长合法链下一次出块奖励的是7/8，一个区块最多可以包括两个uncle block。

18、当uncle block出现第三个怎么办？

19、为了商业利益，可能出现下一区块故意不认uncle block的情况，就相当于换血，杀敌一千自损八百。1/32出块奖励换7/8出块奖励。解决思路就是模糊uncle block的定义，不仅可以差一辈，差几辈都叫uncle block，都可以包含进来获得额外奖励，uncle block也获得出块奖励。uncle block最多相聚7代，而且每多差一代，出块奖励会降低1/8，即合法的uncle block只有6个。uncle reward 会随着隔着的代数的增加而减少。at most seven generation 

20、uncle block上的交易不会在主链上执行，uncle block和主链上交易可能由冲突。而且就根本不检查uncle block上的交易。只检查uncle block的合法性。uncle block上的交易也不会执行。

21、uncle block后面也出现了后续区块是没有用的，否则forking attack就变得很容易了。而且forking attack成本极低，打得过就打，打不过就加入。

22、所以Ethereum规定，只有分叉后的第一个uncle block可以获得分叉奖励。

23、LiteCoin 就是基于scrypt算法的模型，曾经是第二大数字货币。这个算法就增加在运算过程中对内存的访问需求。

24、Ethereum 用的是一大一小两个数据集，小的是一个16M的cashe ，大的是1G的dataset，叫DAG。大的是从小的cashe生成出来的。轻节点保存小的，只有挖矿的矿工才需要保存大的数据集。其算法叫ethash。

25、Ethereum 发展分为四个阶段，分别是Frontier、Homestead、Metropolis(它又分为两个小阶段分别是Byzantium和Constantinople)、Serenity。难度炸弹的回调发生在Byzantium这个子阶段，在EIP(Ethereum Improvement Proposal)中决定，同时把block reward从5个ETH降低到3个ETH。

26、Proof of stake（权益证明）

Ethereum 中用的权益证明协议用的时Casper the Friendly Finality Gadget(FFG),它在过渡阶段也是要和工作量证明混合使用的，为工作量证明提供 Finality。单纯基于挖矿的交易是有可能回滚的。

27、Casper 协议工作过程：引入了一个概念Validator,要想成为Validator，必须投入一定量的Ether作为保障金，保障金会被系统锁定，Validator的职责是推动系统达成共识，投票决定哪条链是最长合法链，投票的权重取决于保障金的多少。具体做法类似two-phae commit，第一轮投票是Prepare Message，第二轮投票的Commit Message,每一轮投票都要超过2/3才算通过。实际系统中不在区分这两个第几轮，而且每50个区块为一epoch，每一个epoch对于上一个epoch来说是Commit Message，对于下一轮来说的Prepare Message。

28、智能合约的账户保存了合约当前的运行状态，包括balance当前余额、  nonce交易次数、  code合约代码、  storage存储，数据结构是一颗MPT。

Solidity是智能合约最常用的语言，语法上与Javascript很接近。

智能合约调用另一个合约中的函数有两种调用方式：直接调用；使用address类型的call（）函数。

29、智能合约的创建和运行：

智能合约的代码写完后，要编译成bytecode

创建合约：外部账户发起一个转账交易到0x0的地址,注：转账金额为0，但是要支付交易费；合约的代码放在date域里

智能合约运行在EVM上

以太坊是一个交易驱动的状态机：调用智能合约的交易发布在区块链上后，每个矿工都会执行这个交易，从当前状态确定性地转移带下一个状态。

30、汽油费（gas fee)：

智能合约是个Turning-complete Programming Model

执行合约中的指令要收取汽油费，由发起交易的人来支付

EVM中不同指令消耗的汽油费不一样，简单的指令很便宜，复杂的或者需要存储状态的指令就很贵。

汽油费会先扣掉，多退少滚，对于公共资源的访问是不需要汽油费的

31、错误处理：

智能合约中不存在自定义的try-catch

一旦遇到异常，除特殊情况外，本次执行操作全部回滚

可以抛出错误的语句：assert(bool condition):如果条件不满足就抛出，用于内部错误；require（bool condition）：如果条件不满足就抛出，用于输入或者外部组件引起的错误；revert（）：终止运行并回滚状态变动。

32、嵌套调用：

智能合约的执行具有原子性：执行过程中出现错误会导致回滚

嵌套调用是指一个合约调用另一个合约中的函数

嵌套调用是否会出发连锁式回滚？如果被调用的合约执行过程中发生异常，会不会导致发起调用的这个合约也跟着一起回滚？有些调用方法会引起连锁式回滚，有些则不会。

一个合约直接向另一个合约里转账，没有指明调用哪个函数，仍然会引起嵌套调用。

33、发布到区块链上的交易是不是都是成功执行的？不一定

如果智能合约执行过程中出现了错误，要不要也发布到区块链上？不会

智能合约是不是支持多线程多核并行处理？Solidity没有支持多线程的语句，多线程的问题在于多个核对内存访问顺序不同，执行结果有可能是不确定的，所以不支持。

34、DAO:Decentralized  Autonomous  Organization 

​        DAC:Decentralized  Autonomous   Corporation

35、反思！

smart  contract  is  anything  but smart.

Irrevocability  is  a  double edged  sword .

Nothing  is  irrevocable 

开源并不一定安全，并没有多数人去看源代码

区中心化并不是全自动化，不是让机器决定一切，不能有人为的干预，也不是已经制定的规则就不能修改，而是对规则的修改要用去中心化的思想来完成。

decentralized不等于distributed,去中心化和分布式不是等价的，一个去中心化的系统必然是分布式的。分布式的平台上可以运行中心化的应用，也可以运行去中心化的应用

