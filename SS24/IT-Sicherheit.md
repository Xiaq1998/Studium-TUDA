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

### 2. BGP prefix hijack attacks

### 3. BGP security with RPKI

### 4. RPKI: misconfigurations and attacks

