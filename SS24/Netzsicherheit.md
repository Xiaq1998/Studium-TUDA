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

SSH(Secure Shell) 最初设计用于提供一个安全（但轻量级）的替代方案，以取代Unix的r工具（如login、rsh、rcp和rdist），因此SSH代表了一个应用层或会话层协议

+ SSH Architecture:
  + SSH follows a **client-server** approach
  + Every SSH server has at least one **host key 主机密钥**
  + SSH version 2 offers two different trust models:
    + （本地数据库信任模型）Every client has a loacl database that associates each host name with the corresponding public host key
    + （CA认证信任模型）The hostname to public key association is certified by a CA and every client knows the public key of the CA

**SSH Protocol Stack**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-06-26 00.59.27_VV1pnL.jpg" alt="Screenshot_2024-06-26 00.59.27_VV1pnL" style="zoom:50%;" />

**SSH Transport Layer Protocol**

+ （服务器认证）server authentication 

  + occurs at transport layer, based on server/host key pair(s) 服务器身份验证发生在传输层，基于服务器/主机密钥对

  + server authentication requires clients to know host keys in advance 服务器身份验证要求客户端提前知道主机密钥

+ （数据包交换）packet exchange

  + establish TCP connection
  + can then exchange data
    + identification string exchange, algorithm negotiation, key exchange, end of key exchange, service request
  + using specified packet format

