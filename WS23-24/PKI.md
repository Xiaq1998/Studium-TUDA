# Public Key Infrastrukturen

## 1. Security Goals

**Confidentiality (Vertraulichkeit) 保密性**

​    The practice of keeping secrets, maintaining privacy, or concealing valuables.

**Integrity (Integrität) 完整性**

​    The integrity of the data is the fact that the data has not been modified.

**Availability (Verfügbarkeit) 可用性**

​    The property that legitimate principlas are able to access a service within a timely manner whenever they may need to do so.

**Authentication (Authentifizierung) 验证性**

​    The process by which one entity*(verifier)* is assured of the identity of a second entity*(the claimant)* that is participating in a protocol.

**Data authenticity (Datenauthentizität) 数据真实性**

​    The ability to determine the origin of the data, includes integrity.

**Non-repudiation (Verbindlichkeit) 不可否认性**

​    Reduce the ability of a party to repudiate an electronic transaction.

**Anonymity (Anonymität) 匿名性**

​    Anonymity is the concept of being indistinguishable from others who perform the same or similar actions as oneself.



## 2. Cryptography

### Two Types of Cryptography

#### Symmetric encryption 对称加密

Symmetric encryption use the same key for encryption and decryption, or two keys that can be easily deduced from each other.

**Cryptographic Hash Functions**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-15 16.36.23_ohw9l8.jpg" alt="Screenshot_2024-01-15 16.36.23_ohw9l8" style="zoom:50%;" />

* Different ways of building hash functions: Merkle-Damgard construction, sponge constructions.

​       *Examples:* MD~5~, SHA~2~, SHA~3~

* Properties of Cryptographic Hash Functions: One way / Collision resistant

**Key exchange problem**

​                ==n(n-1)/2 = O(n^2^)==

**Symmetric crypto problems**

​    Key agreement / Key management / Key attribution

The key server knows all secret keys.

####Asymmetric encryption 非对称加密

Public key is used for encryption *(PKE, Public Key Encryption)*, the secret key is used for decryption.

The server does not know any secret information.

**Asymmetric crypto problems**

* Performance
* Public key availability
* Public key ownership
* Public key validity

#### Hybrid encryption 混合加密

**Hybrid encryption problems**

* Public key availability
* Public key ownership
* Public key validity

**Authenticated Key Exchange 认证密钥交换**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-15 16.59.09_HwLYWR.jpg" alt="Screenshot_2024-01-15 16.59.09_HwLYWR" style="zoom:50%;" />



### Security in cryptography

**Two approaches**

* Game-based: Security defined as a game between an adversary and a challenger.
* Simulation-based / Universal Composability(UC): Security defined as the indistinguishability between ideal and real world.

**Signature Scheme - Security: EUF-CMA 存在不可伪造性**



## 3. PKI Challenges

####PKI Key Infrastructures

​    a Public Key Infrastructure (PKI) is designed to facilitate the use of public key cryptography.

* Consists of hardware, software, people, policies, and procedures
* Deals with the management of digital certificates in distributed environment (creation, distribution, usage, storage, and revocation)

#### Why PKI?

**Assure that the public key is available (Availability)**

* Directories: (L)DAP, Active Directory
* Web PAges: HTTP(s)
* File transfer: (s)FTP
* Services: OCSP, SCVP

**Assure that the public key is authentic (Authenticate  真实性)**

* Bind publick key uniquely to electronic identity
* Seal the binding
* Answer for the binding

**Assure that the public key is valid (Validity 有效性)**

* Monitor binding public key &harr; electronic identity &harr; key owner
* Establish time constraints 设定时间限制
* Provide means to revoke binding 提供撤销绑定的方法

*Example: Certificate revocation list (CRL)*

**PKI support security (Security of key pairs)**

* Select suitable algorithms and key sizes
* Monitor possible security threats and react adequately
* Provide suitable
  * means to generate key pairs
  * formats and media to store private keys
  * means of delivering private keys

*Example: PSE (Smart card)*

**PKI support interoperability 互操作性**

​    Comply to accepted (international) standards. 遵守公认的（国际）标准

​    **Enforce policies 执行政策**  

* Certificate policy (CP) 证书政策: States what to comply to
* Certificate practice statement (CPS) 证书实践证明: States how to comply



## 4. Certificates

### Pbulic key certificates

**Definition**

​    Public key certificates: data structures that bind publick key vaules to subjects.

*Example: Secure browsing, Click on icon*

**Publick Key Certificate (PKC)**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-17 11.10.54_BvKcGU.jpg" alt="Screenshot_2024-01-17 11.10.54_BvKcGU" style="zoom:50%;" />

**Certificate properties**

* Protected binding of a key to the key holder
* Its authenticity is independent of the means of transportation
* It can be used online and offline
* It is a proof of the binding
* It can be used for key servers

**Certificate standards**

* X.509
* Pretty Good Privacy (PGP)
* WAP certificates
* Card Verifiable Certificates (CVC)
* Simple PKI / Simple Distributed Security Infrastructure



### X.509 certificates

**Relevant standards**

* X.509 (ITU-T)
* PKIX (RFC 5280)

**Encoding**

* Abstract Syntax Notation Nr. 1: ASN.1  X.509证书通过ASN.1来描述
* Distinguished Encoding Rules: DER  X.509证书通过DER编码来生成二进制

#### Contents

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-17 11.22.34_afvGiv.jpg" alt="Screenshot_2024-01-17 11.22.34_afvGiv" style="zoom:50%;" />

**Certificate (ASN.1)**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-17 11.26.05_UDNIqF.jpg" style="zoom:50%;" />

* 
