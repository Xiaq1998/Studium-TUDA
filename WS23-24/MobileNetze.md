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



## Chapter 05, Module 01

### Bluetooth Introduction

**What is Bluetooth**

Bluetooth is a low-power, short-range wireless technology for WPAN (wireless personal area network)

**Application Scenarios**

* WPAN has a range less than 100m, typically ~10m
* Two types of communications, two protocols
  + Bluetooth Classic: Basic Rate / Enhanced Data Rate (BR / EDR) for continuous communication
  + Bluetooth Low Energy: Low Energy (LE) for bursty communication
* Three general application areas:
  + Real-Time voice and data transmissions
  + Cable replacement
  + Ad hoc and mesh networking

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-25 17.22.29_iWpAgm.jpg" alt="Screenshot_2024-01-25 17.22.29_iWpAgm" style="zoom:50%;" />



### Bluetooth Classic

**Physical layer specifications**

* RF band: 2.4 GHz ISM band, 2.402 - 2.480 GHz (Total bandwidth: 79 MHz)
* 79 RF channels, each taking 1 MHz
* Frequency hopping spread spectrum (FHSS) hops up to 1.6 kHz, each slot (=625us) may use a different RF channel
* Devices divided into 3 classes according to TX output power
  + Class 1: Max 20 dBm (100 mW) - typical 100m LOS range
  + Class 2: Max 4 dBm (2.5 mW) - typical 10m LOS range
  + Class 3: Max 0 dBm (1 mW) - typical 1m LOS range
* Modulation
  + Both BR and EDR has symbol rate of 1 Msym/s
  + Basic Rate: GFSK (data rate = 1 Mbps)
  + Enhanced Data Rate: /4-DQPSK (data rate = 2 Mbps), 8DPSK (data rate = 3 Mbps)



####Piconet 微微网

**Piconet:** The basic unit of networking in Bluetooth classic is a piconet.

* A piconet has one master and up to seven slaves
  + slaves can only transmit when requested by master
* Up to 255 parked slaves
  + Each station gets an 8-bit parked address
* Bi-directional communication between master and slave
* Master determines the frequency hopping sequence (FHS) and clock that are used by all devices in a piconet
* Both FHS and master's clock are used for communication scheduling
* Slaves are polled by the master for transmission
* Communication uses a TDMA scheme

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-25 17.46.25_D5zRvu.jpg" alt="Screenshot_2024-01-25 17.46.25_D5zRvu" style="zoom:50%;" />

* A slave has a 3-bit logical transport address (LT_ADDR)
* A stand-by device does not need an LT_ADDR, as it does not communicate with anyone
* A piconet is active on **1 RF channel at a time**
* Multiple co-existing piconets share the 79 RF channels, which increases the total throughput
* Collison can occur if two or more piconets use the same RF channel at the same time. Retransmission and FEC (forward error correction) can fix the rare collisions
* A scatternet consists of two or more interconnected piconets
* Communication among more than & devices is possible
* A bridge node joins more than one piconets
* A bridge node can be active in one piconet at a time
* Timeshare and must synchronize to the master of the current piconet

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-25 20.20.28_cH12pl.jpg" alt="Screenshot_2024-01-25 20.20.28_cH12pl" style="zoom:50%;" />



#### Frequency Hopping (FH) 跳频

* Each piconet has a unique pseudo-random hopping sequence through all 79 RF channels
* The channel index is computed by a deterministic algorithm with the inputs of master's clock and master's address
* Piconet communication is a FH-TDMA scheme
  + Different piconets use different hopping sequence for communication (FHMA)
  + In a single piconet, the master and slaves transmit in different time slots (TDMA)
* TDMA polling scheme: master starts transmission only in **even slots 偶数时隙**, Slaves starts transmission only in **odd slots 奇数时隙**
* Packets can be 1, 3 or 5 slots long
* The frequency hopping stops during a packet transmission; esay implementation for the transitivers
* Advantages of frequency hopping:
  + Resistant to narrow-band interference
  + Co-existence with other wireless communication in the same band



#### Adaptive Frequency Hopping (AFH) 自适应跳频

* 2.4 GHz ISM band is license-free, therefore very noisy 
  + WiFi, Zigbee, cordless phones and even microwave oven works in this band
* Adaptive Frequency Hopping (AFH) appeared in Bluetooth v1.2 to avoid static interference in WLAN and similar environment
* Further improve communication reliability
* Each channel is labelled as "good" or "bad"
* A master determines the AFH channel map, which contains the binary channel classification
* The number of good channels is at least 20 and at most 79
* A pair of transmissions slots use the same channel
* Frequency hops with half the rate of non-adaptive frequency hopping
* Master determines "AFH channel map" based on (1) local measurement, (2) channel classification specified by the host or (3) reported by slaves



#### Logical links

 Three types of logical links can be established between a master and a slave for transmitting user data

* SCO (Synchronous Connection-Oriented) 同步面向连接: reservation-based access
* eSCO (Extended Synchronous Connection-Oriented) 扩展同步面向连接: reservation-based access
* ACL (Asynchronous Connection-Less) 异步无连接: polling-based access

**SCO**

* Periodic single slot packet assignment.
* Slot reservation (two consecutive slots M &rarr; S, S &rarr; M) at fixed interval, point-to-point link between a master and a slave.
* No retransmission
* **eSCO:**
  + Extends SCO, allow asymmetric transport and retransmissions
* SCO and eSCO are used for data that requires guaranteed delay, but can tolerate packet loss. Typically the dat is also periodic

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-25 22.18.43_60vRbt.jpg" alt="Screenshot_2024-01-25 22.18.43_60vRbt" style="zoom:50%;" />

**ACL**

* Asymmetric bandwidth for variable packet size (1, 3, 5 slots) connectionless packet transmission
* Point-to-multipoint link between a master and all slaves in a piconet
* Unicast ACL packets (M &rarr; S, S &rarr; M) should be ACKed
* Broadcast packets (M &rarr; S) should not be ACKed
* No slot reservation is possible
  + Can not transmit in slots taken by SCO and eSCO
* Retransmission allowed
* ACL is used for data that requires guaranteed reliability, but can tolerate delay; typically the data is also intermittent
* E.g. file transfer, control packets and broadcast packets

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-25 22.23.51_XZ67uT.jpg" alt="Screenshot_2024-01-25 22.23.51_XZ67uT" style="zoom:50%;" />



####Bluetooth Classic Link Layer State Machine

**Operational States:**

* **Standby:** default mode, a device has not joined a piconet
* **Inquiry:** master scans for slave devices, slave responds with its address and clock after a random delay
* **Page:** master invites slaves to join the piconet, slave responds with its device access code
* **Connected:** successful connection between master and slave, slave is assigned the 3-bit address (LT_ADDR)
* **Transmit:** data transmission between master and slave

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-25 22.53.26_thTdc7.jpg" alt="Screenshot_2024-01-25 22.53.26_thTdc7" style="zoom:50%;" />

**Bluetooth Low Power Modes**

* HOLD: low-power mode
  + Slave has no ACL transport, continue with reserved SCO and eSCO transports
  + Slave can do other things like: scanning, paging, inquiring, or attending to the other piconets, or simply sleeping
  + The slave unit keeps its active member address (i.e., LT_ADDR)
  + Before entering Hold mode,the master and slave agree on the time duration for the hold period

* SNIFF: low-power mode
  + Sniff mode frees a slave for predetermined, recurring, fixed time periods
  + Slave listens during D-sniff before fixed sniff intervals (T-sniff)
  + Node can do other things like: scanning, paging, inquiring, or attending to the other piconets, or simply sleeping
  + The slave unit keeps its active member address (i.e., LT_ADDR)

* PARK: very low-power mode
  + Slave give up its 3-bit active member address (i.e., LT_ADDR) and gets an 8-bit parked member address (PMA)
  + Wake up periodically (with some reconnection overhead) and listen to beacons
  + Master broadcasts a train of beacons peroidically
  + The beacon period is communicated to the slave when it is being parked; it can be changed at a beacon interval



### Bluetooth Low-energy

**BLE: Overview**

* Very low energy: a button cell battery lasts for a few years or energy harvesting is enough
* Low throughput: huge number of sensors in smart home and smart factory. Periodically or event-based very small packets (e.g., window open/close, temperature, heart rate)
* Very simple devices: 

### Bluetooth Mesh



