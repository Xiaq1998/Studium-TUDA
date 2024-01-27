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

* CN        Common Name
* L            Locality
* ST          State or Province
* O           Organization
* OU        Organization Unit
* C            Country
* Street    Street Address
* DC         Domain Component
* UID       User Id

#### X.509 extensions

**(non-) critical extensions**

* Extensions are either marked critical or non-critical
* Criticality affects evaluation by the client

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-17 11.59.38_svnXgL.jpg" alt="Screenshot_2024-01-17 11.59.38_svnXgL" style="zoom:50%;" />

**Subject Key Identifier (SKI) 主题密钥标识符**

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

**Correlation 相关性 of SKIE - AKIE**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-19 15.07.54_LICLre.jpg" alt="Screenshot_2024-01-19 15.07.54_LICLre" style="zoom:50%;" />

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

​    Assume two entities, e.g. a client and a server,

​    During transition phase, hybrid certificates should still work if:

* The (legacy) server does not understand "Hybrid"
* The (legacy) client does not understand "Hybrid"
* Both entities do not understand "Hybrid"

Then: hybrid certificates should appear as common X.509 certificates

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

We can trust, that an entity is who it pretends to be & that the used keys/crypto are secure,

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
* Step 3: Retrieve correct signature key
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

Abortive ending of the binding between:

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
* The CRL (Full CRL) contains information about all revoked certificates

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

* Monotonically increasing sequence number
* **Non-critical** extensions, ==must be included in all CRLs==
* To determine when a particular CRL supersedes another CRL
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

* Format like a "normal" CRL + Delta CRL Indicator extension
* Contains ALL changes since Base CRL was issued
* Associated to Base CRL by the BaseCRLNumber

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
* A complete and a Delta CRL issued at the same time must have same CRL number and provide same revocation information

**Delta CRL Indicator** 

* Critical extension
* Identifies a CRL as being a Delta CRL
* Contains a single value called **BaseCRLNumber**
* The BaseCRLNumber identifies the CRL used as the starting point in the generation of the Delta CRL
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
  + Good means that the certificate is not revoked, but it may be expired or even not exist at all

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
* Servers can cahce OCSP responses and reuse them (until nextUpdate time)

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
* Randomly generate 2^Y^ numbers as leaves of a binary tree
* Build a hash-tree
* Put the value of the root node into the certificate (replacing Y~365~ from Micali's system)
* On a day i, release the values of the path from leaf node i and all nodes on the path needed to compute the root

**Effect**

* O(log(#leaves)) hash values have to be released each day, so updates are a little worse than original Micali, but not much
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

**Forward search**

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
* Note: A certificaste must not appear more than once in a prospective certification path
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

1. Determine the set of policy nodes whose parent nodes have a valid_policy of anyPolicy

   <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 22.57.29_5yww1c.jpg" alt="Screenshot_2024-01-27 22.57.29_5yww1c" style="zoom:50%;" />

2. If the valid_policy of any node in the valid_policy_node_set is not in the user_initial_policy_set and is not anyPolicy, delete this node and all its children

   <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-27 22.59.28_aFh6GG.jpg" alt="Screenshot_2024-01-27 22.59.28_aFh6GG" style="zoom:50%;" />

3. If the valid_policy_tree includes a node of depth n with the valid_policy anyPolicy and the user_initial_policy_set is not anyPolicy, perform the following steps:

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



## 14. Time-Stamping









