# IT Sicherheit

## Data Link and Network Layers Security

### 1. Network, subnetwork, networks of networks(Internet)

A network is a set of two or more connected computers

Connect more computers to broadcast channel with Hub/Switch

A network can have multiple subnets

Routers connect different networks

Routers connect networks to Internet

![Screenshot_2024-06-25 00.03.31_3X0Ksn](/Users/summer/Pictures/截屏/Screenshot_2024-06-25 00.03.31_3X0Ksn.jpg)



### 2. TCP/IP layers

**Physical Layer**

+ Delivery of individual **bits** over a medium(air, wire, ...)
+ Examples: Fast Ethernet(100BASE-*), Gigabit Ethernet(1000BASE- *), ...

**Data Link Layer**

+ Delivery of **frames**
+ Identified by media access address(MAC address)
+ Examples: Ethernet, IEEE-802.11, PPP

**Internet Layer**

* Delivery of **packets** from one host to another
* Hosts are now addressable over different Networks(if e.g. IPs are unique)
* Example: IP

**Transport Layer**

+ End-to-end communication of **segments** or **datagrams**
+ Congestion Control, Packet reordering/resending, ...(for TCP)
+ Add the concept of **ports**
+ Examples: TCP, UDP

**Each layer uses the lower and services the upper layer for data transmission. 每层均使用下层并为上层提供服务，以进行数据传输**

![Screenshot_2024-06-25 00.20.50_rlufe9](/Users/summer/Pictures/截屏/Screenshot_2024-06-25 00.20.50_rlufe9.jpg)

![Screenshot_2024-06-25 00.25.19_R9o0O0](/Users/summer/Pictures/截屏/Screenshot_2024-06-25 00.25.19_R9o0O0.jpg)

**Each lower layer creates a new data unit by adding additional header information. 每个较低层通过添加附加标头信息来创建新的数据单元**

**Encapsulation: 封装**

+ Each lower layer adds at least *header* information to create new *data unit*. 每个较低层至少添加标头信息以创建新的数据单元
+ Sometimes also *trailer* information is added. 有时还会添加尾部信息
+ If the previous data unit is too big, it can be *fragmented* (split into several smaller parts). 如果前一个数据单元太大，则可以将其碎片化（分成几个较小的部分）
+ Finally, a layer passes the newly created encapsulated data unit(s) to layer below. 最后，一层将新创建的封装数据单元传递给下一层

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-06-25 00.30.58_MFtLXa.jpg" alt="Screenshot_2024-06-25 00.30.58_MFtLXa" style="zoom: 50%;" />

**Devices on the route do not implement the whole stack of layers. 路由上的设备没有实现整个堆栈层**

![Screenshot_2024-06-25 00.40.55_32j0KY](/Users/summer/Pictures/截屏/Screenshot_2024-06-25 00.40.55_32j0KY.jpg)



### 3. IP and MAC addresses

**Addresses: allow devices to communicate(send and receive data) 允许设备进行通信**

+ **IP addresses** between networks: 32 bits
  + Internet Protocol
  + Used in IP layer in TCP/IP
  + Assigned dynamically 动态分配
  + Does not have to be unique 不必是唯一的

+ **Media Access Control addresses 媒体访问控制地址** inside a network: 48 bit / 6 byte Ethernet, Wi-Fi, Bluetooth
  + Used in MAC protocol in data link layer
  + Assigned by vendor 由供应商分配
  + Unique

**Issues with unique fixed IP addresses**

+ Why not use hardcoded IP addresses? 为什么不使用硬编码IP地址

  &rarr;  IP addresses cost money:

  + Wasted IP address wastes money. If you change manually (手动的), this is too much overhead (开销).

+ How many IPv4 addresses?

  &rarr;  2^32^ 



### 4. Address Resolution Protocol(ARP) 

**ARP 地址解析协议**

![Screenshot_2024-06-25 16.27.39_fOKzax](/Users/summer/Pictures/截屏/Screenshot_2024-06-25 16.27.39_fOKzax.jpg)

+ 左边的电脑需要知道右边电脑的MAC地址：**ARP Request**广播请求——Who has 192.168.1.1？Tell 192.168.1.122
+ 右边电脑收到广播请求后回复其MAC地址：**ARP Reply**——192.168.1.1 is at c8:0e:14:41:e2:bd
+ ARP Table：ARP表缓存响应，用于缓存IP地址和MAC地址的映射关系

**ARP Spoofing 欺骗 &rarr; ARP Poisoning**

![Screenshot_2024-06-25 16.22.38_gW4v2Q](/Users/summer/Pictures/截屏/Screenshot_2024-06-25 16.22.38_gW4v2Q.jpg)

+ ARP Spoofing: 攻击者(Host 3) 发送虚假的ARP响应，声称128.64.16.0的MAC地址是33:33:33:33:33:33

+ ARP Poisoning: 网络中的其他设备(例如：Host 1 & Host 2) 接收到虚假的ARP响应后，将错误的IP-MAC映射关系更新到自己的ARP表中

  &rarr; 结果：当Host 1或Host 2尝试与网关128.64.16.0通信时，数据包会被错误地发送到攻击者(Host 3)

**What can attack do with ARP poisoning?**

+ Eavesdrop on packets(passwords, DNS requests, communication) 窃听数据包
+ Intercept and manipulate packets(MitM, Man-in-the-Middle 中间人攻击) 拦截和操纵数据包
+ Drop packets creating DoS 丢弃数据包并造成DoS



### 5. Dynamic Host Configuration(DHCP)

**DHCP 动态主机配置协议——工作过程**

![Screenshot_2024-06-25 16.36.00_Gc8wHO](/Users/summer/Pictures/截屏/Screenshot_2024-06-25 16.36.00_Gc8wHO.jpg)

+ **DHCP Discover** &rarr; 客户端发送DHCP Discover消息，寻找DHCP服务器
  + 客户端发送一个DHCP Discover消息
    + src（源地址）：0.0.0.0
    + dest（目的地址）：255.255.255.255
  + 这是一条广播消息，表示希望获取一个IP地址
+ **DHCP Offer** &rarr; 每个DHCP服务器响应DHCP Offer消息，提供一个可用的IP地址
  + DHCP服务器接收到DHCP Discover消息后，会响应一个DHCP Offer消息
    + src：223.1.2.5
    + dest：255.255.255.255
  + 该消息包含：
    + yiaddrr（服务器分配给客户端的IP地址）：223.1.2.4
    + Lifetime（租期时间）：3600secs
    + DNS IP（DNS服务器地址）：223.1.2.3
    + GW IP（网关地址）：223.1.2.4
+ **DHCP Request** &rarr; 客户端选择一个DHCP Offer，发送DHCP Request消息请求分配该IP地址
  + 客户端从接收到的多个DHCP Offer消息中选择**第一个响应**，并发送一个DHCP Request消息，确认接收其中一个提供的IP地址
  + 该消息包含客户端希望使用的IP地址：
    + yiaddrr：233.1.2.4
+ **DHCP ACK** &rarr; DHCP服务器确认请求，发送DHCP ACK消息，最终确认IP地址分配
  + 选定的DHCP服务器接收到DHCP Request消息后，会发送一个DHCP ACK消息，确认客户端可以使用该IP地址
  + 该消息包含确认的IP地址及租期时间等信息

**DHCP starvation attack 耗尽攻击(DoS)**

**&rarr; 一种拒绝服务攻击，攻击者通过发送大量伪造的DHCP Discover请求，消耗DHCP服务器上的所有可用IP地址池，从而使合法用户无法获取IP地址**

![Screenshot_2024-06-25 17.11.20_MkRrJn](/Users/summer/Pictures/截屏/Screenshot_2024-06-25 17.11.20_MkRrJn.jpg)

+ Attacker
  + 发送大量的DHCP Discover请求
  + 这些请求使用了伪造的MAC地址和事务ID，使每个请求看起来是来自不同客户端
+ DHCP Server
  + DHCP服务器接收到大量的DHCP Discover请求后，会为每个请求分配一个IP地址，并发送DHCP Offer响应
  + 由于每个请求都有不同的伪造的MAC地址，DHCP服务器会认为这是不同的客户端，并为每个请求分配一个IP地址
+ Client
  + 新客户端尝试发送DHCP Discover请求，但由于DHCP服务器的IP地址池已经被耗尽，无法获得可用的IP地址
  + 结果是合法客户端无法从DHCP服务器获取IP地址，无法接入网络

**DHCP Spoofing**

![Screenshot_2024-06-25 17.25.05_NDSkbL](/Users/summer/Pictures/截屏/Screenshot_2024-06-25 17.25.05_NDSkbL.jpg)

+ **DHCP Imposter**
  + 攻击者设置一个伪装的DHCP服务器，试图冒充合法的DHCP服务器
  + 当客户端发送DHCP Discover请求时，伪装的DHCP服务器会快速响应
+ **DHCP Discover**
+ **DHCP Offer**
  + DHCP Imposter接收到Discover消息后，会发送一个DHCP Offer响应
  + 该消息包含：
    + 伪装的IP地址：223.1.2.4
    + 伪装的DNS服务器地址：6.6.6.6
    + 伪装的网关地址：6.6.6.6
  + 由于DHCP Imposter可能响应的速度更快，客户端会选择第一个响应并保存这些信息
+ **DHCP Request**
+ **DHCP ACK**

**What can be done with DHCP Spoofing?**

+ MitM
+ DoS
+ Network Redirection 网络重定向
+ Information Theft 信息窃取

**What target do wo spoof?**

+ The attacker's target is usually to spoof as a legitimate DHCP Server

**What DHCP message do we spoof?**

+ DHCP Offer
+ DHCP ACK



### 6. CIDR and IP addresses' allocation

**Internet protocol version 4(IPv4) uses 32 bit identifiers for addressing interfaces**

+ IPv4 address is written in dotted-decimals 点分十进制 (0 to 255)
+ Each interface has its own IP address 每个接口都有自己的IP地址
+ Routers usually have multiple interfaces(with own IP addresses)
+ Also other hosts might have multiple interfaces

![Screenshot_2024-06-25 17.55.42_JQvBgg](/Users/summer/Pictures/截屏/Screenshot_2024-06-25 17.55.42_JQvBgg.jpg)

**Subnets are sets of interfaces with the same IP prefix which communicate directly 子网是具有相同IP前缀的接口集，可直接通信**

+ Prefix a.b.c.d/p
  + set of IP addresses with same p most significant bits 具有相同p个最高有效位的IP地址集
  + network part 网络部分: p
  + host part 主机部分: remaining(32-p) least significant bits 剩余(32-p)个最低有效位
    + first and last IP of a subnet are reserved for network ID and broadcast 子网的第一个和最后一个IP保留用于网络ID和广播
+ Subnet
  + interfaces with IP addresses in prefix 前缀中具有IP地址的接口
  + can communicate directly with each other(not via router) 可以直接相互通信

+ Subnet mask
  + a 32 bit number that differentiates the host part from the network part



### 7. IP security

+ **IP Spoofing 欺骗**
  + Attacker constructs IP and transport headers with a chosen(spoofed) source IP address 攻击者使用选定的(欺骗性的)源IP地址构建IP和传输标头
  + Requires root privileges 需要root权限

+ **Ingress Filtering 入口过滤**

+ **IP Fragmentation 分段**
  + 最大传输单元(MTU)：网络设备或路径中可以传输的最大数据包大小，不同的网络段可能有不同的MTU值

![Screenshot_2024-06-25 21.17.43_39nYTL](/Users/summer/Pictures/截屏/Screenshot_2024-06-25 21.17.43_39nYTL.jpg)



### 8. Firewalls

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-06-25 21.35.07_ORPhaN.jpg" alt="Screenshot_2024-06-25 21.35.07_ORPhaN" style="zoom:50%;" />

**Protecting the perimeter 保护边界**

+ Blacklisting 黑名单: drop all rest allow 丢弃所有不在允许列表中的流量
+ Whitelisting 白名单: allow all rest drop 允许所有在允许列表中的流量，丢弃其他流量
+ Abort on first match 首次匹配时中止: 一旦匹配到规则，就终止后续规则检查
+ Anti-spoofing Ingress and egress 反欺骗: 检查进入和离开网络的数据包，以防止IP欺骗
+ Service blocking rules:
  + block incoming connections 阻止传入链接
  + restrict outgoing connections 限制传出链接
+ Block incoming requests tu clients 阻止特定协议的入站请求，如：TCP, UDP, ICMP

![Screenshot_2024-06-25 21.41.25_U4j2WA](/Users/summer/Pictures/截屏/Screenshot_2024-06-25 21.41.25_U4j2WA.jpg)

 **Block Spam 阻止垃圾邮件**

+ Attackers can send spam &rarr; prefix gets blacklisted 攻击者可以发送垃圾邮件，这可能导致网络前缀被黑名单
+ Allow SMTP only via Email server 只允许通过指定的电子邮件服务器发送和接收SMTP流量
  + Block port: 25
  + Block egress to port 25 to filter email

![Screenshot_2024-06-25 22.13.10_9OnQha](/Users/summer/Pictures/截屏/Screenshot_2024-06-25 22.13.10_9OnQha.jpg)

**IPtables: packet filter based linux firewall**

+ Iptables is a packet filter-based implementation of the linux kernel firewall - netfilter 是基于包过滤的Linux防火墙实现
+ It defines tables with chain of rules that specify how packets should be treated 它定义了包含规则链的表，这些规则链指定了数据包的处理方式
+ Default rules:
  + iptables -P INPUT DROP: 默认丢弃所有输入数据包
  + iptables -P FORWARD DROP: 默认丢弃所有转发数据包
  + iptables -P OUTPUT ACCEPT: 默认接受所有输出数据包



## Inter-Domain Routing Security

### 1. Interdomain routing with BGP

&rarr; 90s, the Internet takes off and BGP(Border Gateway Protocol 边界网关协议) makes that possible

**How does BGP work? &rarr; Routers exchange BGP messages 路由器交换BGP消息**

+ BGP messages (selected fields):
  + IP prefix is the destination (a.b.c.d/16) IP前缀时目标地址
  + (Selected) attributes:
    + AS(自治系统)-PATH: list of ASes on path from origin to destination 从起始点到目标的自治系统列表
    + NEXT-HOP: next hop AS 下一跳自治系统
+ Router Path Announcement
  + Border routers exchange BGP advertisements 边界路由器（如AS4）向邻居（如AS3）发送包含路径和前缀的BGP广告
+ Border Gateway Router Path Advertisement
  + Routers use most specific prefix to route packets 路由器使用最具体的前缀来决定数据包的路有路径

![Screenshot_2024-06-27 13.40.57_e5KkNA](/Users/summer/Pictures/截屏/Screenshot_2024-06-27 13.40.57_e5KkNA.jpg)

+ 总结
  + BGP通过在边界路由器之间交换路由信息来更新路径
  + 每个AS在接收到路径信息后，会在路径中增加自己的AS，并将更新后的路径信息传递给下一个AS
  + 最终，每个AS都能获得从源到目的地的完整路径信息，并知道下一跳的AS

**BGP Policy-based Routing 基于策略的BGP路由**

+ Policy 策略: to decide which path to accept 决定接受哪条路径

  + e.g., to avoid routing through some countries or to decide if to advertise a path to next AS

+ Provider 提供商: tells all neighbors how to reach customer 通知所有邻居如何到达客户

  + announces paths if and only if to or from customer 仅在涉及到客户的情况下才能发布路径信息

+ Customer 客户: does not want to provide transmit service 不想提供中转服务 &rarr; no motivation, since traffic that passes through does not generate income 没有动力，因为通过其网络的流量不会产生收入

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-06-27 14.13.55_kmB3hf.jpg" alt="Screenshot_2024-06-27 14.13.55_kmB3hf" style="zoom:50%;" />

+ Peer 对等关系: exchange traffic between customers(no $) 在客户之间交换流量

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-06-27 14.14.11_H3dThj.jpg" alt="Screenshot_2024-06-27 14.14.11_H3dThj" style="zoom:50%;" />

**Path Advertisement to Implement Policy 路径广告以实现策略**

+ Shortest path and revenue 最短路径和收益

  + Provider: exports customer's routes to everyone and all routes to a customer 向所有人导出客户的路由，以及所有路由到客户
  + Customer: exports provider's routes to customers 向客户导出提供商的路由
  + To a peer or provider: paths to its own resources and to its customers but not to paths learnt from other providers or peers 仅向自己的资源和客户导出路径，不向其他学到的提供商或对等方导出路径

+ AS2 advertises(AS1|AS2：路径包含AS1和AS2) to AS4 and AS5:

  + if you want to sent to AS1 send through me 如果你想发送到AS1，请通过我（AS2）发送
  + if AS2 does not advertise this, no traffic would flow to AS1 through AS2 如果AS2不广告此路径，则不会有流量通过AS2流向AS1

+ AS4 routes only to/from its customers 仅路由到/来自其客户的流量

+ AS4 does not tell paths to destinations that are not customers 不会告知非客户的目的地路径

  + will not advertise to AS5 a path(AS1|AS2|AS4) 不会向AS5广告（AS1｜AS2｜AS4）的路径

  + AS1 & AS5 are not customers of AS4 &rarr; AS4 does not get paid （AS1和AS5不是AS4的客户，因此AS4不会得到支付）

    + if AS4 tells AS5 that it has a path to AS1, then AS5 could route traffic to AS1 through AS4 &rarr; AS4 has no economic incentive to serve as transmit for traffic from AS5 to AS1 如果AS4告知AS5其有路径到AS1，则AS5可能会通过AS4将流量路由到AS1，而AS4没有经济激励作为AS5到AS1的中转

      &rarr; AS5 does not know there is a route to AS1 via AS4 不知道通过AS4到AS1的路径

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-06-27 14.37.05_9ogC9X.jpg" alt="Screenshot_2024-06-27 14.37.05_9ogC9X" style="zoom:50%;" />



### 2. BGP prefix hijack attacks

**BGP Security:**

+ Hijacks 劫持: 网络流量被错误的或恶意的重定向到不正确的路径
+ Route Leaks 路由泄露

![Screenshot_2024-06-27 15.31.23_ahoNgm](/Users/summer/Pictures/截屏/Screenshot_2024-06-27 15.31.23_ahoNgm.jpg)

**BGP Hijack Goals**

+ Eavesdroppling 窃听
+ Traffic analysis 流量分析
+ DNS poisoning 中毒
+ Spam/phishing 垃圾邮件/网络钓鱼
+ Malware distribution 恶意软件分发
+ Cryptocurrency theft 加密货币盗窃
+ DoS

**BGP Hijack Real Life Example —— April 2010: China Telecom**

+ 中国电信的公告
  + 公告前缀66.174.161.0/24
  + 可能由于且只错误或故意行为导致
+ ISP 1的路径选择
  + 选择了中国电信的路径，导致流量通过中国电信传输
  + 可能因为中国电信的路径看起来更短或其他策略因素
+ Level 3，VZW和22394的路径选择
  + 类似的，选择了通过中国电信的路径，导致流量被重定向

![Screenshot_2024-06-27 15.40.16_7Fktel](/Users/summer/Pictures/截屏/Screenshot_2024-06-27 15.40.16_7Fktel.jpg)

**Prefix hijack attack**

+ prefer shorter route 优先选择较短路径
+ prefer customers over peers and peers over providers 优先选择客户路径而不是对等方和提供商路径
+ Subprefix hijack:
  + prefer a more specific prefix 优先选择更具体的前缀
    + 更具体的前缀意味着该前缀的网络部分更长，主机部分更短，从而指定了一个更小、更精确的子网



### 3. BGP security with RPKI

**How to validate that AS333 is the legitimate origin of 1.2.0.0/16?**

+ Ideas:
  + A list of valid ASes for each prefix
  + Online check in a database(Internet Routing Registries)
  + Offline: digitally signed Route Origin Authorizations

&rarr; Validate BGP announcements with RPKI 使用RPKI验证BGP公告:

+ Only signed origin may announce 1.2/16
  + Routers should filter bogus BGP packets with &**Route Origin Validation** 路由器应该使用 *路由原点验证* 来过滤虚假的BGP数据包
  + Drop announcement of prefixes within 1.2/16 where origin is not AS333 丢弃前缀为1.2/16但源不是AS333的公告

![Screenshot_2024-06-27 16.59.33_UAzX13](/Users/summer/Pictures/截屏/Screenshot_2024-06-27 16.59.33_UAzX13.jpg)

**Resource Public Key Infrastructure(RPKI) 资源公钥基础设施**

+ RFC6480: prefix owner gets Resource Certificate(CR 资源证书)
+ Superprefix owner(e.g., RIPE) signs RC: {prefix, K.owner}~K.RIR~ 
  + RIPE：Réseaux IP Européens 一个为欧洲互联网社区提供协调服务和支持的组织
+ Prefix owner signs ROA: {prefix, AS.origin}~K.owner~
  + ROA：Route Origin Authorization 路由原点授权，一种由前缀所有者创建并签署的加密签名文件，用于授权特定AS对外宣布某个IP前缀
+ Only signed origin may announce 1.2/16 只有签名的源AS可以宣布前缀1.2/16
  + 只有合法的ROA签署的源AS可以对外宣布特定前缀
+ More specific announcement(long prefix) not allowed 不允许更具体的公告（更长的前缀）
  + 防止子前缀劫持攻击，确保前缀公告的合法性和唯一性
+ Announcement of other origin requires another valid ROA 其他源的公告需要另一个有效的ROA
  + 任何其他源要公告同一前缀，必须拥有另一个有效的ROA，确保公告的真实性和授权性

**Internet resources**

+ The Internet is broken up to five zones, each zone managed by a Regional Internet Registry
+ Routers need to obtain validated ROAs 路由器需要获得经过验证的ROA

**RPKI Repository Delta Protocol (RRDP) 存储库增量协议**

&rarr; RRDP是一种用于从RPKI存储库中下载和同步资源对象的协议，主要用于提高RPKI数据的传输效率和可靠性

+ RPs(Relying Party 依赖方) download objects from repositories over RRDP 依赖方从存储库通过RRDP下载对象
+ RRDP lists the data in XML objects 以XML对象的形式列出数据
+ Runs over HTTPS 运行于HTTPS
+ Content of a repository(XML file) can be downloaded over a webserver 存储库的内容（XML文件）可以通过Web服务器下载
+ Data Types:
  + Snapshot.xml
    + 内容：包含存储库中的所有对象
    + 字段：由名称和字节组成
    + 创建：每次有更改时都会重新创建
    + 用途：在客户端进行初始同步时下载该文件，以获取存储库中所有对象的完整快照
  + Delta.xml
    + 内容：包含自上次更新以来的所有更改
    + 用途：用于增量更新客户端的本地状态，减少数据传输量
  + Notification.xml
    + 内容：包含存储库的当前序列号以及指向当前Snapshot.xml和所有Delta.xml的链接
    + 用于：客户端首先下载Notification.xml以获取最新的序列号和更新信息，然后根据需要下载Snapshot.xml或Delta.xml进行同步



### 4. RPKI: misconfigurations and attacks



## BGP Security: Beyond ROV

### Route Origin Validation (ROV) 路由原点验证

**Route Origin Authorization (ROA) 路由原点授权**

&rarr; Prefix-owners sign Route Origin Authorization (ROA), defining allowed origin-AS for each prefix 前缀所有者签署路由原点授权，为每个前缀定义允许的源AS

+ Assume ROA for 1.2/16, origin AS 11. Following would be invalid:
  + Announcements with origin AS 666 and prefix 1.2/16: wrong origin AS
  + and with origin AS 11, and prefix 1.2.3/24: no ROA for subprefix

**Route Origin Validation (ROV) 路由原点验证**

+ Routers deploying ROV drop invalid announcements, mitigating prefix hijacks 部署ROV的路由器会检查收到的BGP公告，验证其源AS是否与ROA中的声明匹配，如果公告无效，路由器将丢弃该公告，从而防止前缀劫持

+ ROV fails against subprefix hijacks 在面对子前缀劫持时ROV可能会失败

  &rarr; IP always routes to the most specific prefix in the routing table

  + 例如，假设有一个前缀1.2/16，合法的ROA声明AS 11是该前缀的源AS
  + 攻击者AS 666宣告了一个更具体的子前缀1.2.3/24
  + 解决方案：
    + ROV++: never send towards subprefix hijack
    + 一种改进的ROV机制，确保不会将流量发送到可能的子前缀劫持路径

+ ROV++ [NDSS21] foils this (and most) subprefix hikacks

  + ROV++通过“从不向子前缀劫持方向发送流量”来防止劫持攻击
  + 子前缀劫持攻击失败：由于流量被黑洞化，没有流量会被路由到攻击者AS 666，从而防止了子前缀劫持

+ ROV fails against Origin Hijacks 在防止源劫持中的局限性

  + Origin hijack: attacker exports announcement with AS-path  containing itself and the legitimate origin 攻击者发布一个包含自己和合法源点的AS路径公告，看起来好像是从合法源点接收到的
  + Problem: ROV(包含ROV++) 会将这种公告视为有效
  + The AS-path contains one more AS (cf. prefix hijack) ⇒ less likely to ‘win’
  +  If there are multiple announcements from same ‘type’ (e.g. customer), prefer shorter AS-path



### BGPsec

**BGPsec: IETF standard against path manipulations 防止路径操纵的IETF标准**

&rarr; BGPsec: 一种由IETF定义的标准，用于防止BGP路径操纵

&rarr; 机制：通过数字签名验证每个AS路径段，确保路径的完整性和真实性

+ 路径签名 Sign
  + ASes sign announcements they export, and validate sigs on incoming announcements. AS签署其导出的公告，并验证传入公告上的签名（即每个AS在将BGP公告发送给下一个AS时，对其路径段进行签名）
+ 签名验证 Verify
  + 接收AS在接收到路径段后，会验证前一个AS的签名
  + 在通过验证后，AS会对新的路径段进行签名，然后发送给下一个AS
  + Add 'next AS' to announcement 将“下一个AS”添加到公告
+ RPKI contains certificates with ASN and public key of that ASN 包含具有ASN的证书以及该ASN的公钥

+ Foils origin hijack 防止源劫持: Attacker can't make a BGPsec-valid origin hijack (or other path-manipulation) 攻击者无法生成有效的BGPsec签名，无法进行BGPsec验证的源劫持或其他路径操纵

+ BGPsec ASes downgrade to BGP for BGP neighbors. BGPsec的AS可能会为了与其BGP邻居通信而降级为普通BGP

  + Why does BGPsec downgrade to BGP?
    + BGPsec ASes do not relay BGPsec info to BGP-only routers. BGPsec AS不会将BGPsec信息转发给仅支持BGP的路由器
    + Even if they did, a rogue AS could just drop the BGPsec info 即使转发了，流氓AS也可能直接丢弃BGPsec信息
      + BGPsec has no registry of adopting ASes 没有采用AS的注册表
      + And adopting ASes may stop signing at any time 采用AS的路由器可能随时停止签名

  &rarr; very limited benefits for partial deployment 部分部署的有限收益

**Security weaknesses of BGPsec**

+ Security benefits are limited to islands (only BGPsec ASes in path) 路径中只有BGPsec
+ Downgrade to (non-authenticated) BGP is trivial for on-path attackers 对于攻击者来说，降级到（未经身份验证的）BGP很容易
+ Only the AS Path is protected; other path attributes can be manipulated 仅AS路径受到保护；其他路径属性可以被操纵
+ No defense against route leaks 无法防御路由泄露
+ BGPsec is also computationally expensive

**BGP-iSec: improved security for BGP**

&rarr; BGP-iSec aims to to improve on the security of BGPsec, esp. in partial adoption, with few modifications to the existing design. 旨在提高BGPsec的安全性，尤其是在部分采用的情况下，对现有设计进行少量修改。

The main modifications: 

+ Enable partial path verification 启用部分路径验证
+ Identify adopters and their PK, prevent unauthorized downgrades to BGP 识别采用者及其PK，防止未经授权降级为BGP
+ Authenticate integrity-protected attributes 验证完整性保护的属性
+ Effective defenses against route leaks 有效防御路由泄露

BGP-iSec Components:

+ Path integrity defense: transitive Signatures
+ Route-leak defenses:
  + Signed OTC attribute
  + Up-Permitted attributes
  + ProConID mechanism

**Transitive Signatures 传递签名**

+ Signatures in BGPsec have the *transitive bit(传递位)* set to **false**. They are not sent to BGP neighbors that do not run BPGsec. （默认情况）在BGPsec中，签名的传递位设置为false。&rarr; 这意味着签名不会发送给不运行BGPsec的BGP邻居
+ Signatures in Secure BGP (S-BGP) had the transitive bit set to **true**, but they were not sent to neighbors who were not running S-BGP. 在S-BGP中，签名的传递位设置为true，但签名仍然不会发送给不运行S-BGP的邻居
+ BGP-iSec sets the transitive bit to **true** and sends signatures to non-adopting neighbors. BGP-iSec将传递位设置为true，并将签名发送给不采用BGPsec的邻居
+ Transitive signatures allow BGP-iSec to enforce downgrade prevention and authenticate adopting (sub)paths. 传递签名允许BGP-iSec执行降级预防和认证采用的（子）路径

+ BGP-iSec prevents fake downgrades: signatures are relayed by all ASes; RPKI identifies adopters, keys. BGP-iSec防止伪造降级攻击，签名由所有AS转发；RPKI识别采用者和密钥
+ Significant security - for some overhead 传递签名提供了显著的安全性，尽管需要一些额外的开销
+ Transitive signatures with partial path verification alone completely prevent hijacks of adopting origins. 仅通过部分路径验证的传递签名，就可以完全防止对采用BGPsec的原点进行劫持
+ Protects announcement integrity, e.g., the OTC anti-leakage mechanism. 传递签名机制保护BGP公告的完整性，防止路径泄露
+ Transitive signatures cannot prevent BGP-compliant leaks
  + With BGPsec, attacker can (leak) origin-hijack by degrading to BGP
  + With transitive signatures (BGP-iSec), attacker can leak announcement they received or hijack from a non-adopting AS, e.g., AS 1.
  + Rogue announcement, but contains a valid signatures by adopting ASes!

**Route leak 路由泄露**

&rarr; Route leak: attacker exports to provider/peer a path it did not receive from a customer. 路由泄露指一个AS将从非客户接收到的路由公告错误的转发给了其他AS，违反了预期的BGP路径传播规则

+ Announcement from customer should only contain an **up-path**(customer exports to provider). In announcement from peer, path should be up except the last (peer) edge.
+ Leaks can be intentional attacks or not (misconfigurations, "fat fingers"), and leak can be BGP-compliant 泄露也可以是合法的

**Defenses against Route Leaks**

+ Prefix and path filtering: only by provider of leaking AS

+ Detect and Fightback (announce subprefix): attacker can do it too

+ Only-to-Customer (OTC) attribute [RFC9234]

  + RFC-9234 defines the OTC attribute, indicating that the route should be propagated Only To Customers 路由应仅传播给客户
  + OTC prevents unintentional leaks; growing adoption 可防止意外泄露；采用率不断提高
  + The OTC attribute is unauthenticated; a malicious attacker can remove it 未经身份验证；恶意攻击者可以将其删除
  + Signed OTC
    + BGP-iSec’ transitive signatures authenticate the OTC attribute, preventing also malicious route leaks. BGP-iSec的传递签名机制可以对OTC属性进行认证，防止恶意的路径泄露
    + By authenticating OTC [RFC9234], BGP-iSec foils significantly more post-ROV routing attacks. 通过对OTC进行身份验证，BGP-iSec可以阻止更多后ROV路由攻击
    + OTC attributes are already in use; authenticates on reaching BGP-iSec adopting AS. OTC属性已在使用中；在到达采用AS的BGP-iSec时进行身份验证
    + BGP-iSec has two other defenses which improve prevention of intentional leaks: **the UP attributes and the ProConID mechanism** 

+ BGP-iSec: UP(Up Permitted) Attributes

  &rarr; indicate whether an announcement can be sent to providers (upward) 用于指示一个公告是否可以发送给提供商（向上传播）

  + The two UP attributes:
    + UP~Pre~: contains a random string x
    + UP~Img~: contains h(x), where h is a crypto-hash function
  + UP attribute的操作机制:
    + 移除UPPre：The UP Preimage is removed when an announcement is sent to a customer or peer(downward) 当公告发送给客户或对等体（向下传播）时，UPPre会被移除
    + 不可逆性：Since the hash function cannot be reversed, the preimage cannot be re-added 由于哈希函数不可逆，移除的前像不能被重新添加
  + Authenticated UP attributes make shortening a leaked AS path more difficult 经过验证的UP属性使得缩短泄露的AS路径更加困难
  + Hash functions are computationally efficient and the digests can be small 哈希函数计算效率高，摘要可以很小
  + Drawback: an eavesdropping adversary can capture the preimage 窃听对手可以捕获原像

+ BGP-iSec: ProConID

  + Adopting AS *X* 签署P~x~
    + P~x~: a list of X's nearest-provider BGP-iSec ASes 是一个包含X最近的提供商BGP-iSec AS的列表
    + ProConID provides even stronger protection against route leaks than UP attributes 提供的针对路由泄露的保护甚至比UP属性更强
    + Provider cones are small on average (median size is around 30) 提供商锥体平均较小（中位数约为30）
    + The overhead of updating and maintaining the ProConID-list is reasonably low 更新和维护ProConID列表的开销相当低

+ AS Provider Authorization (ASPA)

  &rarr; ASPA(Autonomous System Provider Authorization), eliminates many route leaks and some other attacks/misconfigurations

  + ASPA(X): X的供应商的签名列表（在RPKI中）



## Domain Name Systemn Security

### DNS

&rarr; DNS(Domain Name System 域名系统) translates hostnames to resources 域名系统是一种将主机名转换为资源的系统。这些资源通常是IP地址，也可以是其他信息

Example: www.foo.com to 1.2.3.4

![Screenshot_2024-07-02 16.58.06_J2C9GO](/Users/summer/Pictures/截屏/Screenshot_2024-07-02 16.58.06_J2C9GO.jpg)



### DNS cache poisoning

&rarr; DNS cache poisoning(DNS 缓存中毒)，是一种网络攻击，攻击者向DNS解析器注入伪造的DNS记录，从而将用户引导到恶意网站

![Screenshot_2024-07-02 17.02.36_ciMfuh](/Users/summer/Pictures/截屏/Screenshot_2024-07-02 17.02.36_ciMfuh.jpg)



### Query triggering

**How easy is it to spoof a DNS response?**

&rarr; Spoofed response needs to have correct 伪造DNS响应需要: Query ID(TXID, 16-bit) and Source Port(16-bit) 正确的查询ID和源端口

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-07-02 17.12.50_ZSHA4D.jpg" alt="Screenshot_2024-07-02 17.12.50_ZSHA4D" style="zoom:50%;" />

**In cache poisoning attacks, source port and TXID need to match the values in the query 在DNS缓存中毒攻击中，源端口和查询ID需要与查询中的值匹配**

![Screenshot_2024-07-02 17.46.21_pBDd9D](/Users/summer/Pictures/截屏/Screenshot_2024-07-02 17.46.21_pBDd9D.jpg)



### TXID and port randomization

![Screenshot_2024-07-02 17.48.17_pPCDld](/Users/summer/Pictures/截屏/Screenshot_2024-07-02 17.48.17_pPCDld.jpg)

&rarr; Randomize TXID，增加了攻击者成功猜测的难度，因为攻击者要在短时间内尝试2^32^个不同的TXID组合

Query ID(TXID): 16-bit + Source Port: 16-bit &rarr; overall 2^32^ bits

**Cache Poisoning via IP Fragmentation 通过IP碎片化进行缓存中毒——Use case: Certificates Issuance**

![Screenshot_2024-07-02 17.56.57_kLQveB](/Users/summer/Pictures/截屏/Screenshot_2024-07-02 17.56.57_kLQveB.jpg)

**How to trigger DNS requests? 如何触发DNS请求？**

+ With web object: Clients download and issue queries
+ With Email: Send an email to the MX in the domain to a non-existing email address
  + email server returns error message
  + to send error message, do DNS lookup to find the IP address of MX in the sending domain

**Network should block DNS request from Internet. 网络应该阻止来自Internet的DNS请求**



### DNSSEC



## ROV Measuring In The Wild

&rarr; To measure anything in the Internet, we have three options:

1. Observe the Controlplane of BGP 观察BGP的控制平面
   + That is the Routing table of a (or many) BGP server(s) 也就是一个或多个BGP服务器的路由表
   + Publicly available routing tables are exported by so called *Route Collectors* 公共可用的路由表由所谓的路由收集器导出
2. Try to send Data(Dataplane) from point A to point B 尝试从A点到B点发送数据
3. Use both 同时使用两种方式

### Control- vs. Dataplane

**Control Plane 控制平面**

+ Check if a BGP Announcement reached your Router 检查BGP公告是否到达你的路由器
+ if Announcement is RPKI invalid: 如果公告是RPKI无效的
  + All Routers along the Path are not ROV Enforcing 所有路径上的路由器都没有强制执行ROV
+ Problem:
  + Routecollectors have a limited view on the Internet 路由器收集器在互联网上的视野有限
  + A route that is dropped due to its RPKI invalidity (on a router before the collector router), does not reach the Collectors 因RPKI无效而被丢弃的路由（在收集器路由器之前的某个路由器上）不会到达收集器

**Data Plane 数据平面**

+ Send an IP-Packet towards an illegitimate prefix and see if its reachable 向非法前缀发送IP数据包并查看其是否可达
+ If reachable: 
  + All routers along the path to the prefix are not ROV Enforcing 所有路径上的路由器都没有强制执行ROV
+ Problem:
  + BGP can find a way (if there is one) to omit the ROV Enforcing routers. BGP可以找到一种方法（如果有的话）来绕过ROV强制执行路由器

Before we start to measure, there are two types of Approaches that have to be clarified before we even start:

1. Measuring random occurrences of RPKI invalid prefixes on the Internet
2. Actively generating RPKI invalid prefixes for measurement



### Passive/Active Overview

**Passive Measurements**

+ Find announced RPKI invalid prefixes in the wild 目标是找到实际网络中宣布的RPKI无效前缀

  &rarr; measure

+ How to find these?

  + RPKI
  + RouteCollectors

**Active Measurements**

+ Actively announce ROV invalid prefixes 目标是主动宣布ROV无效前缀

+ Create a ROA for a prefix with a owned ASN 为一个拥有的前缀创建一个ROA

+ Announce the sadi prefix with a different(but also owned) ASN 使用不同的（但也是拥有的）ASN（自治系统号）宣布该前缀

  &rarr; Measure 

+ Downsides 
  + High(er) financial costs
+ Upsides
  + Verifiability 



### Measurement Approaches

#### RouteCollector(Control Plane)

**Route collectors 路由收集器**

+ are BGP Servers that contribute to a publicly accessible database of all seen routes 是BGP服务器，它们贡献了所有一直路由的公开访问数据库
+ *routeviews.org* is a project with 45BGP routers of IXPs around the world
+ Newer RIB files(>2020) are roughly 100MB in size for 2 hourly observations 较新的RIB文件大约为100MB，每2小时观察一次

**How to measure ROV with this setup?**

+ Passive Measurement
  1. Download a RIB(RoutingInformationBase) file and find RPKI invalid prefixes by matching ROAs against the BGP announcements 下载一个RIB文件，并通过将ROA与BGP公告匹配来查找RPKI无效前缀
  2. If you found such a prefix you can inspect more RouteCollector RIB files and proceed to 如果找到这样的前缀，可以进一步检查更多的路由收集器RIB文件，并继续
+ Active Measurement
  1. Find your own prefix and proceed the same way as in passive measurement 找到自己的前缀，并以被动测量的方式进行测量
  2. Additionally, announce your prefix from multiple locations(BGP injection points) 此外，从多个位置宣布比的前缀（BGP注入点）



#### TCP Handshake Trigger

**TCP Handshake Trigger 握手触发器**

+ Concept: use a server, that sends a packet to an IP address we own 使用一个服务器发送数据包到我们拥有的IP地址

+ Only suitable for *Active Measurements* 仅适用于主动测量

+ Setup:

  + Sender: owned by us
  + Vantage Point(VP): any TCP speaking server in the Internet
  + Measurement Server: owned by us

+ Process:

  1. 发送TCP(SYN)包：
     + Send a TCP(SYN) packet** from sender with a forged IP origin(the address of the Measurement Server) 发送着从伪造的IP来源（测量服务器的地址）发送一个TCP（SYN）包
  2. 视点回复：
     + The VP answers with a TCP(SYN+ACK) packet the Measurement Server 视点服务器用TCP（SYN+ACK）包回复测量服务器
  3. 接收验证：
     + If the Measurement Server receives that TCP(SYN+ACK) packet, a route exists 如果测量服务器接收到TCP（SYN+ACK）包，说明存在一条路径
  4. 前缀失效处理：
     + Invalidate the prefix of the Measurement Server and wait till the ROA was found by the Relying Parties. Now repeat steps 1-3. 使测量服务器的前缀失效，并等待ROA被相关方发现。然后重复步骤1-3
     + If the Measurement Server has not received a TCP(SYN+ACK) packet from the VP, a ROV enforcing router were along the priginal path 如果测量服务器未收到来自视点的TCP（SYN+ACK）包，说明路径上存在ROV强制路由器

  &rarr; During invalidation, the BGP graph could have already changed: FalsePositives ahead! 在失效期间，BGP图可能已经改变，可能会导致误报



#### IP-ID Sidechannel

![Screenshot_2024-07-04 23.11.04_KLctM1](/Users/summer/Pictures/截屏/Screenshot_2024-07-04 23.11.04_KLctM1.jpg)

**Couting Methods for IP-ID 计数方法**

+ Constant: IP-ID保持不变，不随时间或数据包的变化而变化
+ Local: IP-ID在局部范围内递增，只在特定流量内保持递增
+ Global: IP-ID全局递增，对所有流量的IP-ID都在一个全局计数器下递增
+ Random: IP-ID随机生成，每个数据包的IP-ID都是随机数，没有特定的模式
+ Odd: IP-ID只生成奇数，跳跃递增，可能用于特定类型的流量标识
+ Counters are used to differentiate IP-fragments of multiple streams 使用计数器区分多个流的IP碎片
  + Those are the methods that occur throughout the internet

**IP-ID Side Channel**

![Screenshot_2024-07-04 23.16.53_dLnSid](/Users/summer/Pictures/截屏/Screenshot_2024-07-04 23.16.53_dLnSid.jpg)

Process:

1. 发送数据包

   + Send multiple TCP/IP-Packets from sender to VP without interruption 从发送者连续发送多个TCP/IP数据包到VP

2. 伪造数据包

   + Start sending spoofed TCP/IP-Packets towards the Measurement Server with the following content: 向测量服务器发送伪造的TCP/IP数据包
     + SrcIP = VP's IP
     + TCP Flags = SYN

3. 测量服务器响应

   + The Measurement Server will respond with a TCP SYN/ACK to the VP 测量服务器将回应TCP SYN/ACK 数据包到VP

4. VP响应

   + The VP never sent a TCP SYN to the Measurement Server and will therefore respond with a **TCP RST** Packet. Doing so increases the IP-ID counter of the VP. VP为向测量服务器发送TCP SYN数据包。将回应TCP RST数据包，增加VP的IP-ID计数器

5. 评估IP-ID字段

   + Evaluate the IP-ID Field from the VP Server throughout the measurement 在整个测量过程中评估VP服务器的IP-ID字段

6. 判断计数器增加

   + Did the counter rapidly increased right after sending the spoofed packets to the Measurement Server? 发送伪造数据包到测量服务器后，IP-ID计数器是否迅速增加？&rarr; if yes, VP reached the Measurement Server 如果是，表示VP到达测量服务器

   + 潜在问题（外部过滤）：

     + In case of outbound filtering of the VantagePoint, we can not be sure wether it was due to a Firewall, a ROV enforcing router or BGP rerouting with another ROV enforcing router

       &rarr; Huge Potential for False Positives 可能会导致大量误报

     + 解决方案：Use other VPs

       + Use other VPs in the same subnet or with small divergence in the path by using another subnet 在相同或路径有小偏差的情况下，使用其他VP



#### RIPE Atlas

&rarr; 是一个广泛部署的互联网测量平台，可以用于多种网络健康和连通行检查

+ Organiser: Réseaux IP Européens Network Coordination Centre (RIPE NCC)
+ Can be generally used for: 通用用途
  + overall Internet Health 互联网整体健康状况监测
+ Can be specifically used for: 具体用途
  + Accessibility Check 可访问性检查
  + Ping 
  + Trace route 路由追踪
+ False Postive sources: 潜在误报来源
  + Ping(ICMP) is partially filtered throughout the Internet 在整个互联网中部分被过滤
  + Geographical concentration around the European Union and the near East 地理集中度：主要集中在欧洲联盟和近东地区

#### Advertisement Networks(AdNet)

+ 广告代理机构：
  + Advertisement Agencies selling "Browserarea" to their customers 将“浏览区”出售给其客户
+ For each advertisement:
  + The advertiser pays a small amount of money to have the right to show some advertisement in the browser window of the client
  + The site owner gets payed and even smaller amount to allow the advertisement network sell its site space to the advertiser 

+ Implementation:
  + The AdNet injects a div at the proposed place in the HTML file of the site
  + The advertisers server is linked in that div
  + The Client is actively loading content from the referenced server
+ Downsides:
  + Costs money
  + NoScript / AdBlocker / uBlock / DNS Sinkhole (e.g. PiHole) filter our traffic before the measurement started
  + Requests are out of order
  + (Logical-)OR
  + Client interrupts transmission by “Closing the window”



## Web Security

### Recap

**Web Basics**

+ HTTP(S) is:
  + Simple and widely used
  + Stateless 
  + Unencrypted without S
  + Secured with S
+ HTTP Requests and Responses:
  + Requests are from client to server
  + Responses from server to client with requested content or error code
  + Stateless 
+ URL(Unified Resource Locator) 统一资源定位器
  + protocol://[user[:password]@]hostname[:port]/path/file?query
  + http://www.cased.de:81/topics/forschung.html?id=1

**Cookies**

+ What are Cookies?
  + Small text files (<4KB)
  + Created by server and stored on the client-side (in the browser)
  + Set in HTTP response header
  + Sent back to server by client on subsequent visits
  + Used to store state on client (HTTP is a stateless protocol)
+ Type fo Cookies
  + Validity 有效期: session 会话 vs. persistent 持久性
    + Session Cookie: 在会话结束后或浏览器关闭后删除
    + Persistent Cookie: 根据设置的过期日期存储
  + Origin: first-party 第一方vs. third-party 第三方
    + First-Party Cookie: 由您正在访问的网站设置
    + Third-Party Cookie: 由不同域名的网站设置
  + Other cookie attributes
    + HttpOnly: cannot be read by JavaScript 只能通过HTTP协议发送，JavaScript不能访问
    + Secure: only sent with HTTPS
    + SameSite: 
      + lax: only sent as first-party cookie 仅作为第一方Cookie发送
      + strict: only sent as first-party cookie if Referer is the same site 仅在Referer与当前站点相同时作为第一方Cookie发送
+ Scope of Setting Rules:
  + domain: any domain-suffix of URL-hostname, except TLD 任何URL主机名的域后缀，除了TLD(顶级域名)
  + path: can be set to anything (def. /) 可以设置为任何路径（默认是 ' / '）
    + if set, browser will send cookie only if domain and path fit 如果设置了路径，浏览器只有在域名和路径匹配时才会发送cookie
+ Client-Side Read/Write:
  + Setting a cookie in JavaScript:
    + document.cookie = "name=value; expires=…; "
  + Reading cookies:
    + alert(document.cookie);
  + Deleting a cookie:
    + document.cookie = "name=…; expires= Thu, 01-Jan-70"
    + 将过期时间设置为过去的时间，然后浏览器就会把这个cookie删除
+ HttpOnly Property of Cookies
  + Address bar of browers: 浏览器地址栏的脚本
    + 使用“ javascript: alert(document.cookie)” 命令，可以显示所有非HttpOnly的Cookies
    + Cookie is set to HttpOnly &rarr; invisible to JavaScript
  + Cookie sent over HTTP/S, but not accessible to scripts 通过HTTP/S发送但脚本无法访问的cookie
    + cannot be read via document.cookie 不能通过“document.cookie”来读取
    + also blocks access from XMLHttpRequest headers 也阻止了通过XMLHttpRequest头部访问这些cookies
  + Helps prevent cookie theft via XSS(Cross Site Scripting) 帮助防止通过跨站脚本攻击盗取cookie
    + but does not stop most other risks of XSS bugs
+ SameSite Property of Cookies
  + Cookie should only be sent with requests initiated from the **same registrable domain** 只有在同一个注册域名发起的请求中cookie才会被发送
    + 这意味着，当用户在不同网站之间进行导航或从不同网站发起请求时，带有SameSite属性的cookie不会被发送
  + 作用：Mitigates the risk of CSRF and infrmation leakage attacks 减轻跨站请求伪造攻击的风险
+ Cookie Protocol Problems:
  + Server is blind:
    + does not see cookie attributes
    + does not see which domain set the cookie
    + server processes cookies sent to it
  + Server only sees:
    + Cookie: NAME=VALUE
    + Cookie Parameters remain in the browser
    + Plausibility checks are difficult 合理性检查很困难
  + No encryption or integrity checks are included
    + must be implemented on web application or client side

### Web Security

**Typical Web Application**

+ Written in a mixture of PHP, Java, JavaScript, Python, C, ...
+ Runs on a Web server or Application Server 在Web服务器或应用服务器上运行
+ Interacts with back-end databases and third parties 与后端数据库和第三方交互
+ Prepares and outputs results for users 为用户转北和输出结果
+ Dynamically generated HTML pages 动态生成HTML页面

**Architecture of Web Deployment**

![Screenshot_2024-07-05 15.07.15_UxuNl3](/Users/summer/Pictures/截屏/Screenshot_2024-07-05 15.07.15_UxuNl3.jpg)

**OWASP TOP 10**

&rarr; The Open Web Application Security Project (OWASP) 开放Web应用程序安全项目, released a list of the Top 10 vulnerabilities

Last update was 2021, updated every 4 years



### CSRF

**CSRF - Cross-Site Request Forgery 跨站请求伪造**

&rarr; 是一种网络攻击，攻击者诱导用户的浏览器在用户不知情的情况下发起恶意请求。

+ Also known as: one-click attack / session riding 一次点击攻击 / 会话劫持
+ Simple attack and a lot of vulnerable websites 攻击简单，大量网站易受攻击
+ Forces user's browser to send an unauthorized request to a website that the user is currently authenticated to 强制用户浏览器发送未经授权的请求
+ Security problem is due to the **statelessness of HTTP** 安全问题的根源是：HTTP的无状态性

**How it works**

+ Since request are performed by the user's browser, all cookies will be submitted to the website 请求由用户的浏览器执行：所有的cookie和认证令牌都会提交到目标网站

+ Session identifiers and all authentication tokens will be also submitted 会话标识符和所有认证令牌也会被提交

+ What happens?

  1. Victim opens www.bank.com 受害者打开www.bank.com
     + 用户点击或访问了一个链接或页面，可能是恶意网站上的连接
  2. Browser sends all knwon cookies to *bank.com* 浏览器发送所有已知的cookie到bank.com
     + 包括会话cookie和认证令牌
  3. User is identified and logged in 用户被识别并登录
     + 用户在目标网站（银行网站）上已经有有效的登录会话
  4. Bank performs transfer of 1000 USD to account 1234 银行执行转账操作，将1000美元转账到账号1234
     + 因为请求带有合法的会话和认证信息，银行认为这是合法的请求

  + Fortunately, most banks are using more advanced security methods to control transactions like PIN/TAN, smsTAN, and so on... 大多数银行使用更先进的安全方法来控制交易

**Countermeasures**

+ Additional PIN/TAN input 额外的PIN/TAN输入
+ Random(one-time) tokens associated with the user's current session 随机（一次性）令牌，为每个用户会话生成并关联一个随机的一次性令牌，并在表单中包含该令牌
+ Double Submit Cookies 双提交Cookie
  + store cryptographically strong random value in a cookie
  + site matching a token sent a form value and compare with the token in cookie
  + due to the Same Origin Policy, attacker cannot read/modify the cookie value

+ Enter additional secure password (over HTTPS)

**Mitigation 缓解措施**

+ Session time out after a period of inactivity 在一段时间的非活动后，会话会自动超时
+ Confirmation of actions 在执行重要操作前，要求用户确认
+ Client/User Side:
  + Logoff after using a web service 使用后登出
  + Do not save username/passwords in the browser 不保存用户名/密码
  + Use different browsers to access sensitive applications 使用不同的浏览器
  + Use Add-Ons like no-script to prevent POST based CSRF vulnerabilities to exploit 使用No-Script等插件



### SQL Injection

&rarr; Injections(or code injections) happen when some applications or servers interpret user supplied input. 注入攻击（或代码注入）发生在某些应用程序或服务器解释用户提供的输入时。

**Type of Injections**

+ SQL Injection (the most injections) 
+ JavaScript Code Injection(XSS)
+ XPath Injection
+ LDAP Injection

**What is SQL?**

+ SQL(Structured Query Language 结构化查询语言) is the standard language for requests in relational database management systems(RDBMS 关系数据库管理系统) 结构化查询语言是用于关系数据库管理系统中请求数据的标准语言
+ Used to: SELECT 选择, INSERT 插入, UPDATE 更新and DELETE 删除 data as well as define schema of DB

&rarr; Example: SELECT * FROM members WHERE id="1";

**What is SQL Injection?**

+ SQL Injection:
  + Consists of insertion or "injection" of a SQL query via the input data from the client to the application 是一种通过客户端输入的数据插入或“注入”SQL查询的方法
  + Mainly in the form of POST or GET method in the website 主要以网站中的POST或GET方法的形式存在
  + Exploits poorly filtered or not correctly escaped SQL queries to run malicious code(the "buffer overflow" of RDBMS)  利用过滤不严或未正确转义的SQL查询来运行恶意代码（关系数据库管理系统的“缓冲区溢出”）
+ What happens if somebody can change those values?
  + unexpected behavior of application/database 应用程序/数据库会发生意外行为

**SQL Injection Objectives 目标**

+ SQL injection errors occur when: 注入错误发生在
  + Data enters a program from an untrusted source 数据来自不可信来源时进入程序
  + The data is used to dynamically construct a SQL query 这些数据用于动态构造SQL查询
+ A successful SQL injection exploit can:
  + read sensitive data from the database (confidentiality) 从数据库中读取敏感数据
  + modify databse data(insert/update/delete) (integrity) 修改数据库数据
  + execute administration operations on the database(such as shutdown the DBMS) (availability) 执行数据库上的管理操作
  + and in some cases issue commands to the operating system 在某些情况下向操作系统发出命令
+ SQL and any platform that requires an interaction with a SQL databse may be affected. SQL注入会影响任何需要与SQL数据库交互的平台

**Blind SQL Injection**

&rarr; Blind SQL Injection can be injected without seeing the output. 盲目SQL注入是一种SQL注入攻击，攻击者无法直接看到查询的输出结果

+ Error-based blind SQL Injection: 错误信息型盲目SQL注入
  + abuse error messages to exfiltrate data 利用数据库返回的错误信息来提取数据
+ Time-based blind SQL Injection: 基于时间的盲目SQL注入
  + abuse injected delays to exfiltrate data 通过引入延迟来提取数据，观察查询的执行时间来推断结果
  + e.g., construct query that wait 1 second if a table starts with 'A'

**SQL Injection Countermeasures**

&rarr; Parameterized queries 参数化查询

+ Parameterized queries using bound, typed parameters 参数化查询是一种防范SQL注入的有效方法，通过绑定和使用类型化参数，可以确保输入数据被正确处理
+ Easy to adopt and work in fairly similar ways among most web technologies：在大多数Web技术中都能很容易采用，并且以类似方法工作
  + e.g., Java, .NET, PHP, Perl, Python



### XSS

**Cross-Site Scripting (XSS) 跨站脚本攻击**

&rarr; XSS occurs when a web application interprets(malicious) data from a user. 跨站脚本攻击发生在Web应用程序解释用户提供的（恶意）数据时

Not exclusive JavaScript Problem - but often used, e.g.: VBScript, ActiveX, TypeScript, ... 这种攻击并不仅限于JavaScript，还可以利用其他脚本语言

+ Threats:

  + account hijacking 账户劫持
  + changing of user settings 修改用户设置
  + cookie theft/poisoning 窃取或污染Cookie
  + redirecting 重定向用户到恶意网站

+ Main objective: Modify behavior of original site 主要目标是修改原始网站的行为

  + <SCRIPT> Different languages (e.g. JavaScript) 
    <OBJECT> Applet, Media, ActiveX
    <APPLET> Applet, deprecated
    <EMBED> Embedding Media
    <FORM> Forms

+ XSS:

  &rarr; Attacker injects malicious JavaScript code into a HTML-Page 攻击之将恶意的JavaScript代码注入到HTML页面中

  + XSS攻击分为两种类型：
    + Persistent XSS 持久性: save the malicious JavaScript 恶意JavaScript代码被永久存储在服务器上
    + Non-Persistent XSS 非持久性: executed once by the victim 恶意JavaScript代码不会被存储在服务器上，而是通过特定的触发条件，被一次性执行

+ XSS Countermeasures

  + Blocking "<"and">" is not enough
  + Event handlers(e.g. onMouseover), stylesheets(CSS), encoded inputs(%3C), etc.
  + Any user input must be preprocessed before it is used inside HTML
  + In Python, cgi.escape(string, quot) will replace all special characters with their HTML codes

**JavaScript Introduction**

&rarr; JavaScript是一种在客户端浏览器中执行的编程语言。它被广泛嵌入在网页中，主要用于增强用户与网页的交互体验。

+ Language executed by client browser  客户端浏览器执行的语言
  + Scripts are embedded in Web pages 脚本嵌入在网页中
  + Can run before HTML is loaded, before page is viewed, while it is being viewed or when leaving the page 可以在HTML加载之前、页面被查看之前、页面被查看时或离开页面时运行
+ Attacker gets to execute code on user's machine 攻击者可以利用JavaScript在用户机器上执行代码
  + Often used to exploit other vulnerabilites 通常被用来利用其他漏洞
+ Common usage of JavaScript:
  + Form validation 表单验证
  + Page visualizations and specail effects 页面可视化和特效
  + Navigation systems 导航系统
  + Basic math calculations 基本数学计算
  + Dynamic content manipulation 动态内容操作

**JavaScript Security Model**

+ Script runs in a "sandbox"

  + no direct file access
  + restricted network access

+ Same-Origin Policy (SOP) 同源策略

  &rarr; SOP是一种安全机制，限制了不同来源的脚本之间的交互

  + Can only read properties of documents and windows from the same server, protocol, and port 只有当文档来自相同的服务器、使用相同的协议和端口时，JavaScript才能访问其属性
  + If the same server hosts unrelated sites, scripts from one site can access document properties on the other 如果同一服务器托管多个无关的站点，来自一个站点的脚本不能访问另一个站点的文档属性
  + SOP does not apply to script tags inserted into the site 同源策略不适用于插入到站点中的“<script>”标签
    + this script runs as if it was loaded from the site that provided the page 这种情况下，脚本会以提供该页面的站点的身份运行，可能带来安全隐患



### Magecart & The JavaScript Supply Chain



## PKI & TLS

### Domain Validation

+ How to get a certificate?

  &rarr; DV (Domain Validation 域名验证)

+ How to get a certificate as attacker? 

  &rarr; Intercept DV 

  + Attacker could intercept DNS and point CA to different server 攻击者可以拦截DNS并将CA指向不同的服务器
  + or manipulate HTTP response 操纵HTTP响应

+ Multi-Perspective Validation 多角度验证

  &rarr; Attacker typically topologically constrained, cannot intercept all paths 攻击者通常收到拓扑约束，无法拦截所有路径

+ How to police fraudulent certs? 如何监控欺诈性证书

  &rarr; CT (Certificate Transparency 证书透明性)

  + All CAs must publicly log all created certificates, so misbehaving CAs are found faster 所有证书颁发机构必须公开记录所有创建的证书，这样可以更快地发现行为不当的CA

+ What if **fraudulent certificate** is found? 如果发现欺诈性证书了怎么办

  + Contact CA, revoke certificate 联系CA，请求吊销证书
  + Also used when e.g. cert private key is leaked 证书私钥泄露时也需要吊销证书

+ How does a web client know a certificate was revoked?

  + CRL (Certificate Revocation List) 证书吊销刘表
    + list of revoked certs, signed by CA, link contained in cert
    + Problem: gets larger, in-line download incurs high latency
  + OCSP (Online Certificate Status Protocol) 在线证书状态协议
    + protocol to ask CA whether a given certi is revoked
    + Problem: leaks domain name to CA

+ Fundamental Dilemma: What if OCSP/CRL is unavailable?

  + Hardfail 硬失败
    + Certificate considered invalid 证书被视为无效
    + Pro: more secure
    + Con: vulnerable to DoS, if attacker can block OCSP/CRLs
  + Softfail 软失败
    + Certificate is considered valid 证书被视为有效（目前所有浏览器的默认设置）
    + Pro: no DoS
    + Con: insecure, if attacker can blokc OCSP/CRLs



### Transport Layer Security

&rarr; TLS (Transport Layer Security) provides authentication, confidentiality, reliability with efficient reusability 传输层安全协议，提供了一系列服务，确保数据在网络传输中的安全性和完整性

+ Services provided by TLS
  + Server authentication (mandatory 强制性) 服务器认证
  + Client authentication (optional – if required by the server) 客户端认证
  + Secure connection 安全连接
    + Authentication and integrity of messages 
    + Confidentiality of messages
    + Reliability of messages (prevents message re-ordering, truncating, etc.)
  + Efficiency 效率
    + Allows resuming old TLS sessions in new connections 会话恢复

Websites and apps require：authentication, integrity, confidentiality and availability

+ Example Applications
  + Online banking
  + Online purchases, auctions, payments
  + Restricted website access
  + Software download
  + Web-based email

TLS can be used used to secure applications and websites

+ Pro:
  + Easy to implement and use
  + Deployed in most browsers & servers
+ Con:
  + Protects only if used by the application
  + More vulnerable to Denial-ofService attacks (malicious packets cannot be removed at the IP level) 
  + Can only be used in End-to-End mode



### TLS Authentication via Certificates

&rarr; Connecting to a secure website requires confirming the authenticity of the server 连接到安全网站需要确认服务器的真实性

TLS authentication uses certificates, which bind a public key to a distinguished name. TLS认证使用证书，将公钥绑定到特定名称

+ Certificate Generation:
  1. Bob generates a key pair (private/public). Bob生成密钥对
  2. Bob generates a CertificationRequestInfo containing: 
     + His name
     + His public key
     + Optional Attributes
  3. Bob signs the *CertificateRequestInfo* with his private key. Bob用自己的私钥签名证书请求信息
  4. Bob sends the CertificationRequestInfo and his signature as *Certificate Signing Request (CSR 证书签名请求)* to a *Certification Authority (CA)*. Bob将证书请求信息及其签名作为证书签名请求发送给证书颁发机构
  5. The CA generates an X.509 certificate containing Bob’s name, public key and optional attributes and signs it with its own private key. CA生成X.509证书

Upon receipt of a certificate, the recipient can validate it by verifying CA’s signature 当收到证书时，接收者可以通过验证CA的签名来验证其真实性。

+ Certificate Validation:
  1. Alice obtains Bob's certificate 
  2. Alice checks if CA's signature is valid 检查CA的签名是否有效

For TLS the distinguished name in the certificate is a domain name, not a person 对于TLS，证书中的可分辨名称是域名，而不是个人



### TLS Architecture

The handshake sets all security parameters for the TLS session 握手阶段会设定所有用于TLS会话的安全参数

+ Security Parameters for a TLS session:
  + Connection end 连接端点(Who is server? Who is the client?)
  + Pseudo random function (PRF) algorithm 伪随机函数算法
  + Bulk encryption algorithm (symmetric cipher) 批量加密算法
  + MAC algorithm 消息认证码
  + Compression algorithm 压缩算法 (should not be used, see CRIME)
  + Master secret and other cryptographic keys 主密钥和其他加密密钥
  + Key exchange 密钥交换 (+ signature algorithm)

Data transfer uses the record layer after a successfully completed handshake 在TLS握手成功完成后，数据传输使用记录层进行加密和验证

+ TLS Record Protocol Functions
  + Provides end-to-end encryption using the selected (symmetric) bulk encryption algorithm 提供端到端加密
  + Ensures message authentication and integrity using selected MAC algorithm 确保消息认证和完整性

![Screenshot_2024-07-10 00.09.06_QHbOcY](/Users/summer/Pictures/截屏/Screenshot_2024-07-10 00.09.06_QHbOcY.jpg)



### TLS Handshake

Main purpose of handshake is —— to agree on parameters and authenticate the parties 商定安全参数并对通信双方进行认证

**TLS Handshake Steps:**

+ Agree on cipher suite: 商定密码套件
  + encryption algorithm
  + key exchange algorithm
  + message authentication code (MAC)
+ Exchange random values to generate shared keys 交换随机值以生成共享密钥

**A full handshake involves several messages between client and server**

![Screenshot_2024-07-10 14.09.15_8x7inH](/Users/summer/Pictures/截屏/Screenshot_2024-07-10 14.09.15_8x7inH.jpg)

+ In the **ClientHello** message the client suggests parameters for the TLS session 在ClientHello消息中，客户端建议TLS会话的参数
+ and the Server responds in the **ServerHello** message with its choices 在ServerHello消息中响应其选择
+ In the **ChangeCipherSpec** message the parties switch to encrypted communication 在ChangeCipherSoec消息中，双方切换到加密通信 &rarr; The ChangeCipherSpec Protocol
  + a protocol of its own 独立的协议，用于指示切换加密算法
  + not explicitly needed in TLS 1.3, but sent to prevent middleboxes from trying to parse the following encrypted data 在TLS 1.3中并非强制需要的，但发送此消息可以防止中间设备尝试解析随后的加密数据
  + Consists only of ChangeCipherSpec message (which itself consists of a single byte with value 1) 仅包含一个字节，值=1
  + From here on, everything is encrypted, but not authenticated yet! 从这里开始，所有通信加密，但通信尚未认证
+ Server Authentication via Certificate Chain, This certificate exchange is **mandatory** for the server 通过证书链进行服务器身份验证，此证书交换对于服务器来说是强制的
  + Message **Certificate *** follows immediately after ServerHello 在 ServerHello 消息之后立即发送Certificate 消息
    + First certificate must be servers’s certificate 证书链中的第一个证书必须是服务器的证书
    + Each following certificate must certify the preceding one 每个后续证书必须认证前一个证书
    + Root certificate authority may be omitted 根证书认证机构（CA）可以省略
    + Certificate’s public key must be compatible with a signature algorithm understood by the client 证书的公钥必须与客户端理解的签名算法兼容
  + Server then proves that he is the certificate’s owner using **CertificateVerify *** message 服务器使用 CertificateVerify 消息证明其身份
    + Server signs hash(ClientHello | ServerHello | Certificate) with the private key associated with the certificate
+ After optional ClientCertificate request, the server indicates **end of ServerHello** 在可选的 ClientCertificate 请求之后，
  服务器指示 ServerHello 结束
  + Server may require client to authenticate by sending **CertificateRequest** 服务器可能要求客户端通过发送CertificateRequest消息进行身份验证
  + Server sends **Finished** to both, indicate end and to protect the integrity of previously sent messages 服务器向双方发送 Finished消息，标志 ServerHello 结束，还用于验证先前发送消息的完整性
+ If the server requested authentication, the client’s first answer is a list of **certificates** 如果服务器请求身份验证，客户端的第一个答案是证书列表
  + Similar **certificate *** chain as for server authentication
  + If certificate_authorities in certificate request was nonempty, one of the certificates in the certificate chain should be issued by one of the listed CAs
  + Like the server, the client then proves his authenticity by signing the previous messages and sending a **CertificateVerify *** message
+ And then, the handshake is finished by sending a **Finished** message
  + Contains a hash of all previously sent messages 包含所有先前发送消息的哈希值
  + Integrity-protected by symmetric handshake key material 通过对称握手密钥材料保护器完整性
  + Recipient of the message must verify that contents are correct 消息接收方必须验证内容是否正确
  + Once a side has sent his Finished message and received and validated it’s peers Finished message, it may begin to send and receive application data 一方发送完成消息并接收、验证对方的完成消息后，可以开始发送和接收应用数据
  + This handshake design commonly save 1 round-trip for session creation (for protocols where the clients sends the first data) 这种握手设计通常可以节省一次往返时间以创建会话

**TLS 1.3 zero-RTT handshake (only resumption 仅限会话恢复)**

![Screenshot_2024-07-10 14.40.39_jXAAGm](/Users/summer/Pictures/截屏/Screenshot_2024-07-10 14.40.39_jXAAGm.jpg)

+ Provides even more speed than 1-RTT handshake, no RTT overhead 提供比1-RTT握手更快的速度，没有RTT开销
+ Early data is protected by pre-shared-secret from previous session, server state is stored in session cookie 早期数据由前一个会话的预共享密钥保护，服务器状态存储在会话Cookie中
+ Problem: weaker security guarantees 安全保证较弱
  + Not (less) forward secure 不具备（较少具备）前向安全性
  + No replay protection for early application data, must only be used where message replay is not an issue 早期应用数据没有重放保护
  + Theoretically this should be the case for HTTP GET, practically it’s not 仅在消息重放不是问题的情况下使用



### TLS Cipher Suites and Key Computations

A cipher suite consists of cryptographic algorithms used for various purposes 密码套件由用于各种目的的加密算法组成

**Ingredients of a Cipher Suite:**

+ Key Exchange Algorithm 密钥交换算法
  + 用于协商会话密钥，确保只有通信双方知道这些密钥
  + Example: Ephemeral Diffie-Hellman (DHE) with RSA signed DH Parameters
+ Data Encryption Algorithm数据加密算法
  + 用于对传输的数据进行加密
  + Example: AES with 128-bit key in Galois/Counter Mode (GCM)
+ Hash Function for HMACs 用于HMAC的哈希函数
  + 用于消息认证码（HMAC），确保数据的完整性和真实性
  + Example: SHA256



### Some Security Recommendations for TLS

**Strong Cipher Suites - General Advice on Cipher Suites:**

+ must not negotiate NULL encryption 禁止协商NULL加密
+ must not use RC4 cipher suites 禁止使用RC4密码套件
+ should not use static RSA key transport 不应该使用静态RSA密钥传输
+ must support and prefer cipher suites with perfect forward secrecy 必须支持并优选选择具有完美前向保密性的密码套件
  + Example：Ephemeral Diffie-Hellman and Elliptic Curve Ephemeral Diffie-Hellman

**Perfect Forward Secrecy**

&rarr; can help if long term secret key is compromised

+ Perfect forward secrecy (PFS) or forward secrecy: use fresh session keys for every new session
+ This preserves confidentiality even if long term secret (private) key is compromized
+ In TLS this is the case with Ephemeral Diffie-Hellman (DHE) or Ephemeral Elliptic Curve Diffie-Hellman (ECDHE)
+ Attention: PFS cannot protect against cryptanalysis of the used key excange or the block cipher itself (i.e. if you can break DH)
+ Logjam shows that DH can already be broken if used incorrectly (!)

**Only four of the cipher suites in TLS 1.2 provide PFS **

1. TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
2. TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
3. TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
4. TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 



## Introduction to Binary Security



