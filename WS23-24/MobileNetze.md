# Mobile Networking

## Chapter 04, Module 02

### DMG channel access mechanisms DMG通道访问机制

**Superframe 超帧 for 802.11**

A superframe contains:

* PCF
* DCF

**Directional multi-gigabit access in IEEE 802.11ad 定向多千兆位接入**

* Beacon Interval (BI) 信标间隔 &rarr; superframe of IEEE802.11ad
* Beacon transmission interval (BTI) 信标传输间隔
  + Used for a PCP or AP to transmit beacons to establish the beacon interval and access schedule, to synchronize the network, and to exchange access and capability information, as well as beam training
  + It is not necessary that all beacon intervals contain a BTI
* Association Beamforming Training (A-BFT) 协会波束成形培训
  + Beamforming training period reserved to train the PCPs or APs that transmitted a beacon during the BTI
  + It is also not necessarily present in beacon intervals
* Announcement Transmission Interval (ATI)  公告发送间隔
  + Request and response frames are exchange between the PCP/AP and the other STAs
  + All frame exchanges are initiated by the PCP/AP
  + It is also optionally present in the beacon interval
* Data Transfer Interval (DTI) 数据传输间隔
  + The most important period in the beacon interval for most STAs
  + Used for frame exchanges between all STAs
  + It can be subdivided into multiple iterations of two periods
    + Scheduled Service Period (SP) 预订服务周期
      + Each SP is assigned to a STA-to-STA link by the PCP or AP for high data rate transmission. Mutiple SP can coexist simultaneously 
    + Contention-Based Access Period (CBAP) 基于竞争的访问周期



### DMG CSMA/CA

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-24 21.21.48_wObG9T.jpg" alt="Screenshot_2024-01-24 21.21.48_wObG9T" style="zoom:50%;" />

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-24 21.22.19_8s0HDg.jpg" alt="Screenshot_2024-01-24 21.22.19_8s0HDg" style="zoom:50%;" />

* T1:
  + 1: STA A sends RTS to STA E
  + 1: STA B overhears this message and set the channel to busy
* T2:
  + 2: STA E respondes DMG CTS to STA A
  + 2: STA C overhears this message and set the channel to busy
* T3:
  + 3: STA F sends RTS to STA A &rarr; But STA A is busy
* T4: 
  + 4: Frames arrives for transmission but freeze transmission due to busy channel
* T5:
  + 5: STA D assumes channel free and transmit to STA B
* T6:
  + 6: STA B successfully receives the data and transmit ACK to STA D
  + 6: STA F doesn't receives DMG CTS from STA A &rarr; DIFS + Backoff
* T7:
  + 7: STA D backoffs after successful transmission
* T8:
  + 8: STA F sends RTS to STA A &rarr; But STA A is still busy
* T9:
  + 9: STA E successfully receives the data and transmit ACK to STA A
* T10:
  + 10: STA F doesn't receives DMG CTS from STA A &rarr; DIFS + Backoff (2*CW)
* T11:
  + 11: STA C sends RTS to STA B a DIFS time after the expiry of CS Busy



### Spatial Sharing Technique 空间共享技术

**Channel utilization and spatial reuse** 信道利用和空间复用

* A benefit of directional tramsmission and reception is the reduction in co-channel interference
  + In a distributed network, more transmit-receive pairs can communicate simultaneously

**Spatial sharing technique**

* Spatial sharing assessment phase 空间共享评估阶段
  + PCP/AP initiates radio resource measurement procedure with the intended STAs to assess the possibility to perform spatial sharing
  + The PCP/AP first transmits a directional channel quality request to STA C and STA D to perform channel measurement over SP1's channel allocation
  + Then, it transmits a directional channel quality request to STA A and STA B to measure over SP2's channel allocation
* Spatial sharing execution phase 空间共享执行阶段
  + Based on the channel measurement during the assessment phase, the PCP/AP estimates the channel quality and decides whether to implement spatial sharing



### Dynamic Channel Access 动态通道接入

* Also called dynamic allocation of service period
* Based on polling access scheme which is a master-slave protocol
* The AP (the master) polls each station (slaves) periodically for transmit requests
* Polling Period (PP) 轮询期
  + PCP/AP polls only those STAs that have indicated their intention to participate in the PP, and the polled device sends an SP request in ATI
* Grant Period (GP) 授予期
  + One or more Grant frames with the same resource allocation information are transmitted

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-24 21.45.05_SRCsbC.jpg" alt="Screenshot_2024-01-24 21.45.05_SRCsbC" style="zoom:50%;" />



### Clustering 聚类

* Distributed APs is favorable in mmWave communication to extend its coverage
* Dense deployment of APs results in high interference between spatial sharing co-channel APs
* Clustering feature allows co-channel APs to schedule their transmissions in non-overlapping time periods
* Scheduling information is obtained from the DMG beacons from the neighboring APs
* The AP decides its own transmission based on the schedule of the other APs
* Centralized clustering
  + a single centralized coordination service set exits
* Decentralized clustering
  + no central controller between the distributed PCPs/APs
  + one of the AP/PCP must act as synchronization S-PCP/S-AP, who has a unique ID (i.e., MAC address)
  + assuming 2 clusters scenario, the BI is divided into 2 Beacon SPs
  + Only one member can exclusively transmit during each SP while other stays in receive mode
  + Duration of SP = beacon interval length/2
  + The first beacon SP is reserved for S-PCP/S-AP



### Coverage Extension 覆盖范围扩展

**Relaying for coverage extension 中继以扩大覆盖范围**

* LOS communication is not always possible
  + Direct path is blocked by a wall or human
* mmWave links are susceptible to blockages
* an alternative propagation path using a relay is important: Multihop communications
* Relay is also used to break long hop links (low-rate) to multiple shorter hop links
* Spatial reuse and relay can be jointly exploited to obtain higher channel capacity
* Types of relays:
  + Half-duplex relay: either receive or transmit but not both at the same time
  + Full-duplex relay: the relay can listen/receive and retransmit at the same time



### Multiband Consideration 多频段考虑

* mmWave can provide higher rate, but it could not provide comparable coverage ad quality as microwave systems
  + Microwave: long range, moderate data rate
  + mmWave: short range, high data rate
* Multi-Band operation ensures that mmWave sysyems maintain the coverage and link quality of microwave systems
* A multi-band protocol uses mmWave for high data rates when available and otherweise falls back on lower data rate microwave links
* Challenge
  + Coordination for handover (fall back) is difficult





