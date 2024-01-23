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

### CRS/CRT

### Revocation in PGP

