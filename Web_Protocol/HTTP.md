# #Web及网络基础

```
HTTP,超文本传输协议，完成从客户端到服务器端的流程，协议即是规则的约定

客户端，通过指定的访问地址获取(上传)服务器资源(文件等信息)

服务器，使用HTTP协议的通信
```



## ##TCP/IP，层次

```
TCP/IP协议族：IEEE802.3，FDDI，ICMP，TCP，HTTP，IP，FTP，DNS，PPPoE，UDP，SNMP

TCP/IP协议族分为应用层、传输层、网络层和数据链路层

```

```
应用层：决定了向用户提供应用服务时通信的活动

​    FTP(File Transfer Protocol 文件传输协议)

​    DNS(Domain Name System 域名系统)

​    HTTP(Hyper Text Transfer Protocol 超文本传输协议)
```

```
传输层：对应用层提供处于网络连接种的两台计算机之间的数据传输

​    TCP(Transmission Control Protocol 传输控制协议)

​    UDP(User Data Protocol 用户数据报协议)
```

```
网络层：处理网络上流动的数据包，该层规定通过怎样的传输路线到达对方计算机并将数据包传给对方
```

```
数据链路层：处理连接网络的硬件部分，只要是硬件的范畴均是数据链路层管理
```

```
使用TCP/IP协议族进行网络通信时，按照分层顺序进行通信

发送端：应用层，传输层，网络层，链路层
接收端：链路层，网络层，传输层，应用层

发送端，每通过一层则增加首部
接收端，每通过一层则删除首部

应用层：HTTP数据
传输层：TCP首部+HTTP数据
网络层：IP首部+ TCP首部+HTTP数据
链路层：以太网首部+ IP首部+ TCP首部+HTTP数据
```



## ##IP协议

```
IP(Internet Protocol)协议位于网络层

IP协议的作用是把各种数据包传送给对方，负责传输

IP地址指明节点被分配到的地址，可变的

MAC地址是指网卡所属的固定地址，基本上不会变

IP地址可以与MAC地址进行配对

IP之间的通信依赖MAC地址

通信不在同一局域网则需要在不同设备之间中转，在中转时会利用下一站中转设备的MAC地址来搜索下一个中转目标，此时使用ARP协议

ARP(Address Resolution Protocol)协议，用以解析地址，根据IP地址得到MAC地址
```



## ##TCP协议

```
TCP协议位于传输层，提供可靠的字节流服务，确保可靠性。TCP协议为了更容易传送大数据则将数据分割，且TCP协议能够确认数据最终是否送达到对方。三次握手

握手过程种使用TCP则会有SYN(synchronize)和ACK(acknowledgement)
```

 **TCP三次握手**

```
三次握手：发送端发送一个带SYN标志的数据包给对方
         接受端收到，回传一个带SYN/ACK标志的数据包以示传达确认信息
         发送端再回传一个带ACK标志的数据包，代表握手结束

握手过程中某阶段中断，TCP会再次以相同顺序发送相同的数据包
```

## ##DNS服务

```
DNS(Domain Name System)服务位于应用层，提供域名到IP地址之间的解析服务

DNS协议通过域名查找IP地址，或逆向从IP地址反查域名

计算机可以有IP地址，可以有主机名，可以有域名

用户通常用主机名或域名来访问对方的计算机
```



## ##IP、TCP、DNS与HTTP的关系

```
客户端访问A网页

DNS得到A网页的IP地址

HTTP协议生成正对目标Web服务器的请求报文

TCP协议将HTTP请求分割成报文段并可靠传输给对方

IP协议搜索A网页的IP地址，一边中转一边传送

TCP协议从对方那里得到报文段并重组报文段

HTTP协议对Web服务器请求的内容进行处理

请求的处理结果通过TCP/IP通信协议向用户进行回传
```



## ##URI    URL

**URI**

```
URI(Uniform Resource Identifier)统一资源标识符，由某个协议方案表示的资源的定位标识符，URI用字符串标识某一互联网资源

绝对URI格式：http://user:pass@www.example.jb:80/dir/index,html?uid=1#ch1

http:// 协议方案名

user:pass 登录信息(认证)：指定用户名和密码作为从服务器端获取资源时必要的登录信息(身份认证)

www.example.jb 服务器地址：地址可以是DNS可解析的名称，或192.168.1.1这类IPV4地址名，或[0:0:0:0:0:1]这类IPV6地址名

80 服务器端口号：指定服务器连接的网络端口号

dir/index,html 带层次的文件路径：指定服务器上的文件路径来定位特指的资源

uid=1 查询字符串：针对已指定的文件路径内的资源，可以使用查询字符串传入任意参数

ch1 片段标识符：标记出已获取资源中的字资源(文档内的某个位置)
```

 **URL**

```
URL(Uniform Resource Locator)统一资源定位符，URL表示资源的地点
```



# #简单的HTTP协议

```
HTTP协议用于客户端和服务端之间的通信

通过请求和响应的交换达成通信

请求报文=请求方法+请求URI+协议版本+可选的请求首部字段+内容实体

响应报文=协议版本+状态码+解释状态码的原因短语+可选的响应首部字段+实体主体

HTTP是不保存状态的协议，HTTP协议自身不对请求和响应之间的通信状态进行保存

使用HTTP协议，每当由新的请求发送，会有对应的信响应产生。

协议本身不保留之前一切的请求或响应报文的信息

之后引入Cookie技术，Cookie和HTTP即可保持状态
```

​    

## ##HTTP/1.1可使用的方法

### ###GET：获取资源

```
用来请求访问已被URI识别的资源，指定的资源经服务器端解析后返回响应内容

请求的资源是文本，则返回文本

请求的资源时CGI那样的程序，则返回执行后的输出结果
```

### ###POST：传输实体主体

```
POST比GET更加强大，不仅可以从服务器端获取资源，还能向服务器上传数据
```

### ###PUT：传输文件

```
在请求报文的主体中包含文件内容，然后保存到请求URI指定的位置
```

### ###HEAD：获取报文首部

```
  HEAD与GET方法一样，只是不返回报文主体部分

用于确认URI的有效性及资源更新的日期时间等
```

### ###DELETE：删除文件

```
 DELETE方法按请求URI删除指定的资源
```

### ###OPTIONS：询问支持的方法

```
 OPTIONS用来查询针对请求URI指定的资源支持的方法
```

### ###TRACE：追踪路径

```
让Web服务器端将之前的请求通信换回给客户端

客户端通过TRACE可以查询发送出去的请求是怎样被加工修改/篡改的

请求想要连接到源目标服务器可能会通过代理中转

TRACE用来确认连接过程中发生的一系列操作

 
```

### ###CONNECT：要求隧道协议连接代理

```
与代理服务器通信时建立隧道，实现用隧道协议进行TCP通信

使用SSL(Secure Sockets Layer 安全套接层)和TLS(Transport Layer Security 传输层安全)协议把通信内容加密后经网络隧道传输

CONNECT格式：CONNECT 代理服务器名：端口号 HTTP版本
```

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)

## ##持久连接  管线化

```
HTTP协议初始版本，每进行一次HTTP通信则需要断开一次TCP连接

这之后出现了持久连接：只要任意一端没有明确提出断开连接，则保持TCP连接状态

持久连接减少了TCP连接断开与建立的开销，减轻服务器端的负载，并且使得HTTP请求与响应更快结束，Web页面的显示速度也就相应提高

HTTP/1.1所有连接默认都是持久连接

HTTP/1.0未标准化
```

 

```
持久连接使得多数请求以管线化的方式发送

之前必须是发送请求得到响应才可发送下一个请求

管线化：无需等待响应也可直接发送下一个请求
```



## ##Cookie HTTP

```
HTTP是不保存状态的协议，HTTP协议自身不对请求和响应之间的通信状态进行保存

协议本身不保留之前一切的请求或响应报文的信息

之后引入Cookie技术，Cookie和HTTP即可保持状态

Cookie在请求和响应报文中写入Cookie信息来控制客户端的状态

Cookie根据服务端的响应报文中的Set-Cookie，去通知客户端保存Cookie，下次客户端往该服务端发送请求就自动在请求报文中加Coolie再发出

服务器端得到Cookie，会去检查该请求来来自何处，再对比服务器的记录，得到之前的状态信息

第一次是没有Cookie的，服务器发过来Cookie，客户端保存之后，第二次才有Cookie
```



# #HTTP报文内的HTTP信息

## ##请求报文及响应报文的结构

```
请求报文=报文首部(请求行+请求首部字段+通用首部字段+实体首部字段+其他)+空行(CR+LF)+报文主体

响应报文=报文首部(状态行+响应首部字段+通用首部字段+实体首部字段+其他)+空行(CR+LF)+报文主体

请求行：包含用于请求的方法，请求URI和HTTP版本

状态行：包含表明响应结果的状态码，原因短语和HTTP版本

首部字段：包含表示请求和响应的各种条件和属性的各类首部

其他：可能包含HTTP的RFC里未定义的首部(Cookie等)
```



## ##编码 报文 实体 压缩 分割

```
HTTP传输数据可以按数据原貌直接传输(慢)

也可以再传输过程中用编码(快)
```

 

```
报文：是HTTP通信中的基本单位，由8位组字节流组成，通过HTTP通信传输
```

```
实体：作为请求或响应的有效载荷数据(补充项)被传输，其内容=实体首部+实体主体
```

 

```
HTTP报文的主体用于传输请求或响应的实体主体

通常，报文主体=实体主体

传输编码时，实体主体发生变化，此时不等于报文主体
```

 

```
HTTP协议中存在内容编码(用以压缩)：gzip，compress，deflate，identity

内容编码指明应用再实体内容上的编码格式，并保持实体信息原样压缩

内容编码后的实体由客户端接收并负责解码
```

 

```
传输大容量数据时，会将数据分割成多块

分块传输编码：把实体主体分块

每一块以十六进制标记块的大小，实体主体的最后一块用“0(CR+LF)”标记

由接收的客户端负责解码并恢复到编码前的实体主体

HTTP/1.1存在传输编码机制，在通信时按某种编码方式传输，但只定义作用于分块传输编码中
```



## ##MIME 邮件

```
MIME(Multipurpose Internet Mail Extensions 多用途因特网邮件扩展)：允许邮件处理文本、图片、视频等多个不同类型的数据。发送邮件时可以在邮件里写入文字并添加附件即是因为MIME

在MIME扩展中使用多部分对象集合，以容纳多份不同类型的数据

HTTP协议中采纳多部分对象集合，发送的一份报文主体内可含有多类型实体。通常用于图片或文本文件上传
```



## ##范围请求：获取部分内容的范围

```
范围请求：指定范围发送的请求，首部字段Range，响应返回状态码206 Partial Content

对一份10000字节大小的资源，若使用范围请求，则只请求5001~10000字节内的资源

资源的byte范围5001~10000   Range：bytes=5001-10000
        5001字节之后的全部  Range：bytes=5001-
        1~3000             Range：bytes=-3000，
        5000~7000          Range：bytes=5000-7000
```



## ##内容协商：返回最合适的内容

```
当浏览器默认语言为英文或中文，访问相同URI的Web页面则会对应显示英文版或中文版页面，该机制为内容协商

内容协商：客户端于服务器端就响应的资源内容进行交涉，然后提供给客户端最适合的资源

内容协商以响应资源的语言、字符集、编码方式、某些首部字段等作为判断基准
```

**内容协商有3种类型**

```
服务器驱动协商(由服务器端进行内容协商，对用户而言不一定得到最优内容)

客户端驱动协商(由客户端进行内容协商)

透明协商(服务器驱动和客户端驱动的结合)
```



# #返回结果的HTTP状态码

```
状态码告知从服务器端返回的请求结果

HTTP状态码负责表示客户端HTTP请求的返回结果、标记服务器端的处理是否正常、通知出现的错误等工作
```

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image004.png)

## ##2xx成功

**200 OK**

```
从客户端发来的请求在服务器端被正常处理
```

**204 No Content**

```
请求处理成功但没有资源可返回

服务器接收的请求处理成功，但返回的响应报文中不含实体的主体部分，且不允许返回任何实体的主体

浏览器请求，返回204，浏览器页面不发生更新

用于从客户端发消息给服务器，且不对客户端发新消息内容的情况
```

**206 Partial Content**

```
客户端进行范围请求，服务器成功执行该部分的GET请求

响应报文中包含Content-Range指定范围的实体内容
```



## ##3xx重定向(执行特殊处理以正确处理请求)

**301 Moved Permanently**

```
永久性重定向

请求的资源已被分配新的URI，如果之前将URI保存为书签了，现在就需要更新书签
```

**302 Found**

```
临时性重定向

请求的资源临时定位到其他位置(新的URI)，希望本次使用新的URI访问

已移动的资源对应的URI将来可能会发生变化

区别于301，同样是将URI保存为书签，301需要更新，302仍旧保留
```

**303 See Other**

```
请求对应的资源存在着另一个URI，应使用GET定向获取请求的资源

资源的URI已更新，临时按新的URI访问

区别于302，同样的功能，但303明确表示客户端应采用GET方法获取资源
```

**304 Not Modified**

```
客户端发送附带条件的请求，服务器端资源已找到，但未符合条件请求

304状态码返回时，不包含任何响应的主体部分

304与重定向没有关系

附带条件的请求：GET请求报文中包含If-Match，If-Modified-Since，If-None-Match，If-Range，If-Unmodified-Since中任一首部
```

**307 Temporary Redirect**

```
临时重定向

302标准禁止POST变换成GET，但实际使用并不会遵守该标准

307遵循标准，禁止POST变成GET
```



## ##4xx客户端错误

**400 Bad Request**

```
请求报文中存在语法错误

错误发生时，需修改请求的内容后再次发送请求
```

**401 Unauthorized**

```
认证失败

发送的请求需要有通过HTTP认证(BASIC认证、DIGEST认证)的认证信息

若之前已进行过一次请求，则用户认证失败
```

**403 Forbidden**

```
不允许访问该资源

未获得文件系统的访问授权，访问授权出现问题都可能导致403
```

**404 Not Found**

```
服务器上没有请求的资源

也可用于服务器端拒绝请求且不想说明理由
```



## ##5xx服务器错误

**500 Internal Server Error**

```
服务器在执行请求时发生错误

可能是Web的bug或某些临时故障
```

**503 Service Unavailable**

```
服务器暂时处于超负荷或正在进行停机维护，当前无法处理请求
```



# #与HTTP协作的Web服务器

## ##虚拟主机

```
一台Web服务器可搭建多个独立域名的Web网站，也可作为通信路径上的中转服务器提升传输效率

HTTP/1.1允许一台HTTP服务器搭建多个Web站点，使用虚拟主机，可以是物理层面只有一台服务器但在逻辑层面有多台服务器

多个Web站点同时部署在同一服务器上(相同的IP地址)，在经过DNS域名解析后，访问的IP地址会相同，为了分清，故在发送HTTP请求时，需要在Host首部内完整指定主机名或域名的URI
```



## ##通信数据转发程序：代理、网关、隧道

```
用于通信数据转发的应用程序和服务器可以将请求转发给通信线路上的下一站服务器，并能接收从那台服务器发送的响应再转发给客户端
```

 

**代理**

```
具有转发功能的应用程序，接收客户端并转发给服务器，接收服务器并转发给客户端

代理不改变请求URI，直接发送给前方持有资源的目标服务器

使用代理的原因：利用缓存技术减少网络带宽的流量；组织内部针对特定网站的访问控制，以获取访问为主要目的

缓存代理：代理转发响应时，会预先将资源的副本缓存在代理服务器上，当再次接到对该资源的请求时，将之前缓存的资源作为响应返回，不从服务器获取资源

透明代理：转发请求或响应时，不对报文做任何加工
```

**网关**

```
转发其他服务器通信数据的服务器

接收客户端时，可以对请求进行处理

利用网关可以由HTTP请求转化为其他协议通信，还能提高通信的安全性

网关能使通信线路上的服务器提供非HTTP协议服务

客户端与网关之间的通信线路上会进行加密以确保连接的安全
```

**隧道**

```
在相隔很远的客户端和服务器之间中转，并保持双方通信连接，加密通信

隧道本身不会去解析HTTP请求，请求保持原样中转给之后的服务器

隧道本身是透明的，客户端不用在意隧道的存在
```



## ##缓存

```
缓存：代理服务器或客户端本地磁盘内保存的资源副本

利用缓存减少对源服务器的访问，节省通信流量和通信时间

缓存会变化，存在有效期限，缓存会向源服务器确认资源的有效性并进行更新

缓存可存在于缓存服务器内，也可存在客户端浏览器中，依旧存在有效期限
```



# #HTTP首部

```
HTTP协议的请求和响应报文中必定包含HTTP首部

HTTP报文=报文首部+空行(CR+LF)+报文主体

报文首部：在客户端和服务器处理时起至关重要作用的信息几乎在这里

报文主体：所需要的用户和资源的信息均在这里

请求报文首部=请求行+请求首部字段+通用首部字段+实体首部字段+其他

请求报文首部=方法+URI+HTTP版本+HTTP首部字段

响应报文首部=状态行+响应首部字段+通用首部字段+实体首部字段+其他

响应报文首部=HTTP版本+状态码+HTTP首部字段
```

 

## ##HTTP首部字段

```
使用首部是为了给浏览器和服务器提供报文主体大小、所使用的语言、认证信息等内容

HTTP首部字段=首部字段+字段值，中间由冒号隔开

字段值对应单个HTTP首部字段可以有多个值

HTTP首部字段根据实际用途分为4种
```

**通用首部字段**

```
请求报文和响应报文均会使用的首部
```

**请求首部字段**

```
请求报文使用的首部

补充了请求的附加内容、客户端信息、响应内容优先级等信息
```

**响应首部字段**

```
响应报文使用的首部

补充了响应的附加内容，也会要求客户端附加额外的内容信息
```

**实体首部字段**

```
针对请求报文实体部分和响应报文实体部分使用的首部

补充了资源内容更新时间等与实体有关的信息
```



## ##HTTP/1.1首部字段

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image006.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image008.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image010.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image012.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image014.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image016.png)

## ##非HTTP/1.1首部字段

```
非正式的首部字段

Cookie、Set-Cookie、Content-Disposition
```



## ##End-to-end首部

```
端到端首部

该首部会转发给请求、响应对应的最终接收目标，且必须保存在由缓存生成的响应种，并且它必须被转发

(除去hop-by-hop的8个首部字段，其他字段均属于end-to-end首部
```



## ##Hop-by-hop首部

```
逐跳首部

该首部只对单词转发有效，会因通过缓存或代理而不转发

在HTTP/1.1及之后的版本，若要使用hop-by-hop首部，需提供Connection首部字段

Connection、Keep-Alive、Proxy-Authenticate 、Proxy-Authorization、Trailer、TE、Transfer-Encoding、Upgrade
```



## ##HTTP/1.1通用首部字段(请求和响应均会使用)

**Cache-Control(控制缓存的行为)**

```
指令的参数时可选的，多个指令之间由逗号“，”隔开
```

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image018.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image020.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image022.png)

**表示是否能缓存的指令**

```
public
  其他用户也可利用缓存

private
  缓存只能给特定用户，缓存服务器只为该用户提供资源缓存服务

no-cache
  不缓存过期资源
  防止从缓存中返回过期的资源
  客户端发no-cache，客户端不会接收缓存过的响应，缓存服务器得将请求转发给源服务器
  服务器发no-cache，缓存服务器不能对资源进行缓存，源服务器不对缓存服务器请求的资源进行有效性确认，并禁止其对响应资源进行缓存操作
```



**控制可执行缓存的对象的指令**

```
no-store
  不进行缓存
  暗示请求(和对应的响应)或响应中包含机密信息
  该指令规定缓存不能在本地存储请求或响应的任一部分
```

​                                                                      

**指定缓存期限和认证的指令**

```
s-maxage

s-maxage功能与max-age相同，但s-maxage只适用于供多位用户适用的公共缓存服务器

使用s-maxage之后，直接忽略对Expires首部字段及max-age的处理
```

```
max-age

客户端发max-age，若缓存资源的缓存时间数值比指定时间的数值小，则客户端接收缓存资源，若max-age为0，则缓存服务器将请求转发给源服务器

服务器发max-age，缓存服务器将不对资源有效性进行确认，max-age数值代表资源保存为缓存的最长时间
```

```
HTTP/1.1优先处理max-age指令且忽略Expires首部字段

HTTP/1.0优先处理Expires且忽略max-age
```

```
min-fresh

该指令要求缓存服务器返回至少还未过指定时间的缓存资源

比如min-fresh为60秒之后，则过了60秒的资源无法作为响应返回
```

```
max-stale

缓存资源即使过期也要接收

未指定参数则一直接收；指定参数，即使过期，只要在max-stale范围内依旧接收
```

```
only-if-cached

缓存服务器不重新加载响应，也不会确认资源有效性

若缓存无响应，返回504 Gateway Timeout
```

```
must-revalidate

代理向源服务器再次验证即将返回的响应缓存目前是否有效

若代理无法获取有效资源，返回504 Gateway Timeout

使用must-revalidate则会忽略max-stale
```

```
proxy-revalidate

所有缓存的服务器在接收到客户端带有proxy-revalidate指令的请求返回相应之前，必须再次验证缓存的有效性

 
```

```
no-transform

无论是请求还是响应，缓存都不能改变实体主体的媒体类型

防止缓存或代理压缩图片等类似操作
```

```
cache-extension token

通过cache-extension token可以扩展Cache-Control首部字段内的指令，仅对能理解的缓存服务器有用
```

**Connection(逐跳首部、连接的管理)**

```
·控制不再转发给代理的首部字段
  在请求或响应中，若Connection：Upgrade，则首部字段Upgrade将被代理服务器删除后再转发

·管理持久连接
  HTTP/1.1的默认连接都是持久连接，当服务器端想断开连接时，则Connection：Close
  HTTP/1.0之前默认非持久连接，若想连接持续，则Connection：Keep-Alive
```

**Date(创建报文的日期时间)**

```
表明创建HTTP报文的时间日期
```

**Pragma(报文指令)**

```
Pragma是HTTP/1.1之前版本的遗留字段，仅作为与HTTP/1.0的向后兼容而定义

虽是通用字段，但只用在请求中

客户端会要求所有的中间服务器不返回缓存的资源
```

**Trailer(报文末端的首部一览)**

```
说明在报文主体后记录了哪些首部字段

可用于HTTP/1.1分块传输编码
```

**Transfer-Encoding(指定报文主体的传输编码方式)**

```
规定传输报文主体时采用的编码方式

HTTP/1.1的传输编码方式仅对分块传输编码有效
```

**Upgrade(升级为其他协议)**

```
检测HTTP协议及其他协议能否使用更高的版本进行通信

其参数值可以用来指定一个完全不同的通信协议

通常Upgrade和Connection：Upgrade一起用

首部字段Upgrade的请求，响应可用101 Switching Protocols
```

**Via(代理服务器的相关信息)**

```
追踪客户端与服务器之间请求或响应报文的传输路径，与TRACE方法并用

可避免请求回环

必须在经过代理时附加Via
```

**Warning(错误通知)**

```
告知用户一些与缓存相关的问题的警告

HTTP/1.1的Waring首部是由HTTP/1.0的响应首部Retry-After演变而来
```

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image024.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image026.png)

## ##请求首部字段

```
客户端发往服务器端的请求报文中的字段

用于补充请求的附加信息、客户端信息、对响应内容相关的优先级等内容
```

**Accept(用户代理可处理的媒体类型)**

```
用以通知服务器，用户代理能够处理的媒体类型及媒体类型的相对优先级

以q=来额外表示权重值，用以给媒体类型增加优先级

q的范围为0~1，小数点后3位

不指定q值，默认位1.0

优先返回权重值最高的媒体类型
```

**Accept-Charset(优先的字符集)**

```
通知服务器用户代理支持的字符集及字符集的相对优先顺序

权重值q

该字段用于内容协商机制的服务器驱动协商
```

**Accept-Encoding(优先的内容编码)**

```
告知服务器用户代理支持的内容编码及内容编码的优先顺序

可一次性指定多种内容编码

权重值q

通配符*，指定任意的编码格式
```

**Accept-Language(优先的语言，自然语言)**

```
告知服务器用户代理能够处理的自然语言集(英文或中文等)，以及自然语言及的相对优先级

可一次性指定多种自然语言集

权重值q
```

**Authorization(Web认证信息)**

```
告知服务器，用户代理的认证信息
```

**Expect(期待服务器的特定行为)**

```
告知服务器，期望出现某种特定行为

做不到而发生错误时，返回417 Expectation Failed
```

**From(用户的电子邮箱地址)**

```
告知服务器使用用户代理的电子邮件地址
```

**Host(请求资源所在服务器)**

```
告知服务器，请求的资源所处的互联网主机名和端口号

因为虚拟主机运行在同一个IP上，故使用首部字段Host加以区分

Host是HTTP/1.1规范内唯一一个必须包含在请求内的首部字段
```

**If-Match(比较实体标记，ETag)**

```
条件请求

服务器收到之后，只有判断指定条件为真时，才会执行请求

指定条件为假，则返回412 Precondition Failed
```

**If-Modified-Since(比较资源的更新时间)**

```
如果在If-Modified-Since字段指定的日期事件后，资源发生更新，服务器会接受请求；在指定日期之后都没更新，则返回304 Not Modified

用以确认代理或客户端拥有的本地资源的有效性
```

**If-None-Match(比较实体标记，与If-Match相反)**

```
If-None-Match字段值的ETag值与请求资源的ETag不一致时，服务器处理该请求

在GET或HEAD方法中使用首部字段If-None-Match可获取最新的资源
```

**If-Range(资源未更新时发送实体byte的范围请求)**

```
If-Range字段值(ETag或时间)与请求资源的ETag或时间相同时，作为范围请求处理

不同时，返回全体资源

不适用If-Range则需要进行两次处理
```

**If-Unmodified-Since(比较资源的更新时间，与If-Modified-Since相反)**

```
告知服务器，请求资源在指定日期之后，未发生更新，则能处理请求

发生更新，则返回412 Precondition Failed
```

**Max-Forwards(最大传输逐跳数)**

```
  每次转发数值减一，数值为0时返回响应

用以把握传输路径的通信状况
```

**Proxy-Authorization(代理服务器要求客户端的认证信息)**

```
认证行为发生在客户端与代理之间

接收到从代理服务器发来的认证质询时，客户端会发送包含Proxy-Authorization的请求，以告知服务器认证所需要的信息
```

**Range(实体的字节范围请求)**

```
告知服务器资源的指定范围，只获取部分资源的范围请求

处理请求之后返回206 Partial Content

无法处理该范围请求，返回200 OK以及全部资源
```

**Referer(对请求中URI的原始获取方)**

```
查看Referer就能知道请求的URI来自哪个Web页面

Referer会告知服务器请求的原始资源的URI
```

**TE(传输编码的优先级)**

```
告知服务器客户端能够处理响应的传输编码方式及相对优先级

TE可以指定传输编码也可以指定伴随trailer字段的分块传输编码的方式
```

**User-Agent(HTTP客户端程序的信息)**

```
将创建请求的浏览器和用户代理名称等信息传达给服务器
```



## ##响应首部字段

```
服务器发给客户端的响应报文中使用

用于补充响应的附加信息、服务器信息、以及对客户端的附加要求等信息
```

 

**Accept-Ranges(是否接收字节范围请求)**

```
告知客户端服务器是否能够处理范围请求，以指定获取服务器端某个部分的资源

可处理范围请求，字段值为bytes

不能处理范围请求，字段值为none
```

**Age(推算资源创建经过时间)**

```
告知客户端，源服务器在多久之前创建了响应，字段值单位为秒

若创建响应的是缓存服务器，Age值是缓存后的响应再次发起认证到认证完成的时间值
```

**ETag(资源的匹配信息)**

```
ETag可告知客户端实体标记

是一种将资源以字符串形式做唯一性标识的方式

服务器为每份资源分配对应的ETag值

资源更新时，ETag值也需要更新

即使资源的URI相同，但中文版和英文版的ETag是不同的

强ETag值：不论实体发生多么细微的变化都会改变其值

弱ETag值：只用于提示资源是否相同。只有资源发生根本变化才会改变ETag值，字段值开始处附加W/
```

**Location(令客户端重定向至指定URI)**

```
可以将响应接收方引导至某个与请求URI位置不同的资源
```

**Proxy-Authenticate(代理服务器对客户端的认证信息)**

```
会把由代理服务器所要求的认证信息发送给客户端

发生于代理与客户端之间
```

**Retry-After(对再次发起请求的时机要求)**

```
告知客户端应该在多久之后再次发送请求

与503 Service Unavailable或3XX Redirect一起使用

字段值可以指定为具体的日期时间或是创建响应后的秒数
```

**Server(HTTP服务器的安装信息)**

```
告知客户端，当前服务器上安装的HTTP服务器应用程序的信息
```

**Vary(代理服务器缓存的管理信息)**

```
对缓存进行控制，源服务器会向代理服务器传达关于本地缓存使用方法的命令

服务器收到Vary，当Accept-Language字段值相同，则直接从缓存返回响应

若不同，则需要先从源服务器端获取资源后才能作为响应返回
```

**WWW-Authenticate(服务器对客户端的认证信息)**

```
用于HTTP访问认证

告知客户端使用于访问请求URI所指定资源的认证方案(Basic或Digest)和带参数提示的质询(challenge)

在401 Unauthorized响应中，必定有WWW-Authenticate
```



## ##实体首部字段

```
在请求和响应中的实体部分中使用

用于补充内容的更新时间等与实体相关的信息
```

**Allow(资源可支持的HTTP方法)**

```
通知客户端能够支持Request-URI指定资源的所有HTTP方法

服务器接收到不支持的HTTP方法，则返回405 Method Not Allowed并将所有能支持的HTTP方法写在Allow之后
```

**Content-Encoding(实体主体适用的编码方式)**

```
告知客户端服务器对实体的主体部分选用的内容编码方式
```

**Content-Language(实体主体的自然语言)**

```
告知客户端，实体主体使用的自然语言
```

**Content-Length(实体主体的大小，字节)**

```
表明实体主体部分的大小，单位为字节

对实体主体进行内容编码传输时，不使用Content-Length
```

**Content-Location(替代对应资源的URI)**

```
给出与报文主体部分相对应的URI

报文主体返回资源对应的URI
```

**Content-MD5**

```
检查报文主体在传输过程中是否保持完整，以及确认传输到达

对报文主体进行MD5，得到128为二进制数，再通过Base64编码，将结果写入Content-MD5字段值

但无法检测出恶意篡改，无法查证内容的偶发性改变
```

**Content-Range(实体主体的位置范围)**

```
针对范围请求，返回响应时使用Content-Range，告知客户端返回的范围请求

单位为字节
```

**Content-Type(实体主体的媒体类型)**

```
说明实体主体内对象的媒体类型
```

**Expires(实体主体过期的日期时间)**

```
将资源失效日期告知客户端

未超时，缓存服务器则一直保存

超时，缓存服务器得到请求之后，向源服务器请求资源
```

**Last-Modified(资源的最后修改日期时间)**

```
指明资源最终的修改时间
```



## ##为Cookie服务的首部字段

```
管理服务器与客户端之间状态的Cookie

调用Cookie时，可以检验其有效性，发送方的域、路径、协议等信息

一旦Cookie从服务器发送至客户，服务器则不能显示删除Cookie，但可通过覆盖已过期的Cookie来实现删除操作
```

**Set-Cookie(开始状态管理所使用的Cookie信息，属于响应首部字段)**

  ![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image028.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image030.png)

```
expires属性

指定浏览器可发送Cookie的有效期

省略expires属性时，有效期极限与维持浏览器会话
```

```
path属性

限制指定Cookie的发送范围的文件目录(但可被避开)
```

```
domain属性

指定的域名可与结尾匹配一致

例如，指定a.com之后，a.com，www.a.com等都可以发送Cookie
```

```
secure属性

限制Web页面仅在HTTPS安全连接时才能发送Cookie，才会进行Cookie回收

省略secure时，无论是HTTP还是HTTPS都会对Cookie进行回收
```

```
httponly属性

使得JavaScript脚本无法获得Cookie

用于防止跨站脚本攻击对Cookie的信息窃取，当然，不是专门为了防止XSS才开发的
```

**Cookie(服务器接收到的Cookie信息，属于请求首部字段)**

```
当客户端向获得HTTP状态管理支持时，就会在请求中包含从服务器收到的Cookie

接收到多个Cookie时，同样可以以多个Cookie形式发送
```



## ##其他首部字段

**X-Frame-Options(防止点击劫持攻击，属于响应首部)**

```
控制网站内容在其他Web网站的Frame标签内的显示问题

防止点击劫持攻击

DENY：拒绝

SAMEORIGIN：仅同源域名下的页面匹配时许可
```



**X-XSS-Protection(控制XSS防护机制，属于响应首部)**

```
针对XSS的一种对策，用于控制浏览器XSS防护机制的开关

0：将XSS过滤设置成无效状态

1：将XSS过滤设置成有效状态
```

**DNT(拒绝个人信息被收集，属于请求首部)**

```
Do Not Track，拒绝个人信息被收集，是一种拒绝被精准广告追踪的方法

0：同意被追踪

1：拒绝被追踪
```

**P3P(保护用户隐私，属于响应首部)**

```
利用P3P技术，让Web网站上的个人隐私变成一种仅供程序可理解的形式，以达到保护用户隐私的目的
```



# #确保Web安全的HTTPS

##  ##HTTP的缺点

### ###通信使用明文可能会被窃听

```
按照TCP/IP协议族的工作机制，通信内容在所有的通信线路上都有可能遭到窥视

互联网的任何角落都存在通信内容被窃听的风险

通信加密：通过SSL或TLS，对HTTP的通信内容进行加密。HTTP+SSL=HTTPS

内容加密：对传输的内容本身进行加密
```



### ###不验证通信放的身份可能遭遇伪装

```
HTTP协议中请求和响应不会对通信放进行确认

服务器是否就是请求URI真正指定的主机？

返回的响应是都真正返回到客户端？

正在通信的双方是否具备访问权限？

任何人都可发起请求

不论是谁发送的请求，都会返回响应

需要证书的参与，用以证明客户端与服务器真实存在，完成认证，身份确认
```



### ###无法证明报文完整性，可能已被篡改

```
接收到的内容可能有误，请求或响应被篡改

中间人攻击：请求或响应在传输途中，遭攻击者拦截并篡改内容的攻击

使用散列值检验，数字签名来防止篡改(无法百分百保证)

仅靠HTTP难以实现完整性
```



### ###在某些特定的Web服务器和特定的Web浏览器中存在脆弱性或漏洞

```

```



### ###编程语言开发的Web应用也可能存在漏洞

```
某php呗
```



## ##HTTP+加密+认证+完整性保护=HTTPS

**HTTP加上加密处理和认证以及完整性保护后即是HTTPS**

**HTTPS是身披SSL外壳的HTTP**

```
HTTPS并非是应用层的一种新协议

将HTTP通信接口部分用SSL和TLS协议替代

不使用SSL时，HTTP直接和TCP通信

使用SSL时，HTTP先和SSL通信，再由SSL和TCP通信
```

**相互交换密钥的公开密钥加密技术**

```
HTTPS采用公钥私钥共用的混合加密机制
```

**证明公开密钥正确性的证书**

```
使用数字证书认证机构和其相关籍贯颁发的公开密钥证书以保证公开密钥正确

EV SSL证书可以证明作为通信一方的服务器是否规范，也可确认对方服务器背后的运营企业是否真实存在。用以防止钓鱼攻击
```

**HTTPS的安全通信机制**

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image032.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image034.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image036.png)

 

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image038.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image040.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image042.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image044.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image046.png)

# #确认访问用户身份的认证

## ##BASIC认证(基本认证)

```
从HTTP/1.0就开始使用的认证方式

Web服务器与通信客户端之间进行的认证方式

采用Base64编码，但未加密

认证使用上不够灵活且安全等级不高
```

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image048.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image050.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image052.png)

## ##DIGEST认证(摘要认证)

```
从HTTP/1.1开始使用

采取质询/响应的方式

提供防止密码被窃听的保护机制，但不防止用户伪装

使用上不够灵感，且达不到高度安全

强于BASIC，弱于HTTPS
```

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image054.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image056.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image058.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image060.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image062.png)

## ##SSL客户端认证

```
借由HTTPS的客户端证书完成认证

凭借证书，服务器可确认访问是否来自 已登录的客户端
```

### ###SSL客户端认证的认证步骤

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image064.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image066.png)

### ###SSL客户端认证采用双因素认证

```
SSL一般会与FormBase一同使用，从而实现双因素认证
```

```
双因素认证：认证过程中不仅需要密码这一个因素，还需要申请认证者提供其他持有信息，从而作为另一个因素，组合使用的认证方式

第一个认证因素的SSL客户端证书用来认证客户端计算机

另一个认证因素的密码用来确认这是本人行为
```

**FormBase认证(基于单表认证)**

```
并不是在HTTP协议中定义的

客户端向服务器的Web应用程序发送登录信息，按登录信息的验证结果认证

认证多半为基于单表认证
```

**Session管理及Cookie应用**

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image068.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image070.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image072.png)

![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image074.png)

## ##Keberos认证

```

```



## ##NTLM认证

```

```

# #基于HTTP的功能追加协议

```
起初的HTTP标准规范，制订者主要想把HTTP当作传输HTML文档的协议

放眼如今，HTTP协议存在限制且自身性能有限
```



## ##消除HTTP瓶颈的SPDY

```
SPDY开发目的在于解决HTTP的性能瓶颈，缩短Web页面的加载时间

在协议层次，消除HTTP的瓶颈

SPDY未完全改写HTTP协议，而是从TCP/IP的应用层与运输层之间添加新的会话层

为了安全，SPDY规定通信中使用SSL
```

**HTTP的瓶颈**

**![img](file:///C:/Users/Gintoki/AppData/Local/Temp/msohtmlclip1/01/clip_image076.png)**

**SPDY的设计与功能**

![image-20230726210524182](C:/Users/Gintoki/AppData/Roaming/Typora/typora-user-images/image-20230726210524182.png)

```
SPDY以会话层的形式加入，控制对数据的流动

SPDY介于TCP(SSL)和HTTP之间

之后的HTTP可以多路复用流、赋予请求优先级、压缩HTTP首部、推送数据、服务器提示客户端资源

多路复用流：所有请求的处理都在一条TCP连接上完成，可无限制处理多个HTTP请求

赋予请求优先级：用以解决发送多个请求时，带宽低而导致响应编变慢

压缩HTTP首部：压缩请求响应首部，减少数据包数量和字节数

服务器推送数据：服务器可直接发送数据，不必等客户端的请求

服务器提示客户端请求的资源：资源已缓存的情况下，可以不发请求
```



## ##使用游览器进行全双工通信的WebSocket

```
WebSocket：Web浏览器与Web服务器之间全双工通信标准

WebSocket是建立在HTTP基础上的协议

用以解决Ajax和Comet里XMLHttpRequest附带的缺陷所引起的问题

Ajax能实时从服务器获取内容，但可能导致大量请求产生

Comet在内容上可以实时更新，但一次连接的持续时间边长，维持连接则消耗更多资源

一旦Web服务器与客户端之间建立起WebSocket协议的通信连接，之后所有的通信都依靠该专用协议进行，通信过程中可互相发送JSON、SML、HTML、图片等任意格式的数据

连接的发起方仍是客户端，一旦确定WebSocket连接，服务器和客户端均可向对方发送报文
```



## ##WebSocket协议的主要特点

**服务器推送数据给客户端**

```
服务器可直接发送数据，不必等待客户端的请求
```

**减少通信量**

```
建立起WebSocket连接，就希望一致保持连接
```

**握手请求**

```
HTTP的Upgrade告知服务器通信协议发生改变，从而握手
```

**握手响应**

```
返回101 Switching Protocols，成功握手后，通信采用WebSocket独立的数据帧
```

**WebSocket API**

```
JavaScript调用WebSocket API提供的WebSocket程序接口，以实现WebSocket协议下全双工通信
```

 

## ##Web服务器管理文件的WebDAV

```
WebDAV是一个可对Web服务器上的内容直接进行文件复制、编辑等操作的分布式文件系统，是扩展HTTP/1.1的协议

可创建、删除文件，可对文件创建者管理、文件编辑过程中禁止其他用户内容覆盖的加锁、对文件内容修改的版本控制
```



## ##WebDAV内新增的方法及状态码

**方法**

```
PROPFIND：获取属性

PROPPATCH：修改属性

MKCOL：创建集合

COPY：复制资源及属性

MOVE：移动资源

LOCK：资源加锁

UNLOCK：资源解锁
```

**状态码**

```
102 Processing：可正常处理请求，目前正在处理

207 Multi-Status：存在多种状态

422 Unprocessible Entity：格式正确，内容有误

423 Locked：资源已被加锁

424 Failed Dependency：处理与某请求关联的请求失败，故不再维持依赖关系

507 Insufficient Storage：保存空间不足
```



# #Web的攻击技术

## ##对Web应用的攻击

**以服务器为目标的主动攻击**

```
主动攻击：攻击者通过直接访问Web应用，把攻击代码传入的攻击模式，直接针对服务器上的资源，例如SQL注入攻击和OS命令攻击
```

**以服务器为目标的被动攻击**

```
被动攻击：利用圈套策略执行攻击代码的攻击模式，攻击者不直接对目标Web应用访问发起攻击
```



## ##因输出值转义不完全引发的安全漏洞

```
跨站脚本攻击

SQL注入攻击

OS命令注入攻击

HTTP首部注入攻击

邮件首部注入攻击

目录遍历攻击

远程文件包含漏洞
```



## ##因设置或设计上的缺陷引发的安全漏洞

```
强制浏览

不正确的错误消息处理

开放重定向
```



## ##因会话管理疏忽引发的安全漏洞

```
会话劫持

会话固定攻击

跨站点请求伪造
```



## ##其他安全漏洞

```
密码破解

点击劫持

DoS攻击

后门程序
```

