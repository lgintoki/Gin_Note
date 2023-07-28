# #端口分类(物理/逻辑)

在网络技术中，端口（Port）大致有两种意思：

## ##(1)物理意义上的端口

```
比如，ADSL Modem、集线器、交换机、路由器用于连接其他网络设备的接口，如RJ-45端口、SC端口等等。　
```

　　

## ##(2)逻辑意义上的端口

```
一般是指TCP/IP协议中的端口，端口号的范围从0到65535，比如用于浏览网页服务的80端口，用于FTP服务的21端口等等。
```

```
以下为逻辑意义上的端口。
```

# #端口分类(按范围)

## ##(1)公共端口(Well-KnownPorts)

```
0~1023

也称为常用端口

紧密绑定一些特定的服务
```

## ##(2)注册端口(RegisteredPorts)

```
1024~49151

松散绑定于一些服务，也可以说有许多服务绑定于这些端口
```

## ##(3)动态 和/或 私有端口(DynamicandPorts/PrivatePorts)

```
49152~65535

理论上，不应把常用服务分配在这些端口上

一些特殊的程序，木马常用这些端口
```

# #常用端口

```
0 reserved
1 tcpmux(lrix  默认的无密账号：IP，GUESTUUCP，NUUCP，DEMOS，TUTOR，DIAG，OUTFOBOX)
7 echo(x.x.x.0   x.x.x.255)
19 character generator(UDP回应垃圾字符包，TCP发送垃圾字符数据流直至连接关闭     DOS攻击)
21 ftp
22 ssh
23 telnet(远程登录  得到运行的操作系统  得到密码)
25 smtp(传递SPAM   连接到高带宽的E-Mail服务器并传递信息)
31 MSG anthentication
42 WINS Reolication
53 DNS(区域传递(TCP)  欺骗DNS(UDP)  隐藏其他通信)
67 Bootstrap Protocol Server(引导程序协议服务端)
68 Bootstrap Protocol Client(引导程序协议客户端)
注：67和68端口可以进行中间人攻击  客户端向68广播请求配置，服务器向67广播回应请求
69 TFTP (类似于FTP，但不具有复杂的交互存取接口和认证控制  由于错误配置而被窃取、写入文件)
79 Finger Server(查询远程主机在线用户信息，获取更多主机信息) 
80 HTTP 
99 Mrtagram Relay 
102 Message Transfer Agent over TCP/IP 消息传输代理
109 POP3(缓冲区溢出)
110 SUN公司所有RPC服务端口
113  Authentication Service 用于鉴别TCP连接的用户
119 NEWS新闻组传输协议
135 Location Service (DOS攻击)
137、138、139 NetBios Name Service 
137\138用于UDP，网上邻居传输文件
139 用于windows文件和打印机共享以及SAMBA
143 IMAP2(缓冲区溢出)
161 SNMP(数据存储于数据库中，可以尝试爆破)
177 X Display Manager Control Protocol
389 LDAP、ILS 轻型目录访问协议
443 https
513 Login remote Login(入侵，信息收集)

SqlServer 1433

Oracle 1521

MySQL 3306

Tomcat 8080

fiddler 8888
```

# #端口大全(详)

**0**

```
端口：0 
服务：Reserved 
说明：通常用于分析操作系统。这一方法能够工作是因为在一些系统中“0”是无效端口，当你试图使用通常的闭合端口连接它时将产生不同的结果。一种典型的扫描，使用IP地址为0.0.0.0，设置ACK位并在以太网层广播。 
```

 **1**

```
端口：1 
服务：tcpmux 
说明：这显示有人在寻找SGI Irix机器。Irix是实现tcpmux的主要提供者，默认情况下tcpmux在这种系统中被打开。Irix机器在发布是含有几个默认的无密码的帐户，如：IP、GUEST UUCP、NUUCP、DEMOS、TUTOR、DIAG、OUTOFBOX等。许多管理员在安装后忘记删除这些帐户。因此HACKER在INTERNET上搜索tcpmux并利用这些帐户。
```

**7** 

```
端口：7 
服务：Echo 
说明：能看到许多人搜索Fraggle放大器时，发送到X.X.X.0和X.X.X.255的信息。 
```

**19**

```
端口：19 
服务：Character Generator 
说明：这是一种仅仅发送字符的服务。UDP版本将会在收到UDP包后回应含有垃圾字符的包。TCP连接时会发送含有垃圾字符的数据流直到连接关闭。HACKER利用IP欺骗可以发动DoS攻击。伪造两个chargen服务器之间的UDP包。同样Fraggle DoS攻击向目标地址的这个端口广播一个带有伪造受害者IP的数据包，受害者为了回应这些数据而过载。
```

**21**

```
端口：21 
服务：FTP 
说明：FTP服务器所开放的端口，用于上传、下载。最常见的攻击者用于寻找打开anonymous的FTP服务器的方法。这些服务器带有可读写的目录。木马Doly Trojan、Fore、Invisible FTP、WebEx、WinCrash和Blade Runner所开放的端口。
```

**22**

```
端口：22 
服务：ssh 
说明：PcAnywhere建立的TCP和这一端口的连接可能是为了寻找ssh。这一服务有许多弱点，如果配置成特定的模式，许多使用RSAREF库的版本就会有不少的漏洞存在。
```

**23**

```
端口：23 
服务：Telnet 
说明：远程登录，入侵者在搜索远程登录UNIX的服务。大多数情况下扫描这一端口是为了找到机器运行的操作系统。还有使用其他技术，入侵者也会找到密码。木马Tiny Telnet Server就开放这个端口。
```

**25**

```
端口：25 
服务：SMTP 
说明：SMTP服务器所开放的端口，用于发送邮件。入侵者寻找SMTP服务器是为了传递他们的SPAM。入侵者的帐户被关闭，他们需要连接到高带宽的E-MAIL服务器上，将简单的信息传递到不同的地址。木马Antigen、Email Password Sender、Haebu Coceda、Shtrilitz Stealth、WinPC、WinSpy都开放这个端口。
```

**31**

```
端口：31 
服务：MSG Authentication 
说明：木马Master Paradise、Hackers Paradise开放此端口。
```

**42** 

```
端口：42 
服务：WINS Replication 
说明：WINS复制
```

**53**

```
端口：53 
服务：Domain Name Server（DNS） 
说明：DNS服务器所开放的端口，入侵者可能是试图进行区域传递（TCP），欺骗DNS（UDP）或隐藏其他的通信。因此防火墙常常过滤或记录此端口。
```

**67**

```
端口：67 
服务：Bootstrap Protocol Server(引导程序协议服务端)
说明：通过DSL和Cable modem的防火墙常会看见大量发送到广播地址255.255.255.255的数据。这些机器在向DHCP服务器请求一个地址。HACKER常进入它们，分配一个地址把自己作为局部路由器而发起大量中间人（man-in-middle）攻击。客户端向68端口广播请求配置，服务器向67端口广播回应请求。这种回应使用广播是因为客户端还不知道可以发送的IP地址。
```

```
DHCP (UDP ports 67 and 68)
```

**68**

```
端口：68 
服务：Bootstrap Protocol Client(引导程序协议客户端)
```

**69**

```
端口：69 
服务：Trival File Transfer Protocol(TFTP)
说明：类似于FTP，但不具有复杂的交互存取接口和认证控制。许多服务器与bootp一起提供这项服务，便于从系统下载启动代码。但是它们常常由于错误配置而使入侵者能从系统中窃取任何文件。它们也可用于系统写入文件。 
```

 **79**

```
端口：79 
服务：Finger 
Server 
说明：入侵者用于获得用户信息，查询操作系统，探测已知的缓冲区溢出错误，回应从自己机器到其他机器Finger扫描。
```

**80**

```
端口：80 
服务：HTTP 
说明：用于网页浏览。木马Executor开放此端口。
```

**99** 

```
端口：99 
服务：Metagram Relay 
说明：后门程序ncx99开放此端口。
```

**102** 

```
端口：102 
服务：Message transfer agent(MTA)-X.400 over TCP/IP 
说明：消息传输代理。
```

**109** 

```
端口：109 
服务：Post Office Protocol -Version3 
说明：POP3服务器开放此端口，用于接收邮件，客户端访问服务器端的邮件服务。POP3服务有许多公认的弱点。关于用户名和密码交换缓冲区溢出的弱点至少有20个，这意味着入侵者可以在真正登陆前进入系统。成功登陆后还有其他缓冲区溢出错误。
```

**110**

```
端口：110 
服务：SUN公司的RPC服务所有端口 
说明：常见RPC服务有rpc.mountd、NFS、rpc.statd、rpc.csmd、rpc.ttybd、amd等
```

**113**

```
端口：113 
服务：Authentication Service 
说明：这是一个许多计算机上运行的协议，用于鉴别TCP连接的用户。使用标准的这种服务可以获得许多计算机的信息。但是它可作为许多服务的记录器，尤其是FTP、POP、IMAP、SMTP和IRC等服务。通常如果有许多客户通过防火墙访问这些服务，将会看到许多这个端口的连接请求。记住，如果阻断这个端口客户端会感觉到在防火墙另一边与E-MAIL服务器的缓慢连接。许多防火墙支持TCP连接的阻断过程中发回RST。这将会停止缓慢的连接。
```

**119**

```
端口：119 
服务：Network News Transfer Protocol 
说明：NEWS新闻组传输协议，承载USENET通信。这个端口的连接通常是人们在寻找USENET服务器。多数ISP限制，只有他们的客户才能访问他们的新闻组服务器。打开新闻组服务器将允许发/读任何人的帖子，访问被限制的新闻组服务器，匿名发帖或发送SPAM。 
```

**135**

```
端口：135 
服务：Location Service 
说明：Microsoft在这个端口运行DCE RPC end-point mapper为它的DCOM服务。这与UNIX 111端口的功能很相似。使用DCOM和RPC的服务利用计算机上的end-point mapper注册它们的位置。远端客户连接到计算机时，它们查找end-point mapper找到服务的位置。HACKER扫描计算机的这个端口是为了找到这个计算机上运行Exchange Server吗？什么版本？还有些DOS攻击直接针对这个端口。
```

 **137、138、139**

```
端口：137、138、139 
服务：NETBIOS Name Service 
说明：其中137、138是UDP端口，当通过网上邻居传输文件时用这个端口。而139端口通过这个端口进入的连接试图获得NetBIOS/SMB服务。这个协议被用于windows文件和打印机共享和SAMBA。还有WINS Regisrtation也用它。
```

**143** 

```
端口：143 
服务：Interim Mail Access Protocol v2 
说明：和POP3的安全问题一样，许多IMAP服务器存在有缓冲区溢出漏洞。记住：一种Linux蠕虫（admv0rm）会通过这个端口繁殖，因此许多这个端口的扫描来自不知情的已经被感染的用户。当REDHAT在他们的LINUX发布版本中默认允许IMAP后，这些漏洞变的很流行。这一端口还被用于IMAP2，但并不流行。
```

**161** 

```
端口：161 
服务：SNMP 
说明：SNMP允许远程管理设备。所有配置和运行信息的储存在数据库中，通过SNMP可获得这些信息。许多管理员的错误配置将被暴露在Internet。Cackers将试图使用默认的密码public、private访问系统。他们可能会试验所有可能的组合。SNMP包可能会被错误的指向用户的网络。
```

 **177**

```
端口：177 
服务：X Display Manager Control Protocol 
说明：许多入侵者通过它访问X-windows操作台，它同时需要打开6000端口。
```

 **389**

```
端口：389 
服务：LDAP、ILS 
说明：轻型目录访问协议和NetMeeting Internet Locator Server共用这一端口。
```

**443** 

```
端口：443 
服务：Https 
说明：网页浏览端口，能提供加密和通过安全端口传输的另一种HTTP。
```

**456** 

```
端口：456 
服务：[NULL] 
说明：木马HACKERS PARADISE开放此端口
```

 **513**

```
端口：513 
服务：Login,remote login 
说明：是从使用cable modem或DSL登陆到子网中的UNIX计算机发出的广播。这些人为入侵者进入他们的系统提供了信息。
```

 **544**

```
端口：544 
服务：[NULL] 
说明：kerberos kshell
```

 **548**

```
端口：548 
服务：Macintosh,File Services(AFP/IP) 
说明：Macintosh,文件服务。
```

**553** 

```
端口：553 
服务：CORBA IIOP （UDP） 
说明：使用cable modem、DSL或VLAN将会看到这个端口的广播。CORBA是一种面向对象的RPC系统。入侵者可以利用这些信息进入系统。
```

 **555**

```
端口：555 
服务：DSF 
说明：木马PhAse1.0、Stealth Spy、IniKiller开放此端口。
```

**568** 

```
端口：568 
服务：Membership DPA 
说明：成员资格 DPA。
```

**569** 

```
端口：569 
服务：Membership MSN 
说明：成员资格 MSN。
```

 **635**

```
端口：635 
服务：mountd 
说明：Linux的mountd Bug。这是扫描的一个流行BUG。大多数对这个端口的扫描是基于UDP的，但是基于TCP的mountd有所增加（mountd同时运行于两个端口）。记住mountd可运行于任何端口（到底是哪个端口，需要在端口111做portmap查询），只是Linux默认端口是635，就像NFS通常运行于2049端口。
```

 **636**

```
端口：636 
服务：LDAP 
说明：SSL（Secure Sockets layer）
```

 **666**

```
端口：666 
服务：Doom Id Software 
说明：木马Attack FTP、Satanz Backdoor开放此端口
```

 **993**

```
端口：993 
服务：IMAP 
说明：SSL（Secure Sockets layer）
```

**1001、1011** 

```
端口：1001、1011 
服务：[NULL] 
说明：木马Silencer、WebEx开放1001端口。木马Doly Trojan开放1011端口。
```

 **1024**

```
端口：1024 
服务：Reserved 
说明：它是动态端口的开始，许多程序并不在乎用哪个端口连接网络，它们请求系统为它们分配下一个闲置端口。基于这一点分配从端口1024开始。这就是说第一个向系统发出请求的会分配到1024端口。你可以重启机器，打开Telnet，再打开一个窗口运行natstat -a 将会看到Telnet被分配1024端口。还有SQL session也用此端口和5000端口。
```

 **1025、1033**

```
端口：1025、1033 
服务：1025：network blackjack 
      1033：[NULL] 
说明：木马netspy开放这2个端口。
```

 **1080**

```
端口：1080 
服务：SOCKS 
说明：这一协议以通道方式穿过防火墙，允许防火墙后面的人通过一个IP地址访问INTERNET。理论上它应该只允许内部的通信向外到达INTERNET。但是由于错误的配置，它会允许位于防火墙外部的攻击穿过防火墙。WinGate常会发生这种错误，在加入IRC聊天室时常会看到这种情况。
```

 **1170**

```
端口：1170 
服务：[NULL] 
说明：木马Streaming Audio Trojan、Psyber Stream
Server、Voice开放此端口。
```

 **1234、1243、6711、6776**

```
端口：1234、1243、6711、6776 
服务：[NULL] 
说明：木马SubSeven2.0、Ultors Trojan开放1234、6776端口。木马SubSeven1.0/1.9开放1243、6711、6776端口。
```

 **1245**

```
端口：1245 
服务：[NULL] 
说明：木马Vodoo开放此端口。
```

 **1433**

```
端口：1433 
服务：SQL 
说明：Microsoft的SQL服务开放的端口。
```

 **1492**

```
端口：1492 
服务：stone-design-1 
说明：木马FTP99CMP开放此端口。
```

 **1500**

```
端口：1500 
服务：RPC client fixed port session queries 
说明：RPC客户固定端口会话查询
```

**1503** 

```
端口：1503 
服务：NetMeeting T.120 
说明：NetMeeting T.120
```

**1524** 

```
端口：1524 
服务：ingress 
说明：许多攻击脚本将安装一个后门SHELL于这个端口，尤其是针对SUN系统中Sendmail和RPC服务漏洞的脚本。如果刚安装了防火墙就看到在这个端口上的连接企图，很可能是上述原因。可以试试Telnet到用户的计算机上的这个端口，看看它是否会给你一个SHELL。连接到600/pcserver也存在这个问题。
```

 **1600**

```
端口：1600 
服务：issd 
说明：木马Shivka-Burka开放此端口。
```

**1720** 

```
端口：1720 
服务：NetMeeting 
说明：NetMeeting H.233 call Setup。
```

**1731** 

```
端口：1731 
服务：NetMeeting Audio Call Control 
说明：NetMeeting音频调用控制。
```

 **1807**

```
端口：1807 
服务：[NULL] 
说明：木马SpySender开放此端口。
```

**1981** 

```
端口：1981 
服务：[NULL] 
说明：木马ShockRave开放此端口。
```

**1999** 

```
端口：1999 
服务：cisco identification port 
说明：木马BackDoor开放此端口。
```

 **2000**

```
端口：2000 
服务：[NULL] 
说明：木马GirlFriend 1.3、Millenium 1.0开放此端口。
```

 **2001**

```
端口：2001 
服务：[NULL] 
说明：木马Millenium 1.0、Trojan Cow开放此端口。
```

 **2023**

```
端口：2023 
服务：xinuexpansion 4 
说明：木马Pass Ripper开放此端口。
```

 **2049**

```
端口：2049 
服务：NFS 
说明：NFS程序常运行于这个端口。通常需要访问Portmapper查询这个服务运行于哪个端口。
```

 **2115**

```
端口：2115 
服务：[NULL] 
说明：木马Bugs开放此端口。
```

**2140、3150** 

```
端口：2140、3150 
服务：[NULL] 
说明：木马Deep Throat 1.0/3.0开放此端口。
```

 **2500**

```
端口：2500 
服务：RPC client using a fixed port session
replication 
说明：应用固定端口会话复制的RPC客户
```

 **2583**

```
端口：2583 
服务：[NULL] 
说明：木马Wincrash 2.0开放此端口。
```

 **2801**

```
端口：2801 
服务：[NULL] 
说明：木马Phineas Phucker开放此端口。
```

**3024、4092** 

```
端口：3024、4092 
服务：[NULL] 
说明：木马WinCrash开放此端口。
```

 **3128**

```
端口：3128 
服务：squid 
说明：这是squid HTTP代理服务器的默认端口。攻击者扫描这个端口是为了搜寻一个代理服务器而匿名访问Internet。也会看到搜索其他代理服务器的端口8000、8001、8080、8888。扫描这个端口的另一个原因是用户正在进入聊天室。其他用户也会检验这个端口以确定用户的机器是否支持代理。
```

 **3129**

```
端口：3129 
服务：[NULL] 
说明：木马Master Paradise开放此端口。
```

**3150** 

```
端口：3150 
服务：[NULL] 
说明：木马The Invasor开放此端口。
```

 **3210、4321**

```
端口：3210、4321 
服务：[NULL] 
说明：木马SchoolBus开放此端口
```

 **3333**

```
端口：3333 
服务：dec-notes 
说明：木马Prosiak开放此端口
```

 **3389**

```
端口：3389 
服务：超级终端 
说明：WINDOWS 2000终端开放此端口。
```

 **3700**

```
端口：3700 
服务：[NULL] 
说明：木马Portal of Doom开放此端口
```

 **3996、4060**

```
端口：3996、4060 
服务：[NULL] 
说明：木马RemoteAnything开放此端口
```

 **4000**

```
端口：4000 
服务：QQ客户端 
说明：腾讯QQ客户端开放此端口。
```

 **4092**

```
端口：4092 
服务：[NULL] 
说明：木马WinCrash开放此端口。
```

 **4590**

```
端口：4590 
服务：[NULL] 
说明：木马ICQTrojan开放此端口。
```

 **5000、5001、5321、50505**

```
端口：5000、5001、5321、50505 
服务：[NULL] 
说明：木马blazer5开放5000端口。木马Sockets de Troie开放5000、5001、5321、50505端口。
```

 **5400、5401、5402**

```
端口：5400、5401、5402 
服务：[NULL] 
说明：木马Blade Runner开放此端口。
```

 **5550**

```
端口：5550 
服务：[NULL] 
说明：木马xtcp开放此端口。
```

 **5569**

```
端口：5569 
服务：[NULL] 
说明：木马Robo-Hack开放此端口。
```

 **5632**

```
端口：5632 
服务：pcAnywere 
说明：有时会看到很多这个端口的扫描，这依赖于用户所在的位置。当用户打开pcAnywere时，它会自动扫描局域网C类网以寻找可能的代理（这里的代理是指agent而不是proxy）。入侵者也会寻找开放这种服务的计算机。，所以应该查看这种扫描的源地址。一些搜寻pcAnywere的扫描包常含端口22的UDP数据包。
```

 **5742**

```
端口：5742 
服务：[NULL] 
说明：木马WinCrash1.03开放此端口。
```

 **6267**

```
端口：6267 
服务：[NULL] 
说明：木马广外女生开放此端口。
```

 **6400**

```
端口：6400 
服务：[NULL] 
说明：木马The tHing开放此端口。
```

 **6670、6671**

```
端口：6670、6671 
服务：[NULL] 
说明：木马Deep Throat开放6670端口。而Deep Throat 3.0开放6671端口。
```

 **6883**

```
端口：6883 
服务：[NULL] 
说明：木马DeltaSource开放此端口。
```

 **6969**

```
端口：6969 
服务：[NULL] 
说明：木马Gatecrasher、Priority开放此端口。
```

 **6970**

```
端口：6970 
服务：RealAudio 
说明：RealAudio客户将从服务器的6970-7170的UDP端口接收音频数据流。这是由TCP-7070端口外向控制连接设置的。
```

 **7000**

```
端口：7000 
服务：[NULL] 
说明：木马Remote Grab开放此端口。
```

 **7300、7301、7306、7307、7308**

```
端口：7300、7301、7306、7307、7308 
服务：[NULL] 
说明：木马NetMonitor开放此端口。另外NetSpy1.0也开放7306端口。
```

**7323** 

```
端口：7323 
服务：[NULL] 
说明：Sygate服务器端。
```

 **7626**

```
端口：7626 
服务：[NULL] 
说明：木马Giscier开放此端口。
```

 **7789**

```
端口：7789 
服务：[NULL] 
说明：木马ICKiller开放此端口。
```

 **8000**

```
端口：8000 
服务：OICQ 
说明：腾讯QQ服务器端开放此端口。
```

 **8010**

```
端口：8010 
服务：Wingate 
说明：Wingate代理开放此端口。
```

 **8080**

```
端口：8080 
服务：代理端口 
说明：WWW代理开放此端口。
```

**9400、9401、9402** 

```
端口：9400、9401、9402 
服务：[NULL] 
说明：木马Incommand 1.0开放此端口。
```

 **9872、9873、9874、9875、10067、10167** 

```
端口：9872、9873、9874、9875、10067、10167 
服务：[NULL] 
说明：木马Portal of Doom开放此端口。
```

 **9989**

```
端口：9989 
服务：[NULL] 
说明：木马iNi-Killer开放此端口。
```

 **11000**

```
端口：11000 
服务：[NULL] 
说明：木马SennaSpy开放此端口。
```

 **11223**

```
端口：11223 
服务：[NULL] 
说明：木马Progenic trojan开放此端口。
```

**12076、61466** 

```
端口：12076、61466 
服务：[NULL] 
说明：木马Telecommando开放此端口。
```

**12223**  

```
端口：12223 
服务：[NULL] 
说明：木马Hack’99 KeyLogger开放此端口。
```

 12345、12346 

```
端口：12345、12346 
服务：[NULL] 
说明：木马NetBus1.60/1.70、GabanBus开放此端口。
```

 **12361** 

```
端口：12361 
服务：[NULL] 
说明：木马Whack-a-mole开放此端口。
```

 **13223** 

```
端口：13223 
服务：PowWow 
说明：PowWow是Tribal Voice的聊天程序。它允许用户在此端口打开私人聊天的连接。这一程序对于建立连接非常具有攻击性。它会驻扎在这个TCP端口等回应。造成类似心跳间隔的连接请求。如果一个拨号用户从另一个聊天者手中继承了IP地址就会发生好象有很多不同的人在测试这个端口的情况。这一协议使用OPNG作为其连接请求的前4个字节。
```

**16969**  

```
端口：16969 
服务：[NULL] 
说明：木马Priority开放此端口。
```

 **17027**

```
端口：17027 
服务：Conducent 
说明：这是一个外向连接。这是由于公司内部有人安装了带有Conducent”adbot”的共享软件。Conducent”adbot”是为共享软件显示广告服务的。使用这种服务的一种流行的软件是Pkware。
```

**19191** 

```
端口：19191 
服务：[NULL] 
说明：木马蓝色火焰开放此端口。
```

 **20000、20001** 

```
端口：20000、20001 
服务：[NULL] 
说明：木马Millennium开放此端口。
```

 **20034** 

```
端口：20034 
服务：[NULL] 
说明：木马NetBus Pro开放此端口。
```

 **21554** 

```
端口：21554 
服务：[NULL] 
说明：木马GirlFriend开放此端口。
```

 **22222** 

```
端口：22222 
服务：[NULL] 
说明：木马Prosiak开放此端口。
```

 **23456**

```
端口：23456 
服务：[NULL] 
说明：木马Evil FTP、Ugly FTP开放此端口。
```

 **26274、47262** 

```
端口：26274、47262 
服务：[NULL] 
说明：木马Delta开放此端口。
```

 **27374** 

```
端口：27374 
服务：[NULL] 
说明：木马Subseven 2.1开放此端口。
```

 **30100** 

```
端口：30100 
服务：[NULL] 
说明：木马NetSphere开放此端口。
```

**30303** 

```
端口：30303 
服务：[NULL] 
说明：木马Socket23开放此端口。
```

**30999** 

```
端口：30999 
服务：[NULL] 
说明：木马Kuang开放此端口。
```

**31337、31338**  

```
端口：31337、31338 
服务：[NULL] 
说明：木马BO(Back Orifice)开放此端口。另外木马DeepBO也开放31338端口。
```

 **31339** 

```
端口：31339 
服务：[NULL] 
说明：木马NetSpy DK开放此端口。
```

**31666**  

```
端口：31666 
服务：[NULL] 
说明：木马BOWhack开放此端口。
```

**33333**  

```
端口：33333 
服务：[NULL] 
说明：木马Prosiak开放此端口。
```

 **34324** 

```
端口：34324 
服务：[NULL] 
说明：木马Tiny Telnet Server、BigGluck、TN开放此端口。
```

 **40412** 

```
端口：40412 
服务：[NULL] 
说明：木马The Spy开放此端口。
```

 **40421、40422、40423、40426**

```
端口：40421、40422、40423、40426
服务：[NULL] 
说明：木马Masters Paradise开放此端口。
```

**43210、54321** 

```
端口：43210、54321 
服务：[NULL] 
说明：木马SchoolBus 1.0/2.0开放此端口。
```

 **44445**

```
端口：44445 
服务：[NULL] 
说明：木马Happypig开放此端口。
```

 **50766** 

```
端口：50766 
服务：[NULL] 
说明：木马Fore开放此端口。
```

 **53001** 

```
端口：53001 
服务：[NULL] 
说明：木马Remote Windows Shutdown开放此端口。
```

 **65000** 

```
端口：65000 
服务：[NULL] 
说明：木马Devil 1.03开放此端口。
```

 **88**

```
端口：88 
说明：Kerberos krb5。另外TCP的88端口也是这个用途。
```

 **137**

```
端口：137 
说明：SQL Named Pipes encryption over other protocols name lookup(其他协议名称查找上的SQL命名管道加密技术)和SQL RPC encryption over other protocols name lookup(其他协议名称查找上的SQL RPC加密技术)和Wins NetBT name service(WINS NetBT名称服务)和Wins Proxy都用这个端口。
```

 **161**

```
端口：161 
说明：Simple Network Management Protocol(SMTP)（简单网络管理协议）。
```

 **162**

```
端口：162 
说明：SNMP Trap（SNMP陷阱）
```

 **445**

```
端口：445 
说明：Common Internet File System(CIFS)（公共Internet文件系统）
```

 **464**

```
端口：464 
说明：Kerberos kpasswd(v5)。另外TCP的464端口也是这个用途。
```

 **500**

```
端口：500 
说明：Internet Key Exchange(IKE)（Internet密钥交换）
```

**1645、1812** 

```
端口：1645、1812 
说明：Remot Authentication Dial-In User Service(RADIUS)authentication(Routing and Remote Access)(远程认证拨号用户服务)
```

 **1646、1813**

```
端口：1646、1813 
说明：RADIUS accounting(Routing and Remote Access)(RADIUS记帐（路由和远程访问）)
```

 **1701** 

```
端口：1701 
说明：Layer Two Tunneling Protocol(L2TP)(第2层隧道协议)
```

**1801、3527**  

```
端口：1801、3527 
说明：Microsoft Message Queue Server(Microsoft消息队列服务器)。还有TCP的135、1801、2101、2103、2105也是同样的用途。
```

**2504**  

```
端口：2504 
说明：Network Load Balancing(网络平衡负荷)
```

 

```
网络层—数据包的包格式里面有个很重要的字段叫做协议号。比如在传输层如果是TCP连接，那么在网络层IP包里面的协议号就将会有个值是6，如果是UDP的话那个值就是17—传输层。

传输层—通过接口关联(端口的字段叫做端口)—应用层。 
 用netstat –an 可以查看本机开放的端口号。 
```

 

# #端口大全(简)

 

```
HTTP协议代理服务器常用端口号：80/8080/3128/8081/9080 
SOCKS代理协议服务器常用端口号：1080 
FTP（文件传输）协议代理服务器常用端口号：21 
Telnet（远程登录）协议代理服务器常用端口：23
```

```
  ·HTTP服务器，默认的端口号为80/tcp（木马Executor开放此端口）
  ·HTTPS（securely transferring web pages）服务器，默认的端口号为443/tcp 443/udp
  ·Telnet（不安全的文本传送），默认端口号为23/tcp（木马Tiny Telnet Server所开放的端口）
  ·FTP，默认的端口号为21/tcp（木马Doly Trojan、Fore、Invisible FTP、WebEx、WinCrash和Blade Runner所开放的端口） 
  ·TFTP（Trivial File Transfer Protocol ），默认的端口号为69/udp
  ·SSH（安全登录）、SCP（文件传输）、端口重定向，默认的端口号为22/tcp 
  ·SMTP Simple Mail Transfer Protocol (E-mail)，默认的端口号为25/tcp（木马Antigen、Email Password Sender、Haebu Coceda、Shtrilitz Stealth、WinPC、WinSpy都开放这个端口）
  ·POP3 Post Office Protocol (E-mail) ，默认的端口号为110/tcp 
  ·WebLogic，默认的端口号为7001 
  ·Webshpere应用程序，默认的端口号为9080 
  ·webshpere管理工具，默认的端口号为9090 
  ·JBOSS，默认的端口号为8080 
  ·TOMCAT，默认的端口号为8080 
  ·WIN2003远程登陆，默认的端口号为3389
  ·Symantec AV/Filter for MSE ,默认端口号为 8081 
  ·Oracle 数据库，默认的端口号为1521
  ·ORACLE EMCTL，默认的端口号为1158 
  ·Oracle XDB（ XML 数据库），默认的端口号为8080 
  ·Oracle XDB FTP服务，默认的端口号为2100 
  ·MS SQL*SERVER数据库server，默认的端口号为1433/tcp 1433/udp 
  ·MS SQL*SERVER数据库monitor，默认的端口号为1434/tcp 1434/udp 
  ·QQ，默认的端口号为1080/udp
```

  

```
1 tcpmux TCP 端口服务多路复用
5 rje 远程作业入口
7 echo Echo 服务
9 discard 用于连接测试的空服务
11 systat 用于列举连接了的端口的系统状态
13 daytime 给请求主机发送日期和时间
17 qotd 给连接了的主机发送每日格言
18 msp 消息发送协议
19 chargen 字符生成服务；发送无止境的字符流
20 ftp-data FTP 数据端口
21 ftp 文件传输协议（FTP）端口；有时被文件服务协议（FSP）使用
22 ssh 安全 Shell（SSH）服务
23 telnet Telnet 服务
25 smtp 简单邮件传输协议（SMTP）
37 time 时间协议
39 rlp 资源定位协议
42 nameserver 互联网名称服务
43 nicname WHOIS 目录服务
49 tacacs 用于基于 TCP/IP 验证和访问的终端访问控制器访问控制系统
50 re-mail-ck 远程邮件检查协议
53 domain 域名服务（如 BIND）
63 whois++ WHOIS++，被扩展了的 WHOIS 服务
67 bootps 引导协议（BOOTP）服务；还被动态主机配置协议（DHCP）服务使用
68 bootpc Bootstrap（BOOTP）客户；还被动态主机配置协议（DHCP）客户使用
69 tftp 小文件传输协议（TFTP）
70 gopher Gopher 互联网文档搜寻和检索
71 netrjs-1 远程作业服务
72 netrjs-2 远程作业服务
73 netrjs-3 远程作业服务
73 netrjs-4 远程作业服务
79 finger 用于用户联系信息的 Finger 服务
80 http 用于万维网（WWW）服务的超文本传输协议（HTTP）
88 kerberos Kerberos 网络验证系统
95 supdup Telnet 协议扩展
101 hostname SRI-NIC 机器上的主机名服务
102 iso-tsap ISO 开发环境（ISODE）网络应用
105 csnet-ns 邮箱名称服务器；也被 CSO 名称服务器使用
107 rtelnet 远程 Telnet
109 pop2 邮局协议版本2
110 pop3 邮局协议版本3
111 sunrpc 用于远程命令执行的远程过程调用（RPC）协议，被网络文件系统（NFS）使用
113 auth 验证和身份识别协议
115 sftp 安全文件传输协议（SFTP）服务
117 uucp-path Unix 到 Unix 复制协议（UUCP）路径服务
119 nntp 用于 USENET 讨论系统的网络新闻传输协议（NNTP）
123 ntp 网络时间协议（NTP）
137 netbios-ns 在红帽企业 Linux 中被 Samba 使用的 NETBIOS 名称服务
138 netbios-dgm 在红帽企业 Linux 中被 Samba 使用的 NETBIOS 数据报服务
139 netbios-ssn 在红帽企业 Linux 中被 Samba 使用的NET BIOS 会话服务
143 imap 互联网消息存取协议（IMAP）
161 snmp 简单网络管理协议（SNMP）
162 snmptrap SNMP 的陷阱
163 cmip-man 通用管理信息协议（CMIP）
164 cmip-agent 通用管理信息协议（CMIP）
174 mailq MAILQ
177 xdmcp X 显示管理器控制协议
178 nextstep NeXTStep 窗口服务器
179 bgp 边界网络协议
191 prospero Cliffod Neuman 的 Prospero 服务
194 irc 互联网中继聊天（IRC）
199 smux SNMP UNIX 多路复用
201 at-rtmp AppleTalk 选路
202 at-nbp AppleTalk 名称绑定
204 at-echo AppleTalk echo 服务
206 at-zis AppleTalk 区块信息
209 qmtp 快速邮件传输协议（QMTP）
210 z39.50 NISO Z39.50 数据库
213 ipx 互联网络分组交换协议（IPX），被 Novell Netware 环境常用的数据报协议
220 imap3 互联网消息存取协议版本3
245 link LINK
347 fatserv Fatmen 服务器
363 rsvp_tunnel RSVP 隧道
369 rpc2portmap Coda 文件系统端口映射器
370 codaauth2 Coda 文件系统验证服务
372 ulistproc UNIX Listserv
389 ldap 轻型目录存取协议（LDAP）
427 svrloc 服务位置协议（SLP）
434 mobileip-agent 可移互联网协议（IP）代理
435 mobilip-mn 可移互联网协议（IP）管理器
443 https 安全超文本传输协议（HTTP）
444 snpp 小型网络分页协议
445 microsoft-ds 通过 TCP/IP 的服务器消息块（SMB）
464 kpasswd Kerberos 口令和钥匙改换服务
468 photuris Photuris 会话钥匙管理协议
487 saft 简单不对称文件传输（SAFT）协议
488 gss-http 用于 HTTP 的通用安全服务（GSS）
496 pim-rp-disc 用于协议独立的多址传播（PIM）服务的会合点发现（RP-DISC）
500 isakmp 互联网安全关联和钥匙管理协议（ISAKMP）
535 iiop 互联网内部对象请求代理协议（IIOP）
538 gdomap GNUstep 分布式对象映射器（GDOMAP）
546 dhcpv6-client 动态主机配置协议（DHCP）版本6客户
547 dhcpv6-server 动态主机配置协议（DHCP）版本6服务
554 rtsp 实时流播协议（RTSP）
563 nntps 通过安全套接字层的网络新闻传输协议（NNTPS）
565 whoami whoami
587 submission 邮件消息提交代理（MSA）
610 npmp-local 网络外设管理协议（NPMP）本地 / 分布式排队系统（DQS）
611 npmp-gui 网络外设管理协议（NPMP）GUI / 分布式排队系统（DQS）
612 hmmp-ind HMMP 指示 / DQS
631 ipp 互联网打印协议（IPP）
636 ldaps 通过安全套接字层的轻型目录访问协议（LDAPS）
674 acap 应用程序配置存取协议（ACAP）
694 ha-cluster 用于带有高可用性的群集的心跳服务
749 kerberos-adm Kerberos 版本5（v5）的“kadmin”数据库管理
750 kerberos-iv Kerberos 版本4（v4）服务
765 webster 网络词典
767 phonebook 网络电话簿
873 rsync rsync 文件传输服务
992 telnets 通过安全套接字层的 Telnet（TelnetS）
993 imaps 通过安全套接字层的互联网消息存取协议（IMAPS）
994 ircs 通过安全套接字层的互联网中继聊天（IRCS）
995 pop3s 通过安全套接字层的邮局协议版本3（POPS3）

```

# #Unix特有端口

```
512/tcp exec 用于对远程执行的进程进行验证
512/udp biff [comsat] 异步邮件客户（biff）和服务（comsat）
513/tcp login 远程登录（rlogin）
513/udp who [whod] 登录的用户列表
514/tcp shell [cmd] 不必登录的远程 shell（rshell）和远程复制（rcp）
514/udp syslog UNIX 系统日志服务
515 printer [spooler] 打印机（lpr）假脱机
517/udp talk 远程对话服务和客户
518/udp ntalk 网络交谈（ntalk），远程对话服务和客户
519 utime [unixtime] UNIX 时间协议（utime）
520/tcp efs 扩展文件名服务器（EFS）
520/udp router [route, routed] 选路信息协议（RIP）
521 ripng 用于互联网协议版本6（IPv6）的选路信息协议
525 timed [timeserver] 时间守护进程（timed）
526/tcp tempo [newdate] Tempo
530/tcp courier [rpc] Courier 远程过程调用（RPC）协议
531/tcp conference [chat] 互联网中继聊天
532 netnews Netnews
533/udp netwall 用于紧急广播的 Netwall
540/tcp uucp [uucpd] Unix 到 Unix 复制服务
543/tcp klogin Kerberos 版本5（v5）远程登录
544/tcp kshell Kerberos 版本5（v5）远程 shell
548 afpovertcp 通过传输控制协议（TCP）的 Appletalk 文件编制协议（AFP）
556 remotefs [rfs_server, rfs] Brunhoff 的远程文件系统（RFS）
```

# #IANA正式注册端口

```
1080 socks SOCKS 网络应用程序代理服务
1236 bvcontrol [rmtcfg] Garcilis Packeten 远程配置服务器[a]
1300 h323hostcallsc H.323 电话会议主机电话安全
1433 ms-sql-s Microsoft SQL 服务器
1434 ms-sql-m Microsoft SQL 监视器
1494 ica Citrix ICA 客户
1512 wins Microsoft Windows 互联网名称服务器
1524 ingreslock Ingres 数据库管理系统（DBMS）锁定服务
1525 prospero-np 无特权的 Prospero
1645 datametrics [old-radius] Datametrics / 从前的 radius 项目
1646 sa-msg-port [oldradacct] sa-msg-port / 从前的 radacct 项目
1649 kermit Kermit 文件传输和管理服务
1701 l2tp [l2f] 第2层隧道服务（LT2P） / 第2层转发（L2F）
1718 h323gatedisc H.323 电讯守门装置发现机制
1719 h323gatestat H.323 电讯守门装置状态
1720 h323hostcall H.323 电讯主持电话设置
1758 tftp-mcast 小文件 FTP 组播
1759 mtftp 组播小文件 FTP（MTFTP）
1789 hello Hello 路由器通信端口
1812 radius Radius 拨号验证和记帐服务
1813 radius-acct Radius 记帐
1911 mtp Starlight 网络多媒体传输协议（MTP）
1985 hsrp Cisco 热备用路由器协议
1986 licensedaemon Cisco 许可管理守护进程
1997 gdp-port Cisco 网关发现协议（GDP）
2049 nfs [nfsd] 网络文件系统（NFS）
2102 zephyr-srv Zephyr 通知传输和发送服务器
2103 zephyr-clt Zephyr serv-hm 连接
2104 zephyr-hm Zephyr 主机管理器
2401 cvspserver 并行版本系统（CVS）客户 / 服务器操作
2430/tcp venus 用于 Coda 文件系统（codacon 端口）的 Venus 缓存管理器
2430/udp venus 用于 Coda 文件系统（callback/wbc interface 界面）的 Venus 缓存管理器
2431/tcp venus-se Venus 传输控制协议（TCP）的副作用
2431/udp venus-se Venus 用户数据报协议（UDP）的副作用
2432/udp codasrv Coda 文件系统服务器端口
2433/tcp codasrv-se Coda 文件系统 TCP 副作用
2433/udp codasrv-se Coda 文件系统 UDP SFTP 副作用
2600 hpstgmgr [zebrasrv] HPSTGMGR；Zebra 选路
2601 discp-client [zebra] discp 客户；Zebra 集成的 shell
2602 discp-server [ripd] discp 服务器；选路信息协议守护进程（ripd）
2603 servicemeter [ripngd] 服务计量；用于 IPv6 的 RIP 守护进程
2604 nsc-ccs [ospfd] NSC CCS；开放式短路径优先守护进程（ospfd）
2605 nsc-posa NSC POSA；边界网络协议守护进程（bgpd）
2606 netmon [ospf6d] Dell Netmon；用于 IPv6 的 OSPF 守护进程（ospf6d）
2809 corbaloc 公共对象请求代理体系（CORBA）命名服务定位器
3130 icpv2 互联网缓存协议版本2（v2）；被 Squid 代理缓存服务器使用
3306 mysql MySQL 数据库服务
3346 trnsprntproxy Trnsprnt 代理
4011 pxe 执行前环境（PXE）服务
4321 rwhois 远程 Whois（rwhois）服务
4444 krb524 Kerberos 版本5（v5）到版本4（v4）门票转换器
5002 rfe 无射频以太网（RFE）音频广播系统
5308 cfengine 配置引擎（Cfengine）
5999 cvsup [CVSup] CVSup 文件传输和更新工具
6000 x11 [X] X 窗口系统服务
7000 afs3-fileserver Andrew 文件系统（AFS）文件服务器
7001 afs3-callback 用于给缓存管理器回电的 AFS 端口
7002 afs3-prserver AFS 用户和组群数据库
7003 afs3-vlserver AFS 文件卷位置数据库
7004 afs3-kaserver AFS Kerberos 验证服务
7005 afs3-volser AFS 文件卷管理服务器
7006 afs3-errors AFS 错误解释服务
7007 afs3-bos AFS 基本监查进程
7008 afs3-update AFS 服务器到服务器更新器
7009 afs3-rmtsys AFS 远程缓存管理器服务
9876 sd 会话指引器
10080 amanda 高级 Maryland 自动网络磁盘归档器（Amanda）备份服务
11371 pgpkeyserver 良好隐私（PGP） / GNU 隐私卫士（GPG）公钥服务器
11720 h323callsigalt H.323 调用信号交替
13720 bprd Veritas NetBackup 请求守护进程（bprd）
13721 bpdbm Veritas NetBackup 数据库管理器（bpdbm）
13722 bpjava-msvc Veritas NetBackup Java / Microsoft Visual C++ (MSVC) 协议
13724 vnetd Veritas 网络工具
13782 bpcd Vertias NetBackup
13783 vopied Veritas VOPIED 协议
22273 wnn6 [wnn4] 假名/汉字转换系统[c]
26000 quake Quake（以及相关的）多人游戏服务器
26208 wnn6-ds
33434 traceroute Traceroute 网络跟踪工具
```

# #数据报传输协议DDP端口

```
1/ddp rtmp 路由表管理协议
2/ddp nbp 名称绑定协议
4/ddp echo AppleTalk Echo 协议
6/ddp zip 区块信息协议
```

# #Kerberos端口

```
751 kerberos_master Kerberos 验证
752 passwd_server Kerberos 口令（kpasswd）服务器
754 krb5_prop Kerberos v5 从属传播
760 krbupdate [kreg] Kerberos 注册
1109 kpop Kerberos 邮局协议（KPOP）
2053 knetd Kerberos 多路分用器
2105 eklogin Kerberos v5 加密的远程登录（rlogin）
```

# #未注册端口

```
15/tcp netstat 网络状态（netstat）
98/tcp linuxconf Linuxconf Linux 管理工具
106 poppassd 邮局协议口令改变守护进程（POPPASSD）
465/tcp smtps 通过安全套接字层的简单邮件传输协议（SMTPS）
616/tcp gii 使用网关的（选路守护进程）互动界面
808 omirr [omirrd] 联机镜像（Omirr）文件镜像服务
871/tcp supfileserv 软件升级协议（SUP）服务器
901/tcp swat Samba 万维网管理工具（SWAT）
953 rndc Berkeley 互联网名称域版本9（BIND 9）远程名称守护进程配置工具
1127 sufiledbg 软件升级协议（SUP）调试
1178/tcp skkserv 简单假名到汉字（SKK）日文输入服务器
1313/tcp xtel 法国 Minitel 文本信息系统
1529/tcp support [prmsd, gnatsd] GNATS 错误跟踪系统
2003/tcp cfinger GNU Finger 服务
2150 ninstall 网络安装服务
2988 afbackup afbackup 客户-服务器备份系统
3128/tcp squid Squid 万维网代理缓存
3455 prsvp RSVP 端口
5432 postgres PostgreSQL 数据库
4557/tcp fax FAX 传输服务（旧服务）
4559/tcp hylafax HylaFAX 客户-服务器协议（新服务）
5232 sgi-dgl SGI 分布式图形库
5354 noclog NOCOL 网络操作中心记录守护进程（noclogd）
5355 hostmon NOCOL 网络操作中心主机监视
5680/tcp canna Canna 日文字符输入界面
6010/tcp x11-ssh-offset 安全 Shell（SSH）X11 转发偏移
6667 ircd 互联网中继聊天守护进程（ircd）
7100/tcp xfs X 字体服务器（XFS）
7666/tcp tircproxy Tircproxy IRC 代理服务
8008 http-alt 超文本传输协议（HTTP）的另一选择
8080 webcache 万维网（WWW）缓存服务
8081 tproxy 透明代理
9100/tcp jetdirect [laserjet, hplj] Hewlett-Packard (HP) JetDirect 网络打印服务
9359 mandelspawn [mandelbrot] 用于 X 窗口系统的并行 Mandelbrot 生成程序
10081 kamanda 使用 Kerberos 的 Amanda 备份服务
10082/tcp amandaidx Amanda 备份服务
10083/tcp amidxtape Amanda 备份服务
20011 isdnlog 综合业务数字网（ISDN）登录系统
20012 vboxd ISDN 音箱守护进程（vboxd）
22305/tcp wnn4_Kr kWnn 韩文输入系统
22289/tcp wnn4_Cn cWnn 中文输入系统
22321/tcp wnn4_Tw tWnn 中文输入系统（台湾）
24554 binkp Binkley TCP/IP Fidonet 邮寄程序守护进程
27374 asp 地址搜索协议
60177 tfido Ifmail FidoNet 兼容邮寄服务
60179 fido FidoNet 电子邮件和新闻网络
```



# #常见端口及攻击方式

| 端口号      | 说明                   | 攻击                                                         |
| ----------- | ---------------------- | ------------------------------------------------------------ |
| 21/22/69    | ftp/tftp：文件传输协议 | 爆破\嗅探\溢出\后门                                          |
| 22          | ssh：远程连接          | 爆破OpenSSH；28个退格                                        |
| 23          | telnet: 远程连接       | 爆破\嗅探                                                    |
| 25          | smtp：邮件服务         | 邮件伪造                                                     |
| 53          | DNS：域名系统          | DNS区域传输\DNS劫持\DNS缓存投毒\DNS欺骗\利用DNS隧道技术刺透防火墙 |
| 67/68       | dhcp                   | 劫持\欺骗                                                    |
| 110         | pop3                   | 爆破                                                         |
| 139         | samba                  | 爆破\未授权访问\远程代码执行                                 |
| 143         | imap                   | 爆破                                                         |
| 161         | snmp                   | 爆破                                                         |
| 389         | ldap                   | 注入攻击\未授权访问                                          |
| 512/513/514 | Linux r                | 直接使用rlogin                                               |
| 873         | rsync                  | 未授权访问                                                   |
| 1080        | socket                 | 爆破：进行内网渗透                                           |
| 1352        | lotus                  | 爆破：弱口令\信息泄漏：源代码                                |
| 1433        | mssql                  | 爆破：使用系统用户登录\注入攻击                              |
| 1521        | oracle                 | 爆破：TNS\注入攻击                                           |
| 2049        | nfs                    | 配置不当                                                     |
| 2181        | zookeeper              | 未授权访问                                                   |
| 3306        | mysql                  | 爆破\拒绝服务\注入                                           |
| 3389        | rdp                    | 爆破\Shift后门                                               |
| 4848        | glassfish              | 爆破：控制台弱口令\认证绕过                                  |
| 5000        | sybase/DB2             | 爆破\注入                                                    |
| 5432        | postgresql             | 缓冲区溢出\注入攻击\爆破：弱口令                             |
| 5632        | pcanywhere             | 拒绝服务\代码执行                                            |
| 5900        | vnc                    | 爆破：弱口令\认证绕过                                        |
| 6379        | redis                  | 未授权访问\爆破：弱口令                                      |
| 7001        | weblogic               | Java反序列化\控制台弱口令\控制台部署webshell                 |
| 80/443/8080 | web                    | 常见web攻击\控制台爆破\对应服务器版本漏洞                    |
| 8069        | zabbix                 | 远程命令执行                                                 |
| 9090        | websphere控制台        | 爆破：控制台弱口令\Java反序列                                |
| 9200/9300   | elasticsearch          | 远程代码执行                                                 |
| 11211       | memcacache             | 未授权访问                                                   |
| 27017       | mongodb                | 爆破\未授权访问                                              |

 

 

# #netstat命令的内部地址和外部地址

```
网络连接有两方参与，自己为内部地址，别人为外部地址

用浏览器打开百度网站，自己的IP是内部地址，百度服务器的IP是外部地址
```

 

# #ipconfig得到的IPV4和百度搜到的IP不同

```
ping得到的是192.168.1.106

百度得到的是121.204.218.202

192.168是内网地址，自己的电脑并未直接连接到互联网，而是经过ADSL拨号，ADSL得到的IP地址又叫公网地址，它是直连互联网的

百度从互联网上搜到的是公网地址
```

