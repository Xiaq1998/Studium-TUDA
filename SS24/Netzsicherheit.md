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



