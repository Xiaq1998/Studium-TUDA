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

**Assure that the public key is available 可用的**

* Directories: (L)DAP, Active Directory
* Web PAges: HTTP(s)
* File transfer: (s)FTP
* Services: OCSP, SCVP

**Assure that the public key is authentic 真实的**

* Bind publick key uniquely to electronic identity
* Seal the binding
* Answer for the binding

**Assure that the public key is valid 有效的**

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

**Enforce policies 执行政策**  

* Certificate policy (CP) 证书政策: States what to comply to
* Certificate practice statement (CPS) 证书实践证明: States how to comply



## 4. Certificates

### Pbulic key certificates

**Definition**

​    Public key certificates: data structures that bind public key vaules to subjects.

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

**Distinguished Names**

* CN        Common Name 通用名
* L            Locality 地点
* ST          State or Province 州或省
* O           Organization 组织
* OU        Organization Unit 组织单位 
* C            Country 国家
* Street    Street Address  街道地址
* DC         Domain Component 域组件
* UID       User Id 用户ID

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
  + keyIdentifier (as in SKIE, but identifies public key of issuer)
  + authorityCertIssuer (name of the issuer of the issuer's certificate)
  + authorityCertSerialNumber (serial number of the issuer's certificate)

**Correlation 相关性 of SKIE - AKIE**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-19 15.07.54_LICLre.jpg" alt="Screenshot_2024-01-19 15.07.54_LICLre" style="zoom:50%;" />

**Key Usage 密钥用法**

* Defines the purpose of the key contained in the certificate
* CAs conforming to RFC5280 must include this extension
* Given as a bit string of length 9：
  + digital Signature (0)
  + non Repudiation (1)
  + key Encipherment (2) 密钥加密
  + data Encipherment (3) 数据加密
  + key Agreement (4)
  + key Cert Sign (5)
  + CRL Sign (6)
  + encipher Only (7) 仅加密
  + decipher Only (8) 仅解密

**Subject Alternative Name 主体别名**

* Allows additional identites to be bound to the subject of the certificate
+ *Example: DNS name, IP address, Internet electronic mail address*, Uniform resource identifier (URI) 统一资源标识符
* Before included, this information must be verified since it is bound to a public key

**Issuer Alternative Name 发行人替代名称**

* Associates Internet style identities with the certificate issuer
* Should not be marked critical
* Same format as Subject Alternative Name extension

**Subject Directory Attributes 主体目录属性**

* Used to convey identification attributes (e.g. nationality) of the subject
* Sequence of one or more attributes
* Must be non-critical

**Extended Key Usage**

* Indicates one or more purposes for which the certified publick key may be used, in addition to or in place of the basic puroises indicated in the key usage extension.
  + *Example: Code signing, OCSP signing, Timestamping*

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
* Authority Information Access
* Subject Information Access



### Hybrid certificates

**Hybrid certificates**

* Binding between identity and two independent public keys (primary and secondary)
* Binding certified with two signatures (primary and secondary)
* Usage of two independent signature schemes in parallel
  + Secure as long as at least one of the used schemes is secure
* Standard conformity to X.509

#### Building hybrid certificates

* Different approaches exist. In this lecture:
  + Concatenation 级联
  + Certificate Encapsulation 证书封装
  + Key-signature encapsulation 密钥签名封装
* Approaches come with different advantages and disadvantages
* Backwards compatibility  should be provied

**Backwards compatibility 向后兼容性**

Assume two entities, e.g. a client and a server,

during transition phase, hybrid certificates should still work if:

* The (legacy) server does not understand "Hybrid"
* The (legacy) client does not understand "Hybrid"
* Both entities do not understand "Hybrid"

Then: hybrid certificates should appear as common X.509 certificates

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-30 18.58.46_1M7qtd.jpg" alt="Screenshot_2024-01-30 18.58.46_1M7qtd" style="zoom:50%;" />



#### Concatenation

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-18 17.16.04_c01QVK.jpg" alt="Screenshot_2024-01-18 17.16.04_c01QVK" style="zoom:50%;" />

* Public key = concatenation of primary and secondary key
  + public key = pk1|pk2
* Signature is concatenation of a primary and a secondary signature
  + signature = sig1|sig2
* Algorithm OID identifies both signature schemes

**Advantages**

* Minimal (data) overhead
* Easy to implement
* No downgrade attackes

**Disadvantages**

* New OIDs for combined signature schemes required (treated as one signature algorithm)
* No backwards compatibility, "new" signature algorithms must be known to clients

#### Certificate Encapsulation

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-18 17.26.21_OzcOm2.jpg" alt="Screenshot_2024-01-18 17.26.21_OzcOm2" style="zoom:50%;" />

* Standard X.509 certificate
* One additional, non-critical extension &rarr; hybridCert extension
* hybridCert extension contains a complete X.509 cert
* Identical contents as hybrid certificate except:
  + Public key replaced by secondary subject public key
  + Signed with a secondary signature scheme and key by the issuer
  + Inner certificate has no hybridCert extension

**Advantages**

* Easy implementation
* Backwards compatibility

**Disadvantages**

* Redundant information (issuer, subject, validity period, ...)
  + &rarr; data overhead
  + &rarr; consistency check required
* Potential downgrade attacks to be considered during validation

#### Key-signature encapulation

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-18 17.37.15_AINyw1.jpg" alt="Screenshot_2024-01-18 17.37.15_AINyw1" style="zoom:50%;" />

* Standard X.509 certificate
* Two additional, non-critical extensions
  + ==hybridKey extension== contains secondary public key
  + ==hybridSig extension== contains secondary signature

**Advantages**

* No redundant information &rarr; minimal (data) overhead
* Backwards compatibility

**Disadvantages**

* More complex implementation
* Potential downgrade attacks to be considered during validation

**hybridKey extension**

* extension OID: id-ce 211
  + OID used in reference implementation
* Criticality: non-critical
* hybridKey: SubjectPublicKeyInfo
  + The algorithm OID of the secondary public key and its parameters
  + The secondary public key of the certificate holder

**hybridSig extension**

* extension OID: id-ce 212
  + OID used in reference implementation
* Criticality: non-critical
* Signature algorithm: AlgorithmIdentifier
  + The algorithm OID and its parameters used for the secondary signature
* Signature value: Bitstring
  + The actual signature value (over the TBS-part of the certificate)

**Implementation challenges**

* Secondary signature value is part of final tbsCertificate, but can not be included during creation of secondary signature

* tbsCertificate used for creating secondary signature must include hybridSig extension with correct byte length

  &rarr; otherweise the tbsCertificate changes when added later

* Original tbsCertificate for secondary signature needs to be recreated during verification

**Certificate creation**

1. Create standard tbsCertificate with all required extensions
2. Add hybridKey and hybridSig extensions
   + hybridSig extension contains placeholder bitstring (zero bytes) of identical length as final signature value
3. Sign resulting tbsCertificate with secondary signature algorithm and key of certificate issuer to obtain secondary signature
4. Replace zero bytes with resulting secondary signature value
5. Sign final tbsCertificate with primary signature algorithm andk key of the certificate issuer

**Hybrid certificate verification**

1. Verify primary signature of certificate with primary public key of issuer
2. Extract tbsCertificate from the certificate
3. Read signature algorithm OID from hybridSig extension &rarr; defines byte length of signature
4. Replace signature bytes in hybridSig extension with zero bytes &rarr; recreates tbsCertificate which was originally signed with secondary key
5. Use resulting tbsCertificate to verify the secondary signature with the secondary public key of the issuer
6. The certificate is valid, if primary and secondary signature are both valid, els invalid



### PGP certificate

**Pretty Good Privacy (PGP)**

* Software suite that facilitates e-mail and file protection: Encryption & Signing
* Developed by Philip Zimmermann in 1991
* Follows the OpenPGP standard (RFC 4880)

**GNU Privacy Guard (GnuPG, GPG)**

* A free open source alternative to PGP
* Implements to OpenPGP standard (RFC4880)

**Contents**

* Pubilc Key Packet
  + Version + Creation Time + Public Key Algorithm + Public Key (RSA case)
* User ID Packet
  + A User ID packet consists of UTF-8 text that is intended to represent the name and email address of the key holder.
* Signature Packet



### Other certificate types

**WAP certificates (Wireless Application Protocol) 无线应用协议证书**

* Like X.509 certificates but **smaller**
* For usage in **mobile Internet**
* Serial Number: ususally not longer than 8 bytes
* Algorithms: e.g. SHA256withECDSA
* Extensions: not all are included

**Card verifiable certificate (CVC)**

* Even more compact than WAP certificates
* For usage on smart cards (authentication)
* Signature with message recovery (ISO 9796)
* Contains barely more than Issuer, Subject, Public Key, Validity

**Attribute certificates (AC) 属性证书**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-19 13.39.03_tBRYa5.jpg" alt="Screenshot_2024-01-19 13.39.03_tBRYa5" style="zoom:50%;" />

* Similar to a PKC but contains no public key
* May contain attributes associated with the AC holder
* Example attributes: group membership, role, security clearance, ......

**Why attribute certificates?**

The placement of authorization information in PKCs is usually undesirable because:

* Authorization information often does not have the same lifetime as the binding of the identity and the public key
* PKC issuer is not usually authoritative for the authorization information



## 5. Trust Models

We trust certificates because we trust the system(s):

* Direct Trust
* Web of Trust
* Hierarchical Trust

**Meaning of trust in PKI**

In PKI, trust means::

* That certifiers reliably check authenticity of entities
* Follow certain standards and policies regarding their processes

We can trust, that an entity is who it pretends to be & that the used keys/crypto are secure.

**But not,** that an entity is indeed trustworthy in its behavior, e.g., that the online shop owner actually sends out the goods you pated for — not in the scope of PKI.



### Direct trust

User receives public key directly from owner or User verifies public key directly with owner

**Most common**

* Fingerprint comparison
  + Fingerprint = hash of certificate (incl. signature) in DER format
* Face to face verification
* Phone verification
* Web page verification
* Printed media verification

**Certificate installation**

* Step 1: Get certificate
* Step 2: View certificate &rarr; Fingerprints
* Step 3: Compare finger print
* Step 4: Decide certificate purposes

**Software signing**

* Step 1: Get software
* Step 2: Download checksum and signatures
* Step 3: Retrieve correct signature key 检索正确的签名密钥
* Step 4: Verify Signature
* Step 5: Check the ISO

**SSH step**

* SSH: Secure Shell
  + Cryptographically secure operation of network services over insecure networks, e.g. remote login or command line execution
  + User authentication based on password or public key
  + Computer authentication based always on public key
* Public-key-based user authentication
  + The user creates a key pair on the client side
  + The user deposits the public key on the server
  + The user must reomove compromised keys from the host
* Public-key-based computer authentication
  + Protection against DNS- or IP-Spoofing
  + The public key of the server is transmitted during the first login
  + The user must verify the fingerprint by asking the server's administrator
  + Warning in case of public key alteration

**Key validation problem**

* ==n*(n-1) validations = O(n^2^)==
* Worse complexity than secret key exchange



### Web of trust

* Decentralized trust model
* To establish the authenticity of the binding public key &hArr; user
* Udes in PGP, GnuPG, and other OpenPGP-compatible systems
* Each party = end-user & certification authority at the same time &rarr; All users distribute their own public keys, and certify those of ohter users

#### Key validity

Is the key owner who they claim to be?

**Key validity levels**

Levels: unknown &rarr; marginal &rarr; complete &rarr; ultimate

* Unknown: Nothing is known about this key
* Marginal: The key probably belongs to the name
* Complete: The key definitely belongs to the name
* Ultimate: Own keys

**Assigning Key validity**

* Manually set (key signing)

  + direct trust, trust anchor
  + Bob's key validity is compelte for Alice becasue she decided it when signing the key after verifying the fingerprint

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-20 17.07.32_YOKwsu.jpg" alt="Screenshot_2024-01-20 17.07.32_YOKwsu" style="zoom:50%;" />

  *Alice sets key validity of Bob by signing his key (after verification)*

* Computed from the trust in the corresponding singers, only considering singers with key validity **"complete"**

  + complete (1): If the key is ==signed by at least one user with owner trust **complete**==

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-20 17.10.13_GuKbtj.jpg" alt="Screenshot_2024-01-20 17.10.13_GuKbtj" style="zoom:50%;" />

    *Alice computes key validity using Bob's signatures*

    *Alice computes key validity using Bob's and Charlie's signatures*

  + complete (2): If the key is signed by ==at least *x* names with owner trust **marginal**==

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-20 17.28.56_Vhjr4l.jpg" alt="Screenshot_2024-01-20 17.28.56_Vhjr4l" style="zoom:50%;" />

  + marginal: If the key is signed by ==less than *x* names with owner trust **marginal**==

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-20 17.29.28_I0pA2W.jpg" alt="Screenshot_2024-01-20 17.29.28_I0pA2W" style="zoom:50%;" />

  + unknown: If the key is signed by on name with at least owner trust marginal

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-20 17.34.19_OqUley.jpg" alt="Screenshot_2024-01-20 17.34.19_OqUley" style="zoom:50%;" />



#### Owner trust

Is the key owner reliable? (in respect to signing keys of others)

**Owner trust levels**

Levels: unknown &rarr; none &rarr; marginal &rarr; complete &rarr; ultimate

* Unknown: Nothing can be said about the owner's judgment in key signing
* None: The owner is known to improperly 不恰当的 sign keys
* Marginal: The owner is known to properly 恰当的 sign keys
* Complete: The owner is known to put great care in key signing
* Ultimate: The owner is known to put great care in key signing, and is allowed to make trust decisions for you

**Assigning owner trust**

* manually set (trust setting)
  + direct trust, trust anchor



#### Trust signatures & trusted introducers

* Trust signature = special type of signature
  + The signer asserts that the key is not only valid but also trustworthly at the specified level
* Allows trust delegation along a chain of signatures
* Not widely used, often not implemented by PGP clients

**Example**

* Thunderbrid
* Sign and encrypt message
* Decrypt and verify message

**PGP Disadvantages**

* PGP lacks forward secrecy  缺乏前向保密性
* No supervision regarding upgrading algorithms and parameters (e.g., use of old ciphers)
* Bad scalability



### Hierarchical trust

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-20 17.50.40_4TmuaU.jpg" alt="Screenshot_2024-01-20 17.50.40_4TmuaU" style="zoom:50%;" />

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-20 17.51.25_c4qJHI.jpg" alt="Screenshot_2024-01-20 17.51.25_c4qJHI" style="zoom:50%;" />

####Trust models in multiple hierarchies

* Trusted Lists

  + Every participant has a list of trusted CAs
  + ==Alice trusts TC~2~ and TC~3~==
  + Every user maintains their own list (like in the Web of Trust)
  + Used in web browsers (preinstalled + user defined)
  + Alice to Freya (Certification path)

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-20 17.55.41_xkg4Nb.jpg" alt="Screenshot_2024-01-20 17.55.41_xkg4Nb" style="zoom:50%;" />

* Common Root

  + Every user who trusts TC~1~, accepts every other end-user certificate

  + Alice to Freya (Certification path):

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-20 17.57.53_KhifIF.jpg" alt="Screenshot_2024-01-20 17.57.53_KhifIF" style="zoom:50%;" />

* Cross Certification

  + TC~2~ issues a CA-certificate for TC~3~ & TC~3~ issues a CA-certificate for TC~2~ **(not always bilateral)**
  + Every user who trusts TC~3~, accepts every certificate, that was issued by TC~2~ (or a subordinate CA)
  + Every user who trusts TC~2~, accepts every certificate, that was issued by TC~3~ (or a subordinate CA)
  + Alice to Freya (Certification path):

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-20 18.01.00_GPLmhq.jpg" alt="Screenshot_2024-01-20 18.01.00_GPLmhq" style="zoom:50%;" />

  + Other possibility (1)

    + TC~2~ issues one CA-certificate to TC~7~ and vice versa

    + Harper accepts the certificate of Ellen and vice versa

    + Ellen does not accept the certificate of Freya

      <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-20 18.05.05_3Wo277.jpg" alt="Screenshot_2024-01-20 18.05.05_3Wo277" style="zoom:50%;" />

  + Other possibility (2)

    + TC~4~ issues one CA-certificate to TC~6~ and vice versa

    + Alice accepts the certificate of Freya and vice versa

    + Freya does not accept the certificate of Ellen

      <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-20 18.09.09_CtT4zZ.jpg" alt="Screenshot_2024-01-20 18.09.09_CtT4zZ" style="zoom:50%;" />

  + Cross-certification problem

    + ==n*(n-1) cross-certificates = O(n^2^)==

* Bridges

  + Bridge TC has cross-certification with TC~2~ and TC~3~

  + Alice accepts all certificates beneath TC~3~

  + Freya accepts all certificates beneath TC~2~

  + Alice to Freya (Certification path):

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-20 18.13.50_Ct4I3S.jpg" alt="Screenshot_2024-01-20 18.13.50_Ct4I3S" style="zoom:50%;" />

  + Bridge enforces minimal policy

  + Bridge trust center

    + The bridge TC acts as a connector
    + This TC is not subordinate to a third CA



#### Basic Constraints

**Basic Constraints 基本约束 (X.509 certificate extension)**

* Must be included in CA certificates
* It is marked critical
* If pathlength is not present &rarr; no limit

**Identifies**

* whether the subject of the certificate is a CA
* the maximum number of non-self-issued intermediate certificates that may follow this certificate in a valid certification path

**Example**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-20 18.20.17_CJNgAK.jpg" alt="Screenshot_2024-01-20 18.20.17_CJNgAK" style="zoom:50%;" />

* ca
  + = true: 表示该证书是CA证书，且允许颁发其他证书
  + = false: 表示该证书被视为最终实体证书
* pathLength
  + = 1: 表示可以颁发最大路径为1（包括其自身）的证书
  + = 0: 表示该证书只能签署最终实体证书，不能用于创建具有任何中间CA证书的证书途径



## 6. The Wek PKI

**CAs do not always adhere to the rules, e.g.,**

+ prohibited algorithms (key size too small, ...)
+ Unauthorized issuance
+ Audit issues

**Web PKI - CA/Browser Forum**

* Baseline Requirements
  + a subset of the requirements that a CA must meet in order to issue digital certificates for SSL/TLS servers to be publicly trusted by browsers
* Extended Validation Certificate Guidelines
  + Stricter set of guidelines providing stronger guarantees for the identity of the certificate holder

**Problems**

* Huge number
* Governmental access
* No globally standardized mechanism to ensure a CA's trustworthiness
* Any CA ultimately fallible

**Certificate Transparency 证书透明度**

1. Website owner requests a certificate from the **Certificate Authority (CA) **证书颁发机构
2. CA issues a precertificate
3. CA sends precertificates to logs
4. Precertificates are added to the logs
5. Logs return SCTs to the CA
6. CAs send the certificate to the domain owner
7. Browsers and user agents help keep the web secure
8. Logs are cryptographically monitored



## 7. Revocation

**Certificate revocation**

Abortive ending 异常终止 of the binding between:

* subject and key (public key certificate)
* subject and attributes (attribute certificate)

The revocation is initiated by **the subject** or **the issuer**.

**Revocation requirements**

* Revocation infrmation is publicly available
* Authenticity can be checked by everyone
* Revoked certificate is unambiguously identified 明确标识已吊销证书
* Information about the time of the revocation
* Optional:
  + revocation reason
  + Temporary revocation 临时撤销 (on hold / suspended)
* X.509: CAs are responsible for publishing revocation information



### CRLs I (Basic CRLS)

#### CRL

**CRL (Certificate Revocation List) 证书吊销列表**

* Signed (&rarr; authenticated) list of revoked certificates
* "Blocklist", i.e., no positive information about the validity of a certificate
* Standard mechanism (e.g., X.509) 标准机制
* Wide-spread mechanism

**Structure of a CRL**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-23 14.25.55_O9jun6.jpg" alt="Screenshot_2024-01-23 14.25.55_O9jun6" style="zoom:50%;" />

* Version: currently version 2
* Signature ID: signature algorithm
* Issuer: issuer name
* This Update: issuance time of the CRL 签发时间
* Netx Update: date of the netxt update
* List of revoked certificates: **sequence of CRL entries CRL条目的序列**
* CRL extensions (version 2): extensions for the whole CRL

**Structure of a CRL entry**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-23 14.29.41_edSRje.jpg" alt="Screenshot_2024-01-23 14.29.41_edSRje" style="zoom:50%;" />

* userCertificate: serial number of the certificate
* revocationDate: revocation time for this certificate
* CRLEntry-extensions (version 2): extensions regarding this CRL entry only 仅与此CRL条目相关的扩展

**CRL properties**

* Can be used offline (CRL caching)
* Easy implementation & management
* High information content (extendable)
* The CRL (Full CRL) contains information about all revoked certificates &rarr; size increases monotonically
* All information is transferred at the same time
  + High load (peak) at "next update" time
  + Long validity period &rarr; bad timeliness
  + Short validity period &rarr; bad performance
  + Workarounds & modifications
    + Lean CRLs
      + expired certificates are removed from the CRL 过期的证书将从CRL中删除
      + expired certificates can not be checked anymore
    + Variants of CRLs beside basic complete CRLs
      + Over-issued CRLs
      + Delta CRLs
      + Indirect CRLs
      + Partitioned CRLs
      + Redirect CRLs

**Publishing CRLs**

* Most common:
  + Web pages (HTTP)
  + LDAP
* Other possibilities:
  + File transfer protocol (FTP)
  + CRL push service (Broadcasts)
    + CRLs are delivered to registered clients
    + Searching for a CRL is unnecessary
    + Can only be used online
    + Suitable for e.g., Computer in intranet, Servers
    + Covers only certificates of few PKIs

**Locating a CRL**

* Using the policy:
  + The policy of the issuer names places where its CRLs are published
* Using the certificate:
  + CRLDistributionPoints extension
    + X.509 certificate extension
    + Non-critical
    + Identifies how CRL information is obtained
    + Usage recommended
    + Realized by the most typical applications



#### CRL extensions (X.509)

CRL extensions affect the CRL as a whole or each single CRL entry (all of them)

**AKI / IAN** (As in X.509 certificates)

* Authority Key Identifier
* Issuer Alternative Name

**CRL Number**

* Monotonically increasing sequence number 单调递增的序列号
* **Non-critical** extensions, ==must be included in all CRLs==
* To determine when a particular CRL supersedes another CRL 确定特定的CRL何时取代另一个CRL
* Two CRLs for same scope generated at different times must not have same CRL number
* Supports the use of Delta CRLs

**Issuing Distribution Point**

* **Critical** extension
* Identifies the CRL distribution point and scope
* Indicates whether the CRL covers revocation for
  + end-entity certificates only
  + CA certificates only
  + attribute certificates only
  + a limited set of reason codes



#### CRL entry extensions (X.509)

CRL entry extensions affect the current CRL entry and maybe some following ones (but not necessarily all of them)

**Reason Code**

* **Non-critical** extension
* Identifies the reason for certificate revocation

**Hold Instruction Code**

* Non-critical extension
* Indicates the action to be taken after encountering a certificate that has been placed on hold
* Standard actions:
  + None
  + Contact issuer or reject certificate
  + Reject certificate

**Invalidity Date**

* Non-critical extension
* Provides the (suspected) date on which the certificate became invalid
* CRL issuers are strongly encouraged to share this date with CRL users



### CRLS II (CRL Variants)

**Over-Issued CRLs**

* CRLs issued more frequently than "nextUpdate" requires
* e.g., on a regular basis or with every certificate revocation
* Frequency of the updates is chosen by the client

**Delta CRL**

* Format like: a "normal" CRL + Delta CRL Indicator extension
* Contains ALL changes since Base CRL was issued
* Associated to Base CRL by the **BaseCRLNumber**

  &rarr; Better network load, netter scalability

  &rarr; Slightly increases administration costs

**CRL segmentation**

* Revocation information for disjoint sets of certificates is spilt up into multiple Partitioned CRLs
* Relevant CRL identified:
  + Directly: Multiple CRLDistributionPoints, or
  + Indirectly: CRLDistributionPoint extension points to a special Redirect CRL
* Redirect CRL
  + Set of pairs
  + The scope describes a set of certificates
  + Advantage: Can be changed later



####X.509 CRL extensions

**CRL Number (cont.)** 

* CRL numbers are used to identify complementary complete CRLs and Delta CRLs
* CRL numbering conventions for Delta CRLs
  + Complete and Delta CRLs for a given scope must share one numbering sequence
* A complete and a Delta CRL issued at the same time must have same CRL number and provide same revocation information 同时颁发的完整CRL和Delta CRL必须具有相同的CRL编号并提供相同的吊销信息

**Delta CRL Indicator** 

* Critical extension
* Identifies a CRL as being a Delta CRL
* Contains a single value called **BaseCRLNumber**
* The BaseCRLNumber identifies the CRL used as the starting point in the generation of the Delta CRL. BaseCRLNumber标识用作生成此Delta CRL起点的CRL
* The reference base CRL must be published as a complete CRL

**Freshest CRL** 

* a.k.a. Delta CRL Distribution Point
* Non-critical extension
* Identifies how to obtain Delta CRLs
* Must not appear in Delta CRLs
* Thie extension also exists as a standard X.509 certificate extension

**Indirect CRLs**

* Issuer of the CRL is not the issuer of the certificates
* Revocation can be delegated
* Revocation instance can operate online even if certificate issuer is offline

**Certificate Issuer** (X.509 CRL entry extension)

* Critical extension
* Identifies the certificate issuer associated with an entry in an indirect CRL
* If this extension is not present:
  + on the first entry in an indirect CRL
  + on subsequent entries



### OCSP

**OCSP (Online Certificate Status Protocol) 在线证书状态协议**

* RFC 6960
* Client-Server architecture, where clients:
  + request status of certificates from an OCSP responder (server)
  + communicate online, in (near) real time
  + can request status of multiple certificates inside a single query

**OCSP-Responder**

Responder:

* Provides signed answers
* Has a certificate with the extension **extendedKeyUsage = OCSPSigning**

Possible responses (basic version):

* Unknown, nothing known about the certificate, e.g., issuer unknown
* Revoked, certificate revoked or may not exist
* Good, no such certificates is within its validity period and is revoked
  + Good means that the certificate is not revoked, but it may be expired 到期 or even not exist at all

**Structure of an OCSP request**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-24 13.06.37_lTGnBo.jpg" alt="Screenshot_2024-01-24 13.06.37_lTGnBo" style="zoom:50%;" />

**Structure of an OCSP response**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-24 13.07.48_3iKVQm.jpg" alt="Screenshot_2024-01-24 13.07.48_3iKVQm" style="zoom:50%;" />

**Structure of an OCSP response - SingleResponse**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-24 13.08.53_vmiEA3.jpg" alt="Screenshot_2024-01-24 13.08.53_vmiEA3" style="zoom:50%;" />

**Signed response acceptance requirements**

* The certificate identified in a received response corresponds to the certificate identified in the corresponding request
* The signature on the response is valid
* The identity of the signer matches the intended recipient of the request
* Thetime at which the status being indicated is known to be correct (thisUpdate is sufficiently recent)
* When available, the time at or before which newer information will be available about the status of the certificate (nextUpdate) is greater than the current time

**OCSP server revocation**

Problem: Is the certificate of the OCSP server valid?

Approaches:

* No revocation for the certificates of OCSP resonders
  + Speical extension ocsp nocheck
  + Short validity period
* Use CRLs
* Leave it to the verifier

**OCSP Stapling**

Transport Layer Security (TLS) Extensions: Extensions Definitions - RFC 6066:

* During the TLS handshake, servers may return a suitable certificate status response along with their certificate
* Servers can cahce OCSP responses and reuse them (until nextUpdate time) 服务器可以缓存OCSP响应并重用它们

Transport Layer Security (TLS): Multiple Certificate Status Request Extension - RFC6961:

* Mainly solves two problems of RFC 6066:
  + RFC 6961 allows to staple multiple OCSP responses
  + RFC 6961 allows the client to offer the server multiple status methods

**OCSP Must-Staple (X.509 certificate extension)**

* X.509V3 Tranpsort Layer Security (TLS) Feature Extension - RFC7633
* Should not be marked critical
* Indicates, that server must staple OCSP status information
  + hard fail possible on absence of stapled OCSP info



### Hash-Based Revocation CRS/CRT

**Hash-based revocation**

* No explicit revocation necessary
* But explicit validation
* By publishing "not revoked" information

#### CRS (Certificate revocation system) 证书吊销系统

* Proposed by Micali in 1996
* Instead of producing CRLs, the CA updates the directory daily by indicating the status of each issued certificate
* In order to do this, it uses an authentication system based on a one-way function

**One-way functions**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-24 15.30.01_p0dbMI.jpg" alt="Screenshot_2024-01-24 15.30.01_p0dbMI" style="zoom:50%;" />

* Here:
  + a function **f** which is one-way, and can be used repeatedly (i.e. f(x),f(f(x)), ..., f(f(f(...f(x)))))
  + typical representatives: cryptographic hash functions

**A 3 day authentication system**

* Choose a random number **r~0~** and a one-way function **f**
* Calculate:
  + **r~1~** = f(r~0~)
  + **r~2~** = f(f(r~0~)) = f(r~2~)
  + **r~3~** = f(f(f(r~0~))))) = f(r~2~)
* Sign **r~3~** and publish **r~3~** and the signature
* On day one, to prove it is you, publish **r~2~**
* Verifiers then can calculate **f(r~2~)**, find that it is **r~3~** and know that it must be you
* On day two, give them **r~1~** and on day three, give them **r~0~**

 **Micali's CRS**

* Functionality
  + For each certificate, choose two random numbers, **N~0~ and Y~0~**
  + Compute **Y~365~** = f^365^(Y~0~) and **N** = f(N~0~) and put them into the certificate
  + On day i:
    + if the certificate is still valid, publish the value **C** = Y~365-i~ = f^365-i^(Y~0~)
    + if it is invalid, publish **C = N~0~**
* Properties
  + C servers as proof of authenticity or revocation
  + Update bandwidth is high, depending on the total number of certificates
  + Verification of known certificates is low-bandwidth
  + If a user has never verified a particular certificate before, on day 364 he must calculate **f^364^(C)** to verify it
  + If we increase the rate of updates, we increase the computation time needed



#### CRT (Tree-based system)

* Choose a cryptographically strong (one-way) hash function h
* Randomly generate **2^Y^** numbers as leaves of a binary tree
* Build a hash-tree
* Put the value of the root node into the certificate (replacing Y~365~ from Micali's system)
* On a day i, release the values of the path from leaf node i and all nodes on the path needed to compute the root

**Effect**

* **O(log(#leaves))** hash values have to be released each day, so updates are a little worse than original Micali, but not much
* Computation time is now als O(log(#leaves)), which is much better

 

### Revocation in PGP

**Revocation Certificate**

* Keep this certificate secret
* Others could revoke the key if they have it

**Revocation in PGP**

* By publishing the revocation certificate (on PGP key servers)
* The key owner (the subject) is responsible for revocation
* The private key is required to generate the revocation certificate
  + If the private key is lost, and no revocation certificate has been generated before: revocation is impossible

**PGP key servers —— key removal?**

* Can one remove a key from key servers in order to "revoke" it?
* No
  + Most PGP servers are not designed to support this
  + There is no mechanism to remove keys once published
  + PGP servers are regularly synced
  + Everybody could upload the removed key again



## 8. The Web PKI ——Revocation

**Problems**

* Detection
  + Wrong / malicious certificate must be detected
  + How to do this in a system, where hundreds of CAs can potentially issue certificates?
* Distribution / availability
  + Delays in general not accepted (by users)
  + Hard vs. soft fails
* Too-big-to-fail
  + Revocation may endanger functioning of whole infrastrucutres (large CAs)

**Approachs**

* Detection
  + Public key pinning
    + a pin is a relationship between a hostname and a cryptographic identity
    + key pinning is a trust-on-first-use (TOFU) mechanism
  + Public logs
    + e.g. Certificate Transparency
  + DNSSEC + DANE (DNS-Based Authentication of Named Entities)
    + DNSSEC: signed DNS responses
    + NANE: DNS records also contain public keys of servers
  + Notaries
    + Ask third party
* Distribution / availability
  + OCSP must-staple
  + Proprietary push and aggregation mechanisms
    + OneCRL —— intermediate CA certificate
    + CRLite ——end entity certificates
    + CRLSets (Chrome)
    + Other browsers come with own mechanisms
  + No revocation checking for certificates with a validity period < 10 days
* Too-big-to-fail
  + Implementation of **chain model** for certificate validation
    + Chain model problems: Signature key compromise &rarr; Signature and time information in certificates are unreliable
  + Fine grained revocation & path validation with forward secure signatures



## 9. Validity Models

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-25 13.16.00_8PGtsl.jpg" alt="Screenshot_2024-01-25 13.16.00_8PGtsl" style="zoom:50%;" />

### Shell Model

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-25 12.24.47_6IIMRQ.jpg" alt="Screenshot_2024-01-25 12.24.47_6IIMRQ" style="zoom:50%;" />

* Signature time: 所有证书中有一个有效时就能创建签名 （证书不都有效时可以签名，但是直到所有证书都有效才能验证）
* Vertification time: 所有证书在验证时都有效，则签名自动有效
* 用于RFC5280的路径验证，如：上网时浏览器检查Web服务器的证书或证书链



### Modified or hybrid model

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-25 12.25.20_6uCL5x.jpg" alt="Screenshot_2024-01-25 12.25.20_6uCL5x" style="zoom:50%;" />

* Signature time: 只有所有证书均有效时才能创建签名
* Verification time: 只检查在签名时，所有证书是否有效 （即，所有证书在签名时都是有效的）

### Chain Model

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-25 12.25.45_q4pZyE.jpg" alt="Screenshot_2024-01-25 12.25.45_q4pZyE" style="zoom:50%;" />

* Signature time: 只要最底层的证书有效，且链上的证书2签署能够追溯到证书1有效时创建签名
* Veritification time: 只要算法不过期，检查每一个上级证书是否在对当前证书签名时有效



## 10. Certification Service Provider (Trust Center)

### CSP

**Certification service provider (CSP) 认证服务商**

* Serves as trust anchor in hierarchical PKIs
* Responsible for correct operation of the PKI
* Trusted third party
* "Home" of the issuer
* Provides entities with PKI services

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-25 13.25.46_XC0oXz.jpg" alt="Screenshot_2024-01-25 13.25.46_XC0oXz" style="zoom:50%;" />

**CSP components (authorities)**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-25 13.28.30_QeCqbG.jpg" alt="Screenshot_2024-01-25 13.28.30_QeCqbG" style="zoom:50%;" />

#### Registration authority (CA) 登记机关

* Contact point for (prospective) PKI entities
* Register prospective entities
* Establish "customer relationship"
* Accept requests from entities
* Usually online

**Key/certificate life cycle and RA**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-25 13.32.28_Pbx1iv.jpg" alt="Screenshot_2024-01-25 13.32.28_Pbx1iv" style="zoom:50%;" />

**Procedure in CSP**

1. determines identity and public key
2. generates digital name
3. issues certificate

#### Registration

**Establish**

* identitiy
  + whatever makes an entity definable and recognizable
  + whatever maks something the same or different
  + Example: 
    + Name &rarr; biometrical data
    + Residence &rarr; employer
    + Citizenship &rarr; name of the parents

* contact information
  + Information about the accessibility of a participant, e.g.:
    + pstal address
    + Telephone number
    + email address
* client preferences
  + Choice of the cryptosystem and parameters
  + Delivery (smart card, PIN-letter, etc.)
  + Certificate's validity period
  + Pseudonym 签名
* billing data
* public keys and proof-of-possession (optional)



### Client keys

* The clients may generate their own keys
* How to transfer the public key to the Certification Service Provider?
  + PKCS#10
    + Public-key + additional attributes
    + Signature with the corresponding private key
  + Directly in the browser
    + special HTML-Form field
    + modified PKCS#10-format
    + Signature with a private key that is generated in the browser

#### PKCS#10

* Defines syntax for certification requests (a.k.a CSR, certificate signing request 证书签名请求)
* Response format (how to send back the certificate): out of scope of PKCS#10

**Certification request construction**

1. Requesting entity generates **CertificationRequestInfo**

   <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-25 14.02.18_sXVjKC.jpg" alt="Screenshot_2024-01-25 14.02.18_sXVjKC" style="zoom:50%;" />

2. **CertificationRequestInfo** value signed with the subject entity's private key

   <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-25 14.02.52_wpGq2E.jpg" alt="Screenshot_2024-01-25 14.02.52_wpGq2E" style="zoom:50%;" />

3. **CertificationRequestInfo** + a signature algorithm identifier + signature value = **CertificationRequest**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-25 14.03.27_HijQ7M.jpg" alt="Screenshot_2024-01-25 14.03.27_HijQ7M" style="zoom:50%;" />

**Building a hybrid CSR**

* The **extensionRequest** attribute type may be used to carry information about certificate extensions the requester wishes to be included in a certificate
* Same procedure as for hybrid certificates (hybridKey- and hybridSig extension)
  + hybridSig extension contains secondary signature over CertificationRequestInfo (PoP)

### Proof-of-Prossession (PoP) 所有权证名

**PoP: CRMF** (certificate request message format) 证书请求报文格式

* Defines a ProofOfPossession field to include PoP information into certificate request messages
* Contents of PoP field depend on key type
  + **Signature keys:** signature on a piece of data containing the requestor's identity
  + **Encryption keys:** providing private key to CA/RA, direct method, indirect method
    + Direct: Encrypt a value and have the entity decrypt it
    + Indirect: Encrypt the certificate and have the entity decrypt it
  + **Key agreement keys:** establishing ephemeral key + employing one of the methods defined for encryption keys or providing a MAC over certificate request computed with the ephemeral key
    + Establishment of a shared secret key between CSP and entity

**PoP: PKCS#10**

In PKCS#10 this is performed by signing the request

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-25 14.13.20_j1yNtc.jpg" alt="Screenshot_2024-01-25 14.13.20_j1yNtc" style="zoom:50%;" />



### Secure "Out-of-Band" channel 

Independent of the PKI:

* Face-to-face communication (i.e. local presence)
* Previoulsy established shared secrets (e.g. passwords)
* Third-party services (e.g. Postident)

**Registration with Postident**

1. The CPS issues a coupon
2. The customer delivers the coupon to the post office
3. The post office employee checks a valid offical document (ID-card, passport, etc.) and fills out an application with the customer's data
4. The application is signed by the customer and the post office employee
5. The post office employee sends the application and coupon to the CSP

**Data sources**

* Independent ascertainment by the RA
  + personal contact
  + online registration
* Usage of data from third parties
  + E.g. staff database, registry office
  + security depends on the data source
  + input assistance or trusted source

**RA models**

* Centralized
  + One RA for all participants
* Decentralized (Local Registration Authority, LRA)
  + Different RAs for different participant groups
  + Reasons for decentralization:
    + Topology
    + Separation of the responsibilitite
    + On-site registration
    + Fail-safeness
* Hybrid models
  + E.g. distributed collection of data, but centralized data management



### Classification for TLS certificates

* Also not part of X.509 standard but commonly agreed

* Describles the strength of performed identity validation

* Indicated via OID in the X.509 Certificate Policies extension

* 3 types:

  + domain validation (DV): 

    + existence & control over domain verified

    + OID value: 2.23.140.1.2.1

  + organization validation (OV):

    + some additional checks regarding the requesting organization
    + OID value: 2.23.140.1.2.2

  + extended validation (EV):

    + thorough validation of the requesting organization
    + OID value: 2.23.140.1.1

#### Extended validation certificates

In order to issue an extended validation (EV) certificate, thorough validation is performed.

* Scope: EV Certificates are intended for use in establishing web-based data communication conduits via TLS/SSL protocols
* Primary purposes
  + Identify the legal entity that controls a website
  + Provide reasonable assurance that the website is controlled by a specific legal entity identified by: name, address of place of business, jurisdiction of incorporation, and registration number
  + Enable the encrypted communication of information
* Secondary purposes
  + Establish the legitimacy of a business by confirminf its legal and physical existence
  + Assist in addressing problems related to phishing and other forms of online identity fraud



### Directory services (DS) 目录服务

* Publish PKI information
* Deliver PSEs
* Manage certificate lifecycle
* Usually online
* Example:
  + Certificate notification
  + Certificate retrieval
  + (Automatic) certificate installation



## 11. Policies 政策

**PKI policies & practice statements**

* Certificate policy (CP)
  + States what to comply with
* Certificate practice statement (CPS)
  + States how to comply

**RFC 3647**

* Framework for CPs and CPSs
* List of topics that potentially need to be convered in a CP or CPS

**Certificate policy (CP) 证书政策**

* Definition:
  + A named set of rules that indicates the applicability of a certificate to a particular community and/or class of application with common security requirements
* Example:
  + A CP might indicate applicability of a certain type of certificate for authentication in business-to-business transactions

**Certification practice statement (CPS) 认证实践证明**

* Definition:
  + A statement of the practices that a certification authority employs in issuing, managing, revoking, and renewing or re-keying certificates

**Differences between CP & CPS**

* CP and CPS address the same set of topics
* Primary difference: the focus of their provisions
  + CP - states requirements and standards imposed by PKI
    + &rarr; what participants must do
  + CPS - states how to meet the requirements stated in the CP
    + &rarr; how to perform functions and implement controls
* Additional difference: their scope of coverage
  + CP: best serves as the vehicle for communicating minimum operating guidelines that must be met by interoperating PKIs
    + &rarr; generally applies to multiple CAs / organizations /domains
  + CPS: applies only to a single CA / organization, not generally a vehicle to facilitate interoperation

**X.509 certificate extensions supporting the use of Cps**

* Certificate Policies extension 证书政策扩展
  + Policy information term:
    + a policy identifier (as OID) + optional policy qualifiers
    + In end-entity certificates:
      + Indicates the policy under which the certificate has been issued and the purposes for which the certificate may be used
    + In CA certificates:
      + Limits the set of policies for certification paths which include this certificate
      + Circumvention of limitation: by use of special policy "anyPolicy"
* Policy Mappings extension (see next chapter "Path validation")
* Policy Constraints extension (see next chapter "Path validation")



## 12. Certification Path Building

**Public information**

* Where it this information published?
* How can I find a certificate?
* How can I find a CRL?
* What are the CRL distribution points in a certificate?

**Possible solutions**

* DNS
* OCSP Responders
* Web Servers and HTTP
* FTP
* Certificate store access via HTTP
* LDAP

### LDAP 轻量级目录访问协议

LDAP: Lightweigt Directory Access Protocol

* Offers various and flexible solutions
* Most used soltion:
  + RFCs 4510 - 4513
* Information is organized hierarchically in a tree structure
* Directory accessed through a client

**Data Model**

* Data is stored as entries
* Every entry has a unique identifier: a Distinguished Name (DN) 专有名称
  + Entry's DN = its Relative Distinguished Name (RDN) + parent entry's DN
  + Usually the subjectDN of an X.509 certificate matches the DN of the LDAP
* Every entry has one or more attributes
* Every attributes has a name (type) and one or more values

**Distinguished Names**

* CN: Common Name
* L: Locality
* ST: State or Province
* O: Organization
* OU: Organizational Unit
* C: Country
* STREET: Street Address
* DC: Domain Component
* UID: User Id

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 00.22.50_tOXKq6.jpg" alt="Screenshot_2024-01-27 00.22.50_tOXKq6" style="zoom:50%;" />

### RFC 4158 Certification Path Building

**Certification Path Building**

* Criterion 1: The implementation is able to find all possible paths, excepting paths containing repeated subject name/public key pairs
* Criterion 2: The implementation is as efficient as possible.

**Forward search (issuedToThisCA)**

Start with the end entity certificate

Only use certificates found in:

* cACertificate attributes
* Forward (issuedToThisCA) element of the crossCertificatePair attributes
* Example: (Cert = W, TA = K, **CP = K &rarr; Bridge &rarr; Q &rarr; S &rarr; U &rarr; W**)

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 00.28.22_BRicTX.jpg" alt="Screenshot_2024-01-27 00.28.22_BRicTX" style="zoom:50%;" />



## 13. Path Validation

### Certification path validation

**Path validation** verify the binding: subject distinguishe name (SDN) or subject alternative name (SAN) &harr; subject public key

**Steps:**

1. **Initialization:** Performed exactly once
2. **Basic certificate processing:** Once for each certificate
3. **Preparation for next certificate:** Once for each certificate (except the last one)
4. **Wrap-up:** Performed exactly once

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 17.53.10_YMQtB9.jpg" alt="Screenshot_2024-01-27 17.53.10_YMQtB9" style="zoom:50%;" />



### Initialization 初始化

#### Input variables

**Input variables - 1: Prospective certification path of length n**

* The certification path to be validated
* Note: A certificaste must not appear more than once in a prospective certification path 证书不得在预期的认证路径中出现多次
* Exapmle: (Path length = 3)

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 17.58.19_IOblxv.jpg" alt="Screenshot_2024-01-27 17.58.19_IOblxv" style="zoom:50%;" />

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 17.58.43_Qx4IS3.jpg" alt="Screenshot_2024-01-27 17.58.43_Qx4IS3" style="zoom:50%;" />

**Input variables - 2: Current date/time**

* This is the time at which the path validation runs
  + Shell model
  + Hybrid model by "cheating"

**Input variables - 3: User-initial-policy-set**

* A set of certificate policy identifiers
  + The polices acceptable to the certificate user
  + Contains "anyPolicy" if the user is not concerned about certificate policies
* Example:
  + {1.2.3.4, 9.8.7.6}
  + or more "readable" {gold, silver}

**Input variables - 4: Trust anchor information**

* May be provided in form of a self-signed certificate
* is trusted because it was delivered by some trustworthy out-of-band procedure

(1) the trusted issuer name

(2) the trusted public key algorithm

(3) the trusted public key

(4) optionally, the trusted public key parameters associated with the public key

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 18.36.45_kdZlDB.jpg" alt="Screenshot_2024-01-27 18.36.45_kdZlDB" style="zoom:50%;" />

**Input variables - 5: Initial-policy-mapping-point**

* Indicates if policy mapping is allowed in the certification path
* Either true or false
* &rarr; X.509 extension Policy Mappings

**Input variables - 6: Initial-explicit-policy**

* Indicates if the path must be valid for at least one of the certificate policies in the user-initial-policy-set
* Either true or false
* &rarr; X.509 extension Policy Constraints

**Input variables - 7: Initial-anyPolicy-inhibit**

* Indicates whether the anyPolicy OID should be processed if it is included in a certificate
* Either true or false
* &rarr; E.509 extension Inhibit anyPolicy

**Input variables - 8: Initial-permitted-subtrees**

* Indicates which names are allowed for subject names in the path
* For each name type (e.g., X.509 distinguished names, email addresses, or IP addresses): a set of subtrees defining the acceptable names

**Input variables - 9: Initial-excluded-subtrees**

* Indicates which names are not allowed for subject names in the path
* For each name type: a set of subtrees defining the prohibited names
* &rarr; X.509 extension Name Constraints

**Initialization**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-02 22.30.20_nU05ED.jpg" alt="Screenshot_2024-02-02 22.30.20_nU05ED" style="zoom:50%;" />



#### X.509 extension

**Policy Mappings**

* Only for CA certificates
* Should be marked critical
* Contains pairs of (Policy) OIDs the issuing CA considers equivalent
* Each pair: Indicates equivalence of an issuing CA's policy with a subject CA's policy

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 18.54.34_KMfAru.jpg" alt="Screenshot_2024-01-27 18.54.34_KMfAru" style="zoom:50%;" />

* Example: Policy evaluation (User requires "Gold")

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 18.55.53_Ds32cP.jpg" alt="Screenshot_2024-01-27 18.55.53_Ds32cP" style="zoom:50%;" />

**Policy Constraints**

* Only for CA certificates
* Must be marked critical
* Contains two integers:
  + Allowed number of subsequent certificates before an explicit policy is required
  + Allowed number of subsequent certificates before policy mapping is no longer permitted

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 18.58.48_HkaO6m.jpg" alt="Screenshot_2024-01-27 18.58.48_HkaO6m" style="zoom:50%;" />

**Inhibit anyPolicy**

* Only for CA certificates
* Must be marked critical
* Contains on integer:
  + Allowed number of subsequent certificates before anyPolicy is no longer permitted
  + Self-issued certificates not counted, may still use anyPolicy
* Example: Policy evaluation (User requires "Gold")
* E.g. Value of "1" &rarr; anyPolicy may be processed in next certificate in the path, but not in additional ones.

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 19.00.56_Mklaly.jpg" alt="Screenshot_2024-01-27 19.00.56_Mklaly" style="zoom:50%;" />

**Name Constraints**

* Only for CA certificates
* Must be marked critical
* Indicates the name space for allowed subject names in subsequent certificates
* Applys to SubjectDN and SubjectAlternativeName

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 19.02.32_PMpEA0.jpg" alt="Screenshot_2024-01-27 19.02.32_PMpEA0" style="zoom:50%;" />



### Process cert

#### Valid_policy_tree

**Algorithm variable**

* A tree of certificate policies + their optional qualifiers
* Leaves represent valid policies at respective stage in the certification path validation
* If valid policies exist:
  + tree depth = the number of processed certificates
* If valid policies do not exist:
  + the tree is set to NULL, policy processing ceases

**Nodes**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 19.17.49_n0AcZb.jpg" alt="Screenshot_2024-01-27 19.17.49_n0AcZb" style="zoom:50%;" />

**Initial state**

depth 0:

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 19.19.35_uV375j.jpg" alt="Screenshot_2024-01-27 19.19.35_uV375j" style="zoom:50%;" />



#### Basic certificate processing

**Once for each certificate:**

1. Basic verification
   + Certificate signature can be verified with the working_public_key_algorithm, working_public_key, and working_public_key_parameters?
   + Certificate is valid in time?
   + Not revoked or on hold?
   + Issuer Name = working_issuer_name?
2. SDN and SANs belong to permitted_subtrees?
3. SDN and SANs do not belong to excluded_subtrees
4. Policy processing
5. If policies not present, then set valid_policy_tree to NULL
6. Verify explicit_policy or valid_policy_tree

**policy processing - exact match**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 22.32.18_FYRs0Q.jpg" alt="Screenshot_2024-01-27 22.32.18_FYRs0Q" style="zoom:50%;" />

**policy processing - leaf node-anyPolicy**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 22.33.11_nB3myw.jpg" alt="Screenshot_2024-01-27 22.33.11_nB3myw" style="zoom:50%;" />

**policy processing - certificate-anyPolicy**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 22.33.58_57dpYW.jpg" alt="Screenshot_2024-01-27 22.33.58_57dpYW" style="zoom:50%;" />

**policy processing - deletion of nodes w/o children**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 22.34.51_y75N9d.jpg" alt="Screenshot_2024-01-27 22.34.51_y75N9d" style="zoom:50%;" />



### Prepare for next cert

* Once for each certificate (except the last one)
* Process policy mappings
* Update algorithm variables

**Policy mapping**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 22.46.10_FaV71n.jpg" alt="Screenshot_2024-01-27 22.46.10_FaV71n" style="zoom:50%;" />

**Policy mapping to ANY**

==This is not allowed!==

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 22.46.58_nlTVJx.jpg" alt="Screenshot_2024-01-27 22.46.58_nlTVJx" style="zoom:50%;" />

**Policy mapping from ANY**

==This is not allowed!==

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 22.49.02_Y0jt9y.jpg" alt="Screenshot_2024-01-27 22.49.02_Y0jt9y" style="zoom:50%;" />



### Wrap-up

* Only for certificate n
* Update (some) algorithm variables
* Recognize and process extensions fo certificate n
* Finalize valid_policy_tree: Calculate the intersection of the **valid_policy_tree 有效策略树** and the **user_initial_policy_set (uips) 用户初始策略集**

**Finalize_valid_policy_tree**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 22.54.30_GbwdFG.jpg" alt="Screenshot_2024-01-27 22.54.30_GbwdFG" style="zoom:50%;" />

1. Determine the set of policy nodes whose parent nodes have a **valid_policy 有效策略** of anyPolicy

   <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 22.57.29_5yww1c.jpg" alt="Screenshot_2024-01-27 22.57.29_5yww1c" style="zoom:50%;" />

2. If the valid_policy of any node in the **valid_policy_node_set 有效策略节点集** is not in the user_initial_policy_set and is not anyPolicy, delete this node and all its children

   <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 22.59.28_aFh6GG.jpg" alt="Screenshot_2024-01-27 22.59.28_aFh6GG" style="zoom:50%;" />

3. **(Wrap-up)** If the valid_policy_tree includes a node of depth n with the valid_policy anyPolicy and the user_initial_policy_set is not anyPolicy, perform the following steps:

   + for each P-OID in the user_initial_policy_set that is not the valid_policy of a node in the valid_policy_node_set, create a child node whose parent is the node of depth n-1 with the valid_policy anyPolicy
   + delete the node of depth n with the valid_policy anyPolicy

   <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 23.06.16_xEBn9C.jpg" alt="Screenshot_2024-01-27 23.06.16_xEBn9C" style="zoom:50%;" />

4. result

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 23.06.49_j0szEV.jpg" alt="Screenshot_2024-01-27 23.06.49_j0szEV" style="zoom:50%;" />

**Output**

* If either (1) the value of explicit_policy variable is greater than zero or (2) the valid_policy_tree is not NULL, then path processing has succeeded
* If successful
  + success indicator
  + Valid_policy_tree
  + Working_public_key
  + Working_public_key_algorithm
  + Working_public_key_parameters
* Else
  + failure indicator



### Path validation for hybrid certificates

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 13.40.42_YWkCW6.jpg" alt="Screenshot_2024-01-29 13.40.42_YWkCW6" style="zoom:50%;" />

* Hybrid certificates (HC):
  + 2 keys
  + 2 signatures
  + 2 different crypto systems used
* Challenge:
  + Standard path validation only considers a single key/signature
* Goal:
  + Adapt path validation such that
    + Binding of both keys to subject are verified
  + While
    + Downgrading attacks are prevente
    + Full backward compatibility is ensured



#### Hybrid verification

Adaptations of standard path validation algorithm:

* 3 variables concerning second key/signature to be added for HC enabled clients
  + the second trusted public key: w_pk_2
  + the second trusted public key algorithm: w_pk_a_2
  + optionally, the trusted public key parameters associated with the second public key: w_pk_p_2
* 1. Initialization
     + Additionally set w_pk_2, w_pk_a_2, w_pk_p_2 with given trust anchor information
  2. Basic certificate processing
     + no adaptations
  3. Preparation for next certificate
     + Process hybrid certificate extensions, update w_pk_2, w_pk_a_2, w_pk_p_2
  4. Wrap-up
     + Process hybrid certificate extensions, update and additionally output w_pk_2, w_pk_a_2, w_pk_p_2

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 13.50.00_orR9du.jpg" alt="Screenshot_2024-01-29 13.50.00_orR9du" style="zoom:50%;" />

#### Downgrading attack 降级攻击

* Assume: Adversary can break one of the crypto systems
* Downgrading attack:
  + Adversary exchanges (undetected) the hybrid certificate(s) by standarad certificate(s)

&rarr; Security downgraded to security of single (broken) crypto system

**Backward compatibility & security downgrading**

* Backward compatibility - 4 scenarios to be covered:
  + 1. Both entities are not HC enabled
    2. Certificate holder is HC enabled, relying entity is not
    3. Relying entity is HC enabled, certificate holder is not
    4. Certificate holder and relying entity both are HC enabled
  + Scenario 1-3:
    + No downgrading senseful (single crypto system used anyway)
  + Scenario 4:
    + Adversary may pretend one of the other scenarios to apply a downgrading attack
    + Entities must be able to unambiguously distinguish between scenarios 1-3 and a potential downgrading attack

#### Downgrading attack prevention

1. Trusted list with hybrid and non-hybrid (only single key) trust anchors?

   <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 13.59.13_NQhPrC.jpg" alt="Screenshot_2024-01-29 13.59.13_NQhPrC" style="zoom:50%;" />

   Adversary may issue non-hybrid certificate chain starting from non-hybrid trust anchor

   &rarr; All trust anchors must be hybrid

2. Trust anchors hybrid - sufficient?

   <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 14.00.26_yaqaKi.jpg" alt="Screenshot_2024-01-29 14.00.26_yaqaKi" style="zoom:50%;" />

   Adversary may issue non-hybrid certificate chain starting from any non-hybrid CA

   &rarr; All subordinate CAs must be hybrid

3. Classical certificates for ent entities acceptable (to support scenario 1 + 3)?

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 14.01.33_fuAMNA.jpg" alt="Screenshot_2024-01-29 14.01.33_fuAMNA" style="zoom:50%;" />

​      Adversary may switch from hybrid to non-hybrid

​     &rarr; All end entity certificates must be signed with both keys of the parent certificate



#### Partially hybrid certificates for end entities

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 14.04.25_JbcUXD.jpg" alt="Screenshot_2024-01-29 14.04.25_JbcUXD" style="zoom:50%;" />

* Partially hybrid certificates (PHC) contain:
  + 1 key (as classical certificate)
  + 2 signatures
  + 2 different crypto systems used for signing
* Why needed?
  + Hybrid verification &rarr; can not be forged by adversary
  + Explicit statement by the CA, that subject does not support a second crypto system
  + Relying entity can distinguish valid scenarios from attacks





## 14. Time-Stamping 时间戳

**Time-Stamping Authority (TSA) 时间戳权威**

* supports assertions of proof that a datum existed before a particular time
* may be operated as a Trusted Third Party (TTP) service

**TSA requirements (RFC 3161)**

1. Use trustworthy source of time
2. Produce a time stamp toke upon receiving a valid request
3. In each time stamp token include:
   + trustworthy time valude
   + unique integer (serial number)
   + identifier for the security policy under which the token was created
4. Only time stamp a hash representation of the datum, i.e., a data imprint associated with a one-way collision resistant hash-function uniquely identified by an OID
5. Examine the OID of the hash-function and verify that the hash value length is consistent with the hash algorithm
6. Not to examine the imprint being time-stamped in any way
7. Not to include any identification of the requesting entity in the time stamp tokens
8. Sing time stamp tokens using a key reserved for this purpose
9. Include additional information in the time stamp token, if asked by the requester using the extensions field, only for the extensions that are supported by the TSA

**Structure of a time-stamping request**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 14.15.11_KaS26X.jpg" alt="Screenshot_2024-01-29 14.15.11_KaS26X" style="zoom:50%;" />

**Structure of a time-stamping response**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 14.15.52_DK7WQI.jpg" alt="Screenshot_2024-01-29 14.15.52_DK7WQI" style="zoom:50%;" />

**timeStampToken**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 14.16.30_39YDLP.jpg" alt="Screenshot_2024-01-29 14.16.30_39YDLP" style="zoom:50%;" />





## Alte Klausur

### SS2022

* Bennen Sie das Vertrauensmodell von PGP.

  —— Web of Trust

  

* Welches Gültigkeitsmodell wird in der Web PKI verwendet?

  —— Chain Model

  

* Nennen Sie die drei grundlegenden Komponenten eines Certificate Service Providers.

  —— RA (Rigistration Authority), CA (Certification Authoirty), DS (Directory Services)

  

* Nennen Sie zwei Standard-Erweiterungen, die für das Path Building verwendet werden, aber für die Path Validation unwichtig sind.

  —— Authority Information Access, CRL Distribution Points

  

* Welche zwei Dokumente geben Aufschluss über die für eine CA spezifizierten Sicherheitsrichtlinien und wie diese umgesetzt 把...付诸实施 werden?

  —— CP (Certificate policy): Die CP beschreibt welche Rithlinien sich die teilnehmende Person hält.

  ​        CPS (Certificate practice statement): Die CPS beschreibt wie in der CP festgelegten Anforderungen in der Praxis umgesetzt werden.

  

* Nennen Sie eine Art hybride Zertifikate zu erstellen, die Sie in der Vorlesung kennengelernt haben.

  —— Concatenation, Certificate encapsulation, Key-signatur encapsulation

  

* Sie haben in der Vorlesung die alternativen Revokationssysteme CRS und CRT kennengelernt. Nehmen Sie jeweils für CRS bzw. CRT an, dass das System 52 Woche verwendet werden soll und jede Woche der aktuelle Revokationsstatus veröffentlicht wird. Beantworten Sie die folgenden Fragen jeweils für CRS sowie für CRT. Kennzeichnen Sie eindeutig auf welches der beiden Verfahren sich die Antwort bezieht. (32<52<64)
  + Wie viel initiale Zufallswerte werden benötigt?

    —— CRS: 2, CRT: 65(64+1)

  + Bei Veröffentlichung des Zertifikats wird auch der Wert *Y* veröffentlicht. Dieser wird mittels einer Einwegfunktion *f* aus einem oder mehreren der initial gewählten Zufallswerte berechnet. Wie oft muss *f* angewendet werden, um *Y* zu berechnen?

    —— CRS: 1, CRT: [log^2^(60)] + 1 =7

  + Wie viel Werte werden pro Woche für die Verifikation veröffentlich?

    —— CRS: 1, CRT: 7
    
    

* Was ist die aktuelle Version bei X.509 Zertifikaten und was war die Neuerung beim Übergang zu dieser Version?

  —— Version 3. Es kamen die Erweiterung hinzu.



### SS2019

#### Verschiedenes

* Zeitstempel

  1. Was versteht man unter einem Zeitstempel (Timestamps)? 如何理解时间戳？

     —— Eine von einer vertrauenswürdigen Partei signierte Zeitangabe.  一个由受信任方签署的时间公告.

  2. Wozu verwendet man Zeitstempel-Ketten? 时间戳的作用？

     —— Gültigkeitserhat von Signaturen über lange Zetiräume, bspw. Bei der Archivierung. 长期保留签名的有效性，例如在归档期间.

  

* PKCS

  1. Wofür wird PKCS#10 verwendet?

     —— Certification Requests

  2. Wofür wird PKCS#12 verwendet?

     —— Sichere Speicherung privater Schlüssel 私钥的安全存储

  

* Alternative zum CA System

  1. Wie nennt man das System, bei dem Nutzer die Schlüssel anderer Nutzer signieren? 用户签署其他用户密钥的系统叫什么？

     —— PGP

  2. Bei diesem System werden mit jedem Schlüssel zwei Werte, die jeweils unterschiedliche Level haben können, assoziiert. Wie heißen diese beiden Werte?

     —— Owner Trust, Key Validity

  3. Wie nennt man die Datenstruktur, in der Nutzer die öffentlichen Schlüssel anderer Nutzer speichern? 用户存储其他用户公钥的数据结构叫什么？

     —— Public Keyring

  4. Wer ist in diesem System für die Revokation von Schlüsseln verantwortlich?

     —— der Schlüssel Eigentümer

  

* Alternativen zu CRLs

  1. Wie nennt man die Rovokationsmethode, bei der Clients den Revokationsstatus von Zertifikaten bei einem Server anfragen können? 客户端通过该方法可以查询服务器的证书吊销状态

     —— OCSP (Online Certificate Status Protocol) 在线证书状态协议

  2. Wie nennt man die Methode, bei der bspw. ein TLS Server sämtliche Revokationsinformationen zu seinen Zertifikaten direkt bei Verbindungsaufbau mitliefert? 例如，TLS服务器在建立连接时直接提供其证书的所有吊销信息

     —— OCSP Stapling

  3. Sie haben in der Vorlesung einen Revokationsmechanismus kennen gelernt, bei dem statt Revokationen explizite Gültigkeitstoken veröffentlich werden. 发布显式有效令牌而不是撤销. Welches kryptographische Primitiv wird als Basis für diesen Mechanismus verwendet? 使用哪种加密原语作为该机制的基础？

     —— Hash-Function (in RCS/CRT)

  

* Zertifikatsklassen

  1. Wie nennt man die Klasse von Zertifikaten, bei der eine besonders gründliche Überprüfung der antragsstellenden Organisation erfolgt? 对申请组织进行特别彻底检查的证书类别名称

     —— Extended Validation (EV) Zertifikate

  2. Was ist die zugehörige OID?

     —— 2.23.140.1.1



#### Hybride Zertifikate

* Bennen Sie zwei der drei Verfahren und beschreiben Sie stichpunktartig wie diese Verfahren funktionieren.

  1. Concatenation 级联

     —— Die beiden im Zertifikate enthaltenen Schlüssel, sowie die beiden Signaturen werden jeweils konkateniert.

  2. Certificate encapsulation 证书封装

     —— Ein komplettes Zertifikat enthält den zweiten Schlüssel, sowie die zweite Signatur, wird in eine spezielle Extension (hybridCert extension) geschrieben.

  3. Key-signature encapsulation 密钥签名封装

     —— Es werden zwei zusätzliche Extensions erstellt, hybridKey- and hybridSig extensions.

     hybridKey: enthält den zusätzlichen Schlüssel

     hybridSig: enthält die zusätzliche Signatur über das Zertifikat



* Abwärtskompatibilität (Backward Compatibility) 向下兼容. D.h.die hybriden Zertifikate können auch auf Legacy Systemen verwendet werden, die noch nicht für die Unterstützung von hybriden Zertifikaten vorbereitiet wurden.

  1. Welches der von Ihnen in a) benannten Verharen unterstützt Abwärtskompatibilität? Nennen Sie ein Verfahren.

     —— Certification encapsulation / Key-signature encapsulation

  2. Nenne Sie eine notwendige Bedingung, damit das genannte Verfahren Abwärtskompatibilität bietet. Begründen Sie Ihre Antwort.

     —— Die extension muss non-critical sein.



#### Hierarchical Trust, AKIE

* Können zwei unterschiedliche Zertifikate denselben Wert im keyIdentifier Feld in der AKIE haben, jedoch einen unterschiedlichen Wert im authorityCertIssuer Feld?

  —— Ja, wenn die Zertifikate von derselben CA mit demselben Schlüssel ausgestellt worden sind. Und die CA mehrere Zertifikate für diesen Schlüssel von unterschiedlichen Issuern hat.



#### CRLs

* Mit welcher Extension kann eine CA bekannt machen, dass sie Delta-CRLs ausgibt und wo man diese herunterladen kann? Wo ist diese Erweiterung überall zu finden?

  —— Freshest CRL (Delta CRL Distribution Point).
  
  ​         In Zertifikaten und Full-CRLs zu finden



* Geben Sie 3 weitere Arten von CRLs an, die Sie neben Full-, Base-, Delta-CRLs kennengelernt haben und geben Sie deren Haupt-Eigenschat an.

  —— over-issued CRLs: CRLs die öfter ausgegeben werden als durch "nextUpdate" erforderlich wäre.

  —— indirect CRL: der Issuer der CRL ist nicht der Issuer der enthaltenen Zertifikate.

  —— Segmented CRL: CRLs, die nur Zertifikate mit einem bestimmten Scope beinhalten.



### SS2018

#### Verschiedenes

* Definieren Sie kurz Public Key Zertifikate. Benennen Sie dabei den Hauptzweck und wie die Authentizität von Zertifikaten geschützt wird.

  —— Zertifikate sind datenstrukturen die einen öffentlichen Schlüssel an eine Identität/ Subject binden.

  ​        Zertifikate sind von einer vertrauenswürdigen Partei (CA) digital signiert.

  

* Benennen Sie 3 Vertrauensmodelle, die Sie in der Vorlesung kennengelernt haben.

  —— Direct Trust, Web of Trust, Hierarchical Trust

  

* Was ist die aktuelle Version bei X.509 Zertifikaten und was war die Neuerung beim Übergang zu dieser Version.

  —— Version 3. Es kamen die Erweiterungen hinzu.

  

* Nennen Sie die 2 Arten von Perosonal Security Environments, die zur Aufbewahrung von privaten Schlüsseln dienen können. 列出可用于存储私钥的2种个人安全环境 Nennen Sie jeweils ein Beispiel.

  —— Hardware PSE. Z.B., Smartcard

  ​         Software PSE. Z.B., PKCS#12

  

* Erklären Sie stichpunktartig, wie der Proof-of-Possession (PoP) für verschiedene Schlüsselarten durchgeführt wird

  + Signature key: Signieren einer Nonce, oder des Certificate Requests 签署随机数或证书请求
  + Encryption key: Entschlüsselung eines durch den CSP verschlüsselten Datums 对CSP加密的日期进行解密
  + Key-agreement key: Establishment of a shared secret key between CSP and entity



#### X.509 Extension

* Können zwei unterschiedliche Zertifikate den selben Key Identifier Wert in der SKIE haben? Begründen Sie ihre Antwort.

  —— Ja, das ist bei Zertifikaten die denselben Schlüssel haben der Fall.

  

* Welcher Extension kann man entnehmen:

  + Wo die zugehörige CRL (关联的CRL) zu finden ist?

    —— CRL Distribution Points

  + Wo/Wie der zuständige OCSP Responder zu erreichen ist?

    —— Authoirty Information Access



#### Zertifikatssperrung

OCSP

* Mit welcher Art von Architektur ist OCSP umgesetzt?

  —— Client-Server Architektur

  

* Nennen Sie die 3 möglichen OCSP Statusantworten.

  —— Good, Revoked, Unknown

  

* Wie kann eine CA einen OCSP Responder autorisieren, Revokationsinformationen für sie bereitzustellen? CA如何授权OCSP响应者向他们提供吊销信息

  —— Die CA gibt ein Zertifikat für den OCSP Responder aus, bei dem "OCSP Signing" in der Extended Key Usage Erweiterung enthalten ist.

  

* Erklären Sie kurz OCSP Stapling. Nennen Sie außerdem einen Vorteil von OCSP Stapling gegenüber herkömmlichem OCSP.

  —— TLS Extension die es dem Server erlaubt, beim Handshake OCSP responses für das Serverzertifkat und den Zertifizierungspfad mitzuschicken. TLS扩展，允许服务器在握手期间发送服务器证书和证书路径的OCSP响应

  —— Vorteil: Load-Reduzierung beim OCSP Server



#### Certificate Path Processing

* Benennen Sie die Zertifikatserweiterung mit der eine CA das PolicyMapping in nachfolgenden Zertifikaten unterbinden kann. CA可以使用该扩展来阻止后续证书中的策略映射.

  —— Policy Constraints

  

* Ein CA Zertifikat in einem Zertifizierungspfad beinhaltet die Inhibit anyPolicy Erweiterung mit dem Wert 2. Was bedeutet das für die Pfadvalidierung?

  —— Die anyPolicy darf noch in maximal 2 nachfolgenden Zertifikaten verarbeitet werden.



### SS2017

#### Gültigkeitsmodelle

**Kettenmodell**

* Um das Kettenmodell in der Praxis einsetzen zu können sei folgendes gegeben: Alle involvierten CAs sind vertrauenswürdig und Endentitäten fügen vor dem Signieren eines Dokuments immer eine Zeitangabe hinzu, die mitsigniert wird. Wozu wird diese Zeitangabe benötigt? 为了能够在实践中使用链模型，给出以下条件：所有涉及的CA都是值得信赖的，并且最终实体总是在签署文档之前添加时间指示，该文档也被签名。为什么需要这个时间信息？

  —— Eine Signatur enthält per se keine Zeitangabe. Ohne zusätzliche Zeitangabe kann nicht nachvollzogen werden, wann eine Signatur erstellt wurde und somit ist unklar zu welchem Zeitpunkt verrifiziert werden muss. 签名本身不包含时间指示。如果没有额外的时间信息，就无法确定签名的创建时间，因此不清楚需要在那个时间点进行验证

  

* Nehmen Sie nun an, ein Angreifer gelangt zum Zeitpunkt X in den Besitz des Schlüssels einer teilnehmenden CA. Wird die Verwendung des Kettenmodells dadurch (bei Zertifikatsketten die diese CA enthalten) unsicher, wenn alle angegebenen Signaturestellungsdaten vor Zeitpunkt X liegen? Begründen Sie ihre Antwort. 现在假设攻击者在时间X拥有参与CA的密钥。如果所有指定的签名创建日期都在时间X之前，这是否会使链模型的使用不安全？

  —— Ja. Da der Angreifer den Schlüssel hat, kann er beliebige Zertifikate, mit beliebigen Zeitabgaben (auch vor Datum X) erstellen. Der Verifizierer kann daher nicht sicher sein, ob ein Zertifikat tatsächlich vor der Kompromittierung von der CA erstellt, oder nach der Kompromittierung durch den Angreifer erstellt und rückdatiert wurde. 由于攻击者拥有密钥，因此它可以在任何时间（甚至在日期X之前）创建任何证书。因此，验证者无法确定证书实际上是由CA在泄露之前创建的，还是由攻击者在泄露之后创建并回溯的

  

* Nennen Sie zwei Möglichkeiten, die einen sicheren Einsatz des Kettenmodells trotz der Annahme möglicher Schlüsselkompromittierungen oder nicht vertrauenswürdiger Teilnehmer ermöglichen. 列出两种能够安全部署链模型的方法，尽管假设可能存在关键泄露或参与者不可信

  —— Verwendung vorwärtssicherer Signaturverfahren

  ​        Verwendung von Zeitstempeln durch vertrauenswürdige Dritte

  

* Nennen Sie ein Szenario, in dem das Kettenmodell verwendet werden kann, nicht jedoch das Schalenmodell.

  —— Jede Anwendung, bei der Signaturen auch nach Ablauf der Zertifikatsgültigkeit überprüfbar bleiben müssen. 即使在证书过期后签名也必须保持可验证的任何应用程序
  
  

**Web PKI**

* Welches Gültigkeitsmodell kommt in der Web PKI zum Einsatz?

  —— Chain Model

  

* Es stellt sich heraus, dass eine große CA, welche einige Millionen Serverzertifikate ausgegeben hat, nicht mehr vertrauenswürdig ist. Dieser CA kann jedoch nicht ohne Weiteres das Vertrauen entzogen werden (durch Revolution ihres Signaturschlüssels). Warum ist das der Fall? Unter welcher Bezeichnung ist dieses Problem bekannt? 事实证明，颁发了几百万张服务器证书的大型CA不再值得信任。然而，不能轻易的从该CA撤销信任（通过彻底改变其签名密钥），为什么会这样？这个问题的名称是什么？

  —— Die Revokation würde alle ausgegeben Serverzertifikate auf einen Schlag ungültig machen. Es wäre dann nicht mehr möglich zu den Servern eine sichere Verbindung aufzubauen. 撤销将使所有颁发的服务器证书一举失效，这样就无法再与服务器建立安全连接了

  ​        Too-big-to-fail Problem

  

* Wie kann das Problem aus (ii) ohne zusätzliche Infrastruktur verhindert werden? Benennen Sie eine notwendige Eigenschaft der verwendeten Signatureverfahren, das eingesetzte Gültigkeitsmodell und erläutern Sie kurz wie Revokation durchgeführt wird.

  —— Vorwärtssicherheit Signaturverfahren

  ​        Kombination aus Kettenmodell und Schalenmodell

  ​        Feingranulare Revokation, i.e. bei Revokation muss mitgeteilt werden, ab welchem Schlüsselindex revoziert wird.



#### Certificate Path Processing

* Wie nennt man es, wenn sich 2 CAs gegenseitig Zertifikate ausstellen?

  —— Cross-Certification

  

* Wie kann eine CA erreichen, dass eine ihr untergeordnete CA ausschließlich Zertifikate für Endentitäten, nicht aber für untergeordnete CAs ausstellen kann? CA如何确保其下属CA只能为最终实体颁发证书，而不能为下级CA颁发证书？

  —— Die CA setzt in der *Basic Constraints Extension* die pathLen = 0 



### SS2016

#### Gültigkeitsmodelle

* Kann man den in RFC5280 angegebenen Prüfalgorithmus zur Pfadvalidierung so verwenden, dass er nach dem Hybridmodell prüft? Wenn ja, wie? Wenn nein, begründen Sie Ihre Antwort. 是否可以使用RFC5280中规定的路径验证测试算法来根据混合模型进行测试？

  —— Ja, indem man dem Algorithmus bei Initialisierung anstelle der aktuellen Werte Datum/Zeit-Werte als Input übergibt, zu denen die Prüfung nach Hybridmodell durchgeführt werden soll. 通过在初始化期间将算法日期/时间值而不是当前值作为输入，应执行混合模型检查

  

* Es sollen Dokumentensignaturen archiviert werden. 文件签名应存档 Welches Gültigkeitsmodell muss angewandt werden, sodass eine Signaturprüfung auch in Zukunft zum Resultat gültig führt, insofern das zum Zeitpunkt der Archivierung der Fall war? Begründen Sie ihre Antwort.

  —— Hybridmodell oder Kettenmodell

  ​        Beide Modelle haben die Eigenschaft, dass einmal gültige Signaturen immer gültig bleiben, da der/die Verifikationszeitpunkte unabhängig vom Zeitpunkt der Durchführung der Verifikation sind.



#### Zertifikatssperrung

* Nennen Sie 2 Anforderung (Requirements) die bei der Zertifikatssperrung erfüllt sein müssen. Geben Sie genau 2 Lösungen an. Es werden nur die ersten 2 Lösungen gewertet. 列出证书吊销必须满足的2项要求

  —— Revokationsinformationen sind öffentlich verfügbar

  ​         Die Authentizität der Revokationsinformationen ist durch jedermann prüfbar

  

* Wer ist in einer hierarchischen PKI für Revokation und deren Veröffentlichung verantwortlich? Wer ist bei PGP dafür zuständig?

  —— Hierarchischen PKI: CAs

  ​         PGP: die Nutzer selbst

  

* Alice hat Bobs X.509 Zertifikat und möchte es auf Revokation prüfen. Wo im Zertifikat findet Alice die Addresse des zuständigen OCSP Responders, wo die URL für den Download der entsprechenden CRL? Alice在证书的哪个位置找到负责的OCSP响应者的地址？ 下载相应CRL的URL在哪里？

  —— OCSP Responder: in der Authoirty Information Access Extension

  ​        CRL Zugriffspunkte: in der CRL Distribution Points Extension

  

* Nennen Sie die 3 möglichen OCSP Status Antworten für ein Zertifikat und erklären Sie kurz deren Bedeutung

  —— Unknown, nothing known about the certificate

  ​         Revoked, certificate revoked or may not exist

  ​         Good, es liegen keine Revokationsinformationen zu diesem Zertifikat vor.

  

* Wie nennt man CRLs, die häufiger ausgegeben werden als das NextUpdat Datum es erfordern würde?

  —— Over-issued CRL

  

* Neben compelte CRLs und indirekten CRLs haben Sie auch delta CRLs kennen gelernt.

  + Wie erkennt man delta CRLs?

    —— an der Delta CRL Indicator Extension

  + Welchen Zweck hat die BaseCRLNumber?

    ——Die BaseCRL Number identifiziert diejenige complete CRL, whelche als Startpunkt für die Erzeugung der delta CRL verwendet wurde.

  + Was enthält eine delta CRL?

    —— Alle Revokationen, die seit der Ausgabe der Base CRL hinzugekommen sind.

  + Wenn man eine complet CRL hat, woran kann man erkennen, ob es auch delta CRLs von dieser CA gibt und wo man diese findet?

    —— Freshest CRL Extension (Delta Distribution Point Extension).

    ​        In Zertifikaten und Full-CRL zu finden.



### SS2015

* Welches Gültigketismodell kommt in RFC5280 zum Einsatz?

  —— Shell Model (SchalenModell)

  

* Erklären Sie kurz das Funktionsprinzip von OCSP Stapling. Nennen Sie 2 Vorteile gegenüber der herkömmlichen Verwendung von OCSP

  —— Beim OCSP Stapling sendet ein Web Server die entsprechenden Status Responses für seine Zertifikatskette direkt beim TLS Handshanke an den Client. 通过OCSP装订，Web服务器使用TLS Handshake将其证书链的响应状态响应直接发送到客户端

  ​         Vorteile: Die Privacy des Clients wird geschützt.

  ​                         Performanzverbesserung
  
  
  
* Welche zwei Möglichkeiten gibt es, den öffentlichen Schlüssel des Ausstellers eines Zertifikats A mithilfe von *Subject Key Identifier Extension (SKIE)* und *Authoirty Key Identifier Extension (AKIE)* zu finden?

  —— Erste Möglichkeit: Man sucht ein Zertifikate B, bei dem der keyIdentifier des SKIE mit dem keyIdentifier des AKIE von Zertifikat A übereinstimmt.

  

* Würde es ausreichen die keyUsage Extension von Bobs Zertifikat um Certificate Sign zu erweitern, damit Bob mit seinem Schlüssel Zertifikate ausstellen darf? Begründen Sie ihre Antwort. 将证书签名添加到Bob证书的keyUsage扩展中好是否足够，使得Bob可以使用他的密钥颁发证书？

  —— Nein. RFC5280 erfordert, dass CA Zertifikat zusätzlich die Basic Constraints Extension beinhalten.

  

* Wie funktioniert die Revokation in GPG? Ist es möglich einen Schlüssel zu revozieren wenn man seinen privaten Schlüssel verloren hat?

  —— Um einen PGP Schlüssel zu revozieren veröffentlicht man ein Revokationszertifikat. Das Revokationszertifikat wird mithilfe des privaten Schlüssels erstellt.

  ​        Sollte der private Schlüssel verloren gehen und man hat zuvor kein Revozierungszertifikat erstellt, oder ist dieses nicht mehr zugereifbar, kann man sein Zertifikat in PGP nicht revozieren.

  
  
* Wird der Owner Trust berechnet? Falls ja geben Sie die Berechnungsregel an. Falls nein, wie wird der Owner Trust bestimmt?

  —— Der Owner Trust wird nicht berechnet.

  ​        Es wird von der Person, welche den Keyring besitzt, gesetzt.




### SS2014

* Bei Hybrid- sowie beim Kettenmodell werden die Signaturerstellungszeitpunkte benötigt.

  + Nennen Sie eine Möglichkeit, diese auf sichere Art und Weise zu bestimmen.

    —— Zeitstempel durch vertrauenswürdige Dritte.

  + Warum ist eine durch den Signatureersteller eingebrachte Zeitangabe im allgemeinen nicht als sicher zu betrachten? 为什么签名创建者指定的时间通常被认为不安全？

    —— Würde ein Schlüssel in der Zukunft kompromittiert, so könnte der Angreifer (da er selbst signieren kann) beliebige Zeitangaben einbringen. Damit wäre es einem Angreifer möglich bspw. ein durch ihn signiertes Dokument auf einen Zeitpunkt vor der Revokation zurückzudatieren und es dadurch als gültig erscheinen zu lassen. 如果将来密钥被泄露，攻击者可以（因为他可以自己签名）输入任何时间信息。例如，这将允许攻击者将他签署的文档回溯到撤销之前的时间，从而使其看起来有效

    
