# 一、概述

协议族：一系列相关协议的集合

协议族的体系结构或参考模型：指定一个协议族中的各种协议之间的相互关系并划分需要完成的任务的设计

传输出错，要么在网络总中自行修复，要么重新传送

一个可靠的文件传输应用并不关心交付的文件数据块的顺序,最终将所有块无差错地交付并接原来顺序重新组合即可

尽力而为的交付，不确保数据在无错情况下交付，直接舍弃出错的数据报文

OSI七层

| 名称        | 协议                         | 描述/例子                            |
| ----------- | ---------------------------- | ------------------------------------ |
| 7应用层     | HTTP、HTTPS、FTP、POP3、SMTP | 为应用程序提供服务                   |
| 6表示层     |                              | 数据格式转化、数据加密               |
| 5会话层     |                              | 建立、管理和维护会话                 |
| 4传输层     | TCP、UDP、DCCP、SCTP         | 建立、管理和维护端到端的连接         |
| 3网络层     | IP、ICMP、IGMP               | IP选址及路由选择(路由器)             |
| 2数据链路层 |                              | 提供介质访问和链路管理(wifi，以太网) |
| 1物理层     |                              | 物理层                               |

TCP/IP五层

| 名称        | 协议                                  |
| ----------- | ------------------------------------- |
| 5应用层     | HTTP、Telnet、FTP、TFTP、DNS、SMTP    |
| 4传输层     | TCP、UDP、DCCP、SCTP                  |
| 3网络层     | IP、ICMP、RIP、IGMP                   |
| 2数据链路层 | ARP、RARP、PPP、IEEE802.3、CSMA/CD    |
| 1物理层     | FE自协商、Manchester、MLT-3、4A、PAM5 |

TCP/IP中的应用层，在OSI七层中等于应用层+表示层+会话层

网络层(IP)提供了一个不可靠的数据报服务,必须由internet中所有可寻址的系统来实现

传输层(TCP和UDP)为端主机上运行的应用程序提供了端到端服务

TCP提供了带流量控制和拥塞控制的有序、可靠的流交付

除了用于多路分解的端口号和错误检测机制之外, UDP提供的功能基本没有超越IP

与TCP不同, UDP支持组播交付

协议复用：允许多种协议共存于同一基础设施中；允许相同协议对象的多个实例同时存在，且不会被混淆

复用，可发生在不同层，并在每层都有不同类型的标识符,用于确定信息属于哪个协议或信息流

封装，第N层的PDU在第N-1层作为不透明、无需解释的信息对待

第N层的多个对象可通过第N-1层的封装而复用

头部用于在发送时复用数据,接收方基于一个分解标识符(硬件地址、IP、端口号)执行分解，头部也包含一些状态信息(例如一条虚电路是正在建立还是已经建立)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)

理想化的互联网络：端主机实现所有层，路由器实现物/链/网共3层

事实上，由于路由器和交换机通常包括类似于主机的功能(例如管理和建立),因此它们需要实现所有层,即使有些层很少使用

网络层之上的各层使用端到端协议

交换机(网桥) 没有使用互联网络协议的地址格式来编址,并在很大程度上以透明于网络层协议的方式运行。从路由器和端系统的角度来看,交换机或网桥实际是不可见的

32位IPV4，128位IPV6

ICMP，控制消息协议，分为ICMPv4和ICMPv6。

ping和traceroute都使用ICMP

IGMP，组管理协议，采用组播寻址和交付来管理作为组播组成员的主机(一组接收方接收一个特定目的地址的组播流量)

TCP,传输控制协议，会去处理数据包丢失、重复和重新排序等IP层不处理的问题。它采用面向连接(VC)的方式,并且不保留消息边界

UDP，用户数据报协议，允许应用发送数据报并保留消息边界,但不强制实现速率控制或差错控制

TCP，可靠的数据流传输，应用层无需处理数据流

UDP，仅保证数据会发出去，不保证数据能不能到达，可靠性由应用层提供

UDP所做的是提供一套端口号,用于复用、分解数据和校验数据的完整性

DCCP，数据报拥塞控制协议，提供了一种介于TCP和UDP之间的服务类型:面向连接、不可靠的数据报交换,但具有拥塞控制功能

拥塞控制包括发送方控制发送速率的多种技术,以避免流量堵塞整个网络

SCTP，流控制传输协议，用于某些特定系统的传输协议，提供类似于TCP的可靠交付,但不要求严格保持数据的顺序；允许多个数据流逻辑上在同一连接上传输,并提供了一个消息抽象；于在IP网络上携带信令消息,这类似于某些电话网络中的用途

每层都会有一个标识符,允许接收方决定哪些协议或数据流可复用在一起

每层通常也有地址信息,它用于保证一个PDU被交付到正确的地方

TCP/IP协议栈将地址信息和协议分解标识符相结合,以决定一个数据报是否被正确接收,以及哪个实体将会处理该数据报。有几层还会检测数值(例如校验和),以保证内容在传输中没有损坏

以太网帧=48位MAC地址+16位以太网类型字段

IPv4，0x0800

IPv6,0x86DD

ARP,0x0806

# 二、Internet地址

32位IPv4，采用所谓的点分四组或点分十进制表示法。共有2^32个地址

点分四组表示法由四个用点分隔的十进制数组成

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image004.png)

128位IPv6，采用称为块或字段的四个十六进制数,这些被称为块或字段的数由冒号分隔。共有2^128个地址

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image006.png)

IPv6简写法：

一个块中前导的零必须压缩

零的块可以省略,并用符号::代替且一个IPv6地址中符号::只能使用一次

在IPv6格式中嵌入IPv4地址可使用混合符号形式,紧接着IPv4部分的地址块的值为ffff,地址的其余部分使用点分四组格式。IPv6地址::ffff:10.0.0.1可表示IPv4地址10.0.0.1(映射)

IPv6地址的低32位通常采用点分四组表示法。IPv6地址::0102:f001相当于IPv4地址::1.2.240.1

32位IPv4分类寻址

每个单播IP地址都有一个网络部分,用于识别接口使用的IP地址在哪个网络中可被发现；以及一个主机地址,用于识别由网络部分给出的网络中的特定主机。

地址中的一些连续位称为网络号,其余位称为主机号

最初以地址中的头几位分为5类，ABCDE。ABC用于单播

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image008.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image010.png)

| 类   | 网络数       | 主机数        |
| ---- | ------------ | ------------- |
| A    | 2^7=128      | 2^24=16777216 |
| B    | 2^14=16384   | 2^16=65536    |
| C    | 2^21=2097152 | 2^8=256       |

地址块中第一个和最后一个地址，不使用

例如，给某个站点分配一个A类网络号18.0.0.0，其中有2^24个地址可分配给主机，即IPv4的范围为18.0.0.0~18.255.255.255，但实际上，只有2^24-2个地址

 

子网寻址(细分主机号)

子网寻址为IP地址结构增加了一个额外部分,但它没有为地址增加长度

子网寻址提供额外灵活性的代价是增加成本。路由器和主机需要确定地址中的子网部分和其中的主机部分，在出现子网之前,这个信息可直接从一个网络号中获得,只需知道是A类、 B类或C类地址

只有划分子网的网络中的主机和路由器知道子网结构

子网掩码

子网掩码是由一台主机或路由器使用的分配位，以确定如何从一台主机对应IP地址中获得网络和子网信息。

IP子网掩码与对应的IP地址长度相同(IPv4为32位，IPv6为128位)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image012.png)

掩码由路由器和主机使用,以确定一个IP地址的网络/子网部分的结束和主机部分的开始

子网掩码中的一位设为1表示一个IP地址的对应位与一个地址的网络/子网部分的对应位相结合,并将结果作为转发数据报的基础

子网掩码中的一位设为0,表示一个IP地址的对应位作为主机ID的一部分

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image014.png)

与，AND，有0得0

或，OR，有1得1

非，NOT，取反

异或，XOR，同0异1

Internet路由系统其余部分不需要子网掩码

站点之外的路由器做出路由决策只基于地址的网络号部分，不需要子网或主机

子网掩码纯粹是站点内部的局部问题

 

可变长度子网掩码(VLSM)

用于分割一个网络号，使每个子网支持不同数量的主机

在同一站点的不同部分，可将不同长度的子网掩码应用于相同网络号

增加地址配置管理复杂性的同时，提高子网结构的灵活性

主机和路由器的每个接口都需要IP地址和子网掩码来描述

掩码决定了网络拓扑的不同

 

广播地址

广播地址=子网掩码取反 OR 子网中主机地址

按位或运算

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image016.png)

类似于128.32.1.255这种，使用255地址作为目的地的数据报，被称为定向广播

至少在理论上，这种广播可作为一个单独的数据报通过Intenet路由直至达到目标子网，再作为一组广播数据报发送给子网中所有主机

255.255.255.255这个特殊地址被保留为本地网络广播(也被称为有限广播)，不会被路由器转发

虽然路由器可能不转发广播，但子网广播和连接在同一网络中的计算机中的本地网络广播依旧会工作，除非被终端主机明确禁用

IPv6没有任何广播地址

广播地址用于IPv4中，而IPv6仅仅是使用组播地址

IPv6

节点本地：只用于同一计算机中的通信

链路本地：只用于同一网络链路或同一IPv6前缀中的地址

全球性：Internet范围

单播IPv6地址的前提：链路本地和某些全球性的IPv6、接口标识符(IID)

IID长度为64位，由一个网络接口相关的链路层MAC地址形成

除了地址是以二进制000开始的地址以外，IID在所有情况下都作为IPv6的低序位，以此保证IID和IPv6地址在同一网络中有唯一前缀