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

* To Be Signed (TBS) Certificate: This part holds all information; this will be signed
* Alglrithm: The algorithm that is used for signing the TBS part
* Signature Vaule: The calculated signature

**TBSCertificate (ASN.1)**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-17 11.34.46_fwI5zn.jpg" alt="Screenshot_2024-01-17 11.34.46_fwI5zn" style="zoom:50%;" />

* Version
  * The X.509 version of the certificate
  * Integer value {v1=0, v2=1, v3=2}
* Serial Nummer
  * The serial number of the certificate
  * Positive integer
  * Must be unique for the same issuer

* Signature
  + The algorithm OID (and needed parameters) used to sign the certificate, e.g., SHA256withRSA
  + Must be the same as the signautre Algorithm

* issuer
  + Name of the certificate issuer (CA) in form of an X.500 DN (distinguished name 专有名称)
  + E.g.: CN = RBG CA, OU = FB Informatik

* validity
  + The period of time that a certificate can be used
  + Given by start and end date: Not before and not after
* subject
  + Name (X.500 DN) of the certificate holder
  + Associated to the public key contained in the certificate
  + The same DN is not allowed to be given to two different entities
* subjectPublicKeyInfo
  + The algorithm OID of the public key and its parameters
  + The public key of the certificate holder

* issuerUniqueID / subjectUniqueID
  + Version 2 and 3 only
  + Bit strings, world wide unique
  + Identifiers an issuer or subject, in case a DN is reused

* Extensions
  + Details see next 

#### X.509 extensions

**(non-) critical extensions**

* Extensions are either marked critical or non-critical
* Criticality affects evaluation by the client

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-17 11.59.38_svnXgL.jpg" alt="Screenshot_2024-01-17 11.59.38_svnXgL" style="zoom:50%;" />

**Subject Key Identifier (SKI) 主体密钥标识符**

* Identifies certificates that contain a particular public key
* Must be included in all CA certificates (non-critical)
* Given as ASN.1 keyIdentifier

**Authority Key Identifier (AKI) 授权密钥标识符**

* Identifies the public key that corresponds to the private key that has signed the certificate  标识与已签署证书的私钥对应的公钥
* Must be included in all certificates (non-critical)
* Facilitates certification path construction
* Consists of the following (optional) fields:
  + keyIdentifier
  + authorityCertIssuer
  + authorityCertSerialNumber

**Key Usage 密钥用法**

* Defines the purpose of the key contained in the certificate
* CAs conforming to RFC5280 must include this extension
* Given as a bit string of length 9

**Subject Alternative Name 主题别名**

* Allows additional identites to be bound to the subject of the certificate

  *Example: DNS name, IP address, Internet electronic mail address*

* Before included, this information must be verified since it is bound to a public key

**Issuer Alternative Name 发行人替代名称**

* Associates Internet style identities with the certificate issuer
* Should not be marked critical
* Same format as Subject Alternative Name extension

**Subject Directory Attributes 主题目录属性**

* Used to convey identification attributes (e.g. nationality) of the subject
* Sequence of one or more attributes
* Must be non-critical

**Extended Key Usage**

​    Indicates one or more purposes for which the certified publick key may be used, in addition to or in place of the basic puroises indicated in the key usage extension.

*Example: Code signing, OCSP signing, Timestamping*

* If present, both key usage and extended key usage extensions must be processed independently
* The certificate must only be used for a purpose consistent with both extensions

**List of other extensions**

* Certificate Policies
* Policy Mappings
* Policy Constraints
* Basic Constraints
* Name Constraints
* CRLDistributionPoints
* Inhibit Any-Policy
* Freshest CRL
* Autohority Information Access
* Subject Information Access

