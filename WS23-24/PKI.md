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



