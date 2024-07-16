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



## Chapter 04: Network Level Security

### Module 01: Intro to Network Level Security

**Layer 3 Security - Network Layer Security**

+ Which technologies did you use?

  + Wireguard
    + simple VPN protocol 简单的VPN协议
    + sends packets over an encrypted UDP tunnel 通过加密的UDP隧道发送数据包
  + OpenVPN
    + complex VPN protocol 复杂的UDP协议
    + several configuration options 有多种配置选项
  + IPSec: direct Extension for IP 直接扩展
  + Ciscos Anyconnect: Proprietary VPN from Cisco

+ Which layer did you choose for your solution?

  + IPSec works on layer 3

  + Other solutions are harder to classify

    &rarr; Except IPSec, most VPNs somewhat violate the classical layer model 除了IPSec，大多数VPN在某种程度上违反了经典层模型

**Scope of Protection Layer 3**

&rarr; Before we discuss the scope of protection, we need to differentiate between **Upper & Lower Layer 3**

+ Upper Layer 3 上层第三层: User space 用户空间

  + Perspective of Internet user 互联网用户的视角

  + Upper Layer 3, is essentially the network layer that was discussed earlier 本质上是前面讨论的网络层

  + Can be accessed by users 用户可以访问

  + Protocols examples: IP, ICMP, etc.

  + Upper Layer 3 Security:

    + Dependency on network technology: none
      + This layer is not dependent on the network technology 这一层不依赖于网络技术
      + The user normally sends out an IP packet using their end-device 用户通常使用他们的终端设备发送IP包
      + Any necessary tunneling/packaging is done by the provider in the backend 任何必要的隧道/封装都是由提供商在后端完成
      + Result: The provider does mind if the content of the packet is encrypted or not, as long as the relevant IP metadata is intact 只要相关的IP元数据是完整的，提供商并不关心数据包的内容是否加密
    + Protection:
      + Data protected in: Black circuits & muxes, circuit & packet switches 在黑色电路和多路复用器、电路和数据包交换机中
      + Data unprotected in: Red LANs, red MTAs, hosts 
    + Protection granularity: hosts, network

    ![Screenshot_2024-07-06 16.25.41_WZX2wJ](/Users/summer/Pictures/截屏/Screenshot_2024-07-06 16.25.41_WZX2wJ.jpg)

+ Lower Layer 3 下层第三层: Telco space 电信空间

  + Perspective of telecommunication providers 电信服务提供商的视角

  + Can not be accessed by normal users 普通用户无法访问

  + Protocol examples: MPLS, Switched Circuits, SNAP, SNDCP, etc.

  + Lower Layer 3 Security:

    + Dependency on provider technology: high 对提供商技术的依赖性很高
      + This layer essentially secures the backend technology 这一层本质上确保了后端技术的安全
      + Lower Layer 3 Security strongly depends on both hardware and software employed by the provider 下层第三层安全性在很大程度上取决于提供商所使用的硬件和软件
    + Protection:
      + Data protected in: Black circuits & muxes 在黑色电路和多路复用器中
      + Data unprotected in: Red LANs & bridges, routers &MTAs 在红色局域网、桥接器、路由器和MTA中
    + Protection granularity 保护粒度: LAN, (sub-)network 

    ![Screenshot_2024-07-06 16.25.10_magAGP](/Users/summer/Pictures/截屏/Screenshot_2024-07-06 16.25.10_magAGP.jpg)

**Developers Perspective**

&rarr; we discuss the third option: Rely on a **network security mechanism** to provide security(Layer 3 and below)

+ Which protocol is most relevant when implementing network security? 实现网络安全时最相关的协议是哪个？

  &rarr; IP or better said IPv4

  + IP is a "narrow" protocol
  + 上层协议（如：电子邮件、WWW、文件共享等）依赖于底层的TCP/UDP协议，再通过IP进行传输
  + 底层协议（如：Token Ring、以太网、WLANIEEE802.11）通过IP协议实现网络连接

+ What IP offers:

  + provides connectionless and best-effort service
  + basically does not give you any guarantees for the delivery packets
  + IP datagrams have no inherent security
    + IP source address can be spoofed
    + Content of IP datagrams can be sniffed
    + Content of IP datagrams can be modified
    + IP datagrams can be replayed



### Module 02: IP Security (IPSec)

**Security Problems of the Internet Protocol(IP)**

&rarr; When an entity receives an IP packet, it has no assurance of:

+ Data origin authentication/data integrity
+ Confidentiality

**IPSec - Overview**

&rarr; IPSec offers security on network layer

+ IPSec is based on the paradigm of a "connection"
  + ...despite the fact that IP is connectionless 尽管IP是无连接的
  + Connection is called "Security Association(SA)" 基于一种称为“安全关联”的连接范式运行
+ Provides security services:
  + Connectionless integrity 无连接完整性
  + Data origin authentication 数据源认证
  + Confidentiality 机密性
  + Rejection of replayed packets 拒绝重放的包
  + Limited traffic flow confidentiality 有限的流量机密性
  + Access control 访问控制
+ IPSec introduces "Protection Protocols":
  + Extra headers between layer 3 and 4 (IP and TCP) to give the destination enough information to identify the "security association": 在第3层和第4层之间添加了额外的头部信息，以提供足够的信息来识别“安全关联”
  + Authentication Header (AH) 认证头
    + Offers message integrity and source authentication but not message confidentiality 提供消息完整性和源认证，但不提供消息机密性
  + Encapsulating Security Payload (ESP) 封装安全负载
    + Offers source authentication, message integrity and confidentiality 提供源认证、消息完整性和机密性
  + Run in two modes:
    + Transport mode, for host-based end-to-end security 传输模式，用于基于主机的端到端安全性
    + Tunnel mode, for security between network borders 隧道模式，用于网络边界之间的安全性

**Authentication Header (AH)**

+ IPSec AH contains an encrypted hash of the whole packet

+ This allows the receiver to verify the authenticity of the addresses and the integrity of the payload and parts of the header

+ Authenticates:

  + IP Header
  + Itself
  + IP Payload

+ Uses HMACs for authentication:

  + Specified are HMACs based on MD5 and SHA1

  ![Screenshot_2024-07-06 17.57.56_HPG76s](/Users/summer/Pictures/截屏/Screenshot_2024-07-06 17.57.56_HPG76s.jpg)

**Encapsulating Security Payload (ESP)**

+ IPSec ESP guarantees the integrity and/or confidentiality of the original datagram combining a secure hash and encrypting the IP payload or the whole IP packet
+ Authenticates itself, IP payload and ESP trailers:
  + HMACs, like with IPSec AH
+ Encrypts IP payload and ESP Trailer:
  + Symmetric encryption(DES, AES, ...)
+ Can be combined with AH

![Screenshot_2024-07-06 18.00.34_2SmcS4](/Users/summer/Pictures/截屏/Screenshot_2024-07-06 18.00.34_2SmcS4.jpg)

**Transport Mode**

+ Sets up a secure end-to-end connection
  + Between tow hosts
+ Keeps original IP header
  + Protocol field is set to indicate that an IPSec header follows
+ Can be used for ESP
+ Can be used for AH & ESP
  + to get encryption together with authenticated IP header
+ Pros:
  + protects IP payload 保护IP有效载荷
  + can do traffic analysis but is efficient (little overhead) 可以进行流量分析，但效率高，开销小
  + good for ESP host to host traffic 适用于ESP主机到主机的通信

**Tunnel Mode**

+ Sets up a secure end-to-end connection

  + Between two networks

    &rarr; not every hosts has to be adapted/maintained

+ Introduces additional IP header

  + With addresses of tunnel endpoints
  + To prevent traffic analysis(when used with ESP)

+ Can be used for AH, ESP, and bot

+ Can be combined with transport mode

  + Between hosts
  + To obtain additional authentication/encryption

+ Pros:

  + encapsulates and protects entire(inner) IP packet 封装和保护整个内部IP包
  + add new header for next hop 为下一跳添加新的头部
  + no routers on way can examine inner IP header 路径上的路由器不能检查内部IP头部
  + good for VPNs, gateway to gateway security 适用于VPN，网关到网关的安全性

**IPSec Working Details**

![Screenshot_2024-07-07 13.31.42_c23gzq](/Users/summer/Pictures/截屏/Screenshot_2024-07-07 13.31.42_c23gzq.jpg)

+ IAD 集成接入设备: 连接总部和分支机构到Internet，使用IPSec协议实现数据加密和认证

+ SA(Security Assocation 安全关联): 用于建立安全隧道

+ R1 converts original datagram into IPSec datagram 将原始数据报转换为IPSec数据包的步骤

  1. 添加ESP Trailer字段：Append to back of original datagram(which includes original header fields) an "ESP trailer" field 将一个“ESP Trailer”字段附加到原始数据报的末尾。这个原始数据报包括原始头字段
     + ESP Trailer: Padding for block ciphers
  2. 加密数据段：Encrypt result using algorithm and key specified by SA 使用由安全关联指定的算法和密钥对结果进行加密
  3. 添加ESP Header字段：Append to front of this encrypted quantity the "ESP header", creating the "envelope" 将这个加密后的数据量的前面添加“ESP Header”字段，创建一个“信封”
     + ESP Header: 
       + SPI, so receiving entity knows what to do
       + Sequence number, to thwart replay attacks
  4. 创建认证MAC：Create authentication MAC over the whole envelope, using algorithm and key specified in SA 使用SA中指定的算法和密钥，在整个新风尚创建一个认证的MAC
  5. 附加MAC到信封：Append MAC to back of envelope, forming payload 将MAC附加到信封的末尾，形成负载
  6. 创建新的IP头：Create brand new IP header, with all the classic IPv4 header fields, which it appends before payload 创建一个全新的IP头，包含所有经典的IPv4头字段，并将其附加到负载之前

  ![Screenshot_2024-07-07 13.47.42_9EmSce](/Users/summer/Pictures/截屏/Screenshot_2024-07-07 13.47.42_9EmSce.jpg)

+ IPSec Sequence Numbers:

  + Protection against replay 重放攻击保护
  + For new SA, sender initializes seq. # to 0 新建SA时，发送方将序列号初始化为0
  + Each time datagram is sent on SA: 每次在SA上发送数据报时，
    + Sender increments seq # counter 发送方递增序列号计数器
    + Places value in seq # field 将#值放入序列号字段
  + Goal:
    + Prevent attacker from sniffing and replaying a packet 防止攻击者嗅探并重放数据包
  + Method:
    + Destination checks for duplicates, but doesn't keep track of all received packets; instead uses a window 目标检查重复数据包，但不跟踪所有接收到的数据包，而是使用窗口机制

+ Algorithm at Receiver

  + If received packet falls in window, packet is new and MAC checks 如果接收的数据包落在窗口内，数据包是新的并且MAC检查通过&rarr; slot in window marked 窗口中的插槽被标记为已使用
  + If received packet is to right of window, MAC check 如果接收的数据包在窗口的右侧，进行MAC检查&rarr; window advanced & right-most slot marked 窗口向前移动，最右边的插槽被标记为已使用
  + If received packet is left of window, already marked or fails MAC check 如果接收的数据包在窗口的左侧，已经被标记或MAC检查失败&rarr; packet is discarded 数据包被丢弃

  ![Screenshot_2024-07-07 14.12.09_l2KDPW](/Users/summer/Pictures/截屏/Screenshot_2024-07-07 14.12.09_l2KDPW.jpg)

  + 窗口机制：
    + 窗口大小：默认W=64
    + N：是接收到的最高序列号
    + 窗口范围：固定窗口大小W，包含最近接收到的N个数据包的序列号
    + 窗口向前移动：当接收到一个有效的新数据包（在窗口右侧），窗口会向前移动以包含这个新序列号
    + 窗口内数据包：当数据包的序列号在当前窗口范围内时，说明这是一个新的数据包，接收方会对其进行MAC验证并标记为已接收
    + 窗口右侧数据包：如果数据包的序列号超出了当前窗口的右边界，接收方会首先进行MAC验证。验证通过后，窗口会向前移动，以包含该数据包，并将相应的插槽标记为已使用
    + 窗口左侧数据包：这些数据包要么已经被接收过，要么是重放攻击。接收方会丢弃这些数据包

**IPSec in IPv6 - Myths**

+ IPv6 is more secure than IPv4
+ IPv6 has better security and it's built in
+ IPv6 has no NAT
+ Global addresses used I'm exposed to the Internet
+ IPv6 Networks are too big to scan
+ IPv6 is too new to be attacked
+ IPv6 is just IPv4 with 128 bits addresses
+ There is nothing new
+ My network is IPv4 only &rarr; IPv6 is not a security problem



### Module 03: IPSec Operation

####Some Implementation consideration

**IPSec Implementation Alternatives:**

+ Host Implementation
  + Advantages of IPsec implementation in end systems:
    + Provision of end-to-end security services
    + Provision of security services on a per-flow basis
    + Ability to implement all modes of IPsec
+ Router (Gateway) Implementation
  + Advantages of IPsec implementation in routers/gateways:
    + Ability to secure IP packets flowing between two networks over a public network such as the Internet:
      + Allows to create virtual private networks (VPNs)
      + No need to integrate IPsec in every end system
    + Ability to authenticate and authorize IP traffic from remote users



####IPSec Databases

**Security Associations (SA) 安全关联**

+ IPsec's security associations

  + Are the abstraction of an IPsec connection 是IPSec连接的抽象

  + Are unidirectional 单向的

    &rarr; Two have to be established for bidirectional communication 双向通信需要建立两个安全关联

  + Consist of (at least) a triplet：由至少一个三元组组成

    + Security Parameter Index (SPI) 安全参数索引: A 32 bit value to distinguish SPI's with identical IP destination address and security protocol
    + IP destination address 目的地址
    + Security Protocol 安全协议: AH or ESP (but not combination in one SA)

  + Define parameters and algorithms for authentication

  + Define parameters and algorithms for encryption

  + There exists a database of Security Associations (SAD)

+ Two kinds of SAs:

  + IKE_SA: "master" 主
    + Long-term validity 长期有效
    + Used to negotiate the CHILD_SA 用于协商CHILD_SA
    + Based on a pre-shared secret or a PKI 机遇预共享密钥或公钥基础设施（PKI）
  + CHILD_SA: "session" 会话
    + Used for data transmission 用于数据传输

+ For establishing a secure communication between two IP hosts: 为在两个IP主机之间建立安全通信

  + Negotiate IKE SA 协商IKE_SA
  + Use IKE SA to negotiate CHILD_SA 使用IKE_SA协商CHILD_SA
  + Use CHILD_SA to encrypt the data to transmit 使用CHILD_SA加密要传输的数据

**Security Parameters Index (SPI) 安全参数索引**

+ Can be up to 32 bits large 长达32位
+ The SPI allows the destination to select the correct SA under which the received packet will be processed: 允许目标选择在接收到的数据包中使用哪个SA进行处理
  + According to the agreement with the sender 根据与发送者的协议
  + The SPI is sent with the packet by the sender 由发送者随数据包一起发送
+ SPI + Dest IP address + IPsec Protocol (AH or ESP) &rarr; uniquely identifies a SA

**SA Database (SAD) 安全关联数据库**

+ Holds parameters for each SA 保存每个SA的参数
  + Lifetime of this SA 生命周期
  + AH and ESP information
  + Tunnel or transport mode 隧道模式或传输模式
+ Every host or gateway participating in IPsec has their own SA database 每个参与IPSec的主机或网关都有自己的SA数据库
+ Is searched using “longest match”: 使用“最长匹配”进行搜索
  1. Search SAD for a match on the combination of SPI, destination, and source addr. If matching process according to SAD entry 根据 SPI、目的地址和源地址的组合在 SAD 中搜索匹配项。如果匹配，则根据 SAD 条目进行处理
  2. Search the SAD for a match on both SPI and destination address. If matching process according to SAD entry 在 SAD 中根据 SPI 和目的地址进行匹配。如果匹配，则根据 SAD 条目进行处理
  3. Search the SAD for a match on only SPI. Process with matching SAD entry. Otherwise, discard packet and log an auditable event 仅根据 SPI 在 SAD 中进行匹配。如果匹配，则根据 SAD 条目进行处理。否则，丢弃数据包并记录可审计事件

**Security Policy Database (SPD) 安全策略数据库**

&rarr; SPD manages SA

+ What traffic to protect? 

  &rarr; Policy entries define which SA or SA bundles to use on IP traffic 策略条目定义了在 IP 流量上使用哪些 SA 或 SA 组合

+ Ordered list of access control entries 访问控制条目的有序列表

+ Nominally static but could be dynamic 通常是静态的，但也可以是动态的

+ Per-interface, inbound & outbound databases, secure trafficdatabase 每个接口的入站和出站数据库，安全流量数据库

+ Each SPD entry specifies: 每个 SPD 条目指定

  + DISCARD 丢弃 (do not let in or out 不允许进入或出去)
  + BYPASS 绕过 (outbound: do not apply IPsec, inbound: do not expect IPsec 出站：不应用 IPsec，入站：不期望 IPsec)
  + PROTECT 保护 (process IPsec (protocols & algorithms) 处理 IPsec（协议和算法）)

+ Traffic characterized by selectors: 通过选择器对流量进行特征描述

  + source/ destination IP addr. (also bit masks & ranges)
  + next protocol, source/ destination ports
  + user or system ID (map to other selectors in an SG)

+ SPD logically separated into three parts:

  1. The SPD-S (secure traffic) contains entries for all traffic subject to IPsec protection. SPD-S（安全流量）包含所有受 IPsec 保护的流量条目
  2. SPD-O (outbound) contains entries for all outbound traffic that is to be bypassed or discarded. SPD-O（出站）包含所有要绕过或丢弃的出站流量条目
  3. SPD-I (inbound) is applied to inbound traffic that will be bypassed or discarded. SPD-I（入站）适用于要绕过或丢弃的入站流量

**Peer Authorization Database (PAD) 对等授权数据库**

&rarr; The PAD provides the link between the SPD and a security association management protocol such as IKE 提供了SPD和安全关联管理协议之间的链接

+ Critical functions:
  + identifies the peers or groups of peers that are authorized to communicate with this IPsec entity
  + specifies the protocol and method used to authenticate each peer
  + provides the authentication data for each peer
  + constrains the types and values of IDs that can be asserted by a peer with regard to child SA creation, to ensure that the peer does not assert identities for lookup in the SPD that it is not authorized to represent, when child SAs are created
  + peer gateway location info, e.g., IP address(es) or DNS names, MAY be included for peers that are known to be "behind" a security gateway

####IPSec Key Management

**IPSec - Key Exchange: Internet Key Exchange (IKE) Protocol 互联网密钥交换**

+ based on Diffie-Hellman key exchange 基于 Diffie-Hellman 密钥交换
  + Supported by “cookies” to prevent denial of service attacks 通过“cookies”防止拒绝服务攻击
+ Sets up IPsec's Security Associations (SA's) 设置 IPsec 的安全关联 (SA)
  + By exchanging/establishing required parameters 通过交换/建立所需参数
+ Consists of two phases:
  + Set up secure control channel 建立安全控制通道
  + Set up security association 建立安全关联

**IKEv1 Key Types**

+ Step 1: Use main mode or agressive mode to establish „secure channel“ 使用主模式或积极模式建立“安全通道”
  + Bidirectional SA, for further use 双向 SA，用于进一步使用
  + For each of main and aggressive, protocols are defined for each of the following key types: 对于主模式和积极模式，每种密钥类型都定义了协议
    + pre-shared secret key
    + public signature keys
    + public encryption keys (old crufty way)
    + public encryption keys (new improved method)
+ Step 2: Use quick mode to establish SA 使用快速模式建立 SA
  + Typically two unidirectional SAs 通常是两个单向 SA

**Main Mode vs. Aggressive Mode**

+ The standard defined one variant as required: 
  + main mode, pre-shared secret keys
  + but nobody uses it
+ the most commonly used scheme became:
  + aggressive mode, pre-shared secret keys

**IKEv1 vs. IKEv2**

+ IKEv1:
  + 9 msgs (ID hiding) or 6 to set up IPsec SA 使用 9 条消息（ID 隐藏）或 6 条消息来建立 IPsec SA
  + 8 different protocols
  + Lots of other issues
    + public encryption keys, must know public key of other side before it sends cert. Original doesn’t even allow sending cert 公共加密密钥，在对方发送证书之前，必须知道对方的公钥。原始版本甚至不允许发送证书
    + original public encryption keys: separately encrypt fields with other side’s public key (requires separate private key ops too). Undefined if field (e.g. name) bigger than an RSA block 原始公共加密密钥：用对方的公钥分别加密字段（也需要单独的私钥操作）。如果字段（例如名字）大于一个 RSA 块，则未定义
+ IKEv2:
  + one protocol, 4 messages, ID hiding 一个协议，4 条消息，ID 隐藏
  + cleaned it up and simplified it a lot

**Traffic Restrictions 流量限制**

+ IPSec Policy:
  + Traffic between these sets of IP addresses (or address ranges), and protocol types, and ports, must have this sort of cryptographic protection 在这些 IP 地址（或地址范围）、协议类型和端口之间的流量必须具有某种加密保
+ Creating SA, specify "traffic selectors" 创建 SA，指定“流量选择器”
+ IKEv1:
  + § Initiator proposes. Responder (if has more restrictive policy) can just say “no” 发起者提出建议。响应者（如果有更严格的策略）可以直接说“不”
+ IKEv2:
  + allowed responder to narrow or say “single address pair” 允许响应者缩小范围或说“单一地址对”

**Lost messages**

+ IKEv1 kind of didn't say
  + had “commit bit”, defined incomprehensibly and almost oppositely in ISAKMP and IKE 有“提交位”，在 ISAKMP 和 IKE 中定义得难以理解且几乎相反
    + ISAKMP: for Bob to tell Alice to wait for his ack. Bob 告诉 Alice 等待他的确认
    + IKE: for Bob to tell Alice to send an ack. Bob 告诉 Alice 发送确认
+ IKEv2:
  + all messages request/response, and requester keeps sending until it gets a response 所有消息都是请求/响应，发起者会一直发送消息直到收到响应

**Fragmentation Attack 分片攻击**

+ IKE runs on top of UDP

  + Message 3 contains certs (depending on authentication choice) and can be really large (encryption of name, name can be very very long). If that’s where cookie is returned, have fragmentation attack 消息 3 包含证书（取决于认证选择），并且可能非常大（名字加密，名字可以非常非常长）。如果此时返回 cookie，可能会遭受分片攻击

    &rarr; Solutions: shorten message 3

**NAT Issues**

&rarr; All sorts of IP protocols violate layering 各种 IP 协议违反分层

+ TCP/UDP:
  + “pseudoheader”: checksum computed on addresses from IP header, and TCP header “伪头”：校验和根据 IP 头和 TCP 头中的地址计算
  + So NAT box must fudge TCP/UDP checksum 因此 NAT 设备必须修改 TCP/UDP 校验和
+ FTP:
  + sends addresses as text string “144.27.8.95“ 以文本字符串形式发送地址“144.27.8.95”
  + NAT must look inside FTP data to change address NAT 必须查看 FTP 数据以更改地址
  + Worse yet! if changes TCP byte numbering: NAT must keep track and fix TCP ack, and msg #’s! 如果更改了 TCP 字节编号：NAT 必须跟踪并修复 TCP 确认和消息编号

**IPSec vs. NAT**

+ AH:
  + Safeguards against spoofing and man-in-the-middle attacks that change the source/destination IPs
  + The hash includes source/destination IPs which are modified by the NAT server
  + Verification of the hash fails on tunnel or transport mode
  + Incompatible with NAT
+ ESP with Tunnel Mode:
  + Full IP packet ciphered and signed but transmitted inside another packet
  + Modification of the outer packet’s IP address does not alter the inner packets content
  + Compatible with NAT

**IPSec vs. SSL/TLS**

+ SSL/TLS is in user space/application; IPsec in OS
  + IPsec protects all apps
+ SSL/TLS is susceptible to a DoS attack:
  + Attacker inserts bogus TCP segment into packet stream:
    + with correct TCP checksum and seq #s
  + TCP acks segment and sends segment’s payload up to SSL.
  + SSL will discard since integrity check is bogus
  + Real segment arrives:
    + TCP rejects since it has the wrong seq #
  + SSL never gets real segment
    + SSL closes conn. since it can’t provide lossless byte stream service
+ What happens if an attacker inserts a bogus IPsec datagram?
  + IPsec at receiver drops datagram since integrity check is bogus; not marked as arrived in seq # window
  + Real segment arrives, passes integrity check and passed up to TCP – no problem!



#### Module 05: VLAN Security

**Virtual LANs can reduce complexity**

+ Before VLAN:
  + One physical cable per subnet 每个子网一条物理电缆
  + Moving hosts requires physical rewiring 移动主机需要重新进行物理布线
  + Adding a new subnet requires adding new wires AND switches 添加新子网需要添加新电线和交换机
  + Bandwidth not shared between subnets 子网之间不共享带宽
+ After VLAN:
  + “Virtual cable” per subnet 每个子网一条“虚拟电缆”
  + Remote reconfiguration of networks 网络的远程重新配置
  + Bandwidth can be shared between subnets 子网之间可以共享带宽

**Typical VLAN Setup**

![Screenshot_2024-07-11 12.47.26_REEOrU](/Users/summer/Pictures/截屏/Screenshot_2024-07-11 12.47.26_REEOrU.jpg)

+ 多个交换机连接了不同的部门设备和服务器
+ 各部门的设备通过交换机连接，并分配有不同的 VLAN ID，以便实现网络隔离和管理

**802.1Q: Overview**

![Screenshot_2024-07-11 12.52.14_bHU9KD](/Users/summer/Pictures/截屏/Screenshot_2024-07-11 12.52.14_bHU9KD.jpg)

+ A layer 2 extension 二层扩展
  + Adds an additional **32 bit field (“tag”)** after the source MAC address 在源 MAC 地址之后添加一个额外的 32 位字段（“标签”）&rarr; 802.1Q Header
+ Each packet gets its own tag 每个数据包都有自己的标签
+ If a packet is not tagged, the switch can add a default tag 如果一个数据包没有被标记，交换机可以添加一个默认标签

**802.1Q: Header**

![Screenshot_2024-07-11 12.54.53_DCsvag](/Users/summer/Pictures/截屏/Screenshot_2024-07-11 12.54.53_DCsvag.jpg)

+ DA & SA 目的MAC地址和源MAC地址

+ TPID - Tag Protocol Identifier (16 bit) 标签协议标识符
  + Indicates that the frame is VLAN tagged 表示帧被 VLAN 标记
  + Value is 0x8100 for 802.1Q tagged frames 对于 802.1Q 标记的帧，值为 0x8100
  + For VLAN unaware devices it looks just like the EtherType/Length field 对于不支持 VLAN 的设备，它看起来就像 EtherType/Length 字段
+ PCP - Priority Code Point (3 bit) 优先级代码点
  + Frame priority according to IEEE 802.1p 根据 IEEE 802.1p 确定帧的优先级
  + From 0 (best effort) to 7 (highest priority)
  + Used for class-of-service (CoS) 用于服务质量 (CoS)
+ DEI - Drop Eligible Indocator (1 bit) 丢弃可行指示符
  + Field formerly used as CFI (Canonical Format Indicator) for Token Ring compatibility 以前用作 CFI（规范格式指示符）以兼容令牌环
  + Indicates if a frame can be dropped in case of congestion 表示在拥塞情况下帧是否可以被丢弃
  + Normally used together with the PCP field 通常与 PCP 字段一起使用
+ VID - VLAN Identifier (12 bit) VLAN标识符
  + Specifies the actual VLAN 指定实际的 VLAN
  + Offers 4094 VLANs 提供 4094 个 VLAN
  + 0x000 (priority frames - CoS) and 0xFFF are reserved

**Modes of Operation**

&rarr; each port of a switch can either be: 交换机端口的操作模式

+ Untagged (Access): 未标记（接入模式）
  + Only regular Ethernet frames are accepted 仅接受常规以太网帧
  + The connected system is not allowed to add tags 连接的系统不允许添加标签
  + Switch adds a defined tag (“native VID”) 交换机添加定义的标签（“本地 VID”）
+ Tagged (Trunk): 标记（干线模式）
  + Switch expects a frame with tag 交换机期望帧带有标签
  + Connected system can set the VID 连接的系统可以设置 VID
  + Untagged packets will be treated as originating from the native VID 未标记的包将被视为来自本地 VID
  + Frames with native VID are typically stripped 带有本地 VID 的帧通常会被剥离

**Possible Attacks:**

+ Double Tagging 双重标记
  + Idea: an Ethernet frame can carry two VLAN extensions 一个以太网帧可以携带两个 VLAN 扩展
  + Attack: an attacker can send frames to other VLANs 攻击者可以向其他 VLAN 发送帧
    1. The attacker adds a second tag (Tag 2) to the frame before sending 攻击者在发送前在帧上添加第二个标签 (Tag 2)
    2. The first switch removes Tag 1 because it’s the ports native VID 第一个交换机移除 Tag 1，因为它是端口的本地 VID
    3. The second switch only sees the attacker’s Tag 2 and outputs the packet to the respective (attacker-controlled) VID 第二个交换机只看到攻击者的 Tag 2，并将数据包输出到相应的（由攻击者控制的）VID
  + Limitation:
    + Attacker needs access to a trunk port 攻击者需要访问一个干线端口
    + Port has to accept frames to the victim VID (Tag 2) 端口必须接收受害者 VID (Tag 2) 的帧
    + Attacker VID (Tag 1) must equal the native VID of the switch’s trunk port, otherwise first tag will not be removed 攻击者 VID (Tag 1) 必须等于交换机干线端口的本地 VID, 否则，第一个标签不会被移除
    + Answers to the packet sent are not getting back to the attacker 发送的数据包的响应不会返回给攻击者
+ Switch Spoofing 交换机欺骗
  + Idea: Switches allow for automatic/dynamic configuration 交换机允许自动/动态配置
    + Using 802.1ak:
      + Multiple VLAN Registration Protocol (MVRP)
      + VLAN Trunking Protocol (VTP) with Cisco hardware
    + 工作原理
      + When a new switch enters the network or the configuration is changed it announces the VLANs to the uplink 当一个新的交换机加入网络或者配置发生改变时，它会向上行链路宣布VLANs
      + Only the switch facing the end system needs to be configured 只有面对终端系统的交换机需要配置
  + Attack: An attacker can use MVRP to announce himself as a switch 攻击者可以使用MVRP宣布自己是一个交换机
    1. Use MVRP to announce all VIDs as configured 使用MVRP宣布所有VIDs已配置
    2. Uplink switches will reconfigure its downlink port accordingly 上行交换机会重新配置其下行端口
    3. Attacker becomes part of all VLANs 攻击者成为所有VLAN的一部分
  + Limitation: 
    + Needs access to one port that supports MVRP/VTP 需要访问一个支持MVRP/VTP的端口

**Attack Mitigation 攻击缓解策略**

+ Switch Spoofing
  + Disable automatic trunk negotiation 禁用自动中继协商
    + at least on “untrusted” ports
    + or only activate it temporarily
  + Explicitly set all non-trunk ports as access ports 明确将所有非中继端口设置为访问端口
+ Double Tagging
  + Set the native VID on trunk ports to an unused VLAN 将中继端口上的本地VID设置为一个未使用的VLAN
  + Explicitly tag native VID packets on a trunk port (must be done on all switches) 明确在中继端口上对本地VID数据包进行标记（必须在所有交换机上进行）
+ Denial-of-Service attacks
  + Use PCP (priorities) to allow mission critical systems to communicate while under a flooding attack 使用PCP（优先级）允许关键任务系统在遭受泛洪攻击时进行通信

**Q&A**

+ Is switch spoofing possible on access ports? 访问端口是否可能进行交换机欺骗？

  &rarr; No, but trunk ports can be created dynamically, e.g. with DTP 不可能，但可以动态创建中继端口，例如使用DTP

+ Is double tagging possible on access ports? 访问端口是否可能进行双重标记？

  &rarr; Yes, if switch accepts tagged frames on access port (and removes it) 是的，如果交换机接受在访问端口上的标记帧（并且移除它们）

  &rarr; Access port VLAN ID must be equal to native VLAN ID on trunk ports 访问端口的VLAN ID必须等于中继端口上的本地VLAN ID

+ How do I get to know the victim VLAN ID for double tagging? 如何知道受害者的VLAN ID以进行双重标记？

  &rarr; Guess, often VLAN ID equals 1 or try all 4094 possibilities 猜测，通常VLAN ID等于1，或者尝试所有4094个可能性

+ Which attack to use if on a trunk port? 在中继端口上使用哪种攻击？

  &rarr; Switch spoofing more powerful 交换机欺骗更强大

  &rarr; But if certain VIDs are blocked only use double tagging 但如果某些VLAN ID被阻止，则只能使用双重标记



### Chapter 05: Link Level Security

#### Module 01: Intro to Link Level Security

**Data Link Layer - Goals**

&rarr; to provide reliable, efficient communication between adjacent machines connected by a single communication channel 通过单一通信通道连接相邻机器，提供可靠、高效的通信

**Scope of Protection Layer 2**

![Screenshot_2024-07-11 13.42.52_hHahsM](/Users/summer/Pictures/截屏/Screenshot_2024-07-11 13.42.52_hHahsM.jpg)

+ Dependency on network technology: Minor 轻微
  + The link layer is dependent on the network technology 链路层依赖于网络技术
  + But: Far less dependent, then lower layer 3 但依赖性远低于第3层
  + Protection:
    + Data protected in: local networks (black/red bridges and corresponding communication links) 本地网络（黑/红桥接和相应的通信链路）
    + Data unprotected in: Outside of the secured network 在安全网络之外
  + Protection granularity: individual hosts, LAN segments 个体主机、局域网段



#### Module 02: Wired Networks

**What is Network Access Authentication 网络访问认证?**

+ (Definition) A mechanism by which access to the network is restricted to authorized entities 网络访问认证是一种通过限制授权实体访问网络的机制
  + Usually identities used are typically userIDs 通常使用用户ID来标识身份

+ Once authenticated, the session needs to be authorized, Authorization can include things like: 一旦身份认证通过，会话需要被授权，授权可以包括以下内容
  + VLANID
  + rate limits
  + filters
  + tunneling

**What could be Problems?**

+ Multi-user machine 多用户设备
  + Each user on a multi-user machine does not need to authenticate once the link is up, so this doesn’t guarantee that only the authenticated user is accessing the network 每个用户在多用户设备上连接后不需要再次认证，因此不能保证只有经过认证的用户在访问网络
+ Hijacking by external attacker 外部攻击者劫持
  + To prevent hijacking, you need per-packet authentication as well 为防止劫持，需要对每个数据包进行认证
  + Encryption orthogonal to authentication 加密与认证是正交的
  + Per-packed MIC based on key derived during the authentication process, linking each packet to the identity claimed in the authentication 每个数据包的MIC（消息完整性检查）基于认证过程中生成的密钥，连接每个数据包与认证中声明的身份

**Network Access Alternatives 网络访问替代方案**

&rarr; Network access authentication has already been implemented at various layers 网络访问认证已经在各个层面实现

+ PHY/MAC 物理层/介质访问控制层
  + Example: 802.11b
  + Pros: no MAC or TCP/IP changes required (all support in firmware) 不需要MAC或TCP/IP更改（所有支持都在固件中）
  + Cons: requires firmware changes in NICs and NASes to support new auth methods, requires NAS to understand new auth types, slows delivery of bug fixes (e.g. WEP v1.0), hard to integrate into AAA 需要网卡（NICs）和网络接入服务器（NASes）固件更改以支持新认证方法，需要NAS理解新认证类型，减缓了漏洞修复（例如WEP v1.0）的交付，难以集成到AAA系统中
+ MAC 介质访问控制层
  + Examples: PPP, 802.1X
  + Pros: no firmware changes required for new auth methods, easier to fix bugs, easy to integrate into AAA, no network access needed prior to authentication, extensible (RFC 2284) 不需要固件更改即可支持新认证方法，易于修复漏洞，易于集成到AAA系统中，认证前不需要网络访问，具有可扩展性（RFC 2284）
  + Cons: requires MAC layer changes unless implemented in driver 需要MAC层更改，除非在驱动程序中实现
+ IP + App-Level Gateway. IP + 应用层网关
  + Examples: hotel access (based on ICMP re-direct to access web server) 酒店访问（基于ICMP重定向访问网页服务器）
  + Pros: no client MAC or TCP/IP changes required (for ICMP re-direct method) 不需要客户端MAC或TCP/IP更改（适用于ICMP重定向方法）
  + Cons: Doesn’t work for all apps, no mutual authentication, partial network access required prior to auth, need to find access control server if not at first hop, typically not extensible, may not derive encryption keys, no accounting (no logoff)
+ UDP/TCP/Application
  + Examples: Proprietary token card protocols 专有令牌卡协议
  + Pros: No client MAC or TCP/IP changes required – can be implemented purely at the application layer 不需要客户端MAC或TCP/IP更改——可以纯粹在应用层实现
  + Cons: requires client software, partial network access required prior to auth, need to find access control server if not at first hop, typically not extensible, no accounting (no logoff)

**Why do Auth at the Link Layer?**

+ It’s fast, simple, and inexpensive 它快速、简单且经济实惠
  + Most popular link layers support it: PPP, IEEE 802 大多数流行的链路层支持它
  + Cost matters if you’re planning on deploying 1 million ports!
+ Client doesn’t need network (services) access to authenticate 客户端无需网络（服务）访问即可认证
  + No need to resolve names, obtain an IP address prior to auth 无需解析名称，在认证前获取IP地址
+ In a multi-protocol world, doing auth at link layer enables authorizing all protocols at the same time 在多协议环境中，在链路层进行认证可以同时授权所有协议
  + Doing it at the network layer would mean adding authentication within IPv4, IPv6, AppleTalk, IPX, SNA, NetBEUI
  + Would also mean authorizing within multiple layers 在多个层次进行授权将导致更多的延迟
  + Result: more delay

**What is IEEE 802.1X?**

&rarr; The IEEE standard for authenticated and auto-provisioned LANs. IEEE 认证和自动配置局域网的标准

+ A framework for authentication and key management: 认证和密钥管理框架

  + IEEE 802.1X derives keys

  + well-known key derivation algorithms
  + can do authentication, or authentication & encryption





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
+ Connectivity 
+ Laptops 
+ Evasion 





## Zusammenfassung

### Fundamentals

**Definition**

+ Asset 资产: an **item of value** to achievement of organizational mission/business objectives. 对实现组织使命/业务目标具有价值的项目
+ Vulnerabilities 弱点: weakness in an information system 信息系统的弱点
+ Threats 威胁: any **circumstance or event** with the potential to cause the security of the system to be compromised. 任何可能导致系统安全受到损害的情况或事件
+ Attacks 攻击: any kind of **malicious activity** that attempts to collect, disrupt, deny, degrade, or destroy information system resources or the information itself. 任何试图收集、破坏、拒绝、降低或毁坏信息系统资源或信息本身的恶意活动
+ Protocol 协议: Communication between **same-layer entities** 同层实体之间的通信
+ Service 服务: Communication between **adjacent Layers** 相邻层之间的通信
+ Connection-oriented
  + Always uses 3 phases: 
    1. Establish Connection 
    2. Transfer data 
    3. Disconnect
  + Analogy: Telephony
+ Connectionless (Datagram Service)
  + Transfer of single data units (often called packets)
  + Analogy: package delivery

**Security Goals**

+ Confidentiality 机密性: Information accessible only for sender and receiver 信息仅供发送者和接收者访问

  &rarr; Need for cryptography (encryption)

+ Integrity 完整性: 

  + Data: Stored/Transmitted data is not modified 存储/传输的数据不会被修改

    &rarr; Need for cryptography, message authentication

  + System: System performs its function as intended 系统按预期执行其功能

    &rarr; Need for hardware mechanism, e.g. secure boot

+ Availability 可用性: Resistance against denial-of-service attacks 抵御拒绝服务攻击

  &rarr; Hard to do with cryptography

  &rarr; Need for access control, routing control

+ Authentication 身份验证:

  + User: Proven identity of communication partners 已证实的通信伙伴身份

    &rarr; Need for means of user authentication

  + Message:  Information associated to communication partner 与通信伙伴相关的信息

    &rarr; Need for means of message authentication

+ Non-Repudiation / Accountability 不可否认性: Denial of communication not possible 无法拒绝通信

  &rarr; Need for digital signatures, “notarization”

**From Goals to Defense**

+ Often used: Cryptography

  &rarr; Mechanisms: Encryption, Digital Signatures, ...

+ Some goals can’t be realized with cryptography alone: 有些目标无法仅靠加密技术实现

  + Availability: can be realized with Access Control 通过访问控制实现
  + Traffic-Flow Confidentiality: requires Traffic-Padding and other mechanisms 需要流量填充和其他机制

**Symmetric vs. Asymmetric**

+ Symmetric: same key to encrypt and decrypt message
+ Asymmetric: two inversely related keys (key pair)

**Four importan concepts**

+ Which security goals can be achieved with Crypto?
  + Confidentiality: Encryption
  + Message Integrity/Message Authentication: Signatures
+ Two additionally relevant concepts:
  + Hashing: Input transformation
  + Diffie-Hellman Key Exchange: Key agreement scheme

**Cryptographic Basics**

+ Software: 
  + Cryptographic libraries (e.g. OpenSSL) 加密库
  + Compiler optimizations 编译器优化
+ Hardware:
  + Specific instructions (e.g. x86 AES instruction set) 特定指令
  + Hardware configurations (e.g. superscalar pipelines) 硬件配置
+ Symmetric Algorithms:
  + Advantage: very fast
  + Disadvantage: need a Pre-Shared Key
+ Asymmetric algorithms:
  + Advantage: usable without shared key
  + Disadvantage: magnitudes slower than symmetric

**Cryptography Handshake**



**ISO-OSI Model**

+ Layer 5: Application (APP) 
  + Include: Application(APP), Presentation(PRES), Session (SES)
  + Abstraction Level: Application-to-Application
  + Addressing method: Application specific addressing
  + DNS

+ Layer 4: Transport (TRANS)
  + Abstraction Level: End-to-End
  + Addressing method: Ports
  + UDP, TCP
+ Layer 3: Network (NET)
  + Abstraction Level: Device-to-Device
  + Addressing method: IP-Addresses
  + IP, ICMP, ARP
+ Layer 2: Data link (MAC)
  + Abstraction Level: Hop-to-Hop
  + Addressing method: MAC-Addresses
+ Layer 1: Physical (PHY)
  + Abstraction Level: Physical Transmission
  + Addressing method: -/-

**IPv4 (The Internet Protocol)**

+ Why an internet layer? 为什么要使用互联网层？
  + Make a bigger network and overcome ALGs 建立更大的网络并克服 ALG
  + Global addressing 全局寻址
  + Virtualize network to isolate end-to-end protocols from network details/changes 虚拟化网络以将端到端协议与网络细节/更改隔离
+ Why a single internet protocol? 为什么要使用单一互联网协议？
  + Maximize interoperability 最大限度地提高互操作性
  + Minimize number of service interfaces 最大限度地减少服务接口数量
+ Why a narrow internet protocol? 为什么要使用狭窄的互联网协议？
  + Assumes least common network functionality to maximize number of usable networks 假设最不常见的网络功能以最大限度地增加可用网络的数量

**Bad Stuff (Malware)**

+ Virus 病毒: Infects files by modifying their source code 通过修改源代码来感染文件
+ Worm 蠕虫: Self-replicating malware that spreads itself through a network 通过网络传播的自我复制恶意软件
+ Trojan 木马: Malware that hides itself in useful software 隐藏在有用软件中的恶意软件
+ These malwares often tend to perform an undesired action: 这些恶意软件往往倾向于执行不良操作
  + Spyware 间谍软件: Collect information from user (such as bank data) 收集用户信息
  + Keylogger 键盘记录器: Spyware that monitors key inputs 监视键盘输入的间谍软件
  + Ransomware 勒索软件: Encrypts target machine, until a ransom is paid 加密目标机器，直到支付赎金
  + Botnets 僵尸网络: Infected machines join a botnet to execute commands on demand (e.g., to drop additional malware) 受感染的机器加入僵尸网络以按需求执行命令

**What Bad Guys Do:**

+ Attacker 1: Eavesdropper 窃听者
  + Attack on Confidentiality 攻击机密性
  + Packet sniffers and wiretappers 数据包嗅探器和窃听器
  + Attacker acts **only passive** 攻击者仅采取被动行为
  + Can not inject packets 无法注入数据包
+ Attacker 2: Off-Path Attacker 路径外攻击者
  + Attack on Authentication 攻击身份验证
  + Trudy can freely inject new packets (actively). Trudy 可以自由注入新数据包
  + Trudy can not read and/or modify any packets in the network. Trudy 无法读取和/或修改网络中的任何数据包
+ Attacker 3: MitM (Man-in-the-Middle)
  + Attack on Confidentiality, Integrity, Authentication 攻击机密性、完整性、身份验证
    + Trudy can freely delay, modify, delete existing packets. Trudy 可以自由延迟、修改、删除现有数据包
    + Trudy can read all messages and can craft new ones. Trudy 可以读取所有消息并可以制作新消息
    + Variation of this attacker: Dolev-Yao Adversary
  + Attack on Availability 攻击可用性
    + Trudy can trivially delay/destroy all packets when in MitM position. Trudy 在处于 MitM 位置时可以轻松延迟/销毁所有数据包

**Defending Systems**

+ Dimension 1: Devices
  + on different nodes
  + Which security service should be realized in which nodes?
    + Integration into Applications
    + Integration into End systems
    + Integration into Intermediate systems
+ Dimension 2: Layers
  + Which security service should be realized in which layer?

![Screenshot_2024-07-16 22.04.52_JG2x7O](/Users/summer/Pictures/截屏/Screenshot_2024-07-16 22.04.52_JG2x7O.jpg)

**Quantizing Vulnerabilities**

+ CVSS (Common Vulnerability Scoring System 通用漏洞评分系统) measures three different sub-scores:
  + Base Score 基本分数: Plain vulnerability score 普通漏洞分数
  + Temporal Score 时间分数: Accounts for temporal parameters 考虑时间参数
  + Environmental score 环境分数: Tailors parameters to a user environment 根据用户环境定制参数

**Reconnaissance 侦察**

&rarr; Gather information about a target 收集有关目标的信息

+ OSINT (Open-Source Intelligence)
  + First reconnaissance step: Analyze publicly available information 分析公开信息
  + Mostly **passive**
+ Defence against OSINT:
  + Keep to a minimum what you put in the public database: only what is necessary 将公共数据库中的内容保持在最低限度，只保存必要的内容

**Active Scanning**

+ Host scanning: Attacker uses ping sweeps to determine live hosts 攻击者使用 ping 扫描来确定活动主机
+ Port scanning: Attacker uses port scans to determine open ports 攻击者使用端口扫描来确定开放端口
+ Fingerprinting/Version Detection: Attackers use port scans to determine information of live services, such as service version 攻击者使用端口扫描来确定活动服务的信息，例如服务版本
+ Network mapping: Attacker often uses traceroute/pathping to determine path to each host discovered during ping sweep 攻击者经常使用 traceroute/pathping 来确定在 ping 扫描期间发现的每个主机的路径
+ Defence against Active Scanning:
  + Filter using firewalls and packet-filtering capabilities of routers 使用防火墙和路由器的数据包过滤功能进行过滤
  + Close all unused ports 关闭所有未使用的端口
  + Scan your own systems to verify that unneeded ports are closed 扫描您自己的系统以验证不需要的端口是否已关闭
  + Intrusion Detection Systems (IDS) 入侵检测系统

### Application Level Security

**Layer 5 Security**

+ Dependency on network technology: None
+ Protection:
  + Data protected in: Entire network, except the application itself
  + Data unprotected in: Application itself

**Application developer 3 options:**

+ Option 1: Implement an application specific security mechanisms (Layer 5) 实施特定于应用程序的安全机制
+ Option 2: Use a security service from a lower layers (Layer 4) 使用较低层的安全服务
+ Option 3: Rely on a network security mechanism to provide security (Layer 3 and below) 依靠网络安全机制提供安全性



## Q&A

1. Resilience Definition 弹性定义
2. How ARP spoofing works. ARP 欺骗的工作原理
3. Can IPSec prevent ARP spoofing. IPSec 能否防止 ARP 欺骗
4. Heartbleed vulnerabilities, Prevention, How it effect Heartbleed 漏洞、预防及其影响
5. Snort rule Snort 规则
6. Why do certificates have an expiration date when there are CRLs? 有 CRL 时证书为什么会有到期日期？
7. Disadvantage of using CRL 使用 CRL 的缺点
8. Advantage of Web of Trust over PKI. Web of Trust 相对于 PKI 的优势
9. Name one IoT product which you won’t use 说出一种你不会使用的 IoT 产品
10. Offline dictionary attack with wpa2 and weakness in wpa3. wpa2 的离线字典攻击和 wpa3 的弱点
11. Why can a recorded TLS 1.2 connection be decrypted afterwards if the PrivatKey is known, why is this not possible with TLS 1.3? 如果知道 PrivatKey，为什么记录的 TLS 1.2 连接事后可以解密，为什么 TLS 1.3 无法做到这一点？
12. How unannounced Prefix hijack works, can BGP routing prevent it? 未通知的前缀劫持如何工作，BGP 路由可以防止它吗？
13. Name two other BGP hijack and explain 说出另外两种 BGP 劫持并解释
14. Advantage of TLS 1.3 over other version. TLS 1.3 相对于其他版本的优势
15. How are downgrade attacks prevented in SSL v3? SSL v3 中如何防止降级攻击？
16. Switch Spoofing, countermeasure, how it works 交换机欺骗、对策、工作原理
17. Hardware fault injection attacks and goals of this attack 硬件故障注入攻击和此攻击的目标
18. Where and how is RC4 used in WEP? WEP 中 RC4 在哪里以及如何使用？
19. In which part is the attack carried out? Why is this possible? -> paper 攻击在哪个部分进行？为什么可能？-> 论文
20. Advantages and disadvantage of applying security measure in application level security 在应用程序级安全中应用安全措施的优点和缺点
21. Name attacks that can be enabled by ARP Spoofing 可以通过 ARP 欺骗启用的名称攻击
22. Goal of ARP Spoofing attack. ARP 欺骗攻击的目标
23. Reconnaissance: potential reason why Nmap recognize port 22 of the host as filtered 侦察：Nmap 将主机的 22 端口识别为已过滤的潜在原因
    + Firewall Blocking: The firewall between the Nmap scanner and the target host is configured to block traffic to port 22. Nmap 扫描器和目标主机之间的防火墙配置为阻止到端口 22 的流量
    + IDS/IPS: An IDS/IPS system may detect the scanning activity and actively block or drop traffic from the Nmap scanner and mark the port as filtered. IDS/IPS 系统可能会检测扫描活动并主动阻止或丢弃来自 Nmap 扫描器的流量，并将端口标记为已过滤
24. How can an attacker with a known plaintext-cyphertext pair (P1,C1) obtain the plaintext P2 from a cyphertext C2 without knowing the decryption key? 具有已知明文-密文对 (P1,C1) 的攻击者如何在不知道解密密钥的情况下从密文 C2 获取明文 P2？
25. PGP: draw signer-signee diagram (simply draw arrows showing who signs whom), then based on this draw different scenarios, whose keys are legitimate 绘制签名者-签名者图（简单地画出箭头表示谁签署了谁），然后根据此图绘制不同的场景，确定谁的密钥是合法的
26. There is ext header address in IPV6 and routing header. Why routing header are not potected, or attack. IPV6 和路由报头中有扩展报头地址。为什么路由报头不受保护或受到攻击
27. Countermeasure of replay attacks 重放攻击的对策
28. Prevention offline dictionary attack 预防离线字典攻击
29. Trust in PGP: Steps. PGP 中的信任：步骤
30. IPSec compares to TLS. IPSec 与 TLS 的比较
31. Definition of Attack, Vulnerability and Threat 攻击、漏洞和威胁的定义
32. An attacker has recorded a TLSv1.2 session? He subsequently received the private key, can he reconstruct the session? Does this still work with TLSv1.3? If not, why not? Which TLSv feature would have prevented this? How are downgrade attacks prevented in SSL v3? 攻击者记录了 TLSv1.2 会话？他随后收到了私钥，他可以重建会话吗？这在 TLSv1.3 中仍然有效吗？如果不行，为什么？哪个 TLSv 功能可以防止这种情况？SSL v3 中如何防止降级攻击？
33. 论文- Paper
    + How des the Wi-Fi power-saving mechanism work? Wi-Fi 省电机制如何工作？
    + 
