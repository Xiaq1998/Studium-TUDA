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
* Very simple devices: must be low cost due to large quantity. Talk simple prtocols with gateways. Star topology, no scatternets or mesh
* Lower cost than Bluetooth classic
* Bluetooth low-energy (BLE) is designed for ultra-low power WPAN communication. Based on Nokia's WiBree
* Currently lot's of devices (e.g., all new smartphones) are equipped with dual-mode chips (Bluetooth classic and BLE)

**Physical Layer**

* RF band: 2.4 GHz ISM band (same as Bluetooth classic)
* Range: 150m in open field
* 40 RF channels, two neighboring channels separated by 2 MHz
* Adaptive frequency hopping
  + 3 channels reserved for advertising
  + 37 channels reserved for data communication
* TX output power
  + Class 1: Max 20 dBm (100 mW)
  + Class 1.5: Max 10 dBm (10 mW)
  + Class 2: Max 4 dBm (2.5 mW)
  + Class 3: Max 0 dBm (1 mW)
* Modulation: GFSK
  + symbol rate = 1 Msps, data rate = 1 Mbps
  + symbol rate = 2 Msps, data rate = 2 Mbps

**Network Topology**

* BLE uses the same idea of piconet as Bluetooth classic
* But
  + There is no limit on the number of slaves
  + A slave can only belong to one Piconet

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 16.26.41_NsESyd.jpg" alt="Screenshot_2024-01-29 16.26.41_NsESyd" style="zoom:50%;" />

**Frequency Hopping**

* Channels are divided into two types: advertising channels and data channels
  + 3 advertising channels for advertising packets
    + Channle #37, #38 and #39
    + Strategically chosen to avoid interference with WiFi
  + 37 data channels for data packets
    + Channel #0 to #36

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 16.28.43_XnRoxA.jpg" alt="Screenshot_2024-01-29 16.28.43_XnRoxA" style="zoom:50%;" />

* Simple frequency hopping algorithm in a data connection
  + ==f(n + 1) = [f(n) + hop] mod 37==
    + f(n) = the current channel id
    + f(n + 1)= the next channel id
    + hop = a value between 5 and 16 randomly chosen by the master
* Different from Bluetooth classic where a master share the same hopping sequence with all its slaves in BLE, each master-slave pair has a unique frequency hopping sequence
* For a master-slave pair, channel hopping happens at each connection event
  + A connection event is the start of a group of packets that are sent from master to slave and back again

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 16.33.05_30B1uo.jpg" alt="Screenshot_2024-01-29 16.33.05_30B1uo" style="zoom:50%;" />

**Adaptive Frequency Hopping (AFH)**

* Same idea as the AFH for Bluetooth classic
* Channel map determined by the master
* AFH may use at least 2 and at most 37 channels
* Channel map can be changed during connection
* Example:
  + Channel. Map: 00000000 01100000 00000111 00000000 01111 (left to right, channel #0 to channel #36)
  + Array of good channels: Good = [9, 10, 21, 22, 23, 33, 34, 35, 36]
  + Number of good channels: N = 9
  + Channel hopping formula: ==f(n + 1) = [f(n) + hop] mod 37, f(0) = 0, hop = 7==
  + The first connection event on f(1) = (0 + 7) mod 37 = 7
  + &rarr; #7 is a bad channel. Remap to Good[7 mod N] = Good[7 mod 9] = Good[7] = 35
  + The second connection event on f(2) = (7 + 7) mod 37 = 14
  + &rarr; #14 is again a bad channel. Remap to Good[14 mod N] = Good[14 mod 9] = Good[5] = 33
  + The third connection event on f(3) = (14 + 7) mod 37 = 21
  + &rarr; #21 is a good channel

**Link Layer State Machine**

* Standby:
  + default state after power on
* Advertising:
  + transmit advertising packets
  + advertising if a device wants to be discovered, to be connected to, or to broadcast data
* Scanning:
  + master scans who are advertising
  + Passive scanning: just scan, does not transmit
  + Active scanning: to obtain more information; after discover a new advertising device, send a scan request to it, and expect a scan response
  + Scan request and scan response packets are transmitted on the advertising channels
* Initiating:
  + master listens for the device that it is attempting to connect to
  + after receiving the advertising packet from the device, master sends a connect request (CONNECT_REQ)
* Connected:
  + in this state, data packets are exchanged between two devices
  + data packets are transmitted on the data channels
    + Master enters connected from initiating
    + Slave enters connected from advertising

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 16.48.41_DC6w3M.jpg" alt="Screenshot_2024-01-29 16.48.41_DC6w3M" style="zoom:50%;" />

**Typical Connection Lifecycle**

A link can be terminated by either master or slave

* ADV_IND
  + advertise that it can be connected to
* CONNECT_REQ
  + request to connect to a slave
* LL_TERMINATE_IND
  + send a terminate indication packet
* LL_ACK
  + an empty ack packet

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 16.50.54_MNW8ym.jpg" alt="Screenshot_2024-01-29 16.50.54_MNW8ym" style="zoom:50%;" />

**BLE Packet Format**

* Preamble: Used by receiver for time and frequency synchronization and to perform automatic gain control (AGC) 自动增益控制
  + Advertising packet: 10101010
  + Data packet: either 10101010 (if LSB of access address is 0), or 01010101 (if LSB of access address is 1)
* Access Address (4 Bytes = 32bits)
* CRC (24-bit): Used for error detection of the packet

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 16.54.05_WIPRlj.jpg" alt="Screenshot_2024-01-29 16.54.05_WIPRlj" style="zoom:50%;" />

**Low Power Potimizations in BLE**

* Short packets:
  + a packet transmission takes at most 376 us. Will not heat up the silicon
  + therefore no need to compensate the carrier frequency drift
* Low overhead in packets:
  + 10 bytes of overhead for unencrypted packets and 14 for encrypted packets
* Delayed and poggybacked acknowledgements:
  + wait to ack until it has data to send
* Single-channle connection event:
  + stay on the same channel for the whole connection event instead of hopping in every slot as in Bluetooth classic;
  + stay longer on a good channel improves packet reliability
* Substrate wakeup
  + if a slave wants to have low latency to master, it needs to be polled often
  + if the slave wants to have high energy efficiency at the same time, it needs to ignore pollings
    + saving slave's energy at the cost of master



### Bluetooth Mesh 蓝牙网状网络

**Introduction to Bluetooth Mesh**

* Bluetooth Mesh Networking is standardized in July, 2017
* It enables many-to-many communication, ideal for IoT applications
* Mesh is a networking technology, and it is based on BLE
* Advantages
  + Multi-hop communication covers much larger area
  + Provide resilience in communication (no single point of failure)
  + Potential of being supported by smartphones, tablets and PCs, which is lacking by other mesh technology (e.g., Zigbee)
* Application scenario: monitoring and control systems, e.g., lighting control in smart buildings

**Publish and Subscribe**

* Bluetooth mesh uses the publish/subscribe messaging system
* Publishing:
  + the act of sending messages to specific addresses
* Subscribing:
  + configure nodes to process messages sent to specific addresses
* A node may subscribe to multiple addresses
* Multiple nodes may publish/subscribe to a single address
* Advantage of using group and virtual addresses with the publish/subscribe communication model:
  + removing and adding new nodes to the network do not require reconfiguration of other nodes
* Example:

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 17.11.11_0auPaf.jpg" alt="Screenshot_2024-01-29 17.11.11_0auPaf" style="zoom:50%;" />

**Features**

* 4 optional features for a node
  + Relay: capable of retransmitting received packets
  + Proxy: acts as interface to mesh network for BLE devices not talking mesh protocol
  + Friend: buffers messages to the low power node (LPN), delivers them when polled by the LPN, typically power-unconstrained nodes
  + Low Power: polls Friend infrequently to receive messages typically power-constrained nodes running on cell battery
* Friend and low-power features work together for power saving
* However, receiving aperipdic messages immediately requires turning on the radio all the time

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 17.15.07_wWwzgJ.jpg" alt="Screenshot_2024-01-29 17.15.07_wWwzgJ" style="zoom:50%;" />

**Mesh Communication**

* Bluetooth mesh only uses the advertising/scanning states of BLE
* Bluetooth mesh uses **flooding** to deliver messages
  + Published messages are broadcast rather than routed directedly to one or more nodes
  + Nodes may rebroadcast (rely) received messages
* Advantages of flooding:
  + Messages arrive at destination via multiple paths, resilient to topology change and node failure
  + No need for routing protocols, which incurs large overhead especially for large networks
  + Better use of the broadcast nature of wireless communication
* Disadvanteages of flooding:
  + Potential of redundant transmissions, so-called broadcast storm
* How to overcome this problem?
  + &rarr; Managed Flooding
  + Heartbeat messages
    + Flooded by nodes periodically
    + Indicate that the source is still alive
    + Used to measure the distance to the source; the distance can be used to set TTL for other messages
  + TTL (time to live) field
    + Mesh PDU includes the TTL field
    + Set as the max number of hops that a message is to be relayed
    + Limit the range of relaying
  + Message cache
    + Cache contains recently heard messages to avoid rebroadcasting
    + If find a message is cache, discard immediately (limit number of transmissions)



## Chapter 05, Module 02

### WPAN Overview

**Design Requirements**

* Battery power: Maximize battery life. A few hours to a few years on a coin cell
* Dynamic topologies: Short duration connections and then device is turned off/goes to sleep
* No infrastrucuture
* Interference avoidance capability: due to higer powered LAN devices
* Simple and extreme interoperability: among billions of devices
* Low cost: a few euros

**802.15.4 Overview**

* 2.4 GHz PHY (2400 - 2483.5 MHz ISM band)
* Data rate: 250 kbps PHY rate
* 16 5-MHz channels (#11 to #26)
* Every 4 data bits are grouped into a symbol (4 nits per symbol)
* DSSS (direct sequence spread spectrum): each symbol (16 possibilities) is mapped to a 32 chip sequence (Pseudo Noise code)
* The chips are Offset QPSK (OQPSK) modulated
* TX power at least -3 dBm (0.5 nW)
  + lower rate, short distance &rarr; lower power &rarr; low energy
* Similar to 802.11: CSMA/CA, Backoff, Beacon, Coordinator (similar to Access point)



### IEEE 802.15.4 PHY

**Direct Sequence Spread Spectrum (DSSS) 直接序列扩频**

* DSSS maps a message symbol into a PN (pseudo noise) chip sequence
* Advantages:
  + very low energy consumption
  + correct chip errors &rarr; robust against interference (time domain)
  + increase bandwidth &rarr; robust to narrow-band interference (frequency domain)
  + coexist with other wireless communications (e.g., Bluetooth, WiFi)
  + line of sight is not required. Pass through walls
  + low cost chips
* Disadvantages:
  + low data rate in terms of the used bandwidth

**PHY Frame Format**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-30 22.38.55_VOdQcA.jpg" alt="Screenshot_2024-01-30 22.38.55_VOdQcA" style="zoom:50%;" />

* Preamble: 4 bytes of 0x00.
  + Synchronize the receiver
* SFD (start-of-frame delimiter): 0x47. 
  + Indicate the start of the frame
* PHY Header: the total number of bytes in PSDU
  + How much btyes to receive in the following frame
* PSDU: data payload



### IEEE 803.15.4 MAC

**Device Classes**

* Network type: Star, and peer-to-peer (mesh, cluster tree)
* PAN Coordinator 个人区域网协调员: a coordinator that is the principle controller of a PAN
* Coordinator: a node that provides coordination and other services to the network
* Full Function Device (FFD) 全功能装置: a device that can become a coordinator if it starts a PAN. An FFD can talk to any other node
* Reduced Function Device (RFD) 减少功能装置: a device that can not become a coordinator. A RFD can only talk to FFD or coordinator
* Each PAN has exactly one PAN coordinator, and zero or more other device

**Cluster Tree Network**

* **Cluster tree 聚类树** is one type of peer-to-peer topology
* A PAN coordinator instructs an FFD to become the PAN coordinator of a new cluster (PAN) adjacent to it
* Cluster tree grows like a tree &rarr; no loops
* Each piconet (cluster) has a unique PAN ID

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-31 00.28.01_HeOIxK.jpg" alt="Screenshot_2024-01-31 00.28.01_HeOIxK" style="zoom:50%;" />

**Device Addressing**

* There are two types of addresses:
  + Extended address
    + Typically set by manufacturer
    + Each device has a unique extended address which is a 64-bit extended universal identifier (EUI-64)
  + Short address
    + A device has a 16-bit short address that is unique in the PAN
    + Short address saves frame size
      + Addressing field is in the PSDU (0, 2, or 8 bytes)
* If a device is the PAN coordinator, its short address is chosen before the PAN starts
* If a device is not the PAN coordinator, the short address is assigned by a coordinator during association
* Both the extended address and the short address can be used for communication

**MAC Frame Format**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-31 00.37.24_j2H7Ir.jpg" alt="Screenshot_2024-01-31 00.37.24_j2H7Ir" style="zoom:50%;" />

**Superframe structure**

MAC supports two modes: Beacon-enabled mode & non-beacon modes

* Beacon-enabled CSMA/CA
  + Coordinator sends beacons periodically
    + To synchronize nodes, identify PAN, and describe superframes structure
  + The active portion consists of 16 equally sized slots
    + CAP (contention access period): any node can use slotted CSMA/CA to access the channel
    + CFP (contention free period): one or more GTS (guranteed time slots)
  + In inactive Portion, everyone sleeps

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-31 00.45.31_pQNHll.jpg" alt="Screenshot_2024-01-31 00.45.31_pQNHll" style="zoom:50%;" />

* Non-beacon-enabled (beaconless) CSMA/CA mode (used by ZigBee)
  + The coordinators do not send beacons, therefore there is no superframe structure
  + No back-off slot alignment is necessary
  + Use unslotted CSMA/CA to access the channel
  + The random back-off period in both slotted and unslotted CSMA/CA is an integer multiple of the unit back-off period

**The Inter-frame Spacing**

* Acknowledgements if requested by the sender
* Short inter-frame spacing (SIFS) if previous transmission is shorter than a specified duration, otherwise, long inter-frame spacing (LIFS)

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-31 00.50.32_Mzj9YB.jpg" alt="Screenshot_2024-01-31 00.50.32_Mzj9YB" style="zoom:50%;" />

**IEEE 802.15.4 CSMA-CA Protocol (ZigBee): Unslotted**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-31 00.51.27_HF5cQR.jpg" alt="Screenshot_2024-01-31 00.51.27_HF5cQR" style="zoom:50%;" />

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-31 00.52.57_hQRhvy.jpg" alt="Screenshot_2024-01-31 00.52.57_hQRhvy" style="zoom:50%;" />



### ZigBee

 #### ZigBee Overview

* ZigBee is an ultra-low power, low data rate, short-range (1 to 100 m) WPAN's technology
* ZigBee is mainly designed for communication in monitoring and control applications (ZigBee and BLE are competitors)
* ZigBee allows running applications on two AA batteries for years (research shows that BLE is even more energy-saving)
* ZigBee supports multi-hop communication (so is Bluetooth mesh)
* ZigBee builds on a subset of the IEEE 802.15.4 PHY and MAC (non-beacon-enabled PANs), and adds upper layer functionalities
* ZigBee standardization is managed by ZigBee Alliance. The first standard came out in 2004
* ZigBee supports up to 254 devices or ^~^65000 simpler nodes
* Multi-hop ad-hoc mesh network
  + Multi-Hop Routing: message to non-adjacent nodes
  + Ad-hoc Topology: no fixed topology. Nodes discover each other
  + Mesh Routing: end-nodes help route messages for others
  + Mesh Topology: loops are possible
* Tri-Band:
  + 16 channels at 250kbps in 2.4GHz ISM
  + 10 channels at 40kbps in 915 MHz ISM band (Americas)
  + 1 channel at 20kbps in European 868 MHz band, 920 MHz in Japan
* ZigBee Application Profiles
  + Smart energy
    + electrical, gas, water meter reading
  + Commercial building automation
    + Smoke detectors, lights
  + Home automation
    + remote control lighting, heating, doors
  + Personal, home, and hospital care (PHHC)
    + Monitor blood pressure, heart rate
  + Telecom applications
    + mobile phones
  + Industrial process monitoring and control
    + temperature, pressure, position (RFID)

**ZigBee Topologies & Device Classes**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-31 18.02.25_cz4qyW.jpg" alt="Screenshot_2024-01-31 18.02.25_cz4qyW" style="zoom:50%;" />

* ZigBee Coordinator (ZC)
  + Selects channel, starts the network, assigns short addresses to other nodes
* ZigBee Router (ZR)
  + Nodes that can route packets to/from other nodes
* ZigBee End-Device (ZED)
  + Can sleep to extend battery life, not capable of being a coordinator or a router, leaf node



#### ZigBee Address Assignment

* Each node gets a unique 16-bit address
* Two schemes
  + Distributed scheme
    + Called Cskip address assignment
    + Good for tree structure
    + Each child is allocated a sub-range of address
    + Need to limit
      + **L~m~ (maximum tree depth)**: MaxDepth
        + If MaxDepth = 6, it is not possible to fit it in 16-bit space
      + **C~m~ (maximun number of children per node)**: MaxChildren
      + **R~m~ (maximum number of router children per parent node)**: MaxRouters
  + Stochastic scheme
    + Parent draws a 16 bit random number between 0 and 2 ^16^-1, a new number is drawn if the result is all-zero (null) or all-one (broadcast)
    + Parent then advertises (broadcasts) the number to the network 4 times
      + If another node has the same address, an address conflict message is returned and the parent draws another number and repeats until no conflict
    + There is no limit for the number of children, router, or depth

**Hierarchical (Tree) Topology**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-31 18.15.49_7fcWwR.jpg" alt="Screenshot_2024-01-31 18.15.49_7fcWwR" style="zoom:50%;" />

**Cskip Address: Example**

* Parameters: 
  + L~m~ = 3 (MaxDepth)]
  + C~m~ = 5 (MaxChildren)
  + R~m~ = 3 (MaxRouter)
* Calculate Cskip (child skip) at each level:

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-31 18.18.14_exVnpS.jpg" alt="Screenshot_2024-01-31 18.18.14_exVnpS" style="zoom:50%;" />

* Two ways of computing Cskip:

  + Method 1: resursively computed from high lever to low level
    $$
    Cskip(n-1)=(Cskip(n)-1)\cdot R~m~+C~m~+1
    $$

    + At level MaxDepth, node has no children, thus **Cskip(3) = 0**
    + At level MaxDepth - 1, node has only leaf children, thus **Cskip(2) = 1**
    + For our problem,
      + Cskip(3) = 0
      + Cskip(2) = 1
      + Cskip(1) = (Cskip(2) - 1)*3 + 5 + 1 = 6
      + Cskip(0) = (Cskip(1) - 1)*3 + 5 + 1 = 21

  + Method 2: computed for any level

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-31 19.25.36_xj0KVq.jpg" alt="Screenshot_2024-01-31 19.25.36_xj0KVq" style="zoom:50%;" />

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-31 20.12.32_4IHSX8.jpg" alt="Screenshot_2024-01-31 20.12.32_4IHSX8" style="zoom:50%;" />

* Address is assigned from low level to high level

* Let *Y* be the i^th^ router child of *X*, *Z* be the j^th^ end-device child of *X*, where (*i*,*j* >= 1):

  + Coordinator: Addr(ZC) = 0
  + Router: Addr(Y) = Addr(X) + (i - 1) * Cskip(level(X)) + 1
  + End-device: Addr(Z) = Addr(X) + MaxRouter * Cskip(level(x)) + j

* The coordinator address is 0 (decimal)

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-31 20.18.20_JLu79o.jpg" alt="Screenshot_2024-01-31 20.18.20_JLu79o" style="zoom:50%;" />

Addr(Y~1~) = Addr(X) + (i - 1) * Cskip(level(X)) + 1

​               = 0 + (1 - 1) * 21 + 1

​               = 1

**Distributed Scheme: Pros & Cons**

* Advantage of Cskip
  + A node can tell from the address whether it is a descendant or not (address implies topology, helpful for routing)
  + Address is guaranteed conflict-free
* Disadvantage of Cskip
  + Does not support a tree with depth larger than 5

#### ZigBee Routing

**ZigBee supports 4 types of routing**

* Broadcast

  + Broadcast is one-to-many communication

  + Broadcast protocol

    + The initiator sets the destination address (dest addr) and radius (same as TTL)
    + If a receiver has seen the packet before, it drops the packet
    + Otherwise, the receiver indicates the packet reception to the upper layer, then it decrements radius
    + If radius > 0 and the device is not ZED, then retransmit

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-31 20.29.02_KL64Gd.jpg" alt="Screenshot_2024-01-31 20.29.02_KL64Gd" style="zoom:50%;" />

  + Multicast (ZigBee Pro)

    + Multicast is based on the idea of broadcast (flooding) but uses less resource, i.e., only transmit to a group of devices
    + Each group is identified by a 16-bit multicast group ID
    + Group members: the devices in the same group
    + A nonmember can be used to relay multicast message to unreachable member device
    + non-member radius (NR) field: limits the number of times a multicast frame is rebroadcast by nonmember devices

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-31 20.32.38_aXIrhM.jpg" alt="Screenshot_2024-01-31 20.32.38_aXIrhM" style="zoom:50%;" />

* Tree Routing

  + Tree Routing assumes Cskip addressing

    + a node knows the address range of its descendants
    + If the address falls within the range, send to the proper child
    + Otherwise, send to the parent

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-31 20.34.32_8v62OM.jpg" alt="Screenshot_2024-01-31 20.34.32_8v62OM" style="zoom:50%;" />

* Mesh Routing

  + The mesh routing is based on the Ad-Hoc On-Demand Distance Vector (AODV) routing protocol
  + AODV is a reactive routing protocol: source starts to discover a route to destination when it first needs to send a packet to the destination
  + Each node maintains a routing table which contains the next hop to a destination node
  + The AODV protocol
  + RREQs are broadcast messages
  + in the example, assume each link has link cost equals 1
  + The path cost is the accumulation of the link cost
  + Each intermediate node keeps the reverse path (min cost path to source)
  + The destination node 5 received the RREQ with min path cost 2 from node 1

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-31 20.39.20_wm4aXF.jpg" alt="Screenshot_2024-01-31 20.39.20_wm4aXF" style="zoom:50%;" />

* Source Routing

  + The problem with AODV is that the routing table may not fit in the memory
    + E.g., suppose a Gateway may have a routing table with ~2000 entries
  + In source routing, the routing is only known to the source
    + only the source potentially requires large memory
  + Source routing is based on Dynamic Source Routing (DSR) protocol
  + DSR is a reactive routing protocol
    1. Route Discover
    2. Route Reply



## Chapter 06, Module 01

#### Introduction to MANET

**Terminology and Paradigms**

* "Ad Hoc"
  + Often omprovised or impromptu; "an ad hoc committee meeting"
  + Formed or used for specific or immediate problems or needs; "ad hoc solutions"
  + Fashioned from whatever is immediately available: improvised; "large ad hoc parades and demonstrations"
* "Spontaneous"
  + Arising from a momentary impulse
  + Controlled and directed internally; "self-acting"
  + Produced without being planted or without human labor; "indigenous"
  + Developing without appartent external influence, force, casue, or treatment

**Intruduction**

(Mobile) Ad Hoc Communication Networks - MANET

* Historical successor of packet radio networks
* Self-organizing, mobile and wireless nodes
* Absence of infrastructure, multi-hop routing necessary
* Systems are both, terminals (end-systems) and routers (nodes)
* Constraints (dynamics, energy, bandwidth, link asymmetry)

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-03 14.08.18_kAYruo.jpg" alt="Screenshot_2024-02-03 14.08.18_kAYruo" style="zoom:50%;" />

**Why do we need routing protocol fro ad-hoc network?**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-03 14.09.22_xJ1ZXo.jpg" alt="Screenshot_2024-02-03 14.09.22_xJ1ZXo" style="zoom:50%;" />

* Links do not necessarily have the same characteristics in both directions
* Channel condition changes from time to time
* Dynamic topology
* Some nodes may be out of range of others
* Must use other peer nodes as routers to forward packets
* Need to find new routes as nodes move or conditions change (highy dynamic and unpredictable)
* Routing protocol captures and distributes state of network
* Routing strategy (algorithm) computes shortest paths

**Characteristics of Ad Hoc Communications**

* Characteristics are dominated by heterogeneity and variability
  + Dynamically changing topology
  + Absence of fixed infrastructure and centralized administration
  + Bandwidth constrained wireless links
  + Energy-constrained nodes

**Main challenges for routing protocol design**

* Mobility of nodes: Dynamic topologies
  + Path breaks
  + Partitioning of a network
  + Inability to use protocols developed for fixed network
* Bandwidth is a scarce resource
  + Inability to have full information about topology
  + Control overhead must be minimized
* Shared broadcast radio channel
  + Nodes compete for sending packets
  + Collisons
* Erroneous transmission medium
  + Loss of routing packets
* Energy-constrained
* Scalability



#### MANET Protocols

**Ad Hoc Routing Paradigms**

* Flooding of data packets
  + simple approach, extremely high overhead
  + many protocols perform flooding of control packets
* Uniform protocols
  + topology-based vs. destination-based
  + proactive vs. reactive paradigms
* Non-uniform protocols
  + hierarchical protocols, cluster-based, flat protocols
  + geographical protocols
  + hybrid protocols

**Reactive Routing**

* Goal: Reduction in routing overhead
  + useful when number of traffic sessions is much lower than the number of nodes
* No routing structure created a priori: Let the structure emerge in response to a need
* Advantages
  + small control overhead
  + adaptive to network dynamics
  + low storage requirements
* Disadvantages
  + High flood-search overhead with mobility, distributed traffic
  + high route acquistion latency
  + low scalability
* Source initiated
  + source floodes the network with route request packet when a route is required to a destination
* Destination replies to request
  + reply uses reversed path of route request
  + setes up the forward path
* Three key protocols
  + Dynamic Source Routing (DSR)
  + Ad-hoc On-demand Distance Vector (AODV) Protocol
  + Location Aided Routing (LAR)

**Proactive Routing**

* Distributed shortest-path protocols
* Based on periodic updates
  + high routing overhead
* Advantages
  + Low delay of route setup process: all routes are immediately available
* Disadvantages
  + high bandwidth requirements 
  + low scalability
  + high storage requirements 
* Routing Protocol
  + Optimized Link State Routing (OLSR)

**Taxonomy of Routing Protocols**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-03 14.34.31_0kuxoN.jpg" alt="Screenshot_2024-02-03 14.34.31_0kuxoN" style="zoom:50%;" />



## Chapter 06, Module 02

### The Ad Hoc On-demand Distance Vector Protocols (AODV)

### Dynamic Source Routing (DSR)

### Location Aided Routing (LAR)

### Optimized Link State Routing (OLSR)



