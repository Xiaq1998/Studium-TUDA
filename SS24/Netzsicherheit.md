# Netzsicherheit

## Chapter 03: Transport Level Security

###Module 04: TLS and SSH

#### TLS

TLS(Transport Layer Security 传输层安全)是IETF标准化的协议，用于在计算机网络中提供安全通信。TLS在SSLv3的基础上进行了改进和扩展。

**TLS 1.3(basic)**

![Screenshot_2024-06-25 23.57.03_UdmG4d](/Users/summer/Pictures/截屏/Screenshot_2024-06-25 23.57.03_UdmG4d.jpg)

**Key Derivation 密钥派生**

![Screenshot_2024-06-26 00.00.10_AmpNmE](/Users/summer/Pictures/截屏/Screenshot_2024-06-26 00.00.10_AmpNmE.jpg)

**More Features of TLS 1.3**

+ Multiple operation modes 多种操作模式:
  + （会话恢复）If the client wants to resume sessions: 0 RTT
    + 客户端可以在没有额外往返时间的情况下恢复之前的会话，从而减少延迟
  + （不同的会话恢复模式）If the client wants to know the server's PK: different resumption
    + 客户端可以在恢复会话是选择是否需要服务器的公钥信息，以适应不同的安全需求
  + （完全操作模式）Full operation mode present too (1 RTT)
    + 需要一次完整的往返时间来建立新的会话，用于初次链接或在恢复会话不合适的情况下使用
+ Cipher suites 密码套件:
  + no more RC4, CBC, and RSA
+ Improved key derivation 改进的密钥派生:
  + independence of HTK, FSK, and MSK: better provable security
  + session hash used in key derivation

#### SSH

SSH(Secure Shell) Version 1最初设计用于提供一个安全（但轻量级）的替代方案，以取代Unix的r工具（如login、rsh、rcp和rdist），因此SSH代表了一个应用层或会话层协议

+ SSH Architecture(Version 2):
  + SSH follows a **client-server** approach
  + Every SSH server has at least one **host key 主机密钥**
  + SSH version 2 offers two different trust models:
    + （本地数据库信任模型）Every client has a loacl database that associates each host name with the corresponding public host key
    + （CA认证信任模型）The hostname to public key association is certified by a CA and every client knows the public key of the CA

**SSH Protocol Stack**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-06-26 00.59.27_VV1pnL.jpg" alt="Screenshot_2024-06-26 00.59.27_VV1pnL" style="zoom:50%;" />

**SSH Transport Layer Protocol**

+ （服务器认证）server authentication 

  + occurs at transport layer, based on server/host key pair(s) 发生在传输层，基于服务器/主机密钥对

  + server authentication requires clients to know host keys in advance 服务器身份验证要求客户端提前知道主机密钥

+ （数据包交换）packet exchange

  + establish TCP connection
  + can then exchange data
    + identification string exchange, algorithm negotiation, key exchange, end of key exchange, service request
  + using specified packet format

**SSH User Authentication Protocol 用户认证协议**

&rarr; （功能）authenticates client to server 将客户端认证给服务器：认证客户端的身份，使其能够安全地连接到服务器

+ three message types:
  + SSH_MSG_USERAUTH_REQUEST 客户端发送的用户认证请求消息
  + SSH_MSG_USERAUTH_FAILURE 服务器返回的认证失败消息
  + SSH_MSG_USERAUTH_SUCCESS 服务器返回的认证成功消息
+ authentication methods used:
  + public-key 公钥认证
  + password 密码认证
  + host-based 基于主机认证

**SSH Connection Protocol 连接协议**

&rarr; runs on SSH Transport Layer Protocol 运输在SSH传输层协议上：SSH连接协议依赖于SSH传输层协议的安全连接

assumes secure authentication connection 假设已经建立了一个安全的认证连接 &rarr; 意味着传输层协议已经完成了服务器认证和客户端认证

used for multiple logical channels:

+ SSH communications use separate channels 使用独立通道
+ either side can open with unique id number 每个通道都有一个唯一的ID编号
+ flow controlled 流控制
+ have three stages:
  + opening a channel 初始化和打开一个逻辑通道
  + data transfer 通过打开的通道传输数据
  + closing a channel 关闭逻辑通道，结束数据传输
+ four types:
  + session 会话，用于执行远程命令和启动远程会话
  + x11 用于转发X11图形会话
  + forwarded-tcpip 转发TCP/IP：用于将TCP/IP连接从客户端转发到服务器或从服务器转发到客户端
  + direct-tcpip 直接TCP/IP：用于直接建立TCP/IP连接

**Port Forwarding 端口转发**

&rarr; convert insecure TCP connection into a secure SSH connection 将不安全的TCP连接转换为安全的SSH连接:

+ SSH Transport Layer Protocol establishes a TCP connection between SSH client & server 在SSH客户端和服务器之间建立一个TCP连接
+ client traffic redirected to local SSH, travels via tunnel, then remote SSH delivers to server 客户端流量被重定向到本地SSH，通过隧道传输，然后远程SSH将其交付到服务器

supports two types of port forwarding:

+ local forwarding 本地转发 (outgoing tunnel 出站隧道) 
  + "hijacks" selected traffic and sends it to remote port 劫持选定的流量并将其发送到远程端口
+ remote forwarding 远程转发 (incoming tunnel 入站隧道)
  + client acts for server, i.e. traffic arriving at the server at a certain port is forwarded to some port at client 客户端为服务器代理，即到达服务器某个端口的流量被转发到客户端的某个端口



### Module 05: QUIC

**Quick UDP Internet Connections 快速UDP互联网连接**

+ Goals/Use case:
  + （主要目标）client with large number of connections to same server 解决客户端与统一服务器之间大量连接的问题
  + originated with **0-RTT** 最初设计时采用0-RTT（零往返时间）
  + avoids TCP and builds directly **on UDP** 基于UDP而非TC
    +  （原因）UDP相对于TCP更轻量，没有TCP的握手和状态管理，适合低延迟和高吞吐量的应用
  + hardened against DoS 防范DoS攻击
+ Why UDP?
  + UDP allows the user-level application to control each packet 允许用户及应用程序控制每个数据包
  + QUIC implements reliable transport in an application library, rather than letting the OS's TCP library handle it 在应用程序库中实现可靠传输

**TCP/TLS Problem #1: Two Handshakes**

+ TLS can not start its key exchange until after the TCP handshake TLS直到TCP握手之后才能开始密钥交换
+ The speed of light is a hard limitation, so latency will become the dominant factor influencing performance of future networks 光速是一个硬性限制，因此延迟将成为影响未来网络性能的主要因素

![Screenshot_2024-06-26 15.25.15_ljQON0](/Users/summer/Pictures/截屏/Screenshot_2024-06-26 15.25.15_ljQON0.jpg)

+ 双握手过程
  + TCP握手
    + Sender首先发送一个SYN(同步)包
    + Receiver回复一个SYN ACK(同步确认)包
    + Sender再发送一个ACK(确认)包，此时TCP连接建立完成
  + TLS握手
    + 在TCP握手完成后，TLS握手才能开始
    + Sender发送ClientHello包
    + Receiver回复ServerHello, ChangeCipherSpec和Finished包
    + Sender回复ChangeCipherSpec和Finished包
  + 之后才能开始传输应用数据(Application Data)

+ QUIC Handshankes
  + worst case
    + combine TCP+TLS handshakes
  + best case
    + zero-RTT handshake

**HTTP Problem #2: Multiple streams are expensive**

+ 多重流请求开销高
  + Web browsers make many requests to load a page 网页浏览器在家在一个页面时会发出许多请求
  + Each request needs:
    + its own TCP+TLS connection (with significant handshake setup latency) 自己的TCP+TLS连接 &rarr; 会带来显著的握手设置延迟
    + wait for an existing request to finish, in order to reuse its connection 等待现有请求完成，以重用其连接
+ 延迟问题
  + 每个请求如果都要独立进行握手，会导致大量的时间消耗，从而增加页面加载时间
+ 解决方案
  + SPDY and HTTP/2 solved this problem by multiplexing many HTTP connections on a single TCP/TLS socket 通过在单个TCP/TLS套接字上多路复用多个HTTP连接解决了这个问题
    + allows a single socket to handle many HTTP requests **in parallel** 允许单个TCP/TLS连接处理多个HTTP请求
    + adds a **stream id** to distinguish multiple streams in a single socket 使用stream id来区分统一连接中的多个流
    + HTTP/2 is used in about 50% of web traffic 目前HTTP/2大约用于50%的网络流量中
+ HTTP/1.1 vs HTTP/2(multiple streams)
  + HTTP/1.1，每个请求都会建立一个单独的TCP连接
    + 连接开销高
    + 并行限制
  + HTTP/2，在单个TCP连接上处理多个请求
    + 单一连接
    + 多路复用
    + 头部压缩（HPACK）
    + HTTP/2 over TCP is prone to head-of-line blocking 首个阻塞问题
      + TCP is a stream-oriented protocol 流导向协议
        + the application must receive data in order(in a stream) 数据按顺序传递
      + HTTP/2 transmits many HTTP requests' data in a single TCP stream 在一个TCP流中传输多个HTTP请求的数据
      + The dropped packet may involve only one (or a subset) of the HTTP streams, so it's necessary to block them all 如果一个数据包丢失，这个丢包可能只涉及到一个或一部分HTTP流，但TCP强制所有流都等待着个丢失的数据包重新传输并被接收

![Screenshot_2024-06-26 16.33.16_sMWgPh](/Users/summer/Pictures/截屏/Screenshot_2024-06-26 16.33.16_sMWgPh.jpg)

**Head-of-line blocking 队列首阻塞**

&rarr; (in general) HOL blocking is when an item at the head of a queue unnecessaril blocks items behind it 当队列首部的一个项目不必要的阻塞了后面的项目时，就会发生队列首阻塞

+ The fundamental problem is:
  + We're using a **FIFO queue 先进先出队列** for items with no ordering dependence 使用了先进先出队列，而项目之间没有顺序依赖
+ QUIC prevents head-of-line blocking
  + QUIC can allow HTTP streams unaffected by a packet loss to continue while delaying those that must be delayed 可以允许不受数据包丢失影响的HTTP流继续传输，同时延迟必须延迟的流
  + QUIC uses one handshake to support an arbitrary number of independent data streams 使用一次握手来支持任意数量的独立数据流

**Problem #3: HTTP headers are inefficient**

+ Human-readable headers in HTTP waste space 可读的HTTP头浪费空间
+ Gzip compression 压缩
  + HTTP body is possible using a Content-Encoding header, but headers are always plain ASCII text
+ Some headers are repeated in each new request to the server
  + because HTTP is stateless
+ QUIC solution:
  + compress headers 头部压缩：using a scheme called QPACK
  + Downside: lose human-readability, must debug w/a tool like Wireshark

**Problem #4: Mobility**

+ Mobile radios are often shut off, disconnecting TCP sessions
+ Mobile device may re-join the network with a different IP address
+ 解决方案：
  + QUIC uses unique connection IDs



## BGP Security

### How does BGP work?

**BGP is a protocol to announce prefixes, everybody has Neighbors**

==&rarr; BGP announces **IP prefixes** to neighbors 向邻居宣告IP前缀==

+ These neighbors have to be configured 这些邻居必须配置好
+ Each BGP speaking device is part of an **AS(Autonomous System 自治系统)** 每个BGP设备都是AS的一部分
+ The path these announcements take is recorded &rarr; this is called the **Autonomous System Path 自治系统路径**
+ The AS Path shows which AS have forwarded the prefix announcement 自治系统路径显示了哪些AS转发了前缀公告
+ The rightmost AS in the AS Path is called the "Originator" 自治系统路径中最右边的AS被称为“起源者”

**BGP Neighbors**

&rarr; directly connected neighbors 直接连接邻居

+ BGP announces IP prefixes to neighbors: 向邻居宣告IP前
  + These neighbors have to be configured 这些邻居必须配置好
  + BGP uses **TCP** to connect to a neighbor 使用TCP连接到邻居
+ TCP brings already: 提供的功能
  + reliable transport: 可靠传输
    + sender knows that receiver got it 发送方知道接收方已收到数据
  + flow control: 流量控制
    + do not send faster than the receiver can receive 不会发送超过接收方接收能力的数据
  + framing: 帧格式
    + putting BGP messages into packets 将BGP消息打包成数据包

**BGP works incremental 增量工作机制**

&rarr; using add- / withdraw- messages 使用添加/撤回消息

+ At session setup, BGP announces "everything" to its neighbor 会话建立时，BGP向其邻居宣告“所有”内容
+ After that, updates are incremental: 更新是增量的
  + If BGP learns about a new prefix, it sends an **add-message** to neighbors 如果BGP了解到新的前缀，它会向邻居发送添加消息
  + If a prefix goes away, it sends a **withdraw message** to neighbors 如果一个前缀消失了，它会向邻居发送撤回消息
+ As long as the BGP session is "up", a router assumes its neighbors are "in sync" (did not forget anything it sent) 只要BGP会话是“正常的”，路由器就会假设其邻居是“同步的”，即没有遗忘之前发送的任何信息



### BGP and Security

**RFC7454 &rarr; Reference Document on BGP Security**

**Simple Measures**

&rarr; Easy to implement

&rarr; Easy to maintain

&rarr; ... but only of limited use

&rarr; ... still should be implemented

&rarr; List of measures:

1. **Maximun Prefix 最大前缀**

   &rarr; 设置最大前缀是为了防止意外或恶意的路由更新泛滥，导致网络中断或设备过载

   + Good counter-measure against misconfigured peers 最大前缀是一种有效的防护措施，针对配置错误的对等体
   + Definition:
     + Define a threshold 阀值
       + 设置一个前缀数量的上限，超过这个数量就会触发警报
     + Define an action if threshold is hit
   + Possible actions:
     + Tear down session 拆除会话 (until manual intervention 直到手动干预)
       + 在检测到超过阀值后，自动拆除会话，直到管理员手动干预为止
     + Tear down and restart 拆除并重启 (after *n* minutes)
       + 在检测到超过阀值后，自动拆除会话，并在n分钟后重新建立会话
     + Waring only
       + 当达到阀值时，仅发出警告，不进行任何会话操作
   + Best practices:
     + Set threshold high enough 设置足够高的阀值(like 10* usual size)
     + Configure a warning at 90% 在90%的阀值配置警告

   ![Screenshot_2024-06-28 13.11.45_cCQSVd](/Users/summer/Pictures/截屏/Screenshot_2024-06-28 13.11.45_cCQSVd.jpg)

2. **MD5 Session Password / TCP AO(Aothentication Option 身份验证选项)**

   &rarr; MD5已经被认为是不安全的，但仍然在使用中。TCP-AO是一个更现代的替代方案，具有更强的安全性

   + Set the same password on each side 在每一侧设置相同的密码
     + 双方必须配置相同的密码，以便对每个TCP包进行签名
   + Password is used to MD5 sign each TCP packet by the sender 密码用于对每个TCP包进行MD5签名
   + Receiver checks the signature 接收方检查签名
     + If it does not match, packet is silently discarded 如果签名不匹配，包将被静默丢弃
   + Still used, even MD5 no longer state of the art
   + More modern approach: TCP-AO with stronger hashes
   + Recommendation: Use this for iBGP, but not for eBGP
     + 对于iBGP (内部BGP)会话，可以使用MD5或TCP-AO来增加安全性
     + 对于eBGP (外部BGP)会话，建议使用更强的安全措施
   + Some password management is important

   ![Screenshot_2024-06-28 13.16.34_Nhg4Bg](/Users/summer/Pictures/截屏/Screenshot_2024-06-28 13.16.34_Nhg4Bg.jpg)

3. **IP Time-to-live security 生存时间安全性**

   &rarr; IP TTL用于防止未授权的远程主机于BGP邻居建立会话，通过设置并检查数据包的TTL值，可以确保数据包只来自直接相连的设备

   + Send IP packets with initial TTL of 255 发送数据包时设置初始TTL为255
   + Receiver checkes if value is really 255 接收方检查TTL值
     + If not, packet is silently discarded 如果TTL值不是255，数据包将被静默丢弃
   + Very easy to implement 只需要在BGP配置中设置相应的TTL值
     + but must be configured on both sides 通信双方都进行配置才能生效
   + Defined in RFC5082

![Screenshot_2024-06-28 13.33.30_qQsYHO](/Users/summer/Pictures/截屏/Screenshot_2024-06-28 13.33.30_qQsYHO.jpg)

### BGP Filtering

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-06-28 13.36.38_ihyMk0.jpg" alt="Screenshot_2024-06-28 13.36.38_ihyMk0" style="zoom:25%;" />

&rarr; BGP过滤可以确保只有可信赖的路由通告被接受和传播，从而保护网络免受错误或恶意路由的影响

**BGP过滤机制**

+ Raw Input 原始输入
  + 所有接收到的BGP路由通告
+ Blocklist 黑名单
  + 列出明确禁止的前缀和路径。被列入黑名单的路由通告会被直接丢弃，不会进入路由表
+ Allowlist 白名单
  + 列出明确允许的前缀和路径。只有被列入白名单的路由通告才会被考虑放入路由表
+ The Good Stuff 有效路由
  + 同时通过黑名单和白名单过滤的路由通告，确保这些路由是可信且有效的

#### Prefix Filtering 前缀过滤

&rarr; Prefix Filtering用于阻止非路由IPv4和IPv6前缀的传播，以保护网络免受错误配置和恶意活动的影响

**过滤内容：**

+ Block non-routable IPv4 prefixes：阻止不可路由的IPv4前缀
  + Private IPv4 space: 私有IPv4空间
    + 10.0.0.0/8
    + 172.16.0.0/12
    + 192.168.0.0/16
  + IPv4 networks reserved for documentation purposes: 保留用于文档目的的IPv4网络
    + 192.0.2.0/24
    + 198.51.100.0/24
    + 203.0.113.0/24
  + IPv4 multicast address space: 组播地址空间
    + 224.0.0.0/4
  + IPv4 reserved for "future use": 预留用于未来使用的IPv4
    + 240.0.0.0/4
+ Block non-routable IPv6 prefixes：阻止不可路由的IPv6前缀
  + Allow **only** 2000::/3
  + Block everything else
+ Filter against too small and too large prefixes 过滤过小和过大的前缀
  + IPv4:
    + Prefix sizes: /8 - /24
    + Block everything smaller or larger (exception: Blackholing 黑洞路由)
  + IPv6:
    + Prefix sizes: /19 - /48
    + might allow a default route from your upstream providers 可以允许从上游供应商接收默认路由

**More Prefix Filtering**

+ IXP Lan Prefixes (and their more specifics)
  + 过滤互联交换点（IXP）的局域网前缀及其更具体的前缀
+ Your own prefixes
  + 过滤掉本公司网络内部使用的前缀，防止泄漏
+ Your customers prefixes
  + 过滤掉客户的前缀，确保只允许合法的前缀通过，防止错误配置导致路由问题



#### AS Path Filtering

&rarr; 即使前缀完全合法，AS路径可能会有问题。通过对AS路径进行过滤，可以确保路径信息的准确性和可靠性

**过滤条件**

+ Private ASes 私有AS号段
  + 64512 - 65534
  + 4200000000-4294967294
+ Reserved ASes 保留的AS号段
  + 参见IANA的特殊用途AS编号
+ Anywhere in the AS path 路径中的自有AS号
  + 如果AS路径中包含自有AS号，前缀会自动被过滤
+ Regular expressions can be used 使用正则表达式
  + but do not overdo it
  + better split it up

**Filtering from Customers**

+ we need the "Allowlist" 需要使用“允许列表”
+ from customers allow only 仅允许客户的前缀
  + 从客户处接收路由通告时，仅允许他们自己的前缀
+ customers prefixes 仅允许客户的AS号
  + customers ASes (anywhere in the path) 无论客户的AS号出现在路径中的任何位置，都应该接受
  + 如果客户AS号不在路径中，则拒绝
+ use this to create an Allowlist per customer 为每个客户创建单独的允许列表
  + 可以确保每个客户只能通告他们自己授权的前缀，防止错误或恶意通告

**Conclusion**

+ protect your BGP routers and sessions
+ filter incoming
+ unwanted IP Prefixes
+ bogus ASes in the path
+ allow from customers using an Allowlist
+ filter outgoing
+ make sure you announce only valid prefixes



### BGP Error Handling

**BGP Message Types**

&rarr; TCP containing BGP messages

+ OPEN
  + initial message for setting up a session 用于建立会话的初始消息
+ UPDATE
  + incremental routing updates: adds and withdraws 增量路由更新消息，包含新增的前缀和撤回的前缀
+ KEEPALIVE
  + send this if you have nothing to send 如果没有其他消息要发送，则发送此消息以保持会话的活跃状态
+ NOTIFICATION
  + to tell the other side there was an error, and then close the BGP session 当发生错误时，用于通知对端并关闭BGP会话

**Update message**

&rarr; Incremental routing updates 用于传递增量路由更新

+ Update messages can contain multiple things:

  + a list of "adds" 新增前缀列表

    + named "Network Layer Reachability Information (NLRI)" 网络层可达性信息
    + with common attributes 包含公共属性

  + a list of "withdraws" 撤回前缀列表

    + withdraws do not have attributes 撤回前缀没有属性

      <img src="/Users/summer/Pictures/截屏/Screenshot_2024-06-29 12.54.43_Bav7DK.jpg" alt="Screenshot_2024-06-29 12.54.43_Bav7DK" style="zoom:50%;" />

+ Attributes of BGP prefixes:

  + Mandatory attributes 必需属性: have to be there 必须存在
    + e.g.: AS-Path
  + Optional attribute 可选属性: are, well, optional 可选的
    + e.g.: MED (Multi-Exit Discriminator 多出口鉴别器)
  + Transitive attributes 可传递属性:
    + are kept on the prefix and forwarded via BGP 在前缀上保留，并通过BGP转发
    + even (!) when not understoodt by the forwarding device 即使转发设备不理解这些属性，也要保留
  + Non-transitive attributes 不可传递属性: are added to a prefix and not forwarded by the receiver 添加到前缀上，但不会被接收者转发

**More about BGP attributes**

+ Flags: first byte of any attribute

  + Optional (1) or Well-Known (0)
  + Transitive (1) or Non-Transitive (0) (well-known is always transitive)
  + Partial (1) or Complete (0) ("Partial" only for optional transitive)
  + Extended Length Bit (0 = one length octet, 1 = two length octets)
  + Rest of the flags are unused

  ![Screenshot_2024-06-29 13.21.24_BaZJun](/Users/summer/Pictures/截屏/Screenshot_2024-06-29 13.21.24_BaZJun.jpg)

+ Attribute Type: Origin

  + Well-known, Transitive, Mandatory, (and quite simple)
  + Length is one octet
  + Possible values:
    + 0 - IGP
    + 1 - EGP
    + 2 - Incomplete

  ![Screenshot_2024-06-29 13.22.46_3IcMVh](/Users/summer/Pictures/截屏/Screenshot_2024-06-29 13.22.46_3IcMVh.jpg)

+ Attribute Type: AS Path

  + Well-known, Mandatory
  + Realized as "sequence of segments"
  + Segment: (type, length, value)
    + Type = 1: Unordered set of ASes traversed
    + Type = 2: Ordered Set of ASes traversed
    + Length: Number of ASes in value part

  ![Screenshot_2024-06-29 13.23.51_Vu29ZH](/Users/summer/Pictures/截屏/Screenshot_2024-06-29 13.23.51_Vu29ZH.jpg)

**What happens if an attribute is malformed?**

&rarr; Update Message Error Handling 更新消息错误处理

All errors detected while processing the UPDATE message must be indicated by sending the NOTIFICATION message with the **Error Code UPDATE Message Error**. The error subcode elaborates on the specific nature of the error. 所有在处理更新消息是检测到的错误必须通过发送带有错误代码的通知消息来指示。错误子代码详细说明了错误的具体性质。

+ Notification 通知消息: 

  + to tell the other side there was an error, and then close the BGP session. 用于告知对方出现了错误，然后关闭BGP会话

+ Error in Update Messages 更新消息中的错误

  &rarr; shut down the BGP session 关闭BGP会话

  + if any of the well-known attributes contain an error:

    + a notification is sent back 会发送回一条通知消息
    + and the BGP session is closed 并且关闭BGP会话

  + this is how it was until RFC7606

  + RFC7607 changes error handling 修订了错误处理

    &rarr; no longer shutting down the session 不再关闭会话

    + if an attribute contains an error the announcement (add) is treated like a withdraw 如果某个属性包含错误，则公告（添加）将被视为撤回
    + so the session stays up and the "bad" prefix is withdrawn from the BGP table 因此会话保持开启，并且“坏”前缀将从BGP表中撤回

**Conclusion**

+ BGP Error handling has been improved over the years 错误处理已在这些年中得到改进
+ In case of malformed attributes, BGP handles an announcement like a withdrawal 在属性格式错误的情况下，BGP将公告视为撤销处理
+ Implementation bugs may cause major disruptions 实现中的错误可能导致重大中断
+ The quality of a BGP implementation is also affected by how quickly critical bugs are fixed 实现的质量也受到修复关键错误速度的影响



### More security: RPKI

&rarr; Resource Public Key Infrastructure (RPKI) 资源公钥基础设施，一种基于公钥基础设施（PKI）的安全框架，用于验证和确保互联网路由信息的准确性和可靠性

**Certificate: based proof of address assignment 基于证书的IP地址分配证明**

+ there are only 5 entities handing out IP resources
+ these are the 5 RIRs(区域互联网注册管理机构)
+ these are the **trust-anchors** in this model
+ they have contractual proof who they gave which resource
+ and sign you a certificate for it

**RPKI**

+ digitally signed route objects 用于数字签名路由对象
+ resource holders can：
  + get their resources signed and can define how they are announced 资源持有者可以让其资源获得签名，可以定义如何公告这些资源
  + define an Origin-AS 定义一个原始自治系统
  + define a maximum length of a prefix 定义一个前缀的最大长度
  + this is called a **"ROA"(Route Origin Authorisation 路由来源授权)**
+ routers can use this to validate BGP announcements
+ what problem does it want to solve?
  + Certificate - based proof of resource assignment 基于证书的资源分配证明
  + Resources are IP prefixes and AS numbers 资源包括IP前缀和AS号码
  + Verifiable originator AS for each prefix 可验证的前缀起始AS
  + Only allow certain prefix lengths 只允许某些前缀长度

**Validating your ROAs**

validator(RPKI验证器) 的功能及其工作流程

+ fetch resource certificates and ROAs from RIRs (via rsync) 从RIRs获取资源证书和ROAs

+ Validates the "chain of trust" 验证信任链

+ check signatures of certificates 检查证书的签名

+ check signatures of ROAs 检查ROAs的签名

+ supplies a validated cache for your routers 提供验证后的缓存

+ RPKI Validator System Architecture:

  ![Screenshot_2024-06-29 14.24.35_EaqUGf](/Users/summer/Pictures/截屏/Screenshot_2024-06-29 14.24.35_EaqUGf.jpg)



## Chapter 06: Selected Topic

### Firewalls

**What's a Firewall** 

+ Barrier between *us* and *them* *我们* 和*他们* 之间的屏障

+ Limits communication to the outside world 与外界通信的限制
  + The outside world can be another part of the same organization 外界可以是统一组织的另一部分

**Limitations**

+ A firewall is "a sort of crunchy shell around a soft, chewy center" 防火墙虽然提供了外围保护，但是内部仍然脆弱

**Why use Firewall?**

+ most hosts have security holes 大多数主机都有安全漏洞
  + Proof: most software is buggy. Therefore, most security software has security bugs
+ Firewalls run much less code, and hence have few bugs(and holes) 防火墙运行代码少的多，因此漏洞比较少
+ Firewalls can be professionally(and hence better) administered 防火墙可以由专业人员管理
+ Firewalls run less software, with more logging and monitoring 防火墙运行较少的软件，但有更多的日志记录和监控
+ They enforce the partition of a network into separate security domains 他们强制将网络分割成独立的安全域
+ Without such a partition, a network acts as a giant virtual machine, with an unknown set of privileged and ordinary users 没有这种分割，网络就像一个巨大的虚拟器，拥有一组未知的特权和普通用户

**Should we fix the network protocols instead? 我们应该修复网络协议吗？**

+ Network security is not the problem 网络安全不是问题所在
+ Firewalls are not a solution to network problems. They are a network response to a host security problem 防火墙不是网络问题的解决方案，它们是对主机安全问题的网络响应
+ Better network protocols will not obviate the need for firewalls. The best cryptography in the world will not guard against buggy code 更好的网络协议不能消除对防火墙的需求。世界上最好的加密技术也无法防止有漏洞的代码

**Firewall Advantages**

&rarr; if you don't need it, get rid of it 如果你不需要它，就把它丢掉

+ No ordinary users, and hence no passwords for them 没有普通用户，因此没有他们的密码
+ Run as few servers as possible 尽量少运行服务器
+ Install conservative software, don't get the latest fancy servers, etc. 安装保守的软件，不要安装最新的花哨服务器等
+ Log everything, and monitor the log files 记录所有内容，并监控日志文件
+ Keep copious backups, including a "Day 0" backup 保持大量备份，包括“第0天”的备份

**Schematic of a Firewall 防火墙示意图**

![Screenshot_2024-07-02 20.46.52_oYn7ng](/Users/summer/Pictures/截屏/Screenshot_2024-07-02 20.46.52_oYn7ng.jpg)

+ Inside 内部网络
+ Outside 外部网络
+ Gateway 网关
+ Filter 过滤器
+ DMZ (Demilitarized Zone) 隔离区
  + Good spot for things like email and web servers 适合放置邮件和网页服务器等服务
  + Outsiders can send email, retrieve web pages 外部人员可以发送邮件、检索网页
  + Insiders can retrieve email, update web pages 内部人员可以检索邮件，更新网页
  + Must monitor such machines very carefully 必须非常仔细的监控这些机器

**Positioning Firewalls 防火墙的定位**

&rarr; Firewalls protect administrative divisions 防火墙保护管理分区

+ Why Administrative Domains?
  + Firewalls enforce policy 防火墙执行策略
  + Policy follows administrative boundaries, not physical ones 策略遵循管理边界，而不是物理边界

**Firewall Philosophies 防火墙的理念**

+ Block all dangerous destinations 阻止所有危险的目的地&rarr; 必须知道网络中所有部分的所有危险内容
+ Block everything; unblock things known to be both safe and necessary 阻止所有内容，只解锁已知安全且必要的内容 &rarr; much safer

**Types of Firewalls**

+ Packet Filters
+ Dynamic Packet Filters
+ Application Gateways
+ Circuit Relays
+ Personal and/or Distributed Firewalls



### Packet Filters

**Packet Filters 包过滤器**

+ Router-based(and hence cheap) 基于路由器
+ Individual packets are accepted or rejected; no context is used 单个数据包被接受或拒绝；不使用上下文
+ Filter rules are hard to set up; the primitives are often inadequate, and different rules can interact 过滤规则难以设置；原语往往不充分，不同规则之间可能相互作用
+ Packet filters a poor fit for ftp and X11 包过滤器不适合FTP和X11
+ Hard to manage access to RPC-based services 难以管理基于RPC的服务访问

**Running without state 无状态运行**

+ We want to permit outbound connections 希望允许出站连接
+ We have to permit reply packets 必须允许回复数据包
+ For TCP, this can be done without state 对于TCP，可以在无状态下运行
+ The very first packet of a TCP connection has just the SYN bit set. TCP连接的第一个数据包只有SYN位被设置
+ All others have the ACK bit set 其他所有数据包都设置了ACK位
+ Solution: allow in all packets with ACK turned on 允许所有设置了ACK的数据包通过

**Locating Packet Filters 包过滤器的位置**

+ Generally have per-interface rules 通常有每个接口的规则
+ Rules are further divided to apply to inbound or outbound packets on an interface 规则进一步细分为应用于接口上的入站或出站数据包
+ Better to filter inbound packets - less loss of information 更好的选择是过滤入站数据包——信息丢失较少

**Filtering inbound packets**

&rarr; If you filter outbound packets to the DMZ link, you can't tell where they came from 如果过滤发送到DMZ链路的出站数据包，你无法知道他们来自哪里

**Packet Filters and UDP**

+ UDP has no notion of a connection. It is therefore impossible to distinguish a reply to a query - which should be permitted - from an intrusive packet. UDP没有连接的概念。因此无法区分查询的回复（应该被允许）和侵入性的数据包
+ Address-spoofing is easy - no connections 地址欺骗很容易——因为没有连接
+ At best, one can try to block known-dangerous ports. But that's a risky game 最多只能尝试阻止已知危险的端口。但这是一个风险很大的游戏
+ The safe solution is to permit UDP packets through to known-safe servers only 安全的解决方案是只允许UDP数据包通过到已知安全的服务器
+ Example (DNS):
  + Accepts queries on port 53 接受端口53上的查询
  + Block if handling internal queries only; allow if permitting external queries 如果只处理内部查询，则阻止；如果允许外部查询，则允许
  + What about recursive queries? 递归查询怎么办？
    + Bind local respnse socket to some other port; allow inbound UDP packets to it 将本地响应套接字绑定到其他端口；允许入站UDP数据包到达
    + Or put the DNS machine in the DMZ, and run no other UDP services 或者将DNS机器放在DMZ中，并运行其他UDP服务

**ICMP Problems**

&rarr; Internet Control Message Protocol，互联网控制消息协议，用于网络设备在互联网上交换控制信息的协议。

+ Often use ICMP packets in response to TCP or UDP packets 经常使用ICMP数据包作为对TCP或UDP数据包的响应
+ Important example: "Path MTU" response 路径MTU响应
+ Must be allowed in or connectivity can break 必须允许这些数据包进入，否则可能会连接中断
+ Simple packet filters can't match things up 简单的包过滤器无法匹配这些数据包

**The Problem with RPC**

&rarr; Remote Procedure Call 远程过程调用，是一种协议，允许程序在不同的地址空间上执行程序代码。

+ RPC services bind to random port numbers. RPC服务绑定到随机端口号
+ There's no way to know in advance which to block and which to permit 无法提前知道哪些端口需要阻止，哪些需要允许
+ Similar considerations apply to RPC clients 类似的考虑适用于RPC客户端
+ Systems using RPC cannot be protected by simple packet filters 使用RPC的系统无法通过简单的包过滤器保护

**FTP, SIP et al.**

+ FTP Clients(and some other services) use secondary channels 使用辅助通道
+ Again, these live on random port numbers 这些通道位于随机端口上
+ Simple packet filters cannot handle this 简单的包过滤器无法处理这些

**Saving FTP**

+ By default, FTP clients send a **PORT command** to specify the address for an inbound connection 默认情况下，FTP客户端发送一个PORT命令以指定入站连接的地址
+ If the **PASV command** is used instead, the data channel uses a separate outbound connection 如果使用PASV命令，数据通道将使用一个单独的出站连接
+ If local policy permits arbitrary outbound connections, this work well 如果本地策略允许任意出站连接，这种方式效果很好

**The Role of Packet Filters**

+ Packet filters are not very useful as general-purpose firewalls 包过滤器作为通用防火墙并不是非常有用
+ That said, they have their place 尽管如此，它们在某些特殊情况下非常有用
+ Several special situations where they're perfect 有几个特定的情况，它们是完美的

**Simplicity**

+ Packet filters are very simple, and can protect some simple environment 包过滤器非常简单，可以保护一些简单的环境
+ Virtually all routers have the facility built in 几乎所有的路由器都内置了这种功能额

**Address Filtering**

+ At the border, block internal addresses from coming in from the outside 在边界处，阻止外部进入的内部地址
+ Similarly, prevent fake addresses from going out 同样的，防止伪造地址外出



### Stateful Packet Filters

**Stateful Packet Filters 状态化数据包过滤器**

+ Most common type of packet filter 最常见的过滤器类型
+ Sovels may - but not all - of the problems with simple packet filters 与简单的过滤器相比，它解决了许多问题，但不是所有问题
+ Requires per-connection state in the firewall 要求防火墙中为每个连接维护状态

**Keeping State**

+ When a packet is sent out, record that 当发送数据包时，防火墙记录该数据包的信息
+ Associate inbound packet with state created by outbound packet 当接收到入站数据包时，防火墙会将其与之前记录的出站数据包状态相关联

**Problems Solved**

+ Can handle UDP query/response 能够处理UDP查询/响应
+ Can associate ICMP packets with connection 能够讲ICMP数据包于连接相关联
+ Solves some of the inbound/outbound filtering issues - but state tables still need to be associated with inbound packets 解决了一些入站/出站过滤问题，但仍需在入站数据包上维护状态表
+ Still need to block against address-spoofing 仍需阻止地址欺骗

**Remaining Problems**

+ Still have problems with secondary ports 仍然存在次级端口问题
+ Still have problems with RPC 仍然存在RPC问题
+ Still have problems with complex semantics(i.e., DNS) 仍然存在复杂语义问题

**Network Address Translators(NAT) 网络地址转换器**

+ Translates source address(and sometimes port numbers) 地址翻译，将私有IP地址翻译成公共IP地址
+ Primary purpose: coping with limited number of global IP address 节省IP地址
+ It's not really stronger than a stateful packet filter



### Application Firewalls

**Moving up the Stack 为什么要向上移动堆栈？**

——Why move up the stack?

+ Apart from the limitations of packet filters discussed last time, firewalls are inherently incapable of protecting against attacks on a higher layer 吃了之前讨论的包过滤器的局限性，防火墙本质上无法保护高层攻击
+ IP packet filters can't protect against bogus TCP data. IP包过滤器无法防止伪造的TCP数据
+ A TCP-layer firewall can't protect against bugs in SMTP. TCP层防火墙无法保护SMTP中的漏洞
+ SMTP proxies can't protect against problems in the email itself, etc. SMTP代理无法保护电子邮件本身的问题

**Advantages**

+ Protection can be tuned to the individual application 保护可以针对个别应用进行调整
+ More context can be available 可以获得更多上下文信息
+ You only pay the performance price for that application, not others 只需为特定应用支付性能开销，而非所有应用

**Disadvantages**

+ Application-layer firewalls don't protect against attacks at lower layers 应用层防火墙无法保护底层攻击
+ They requier a separate program per application 需要为每个应用程序设置一个独立程序
+ These programs can be quite complex 这些程序可能非常复杂
+ They may be very intrusive for user applications, user behavior, etc. 可能对用户应用程序、用户行为等非常具有侵扰性

**Example: Protecting Email**

+ Email Threats:
  + The usual: defend against protocol implementation bugs
  + Virus-scanning
  + Web bugs in HTML email
+ Inbound Email
  + Email is easy to intercept: MX records in the DNS route inbound email to an arbitrary machine 电子邮件容易被拦截，DNS中的MX记录将入站邮件路由到任意机器
  + Possible to use "*" to handle entire domain 可以使用 “ * ”处理整个域 
  + Net result: all email for that domain is sent to a front end machine 该域的所有电子邮件都发送到前端机器
+ Different Sublayers
  + Note that are multiple layers of protection possible here 有多个保护层可供选择
  + The receiving machine can run a hardened SMTP, providing protection at that layer 接收机器可以运行强化的SMTP，在该层提供保护
  + Once the email is received, it can be scanned at the content layer for any threats 一旦收到电子邮件，可以在内容层扫描任何威胁
  + The firewll function can consist of either or both 防火墙功能可以包括以上任何一种或两者
+ Outbound Email
  + No help from the protocol definition here 协议定义没有帮助
  + But - most MTAs(邮件传输代理) have the ability to forward some or all email to a relay host 但是大多数MTA具有将一些或所有电子邮件转发到中继主机的能力
  + Declare by administrative fiat that this must be done 通过行政命令声明必须这样做
  + In a large organization, some groups will run their own MTA 在大组织中，一些小组将运行自己的MTA
+ Combining Firewall Types
  + Use an application firewall to handle inbound and outbound email 使用应用防火墙处理入站和出站电子邮件
  + Use a packet filter to enforce the rules 使用数据包过滤器来执行规则



### Application Proxies

**Small Application Gateways**

+ Some protocols don't need full-fledged handling at the application level 一些协议不需要再应用层进行完整处理
+ That said, a packet filter isn't adequate 也就是说，包过滤器是不够的
+ Solution: examine some of the traffic via an application-specific proxy; react accordingly 通过特定应用代理检查部分流量，并相应地做出反应

**FTP Proxy**

+ Scan the FTP control channel 扫描FTP控制通道
+ If a **PORT command** is spotted, tell the firewall to open that port temporarily for an incoming connection 当FTP控制通道中的PORT命令被检测到时，通知防火墙临时开放该端口以接收传入的连接
+ Can do similar things with RPC - define filters based on RPC applications, rather than port numbers 通过定义基于RPC应用的过滤器，而不是端口号

**Attacks via FTP Proxy**

+ Downloaded Java applets can call back to the originating host 下载的Java小程序可以回调到源主机
+ A malicious applet can open an FTP channel, and send a PORT command listing a vulnerable port on a nominally-protected host 恶意小程序可以打开FTP通道，并发送一个PORT命令，该命令列出一个名义上受保护的主机上的易受攻击端口
+ The firewall will let that connection through 防火墙会允许该连接通过
+ Solution: make the firewall smarter about what host and port numbers can appear in PORT commands 使防火墙更加智能，能够识别和过滤PORT命令中的主机和端口号

**Web Proxies**

+ Again, built-in protocol support 内置协议支持
+ Provide performance advantage: caching 缓存
+ Can enforce site-specific filtering rules 可以执行特定站点的过滤规则



### Circuit Gateways

**Circuit Gateways 电路网关**

+ Circuit gateways operate at (more or less) the TCP layer 电路网关操作在TCP层
+ No application-specific semantics 无应用程序特定语义
+ Avoid complexities of packet filters 避免数据包过滤的复杂性
+ Allow controlled inband connections, i.e., for FTP 允许受控的入站连接，例如用于FTP
+ Handle UDP 处理UDP
+ Most common one: SOCKS. Supported by many common applications, such as Firefox and Pidgin 最常见的电路网关时SOCKS

**Application Modifications**

+ Application must be changed to speak the circuit gateway protocol instead of TCP or UDP 应用程序必须更改为使用电路网关协议，而不是TCP或UDP
+ Easy for open source 开源软件的修改比较容易
+ Socket-compatible circuit gateway libraries have been written for SOCKS - use those instead of standard C libarary to convert application 已经为SOCKS编写了与套接字兼容的电路网关库——使用这些库代替标准C库来转换应用程序

**Adding Authentication 添加认证**

+ Because of the circuit orientation, it's feasible to add authentication 由于电路导向的特性，可以实现认证
+ Purpose: extrusion control 挤出控制



### Personal and Distributed Firewalls

**Rationale**

+ Conventional firewalls rely on topological assumptions - these are questionable today 传统防火墙依赖于拓扑假设——这些在今天值得怀疑
+ Instead, install protection on the end system 相反，在终端系统上安装保护措施
+ Let it protect itself 让终端系统自我保护

**Personal Firewalls**

+ Add-on to the main protocol stack 主协议栈的附加组件
+ The "inside" is the host itself; everything else is the "outside" “内部”是主机本身；其他一切都是“外部”
+ Most act like packet filters 大多数个人防火墙的作用类似于数据包过滤器
+ Rules can be set by individual or by administrator 规则可以由个人或管理员设置

**Saying "No", Saying "Yes"**

+ It's easy to reject protocols you don't like with a personal firewall 使用个人防火墙拒绝不喜欢的协议很容易
+ The hard part is saying "yes" safely 困难在于安全地说“是”
+ There's no topology - all that you have is the sender's IP address 没有拓扑结构——你唯一拥有的是发送者的IP地址
+ Spoofing IP addresses isn't that hard, especially for UDP 伪造IP地址并不难，尤其是对于UDP

**Application-Linked Firewalls**

+ Most personal firewalls act on port numbers 大多数个人防火墙基于端口号进行操作
+ At least one such firewall is tied to applications - individual programs are or are not allowed to talk, locally or globally 至少有一种这样的防火墙与应用程序相关联——个别程序是否被允许进行本地或全球通信
+ Pros 优点: don't worry about cryptic port numbers; handle auxiliary ports just fine 无需担心难以理解的端口号；可以很好的处理辅助端口
+ Cons 缺点: service applications operate on behalf of some other application 应用程序名称有时也难以理解；服务应用程序可能代表其他应用程序运行

**Distributed Firewalls 分布式防火墙**

+ In some sense similar to personal firewalls, though with central policy control 在某种意义上类似于个人防火墙，但具有集中策略控制
+ Use IPsec to distinguish "inside" from "outside" 使用IPsec区分“内部”和“外部”
+ Insiders have inside-issued certificates; outsiders don't 内部人员拥有内部签发的证书，外部人员没有
+ Only trust other machines with the proper certificate 只信任具有正确证书的其他机器
+ No reliance on topology; insider laptops are protected when traveling; outsider laptops aren't a threat they visit 不依赖拓扑结构：内部笔记本电脑在旅行时也能受到保护；外部笔记本电脑来访时不会构成威胁



### The Problems with Firewalls

**Problems**

+ Corrupt insiders
+ IPsec versus Firewalls
  + jj
+ Connectivity 
+ Laptops 
+ Evasion 





