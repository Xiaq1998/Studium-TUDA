#Communication Networks I

## 1. Introduction

### Telegraphy

**Morse Telegraph 摩斯电报**

* One switch to send long and short impulses at sender 一个开关即可在发送器处发送长脉冲和短脉冲

  + Dashes and dot

* Morse Code

  + Variable length

  + Short code for frequently used letters

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-17 18.28.22_Cw7PDf.jpg" alt="Screenshot_2024-02-17 18.28.22_Cw7PDf" style="zoom:50%;" />

**Baudot Telegraph 博多电报**

* Fixed length 5 bit code
  + allows for 2^5^ = 32 symbols
  + rstricted to five bits
    + due to hardware constraints workaround by shifiting alphabet to represent more characters 由于硬件限制，通过移动字母表来表示更多字符的解决方法
* Later standardized by CCITT

**Telegraphy & Telephony**

* **Telegraph networks**
  + Message switching 消息交换
    + Telegram as discrete unit forwarded from sender to receiver via relay stations 电报作为离散单元通过中继站从发送者转发到接收者
    + **No dedicated line** between Sender S and Receiver R 发送方S和接收方R之间没有专用线路
  + Connectionless service
    + Subsequent telegrams from S to R may **use different lines** 从S到R的后续电报可能是用不同线路
    + e.g. in case of line failures 如：发生线路故障
  + Compare: **packet switching** in today's internet 如今互联网中的数据包交换
    + Messages (packets) limited in size
* **Telephone networks**
  + Circuit switching 电路交换
    + **dedicated line** between Sender S (caller) and Receiver R (callee) 发送者S和接收者R之间的专用线路
    + reserved exclusively for entire call duration 专为整个通话期间保留
  + Connection oriented service
    + communication always **follows same path** 沟通始终遵循相同的路径
    + three phases: connect (dial), talk (data exchange), disconnect (hang up)
  + Concepts still in use in today
    + no dedicated lines but, at some components there are reserved resources 没有专用线路，但某些组建有预留资源

**Televison vs. Telegraphy and Telephony**

* Television developed as **broadcast** medium
  + one sender, many receivers
  + inherent property of radio transmission
* Telephony (and telegraphy) developed as **unicast** medium
  + one sender, one receiver
  + inherent property of circuit switched network



### Basic Terminology and Concepts

**Network Components**

Data transfer from end system to end system

* End System (ES)
  + e.g. terminal, computer, telephone
  + e.g. modem 调制解调器, multiplexer 多路复用器, repeater 中继器
* Intermediate System (IS)
  + e.g. router

**Network Structures**

* Poin-to-Point channels

  + net = multitude of cable and radio connections often also called a network, whereby a cable always connects two nodes
  + more prevalent in wide area domains (e.g. telephone)

  + Topologies

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-17 18.53.13_7UdaQe.jpg" alt="Screenshot_2024-02-17 18.53.13_7UdaQe" style="zoom:50%;" />

* Boadcasting channels

  + systems share one communication channel

  + one sends, all others listen

  + used for:

    + wide area: radio, TV, computer communication
    + local area: local networks

  + Topologies

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-17 18.55.11_L29fRn.jpg" alt="Screenshot_2024-02-17 18.55.11_L29fRn" style="zoom:50%;" />

**Protocol: Communication between same Layers**

* Definition
  + A protocol defines the format and the order of messages exchanged between two or more communicating entities, as well as the actions taken on transmission and/or reception of a message or other event 协议定义两个或多个通信实体之间交换的消息的格式和顺序，以及在传输和/或接收消息或其他事件时采取的操作

**Service: Communication between adjacent Layers**

* multiple of primitives / operations / functions
* characterized by the "interface"
* does not reveal anything about the implementation

**Connections and Connectionless Services**

* Connections: Connection Oriented Service 面向连接服务

  + = telephone service
  + 3 phases:
    + to connect
    + to transfer data
    + to disconnect
  + "Connection-oriented" does not imply any additional properties of the connection
    + no reliability, flow control, congestion control is required
    + **TCP** implements them

* Connectionless Service 无连接服务

  + = postal service
  + connectionless networks have no connection establishment phase
    + transfer of isolated unit data
    + go straight to data transfer phase
    + no connection teardown phase
  + no need to maintain connection state
  + communication partner might not be ready for receiving
  + connectionless networks do not implement:
    + reliability, flow control, congestion control
    + **applies to UDP**

  

### Reference Model for Open Systems Interconnection

**ISO OSI (Open Systems Interconnection) Reference Model**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-17 20.29.58_xp85qY.jpg" alt="Screenshot_2024-02-17 20.29.58_xp85qY" style="zoom:50%;" />

**Layers and their Functions**

* Physical Layer
  + Signal representation of bits: sending bit 1 is also received as bit 1 
    + Protocol example: RS232-C = ITU-T V.24, other: ITU-T X.21
* Data Link Layer
  + Reliable data transfer between adjacent stations with frames
    + error correction and recognition within the frame: loss, duplication 
    + flow control
    + MAC (Medium Access Control)
* Network Layer
  + Connection (as relationship between entities) end system to end system
    + routing
    + congestion control
    + example: IP, X.25
* Transport Layer
  + Connection (as relationship between entities) from source (application/process) to destination (application/process)
    + protocol example: TCP
* Session Layer
  + Support a "session" over a longer period
    + synchronization
    + token management
* Presentation Layer
  + Data presentation independent from the end system
    + example: ASCII, Unicode
* Application Layer
  + Application related services
    + examples: electronic mail, file transfer, P2P

**Data Units**

* Application level "messages" are processed as data units
* Following notions for data units have become common:
  + packet: unit of transportation
  + datagram: instead of packet if sent individually (connectionless)
  + frame: with final envelope, ready to send (next to lowest layer)
  + cell: small packet of fixed size
* OSI terminology: "message" is a PDU



### Five Layer Reference Model, Internet Model, OSI Model and Example

**TCP/IP Reference Model: Internet Architecture**

* Physical Layer
  + sending bit 1 is also received as bit 1
* Data Link Layer
  + reliable data transfer between adjacent stations
* Netowkr Layer
  + connection end system to end system
* Transport Layer
  + connection end/source (application/process) to end/destination (application/process)
* Application Layer
  + application related services incl. ISO-OSI L5 and L6



## 2. L1 - Physical Layer Fundamentals

### Basics

A physical connection permits transfer of a bitstream in the modes: Duplex or Semi-duplex

**Bit Rate and Baud Rate 比特率和波特率**

* Baud Rate
  + Number of symbols (characters) transmitted per unit of time 每单位时间传输的符号 （字符）数
  + Baud Rate = Bit Rate (Only if there is 1bit/symbol)
* Bit Rate
  + Number of bits transferred per second (bps)  每秒传输的比特数

**Operating Modes**

* Transfer directions 传输方向
  + Simplex 单工
    + Data is always transferred into one direction only 数据始终仅向一个方向传输
  + Semi-duplex (Half-duplex) 半双工
    + Data is transferred into both directions 数据双向传输
    + But never simultaneously 但绝不能同时进行
  + Full-duplex 全双工
    + Data may flow simultaneously in both directions 数据可以同时双向流动
* Serial and parallel transmission
  + Parallel 并行
    + Signals are transmitted simultaneously over several channels 信号通过多个通道同时传输
  + Serial 串行
    + Signals are transmitted sequentially over one channel 信号通过一个通道顺序传输
* Synchronous Transmission
  + The point in time at which the bit exchange occurs is pre-defined by a regular clock pulse
* Asynchronous Transmission
  + Clock pulse fixed for the duration of a signal
  + Termination marked by stop signal (bit) or number of bits per signal



### Analog and Digital Information Encoding and Transmission 模拟和数字信息编码和传输

**Binary Encoding (non return to zero)**

* "1": voltage on high
* "0": voltage on low
* Pros:
  + simple, cheap
  + good utilization of the bandwidth (1 bit per Baud)
* Cons:
  + no "self-clocking" feature

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-17 23.41.07_xzdY4A.jpg" alt="Screenshot_2024-02-17 23.41.07_xzdY4A" style="zoom:50%;" />

**Manchester Encoding**

* Bit interval is divided into two partial intervals: l1, l2

  + "1": l1:high &rarr; l2: low

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-17 23.44.22_XhvVSI.jpg" alt="Screenshot_2024-02-17 23.44.22_XhvVSI" style="zoom:50%;" />

  + "0": l1: low &rarr; l2: high

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-17 23.44.01_NnOLeM.jpg" alt="Screenshot_2024-02-17 23.44.01_NnOLeM" style="zoom:50%;" />

  + Pros:

    + good "self-clocking" feature

  + Cons:

    + 0.5 bit/Baud

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-17 23.45.30_e8VXoI.jpg" alt="Screenshot_2024-02-17 23.45.30_e8VXoI" style="zoom:50%;" />

**Differential Manchester Encoding**

* Bit interval divided into two partial intervals
  + "1": no change in the level at the beginning of the interval
  + "0": change in the level
* Pros:
  + good "self-clocking" feature
  + low susceptibility to noise because only the signal's polarity is recorded
* Cons:
  + 0.5 bit/Baud
  + (more or less) complex

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-17 23.49.36_w6omBr.jpg" alt="Screenshot_2024-02-17 23.49.36_w6omBr" style="zoom:50%;" />



### Multiplexing Techniques

**Frequency Division Multiplexing (FDM)**

* Principle
  + frequency band is split between the users
  + each user is allocated one frequency band
* Application
  + example: multiplexing of voice telephone channels, phone, cable-tv

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-17 23.50.43_tjwIZB.jpg" alt="Screenshot_2024-02-17 23.50.43_tjwIZB" style="zoom:50%;" />

**Time Divison Multiplexing (TDM)**

* Principle
  + user receives a time slot
  + during this time slot the user has the full bandwidth
* Application
  + multiplexing of end systems
  + in transmission systems



## 3. L2 - Data Link Layer Fundamentals - Logical Link Control

### Fundamentals

**L2 Service**

* (reliable), efficient data transfer between adjacent stations

**L2 Functions**

* Data transmission as frames
* Error control and correction
* Flow control of the frames
* configuration management

**L2 Service Class "Unconfirmed Connectionless Service"**

* transmission of isolated, independent units (frames)
  + loss of data units possible
* Features
  + no flow control
  + no connect or disconnet
* Applications
  + on L1 communication channels with very low error rate
  + possibly during real time data transfer like interactive voice communication

**L2 Service Class "Confirmed Connectionless Service"**

* Receipt of data units (implicitly) acknowledged
  + no loss
  + timeout and retransmit
* Features
  + no flow control
  + no connect or disconnect
  + duplicates and sequence errors may happend due to "retransmit" 由于“重传”可能出现重复和顺序错误
* Application
  + L1 communication channel with high error rate, e.g., mobile communication

**L2 Service Class "Connection-Oriented Service"**

* Connection over error free channel
  + no loss, no duplication, no sequencing error
  + flow control
* 3-phased communication
  + connection 
  + data transfer
  + disconnection

**Operating Mode: Asynchronous and Synchronous**

* Asynchronous transmission
  + each character is bounded by a start bit and a stop bit
  + Pros: 
    + simple, inexpensive
  + Cons: 
    + low transmission rates, may be only some hundreds of bit/sec
* Synchronous transmission
  + several characters pooled to frames
  + frames defined by SYN or flag
  + Pros:
    + higher transmission rates
  + Cons:
    + more complex

**Synchronous Data Transmission: Framing**

* L2 forms a frame from the L1-bits L2从L1位形成帧

* Possibilities for bounding frames

  + character-oriented protocol 面向字符协议

    + Contro Fields: Flag frame areas depend on encoding (e.g. ASCII) 标志帧区域取决于编码

    + Problem: user data may contain "control characters" 用户数据可能包含“控制字符”

      + Solution: Character Stuffing

      + Sender: each control character is preceded by a DLE (Data Link Escape) 每个控制字符前面都有一个DLE（数据连接转义）(but not in user generated data)
      + Receiver: only control characters preceded by DLEs are interpreted as such 仅DLE前面的控制字符被解释为这样

    + Problem: user generated data contains DLE

      + Solution: 
        + the sender inserts an additional DLE before the DLE in the user's data
        + the receiver ignores the first of two back-to-back DLEs
      + Cons:
        + DLE insertion requires additional effort/time

  + count-oriented protpcol 面向计数协议

    + Frame contains length count field
    + Problem: transmission error destroys length count, sender and receiver are not synchronized anymore

  + bit-oriented protocol 面向位的协议

    + Problem: "Flag" in user data
    + Solution: Bif Stuffing
      + sender: inserts a "0" bit after 5 successive "1" (only in the user data stream)
      + receiver: suppresses "0" after 5 successive "1"

  + using invalid characters of the physical layer

    + Invalid: related to the layer in consideration

    + Method: L1 defines digital encoding



### Error Detection and Correction

**Error detection**

* inserting redundancies so that receiver is able to detect an error 插入冗余以便接收器能够检测到错误
* retransmitting in case of an error

**Error correction**

* inserting redundancies so that receiver is able to detect and correct an error

**Error Detection (Hamming)**



### Flow Control and Error Treatment

**Protocol 1: Utopia**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 23.44.15_41Xrd7.jpg" alt="Screenshot_2024-02-18 23.44.15_41Xrd7" style="zoom:50%;" />

* Assumptions
  + error-free communication channel
  + receiving buffer infinitely large
  + receiving process infinitely fast
* DSAP: Data link Service Access Point 数据链路层服务接入点

**Protocol 2: Stop-and-Wait**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 23.50.39_yafZPJ.jpg" alt="Screenshot_2024-02-18 23.50.39_yafZPJ" style="zoom:50%;" />

* Assumptions
  + error-free
  + not infinitely large receiving buffer
  + not receiving process infinitely fast
* Further
  + simplex mode for actual data transfer
  + Acknowledgement requires

**Protocol 3a: Stop-and-Wait / PAR**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 23.51.01_pAhh2T.jpg" alt="Screenshot_2024-02-18 23.51.01_pAhh2T" style="zoom:50%;" />

* Problem: protocol blocks at loss of both frames and ACKs
* Solution:
  + PAR (Positive-Acknowledgement with Retransmit)
  + also called ARQ (Automatic Repeat reQuest)
* Timeout interval
  + too short: unnecessary sending of frames
  + too long: unnecessary long wait in case of error

**Protocol 3b: Stop-and-Wait / PAR / SeqNo**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 23.52.27_Dycp1l.jpg" alt="Screenshot_2024-02-18 23.52.27_Dycp1l" style="zoom:50%;" />

* Problem: loss of ACKs may lead to duplicates
* Solution: sequence numbers
  + each block receives a sequence no.
  + sequence no. is kept during retransmissions range in general: [0, ... , k], k = 2n-1

**Protocol 3c: Stop-and-Wait / NAK+ACK / SeqNo**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 23.55.02_MU5CHx.jpg" alt="Screenshot_2024-02-18 23.55.02_MU5CHx" style="zoom:50%;" />

* Alternative: Active error control

  + include negative ACK (NAK)
  + in addition to ACK

* Situation 1: OK

  + frame correctly transmitted &rarr; ACK sent

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 23.56.54_3jgOC7.jpg" alt="Screenshot_2024-02-18 23.56.54_3jgOC7" style="zoom:50%;" />

* Situation 2: Break at path "sender &rarr; receiver"

  + frame did not arrive &rarr; timer issues retransmit

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 23.57.58_iJutSE.jpg" alt="Screenshot_2024-02-18 23.57.58_iJutSE" style="zoom:50%;" />

* Situation3: Break at path "sender &rarr; receiver"

  + faulty frame arrives 错误帧到达 &rarr; NAK issued

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 23.59.17_OAQ9G3.jpg" alt="Screenshot_2024-02-18 23.59.17_OAQ9G3" style="zoom:50%;" />

* Situation4: Break at path "receiver &rarr; sender"

  + NAK issued

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-19 00.04.52_NUL97f.jpg" alt="Screenshot_2024-02-19 00.04.52_NUL97f" style="zoom:50%;" />

  

### Sliding Window for Flow Control & Error Treatment



## 4. L2 - Data Link Layer Fundamentals - Medium Access Control & Local Area Network (LAN)

### Fundamentals - LAN

**Channel Allocation Problem**

* Pros
  + using schemes such as FDM or TDM
  + guarantess
  + simple
* Cons
  + does not work well with bursty traffic
  + inefficient and with poor performance

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-19 00.08.15_kMbpod.jpg" alt="Screenshot_2024-02-19 00.08.15_kMbpod" style="zoom:50%;" />

###Dynamic Channel Allocation: Contention Free

**TDMA**

* transmission sequence among stations defined by previously distributed reservation requests
* waiting time due to contention period
* exact timing necessary

**Token**

* stations form a virtual or a physical ring
* a token circulates on this ring



### Dynamic Channel Allocation: with Contention

**ALOHA**

* Sending without any coordination whatsoever
* Sender listens at the (return-)channel (after sending)
* In case of collision retransmits after a random time interval
* Cons: high amount of collisions

**Slotted ALOHA**

* Time of sending within a defined time pattern
* Requires centralized synchronization
* Cons: many collisions, but less than Unslotted ALOHA

**CSMA**

* Principle
  + check the channel before sending
  + channel status:
    + busy: no sending activity AND wait until channel is re-checked OR keep checking continuously until channel is available
    + available: send still possibility for collision exists
    + collision: wait for a random time
* Variation 1-Persistent
  + Principle
    + request to send &rarr; channel check
    + channel status:
      + busy: continuous re-checking until channel becomes available
      + available: send (i.e. send with probability *p = 1*)
      + collision: wait random time, then re-check channel
    + Pros: minimizing the delay of own station
    + Cons: low throughput
* Variation p-Persistent
  + Principle
    + request to send &rarr; channel check
    + Channel status
      + busy: wait for the next slot, re-check (continuously)
      + available: send with probability p, wait with probability *1-p* for the next slot, check next slot
      + collision: wait random time, re-check channel
    + Properties: compromise between delay and throughput
* Variation CD (Collision Detection)
  + Principle
    + sending station interrupts transmission as soon as it detects a collision 
      + saves time and bandwidth
      + frequently used (802.3 Ethernet)
      + station must realize during the sending of a frame if a collision occured

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-19 22.04.38_dydsE0.jpg" alt="Screenshot_2024-02-19 22.04.38_dydsE0" style="zoom:50%;" />



### IEEE 802.3: CSMA/CD

**Frame Format**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-19 22.14.36_ThY6JE.jpg" alt="Screenshot_2024-02-19 22.14.36_ThY6JE" style="zoom:50%;" />

* Pad
  + Min. frame length = 64 bytes
  + Shorter frame length is an invalid frame

**Example: Time to send 450 bits at 10 mbps**
$$
\frac{450bits}{10*10^6bits/sec}=45usec
$$
**Properties**

* Pros
  + most widely spread
  + stations connect without shutting down the network
  + practically no waiting period during low workload
* Cons
  + minimum frame size
  + not deterministic (no maximum waiting period)
  + no prioritizing
  + when load increases, collisions also increase



### Ethernet Family

**Fast Ethernet**

* Retain all procedures, format, protocols
* Bit duration reduced from 100ns to 10ns

**Gigabit Ethernet**

* If 100% compatible, retain all procedures, format, protocols

  + bit duration reduced from 100ns to 1ns

  + maximum extension would also be 1/100 of the 10Mbit/s Ethernet

* Shared broadcast mode
  + half duplex mode
  + interconnected by hub function
* Point-to-Point links
  + full duplex mode
  + interconnected by switch function
  + with 1 Gbps in both directions



### IEEE802.5: Token Ring

**Ring**

* Not really a broadcast medium, but a multitude of point-to-point lines

**Station**

* copies information bit by bit from one line to the next (active station) 将信息从一条线一点点复制到下一条线

**Token Protocol**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-19 22.23.01_pCZAlw.jpg" alt="Screenshot_2024-02-19 22.23.01_pCZAlw" style="zoom:50%;" />

* Token: frame with special bit pattern
* One toke circulates on the ring:
  1. before station is permitted to send, it must own and remove the token frome the ring
  2. station may keep the token for a pre-defined time and may send several frames
  3. after sending, the station generates a new token

* Token circulates 20 times
* Token: 3 byte length

**Properties**

* Pros
  + digital technology only
  + multitude of transmission media
  + deterministic behavior
  + random frame lengths
* Cons
  + central monitor
  + delays because of waiting for token



## 5. L3 Network Layer - Fundamentals

### Types of Switching

**Circuit switching 电路交换**

* switching a physical connection
* connection exists physically for the duration of the conversation
* properties
  + connection must occur before transmission
  + establishing a connection takes time
  + resource allocation too rigid 
  + once connection is established it can not be blocked anymore

**Message switching**

* message is stored and passed on by one hop
* all data to be sent are treated as a "message"
* "Store and forward" network
  1. accepted
  2. treatment of possible errors
  3. stored
  4. forwarded 
* Example: early telegram service
* Properties
  + high memory requirements at the node
  + node may be used to its full capacity over a longer period of time by one message

**Packet switching**

* store-and-forward, but transmissions packets limited in size
* packets of limited size
* dynamic route search (no connect phase)
* no dedicated path from source to destination
* Example: internet
* properties
  + possibly only reservation of average bandwidth
  + possibility of congestion
  + high utilization of resources

**Switching by virtual circuit**

* packets (or cells) over a pre-defined path

* setup path from source to destination for entire duration of call

* using state information in nodes but no physical connection

* Example: Former ATM PVC

* Properties

  + all messages of a connection are routed over the same pre-defined data path

  + it is easier to ensure Quality of Service

    

### Services: Concepts

**Connection Oriented Communication**

* 3 phase interaction
  + connect
  + data transfer
  + disconnect
* reliable communication in both directions (duplex) 双向可靠通信
  + no loss, no duplicates, no modification
  + ensures maintenance of the correct sequence of transmitted data 确保维持传输数据的正确顺序
* relatively complex protocols
* Example: telephone service

**Connectionless Communication**

* network transmits packets as isolated units (datagram)
* unreliable communication
  + loss, duplication, modification, sequence errors possible
* no flow control
* comparatively simple protocols
* Example: mail delivery service



### Routing - Overview

**Task of routing**

* To find a route (path)
* Belongs to Network Layer, Layer 3
* Network consists of end systems and routers

**Fundations & Forwarding 转发**

* Routing: to take a decision which route to use
* Forwarding: to define what happens when a packet arrives

**Broadcast and Multicast Routing**

* Unicast 单播
  + 1 - 1 communication
* Multicast 多播
  + 1 - n communication
* Broadcast 广播
  + 1 - all communication



### Congestion Control - Basics

**General methods of resolution**

* to increas capacity
* to decrease traffic

**Strategy 1: to avoid**

* Traffic shaping, leaky bucket, token bucket, reservation (multicast), isarithmic congestion control
* Flow control
* open loop

**Strategy 2: to repair**

* Drop packets, choke packets, hop-by-hop choke packets, fair queuing
* closed loop



### Congestion Control - Avoidance

* Principle
  + Appropriate communication system behavior and design 适当的通信系统行为和设计
* Policies at various layers can affect congestion 各个层面的策略都会影响拥塞

**Avoidance by Traffic Shaping**

* with Leaky Bucket 漏桶

  + Principle

    + continuous outflow
    + congestion corresponds to data loss

  + Bucket size determines maximum capacity until overflow (drop/loss) and possible delay 桶的大小决定最大容量，直到溢出（丢弃/丢失）和可能的延迟

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-19 23.42.12_p27xyh.jpg" alt="Screenshot_2024-02-19 23.42.12_p27xyh" style="zoom:50%;" />

* with Token Bucket

  + Principle
    + permit a certain amount of data to flow off for a certain amount of time 允许一定量的数据在一定时间内流出
    + controlled by "tokens"
    + number of tokens limited 
  + Implementation
    + add tokens periodically until maximum has been reached 定期添加令牌，直到达到最大值
    + remove token depending on the length of the packet （byte counter） 根据数据包的长度删除令牌

**Avoidance by Reservation**

* Admission Control

  + Reserving the necessary resources during connect
  + If buffer or other resources not available
    + alternative path
    + desired connection refused

* Buffer Reservation

  + Congestion not possible 

  + Buffers remain reserved, even if there is no data transmission for some periods 即使没有数据，缓冲区仍然保留传输一段时间

    

### Congestion Control - Reaction and Correction

* Principle
  + No resource reservation 无资源预留
* Necessary steps:
  1. to detect a congestion 检测拥塞
  2. to introduce appropriate procedures for reduction 引入适当的减少程序

**Packet Dropping**

* Principle: incoming packet is dropped, if it can not be buffered

* Buffer Assignment Methods 如果无法缓冲传入数据包，则将其丢弃

  + Permanent buffers per incoming line 每条传入线路的永久缓冲区

  + Maximum number of buffers per output line

    + packet dropped despite there are free lines

    + $$
      m=\frac{k}{\sqrt{s}}
      $$

    + m: max. number of buffers per output line

      k: total number of buffers

      s: number of output lines

  + Minimal number of buffers per output line

    + Such that any line can not be starved

  + Content-related dropping: relevance

* Pros: very simple

* Cons:

  + retransmitted packets waste bandwidth

  + packet must be sent on average x times before it is accepted, the average is:
    $$
    x=\frac{1}{1-p}
    $$
    p: probability that packet will be dropped

    1-p: the packet is sent once with

    p(1-p): the packet is sent twice

**Choke Packets and Explicit Congestion Notification 阻塞数据包和显示拥塞通知**

* Principle
  + to reduce traffic durng congestion by telling source to slow down

**Fair Queuing**



## 6. L3 - Internet Protocol & Addressing

### Internet Protocol Version 4 (IPv4) 

**Addressing - IPv4**

* 32 bit address
* each address is unique worldwide
* structure: Net-ID (Subnet-ID) + ES-ID
* value range: 0.0.0.0 ... 255.255.255.255

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 00.46.34_nJ4osx.jpg" alt="Screenshot_2024-02-20 00.46.34_nJ4osx" style="zoom:50%;" />

* Formats: 5 classes

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 00.47.35_oQiJzt.jpg" alt="Screenshot_2024-02-20 00.47.35_oQiJzt" style="zoom:50%;" />

**IPv4 Datagram Format**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 01.02.17_KoHm6Y.jpg" alt="Screenshot_2024-02-20 01.02.17_KoHm6Y" style="zoom:50%;" />

* IHL: Header Length
* Total Length: full length including the data
* Flags
  + DF: don't fragment 不要分割
  + MF: more fragments (last fragment marked 0) 更多片段
* Fragment offset: offset of this fragment 该片段的偏移量
* TTL: Time To Live



### Internet Protocol Version 6 (IPv6)

**Addressing - IPv6**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 00.59.12_MY0fsg.jpg" alt="Screenshot_2024-02-20 00.59.12_MY0fsg" style="zoom:50%;" />

* 16 byte (4*32 bit) length
* anycast
  + send data to one member of a group

**IPv6 - Format**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 01.12.18_hMbgs4.jpg" alt="Screenshot_2024-02-20 01.12.18_hMbgs4" style="zoom:50%;" />

* Payload Length: Length including the data (but without the 40 byte header)
* Next Header: contains protocol identification
* Hop limit: life cycle in number of hops, max. 255

**Extension Headers**

* are placed between fixed header and payload
* Pros
  + optional
  + help to overcome size limitation
  + allow to append new options without changing the fixed header

**Transition from IPv4 to IPv6**

* some changes compared to IPv4
  + Checksum removed entirely
  + Fragmentation not allowed a routers
  + not all routers are updated simultaneously 并非所有路由器都会同时更新
* How to operate a network with a mix of IPv4 and IPv6 routers?
  + Solution: **tunneling 通道**
    + IPv6 packets carried as payload in IPv4 packets between IPv4 routers



### Internet Control Message Protocol (ICMP)

* Purpose
  + to communicate network layer information between hosts, routers
  + mostly for error reporting
* used by ping program
  + echo request
  + echo reply



### IPv4 Addresses and Routing

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 01.35.14_buADza.jpg" alt="Screenshot_2024-02-20 01.35.14_buADza" style="zoom:50%;" />

**Special IP addresses**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 01.36.47_nE0YlE.jpg" alt="Screenshot_2024-02-20 01.36.47_nE0YlE" style="zoom:50%;" />

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 01.37.06_KJ2Lch.jpg" alt="Screenshot_2024-02-20 01.37.06_KJ2Lch" style="zoom:50%;" />

**Subnetworks**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 01.39.29_4vjoBg.jpg" alt="Screenshot_2024-02-20 01.39.29_4vjoBg" style="zoom:50%;" />

* use subnet mask to indicate split between network + subnet and host part routing with 3 levels of hierarchy

**CIDR: Classless InterDomain Routing 无类域间路由**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 01.49.52_n9iCFm.jpg" alt="Screenshot_2024-02-20 01.49.52_n9iCFm" style="zoom:50%;" />

* CIDR address 

  + includes
    + the standard 32-bit IP address

  + e.g., CIDR address 194.24.8.0/22

    + the "/22" indicates

      + first 22 bits used to identify unique network

      + remaining bits to identify specific host

        

### Address Resolution

**Address Resolution Protocol ARP 地址解析协议 **

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 02.00.21_J42tLj.jpg" alt="Screenshot_2024-02-20 02.00.21_J42tLj" style="zoom:50%;" />

* Process
  1. Broadcast **ARP request** datagram on LAN
  2. Every machine on LAN receives this request and checks address
  3. Reply by sending **ARP response** datagram
  4. Store pair for future requests

**Reverse Address Resolution Protocol RARP 反向地址解析协议**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 02.02.38_qzrdSP.jpg" alt="Screenshot_2024-02-20 02.02.38_qzrdSP" style="zoom:50%;" />

* Retrieve Internet address from knowledge of hardware address 从硬件地址的knowledge中检索互联网地址
  + RARP server responds
  + RARP server has to be available on the LAN
* Application: diskless workstation boots over the network

**Dynamic Host Configuration Protocol DHCP 动态主机配置协议**

* Allows for manual and automatic IP address assignment
* May provide additional configuration information (DNS server, netmask, default router, etc)

* DHCP server is used for assignment
* Client broadcasts **DHCP Discover packet**
* Server answers



## 7. Routing - Basics

### Foundations of Routing

**Classes of Routing Algorithms**

* Non-adaptive Algorithms
  + current network state not taken into consideration
  + Spanning tree
  + Flow-based routing
  + Flooding
* Adaptive Algorithms
  + desicisons are based on current network state
  + centralized routing
  + isolated routing - backward learning
  + distance vector algorithms
  + link state routing

**Non-Adaptive Shortest Path Routing**

* Static Procedure
  + network operator generates tables
  + Tables 
    + are loaded when IS operation is initiated and will not be changed any more
* Pros: 
  + simple
  + good results with relatively consistent topology and traffic
* Cons:
  + very poor performance



### Non-Adaptive Flow-Based Routing

**Procedure**

1. Computation of the average delay per edge 每个边沿平均延迟的计算
   $$
   T_i=\frac{1}{edge capacity-average edge utilization}=\frac{1}{\mu C_i-\lambda_i}
   $$
   
2. Computation of the total average delay of a subnetwork 子网平均延迟的计算

3. Different total average delays result from selecting different paths 通过单边延迟的加权和

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 15.54.22_ZSH74R.jpg" alt="Screenshot_2024-02-20 15.54.22_ZSH74R" style="zoom:50%;" />

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 15.54.28_GaVeFb.jpg" alt="Screenshot_2024-02-20 15.54.28_GaVeFb" style="zoom:50%;" />

* Example: from B to D
  + path BFD with 3 packets/sec

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 15.56.40_ki2eLm.jpg" alt="Screenshot_2024-02-20 15.56.40_ki2eLm" style="zoom:50%;" />

* 入~xy~: average load 平均负载

  + the sum of all mean packets/sec at the respective edge 相应边缘处的所有平均数据包/秒的总和
  + 入~AB~ = AB (AB=9) + AC (ABC=4) + AD (ABFD=1) = 14

* C~xy~: capacity of eache edge in kbps 每条边的容量

  + AB: 20 kbit/sce

* uC~xy~: capacity of each edge at given mean packet size 给定平均数据包大小下每条边的容量

  + AB: 20 kbit/sec and packets in mean 800 bit/packet

  + $$
    \mu C_{AB}=\frac{20kbits/sce}{800bit/packet}=25packets/sec
    $$

* T~xy~: average delay on each edge 每个边沿的平均延迟

  + $$
    T_{xy}=\frac{1}{\mu C_{xy}-\lambda_{xy}}=\frac{1}{25packets/sec-14packets/sec}=90.909msec/packet
    $$

* Weight: the relative traffic of data using this edge 使用该边缘的数据的相对流量

  + $$
    Weight(AB)=\frac{\lambda_{AB}}{\sum_{all lines xy}\lambda_{xy}}=\frac{14}{82}=0.1707
    $$

* total average delay of a subnetwork

  + $$
    \sum Weight(xy)\cdot T_{xy}=86msce
    $$

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 16.11.53_Ob7c7J.jpg" alt="Screenshot_2024-02-20 16.11.53_Ob7c7J" style="zoom:50%;" />



### Adaptive Distributed – Distance-Vector Routing

**Principle**

* IS maintains table stating best known distance to all known destinations and line to be used when sending to a certain destination
* ISs update tables by exchanging routing information with their neighbors

**Node X receives list E(Z) from neighbor Y**

* knows distance X to neighbor Y: e
* gets distance (neighbor) Y to Z: E(Z)
* computes distance X to Z via (neighbor) Y: E(Z) + e
* decides which path to use

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 16.56.22_Zeg9Pg.jpg" alt="Screenshot_2024-02-20 16.56.22_Zeg9Pg" style="zoom:50%;" />

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 16.56.13_6yIOcv.jpg" alt="Screenshot_2024-02-20 16.56.13_6yIOcv" style="zoom:50%;" />

**Example: Initialization of Distance Tables and Sending Vector for 1^st^ time**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 17.10.31_tncTNR.jpg" alt="Screenshot_2024-02-20 17.10.31_tncTNR" style="zoom:50%;" />

* each node sends "updates" to its neighbors
  + update message contains (node, distance) pairs
  + which indicate that the sending node has "distance" hops to "node"
* when another node receives update, it checks:
  + if "announced distance + distance to the announcer" < current distance to "node"
  + then use that route to "node"

**Link Cost DEcreases / INcreases - Property “Count to Infinity”**

* Case A) Link Cost Decreases

  + short paths & route improvement

    &rarr; fast

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 17.20.04_TMuHxT.jpg" alt="Screenshot_2024-02-20 17.20.04_TMuHxT" style="zoom:50%;" />

* Case B) Link Cost Increases

  + long path & route deterioration

    &rarr; slow

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 17.23.22_CSRCPC.jpg" alt="Screenshot_2024-02-20 17.23.22_CSRCPC" style="zoom:50%;" />

**Split Horizon**



### Adaptive Distributed – Link State Routing

**1. Phase**

* Gather information about the adjacent intermediate system

**2. Phase**

* Define the "distance"

**3. Phase**

* Organize the information as link state packet 将信息组织为链路状态数据包

  + including own address, sequence number, age, distance

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 16.22.12_c40XpH.jpg" alt="Screenshot_2024-02-20 16.22.12_c40XpH" style="zoom:50%;" />

**4. Phase**

* Distribute the local information to all IS 将本地信息分发给所有IS
  + by applying the flooding procedure (very robust) 通过应用泛洪程序

**5. Phase**

* Compute now routes

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 16.25.07_PxbAdA.jpg" alt="Screenshot_2024-02-20 16.25.07_PxbAdA" style="zoom:50%;" />

**Adaptive Distributed Routing**

* Distance Vector Routing
  + Intermediate Systems IS
    + maintain table stating
      + best known distance to all known destinations and line to be used when sending to a certain destination
    + update tables
      + by exchanging routing information with their neighbors
* Link State Routing
  + measure the "distance" to the directly adjacent IS
  + distribute information to "everybody" and get this information from the others
  + calculate the ideal route



### Further Routing Principles and Enhancements

**Multipath Routing**

**Hierarchical Routing**

**Overlay Routing**



## 8. Routing - in Mobile Environments

### Challenges in Mobile Communications

**Hidden Terminals**

* Two nodes that are within each others transmission range try to communicate with a third node. This third node is able to receive messages from both nodes and, therefore, collisions may occur at this node.
* Cons:
  + more collisions
  + waste of resources
* CSMA/CD does not fit

* Solutions:
  + Busy Tone: a receiver transmits busy tone when receiving data
  + Reliability achieved by explicitly sent Acknowledgements (ACK)
  + Karn90

**Exposed Terminals**

* Two nodes communicate with each other, a third node, that is within the transmission of the sender but is not in range of the receiver is not allowed to transmit data when CSMA/CD is used. 
* However, as this third node is not within the transmission range of the receiver packets, that were sent by this third node would not result in collisions at the receiver. Tererfore, bandwidth is wasted due to CSMA/CD
* Cons:
  + CSMA/CD does not fit
  + lower effective throughput

**Near and Far Terminals**



### Mobile Routing - Devices making use of Wireless Communications

**Ad Hoc Routing Protocols**

* Proactive
  + Routing information is computed and updated independent of whether there is any traffic between the nodes or not
  + Traditional routing protocols are proactive
    + Link-state
    + Distance-vector
  + Pro: routers that are readily available when required
  + Con: overhead generated due to update mechanism
* Reactive
  + Routes maintained on-demand, i.e., when there is traffic, and no route is known
  + Pro: no overhead due to updates
  + Con: routing has to be completed before the first pack can be sent
* Non-Uniform
  + Some node have dedicated duties wrt routing
  + LAR, OLSR
* Uniform
  + All nodes have the same duties wrt routing
  + Topology-based & Destination-based
  + Proactive (table-driven) & Reactive (on-demand)
  + AODV, DSR

**DSR**

* Reactive routing protocol
* Principle 
  + Source node S **floods Route Request (RREQ)**
  + Each node appends own identifier when forwarding RREQ 每个节点在转发RREQ时附加自己的标识符
  + Destination D on receiving the first RREQ, sends a **Route Reply (RREP)**

**AODV**

* Reactive routing protocol
* Characteristics 
  + no overhead on data packets
  + sequence numbers
    + to prevent loops
    + solves "count to infinity" problem
    + as route freshness criteria
* Route discovery
  + **Broadcast Route Request (RREQ)**
  + Nodes sets up a reverse path pointing towards the source **Route Reply (RREP)**
    + Forward links are setup when RREP travels along the reverse path 当RREP沿反向路径传播时，建立前向链路
* Timers to keep route alive
* Destination Sequence numbers to determine fresh routes

**LAR**

* Based on flooding
* Make use of information about the loaction to limit scope of flooding for route request
* Expected Zone is determined as a region that is expected to hold the current location of the destination node D
* Route requests limited to a Requested Zone contains:
  + the Expected Zone
  + location of the sender node S
* **Only nodes within the request zone forward route requests**
* Con: each node must know its physical loaction to determine whether it is within the request zone



## 9. L4 Transport Layer - Fundamentals

### Transport Layer Function

**Function**

* To provide data tansport reliably, efficiently, at low-cost for process-to-process

**Service**

* to improve the network service quality

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-21 15.11.36_tTiN7L.jpg" alt="Screenshot_2024-02-21 15.11.36_tTiN7L" style="zoom:50%;" />



### Addressing

**Define transport addresses**

* TSAP (Transport Service Access Point) 传输层服务接入点
* Port

**How does the specific address(es) of a service become known? 如何得知服务的具体地址**

* First Approach: TSAP known implicitly
* Second Approach: initial connection protocol
* Third Approach: Name Server (directory server)

**How to localize the respective end-system NSAP(Layer 3)?**

* First Approach: hierarchical addressing
  + e.g., <country>.<network>.<port>
* Second Approach: flat addressing
  + dedicated "name server"
  + request via broadcast



### Duplicates

**how to handle duplicates WITHIN a connection?**

* to use temporarily valid TSAPs 使用临时有效的TSAP
  + TSAP valid for one connection only 只对一个连接有效
  + generate always new TSAPs

**what characteristics have to be taken into account regarding**

* to dentify connections individually
  + each individual connection is assigned a new SeqNo and
  + endsystems remember already assigned SeqNo

**what can be done to ensure that a connection that has been established …**

* to identify PDUs individually: individual sequential numbers for each PDU



### Connect and Disconnect - Reliable Connection

**Three-way Handshake Protocol**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-21 15.29.53_dm3BUn.jpg" alt="Screenshot_2024-02-21 15.29.53_dm3BUn" style="zoom:50%;" />

* CR: Connect Request
  + Initiator (A) sends request with SeqNo (X)
* CC: Connect Confirmation
  + Receiver (B) responds with SeqNo transmitted by the initiator (X) and selected SeqNo (Y) by receiver
* Acknowledgment
  + initiator (A) acknowledges SeqNo X, Y (as received before)

**Disconnect**

* symmetric disconnect
* asymmetric disconnect
  + to disconnect in one direction implies to disconnect in both "directions" 在一个方向上断开意味着在两个“方向”上断开



## 10. Transport Layer Protocols in General UDP - TCP

### UDP - User Datagram Protocol

* UDP is a simple transport protocol
  + unreliable
  + connectionless
  + message-oriented
* UDP is mostly IP with a short transport header
* Characteristics
  + no flow control
  + no error control or retransmission
  + may be used with broadcast/multicast and streaming

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-21 16.36.25_0AYpY4.jpg" alt="Screenshot_2024-02-21 16.36.25_0AYpY4" style="zoom:50%;" />



### TCP - Transmission Control Protocol

* TCP is the Internet transport protocol providing reliable end-to-end byte stream over an unreliable internetwork
* Two-way communications (fully duplex)
* Point-to-point
* TCP must ensure reliability
  + no data loss, no duplicate, no modified data
* Benefits
  + reliable data transmission
  + can be used with LAN and WAN
* Cons:
  + higher resource requirement
  + Connection set-up and disconnect necessary

**Why is connection setup necessary?**

* Mainly to agree on starting sequence numbers

**Set up (3-way handshake)**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-21 16.43.50_kDyhSL.jpg" alt="Screenshot_2024-02-21 16.43.50_kDyhSL" style="zoom:50%;" />



### Flow Control & Congestion Control

**Flow Control**

* controlled by window: advertised window awnd
* flow control required to avoid flooding receiver

**Congestion Control**

* controlled by window: congestion window cwnd
* Phases
  + Phase 1: Slow start (cwnd < ss_thresh)
  + Phase 2: Congestion Avoidance (cwnd >= ss_thresh)

**Slow start**

* To quickly discover the proper sending rate
* **initialize cwnd = 1**
* each time a segment is acknowledged &rarr; **increment cwnd by one (cwnd++)**
* continue until
  + reach ss_thres
  + packet loss
* congestion window size grows very rapidly

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-21 16.54.54_oOXhZG.jpg" alt="Screenshot_2024-02-21 16.54.54_oOXhZG" style="zoom:50%;" />

**Congestion Avoidance**

* timeout = congestion
* each time congestion occurs:
  + ss_thresh is set to 50% of the current size of the congestion window &rarr; ss_thresh = cwnd/2
  + cwnd is reset to one &rarr; cwnd = 1
  + and slow start is entered

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-21 16.57.24_3IolDe.jpg" alt="Screenshot_2024-02-21 16.57.24_3IolDe" style="zoom:50%;" />



## 11. Application Layer - Basics

### Session Layer

**Tasks**

* To control the dialog (interaction) between peers with defined start and end
* To synchronize and re-synchronize the data transfer

**A seesion may consist of multiple transport layer (L4) connections**

**Example:** Video streaming application

**Mechanisms**

* Activities -  a group of dialogs
* synchronization -  enable interrupt and resume
* tokens - determine, whose trun it is



###Data Presentation Layer

**Sender and receiver need common data presentation (common context) to allow for understanding 'communication' of content**

* needed for formats, data types, compression, coding...

**Functions**

* to allow to establish, control and transfer data of a session
* to allow the specification of complex data strucutres
* to provide negotiation of required data structures
* to convert the local representation into a global one

**Example**

* Historic example

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 01.09.59_RfboZM.jpg" alt="Screenshot_2024-02-18 01.09.59_RfboZM" style="zoom:50%;" />

* Coding Rules for Different Data Types

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 01.10.57_KHcun0.jpg" alt="Screenshot_2024-02-18 01.10.57_KHcun0" style="zoom:50%;" />

**Big Endian and Little Endian 大端和小端**

* Big Endian

  + e.g., Motorola 68x0, IBM 370
  + most significant byte (information) first

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 01.13.36_7xM8F5.jpg" alt="Screenshot_2024-02-18 01.13.36_7xM8F5" style="zoom:50%;" />

* Little Endian

  + e.g., Intel, also: Windows OS

  + less significant byte (information) first

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 01.13.42_289f3M.jpg" alt="Screenshot_2024-02-18 01.13.42_289f3M" style="zoom:50%;" />

**Local vs. Global Data Presentation**

* Local presentation of a communication partner
  + n x (n - 1) conversion routines
  + a maximum of one conversion per relationship 每个关系最多转化一次
* Global presentation
  + 2 x n conversion routines
  + 2 conversions per relationship 每个关系2次转化
    + local f1 to global g,
    + global g to local f2
  + Standards:
    + XDR
    + ASN.1

**XDR - External Data Representation 外部数据表示**

* Network format used with SunRPC
* Supports the entire C type system except for function pointers
* Cons:
  + two systems with completely identical representations must convert twice 具有完全相同表示的两个系统必须转换两次

**ASN.1 - Abstract Syntax Notation One**

* Defines the syntax of messages to be exchanged between applications (e.g., their fields) 定义应用程序之间交换的消息的语法

* Most widely used are

  + BER (Basic Encoding Rules) 基本编码规则

    + BER is highly structured, prefixing all values with a tag and a length 高度结构化，为所有制添加标签和长度前缀
    + BER specifies
      + how data should be encoded for transmission, independently of machine type, programming language, or representation within an application program. 如何对数据进行编码以进行传输，与机器类型、编程语言或应用程序内的表示无关

  + PER (Packed Encoding Rules) 打包编码规则

    + PER tries to represent the lengths in the most compact form possible
    + Like BER, PER specifies
      + how data should be encoded for transmission, independently of machine type, programming language, or representation within an application program. 
    + Unlike BER,
      + **tags are never transmitted**, while lengths and values are not transmitted if known by both peers 标签永远不会被传输，且如果双方都知道长度和值，则长度和值都不会传输
    + PER's reason for existence is to **conserve bandwidth** 存在的原因是为了节省带宽

  + RXER (Robust XML Encoding Rules) 强大的XML编码规则

    + Like BER and PER, RXER
      + how data should be encoded for transmission, independently of machine type, programming language, or representation within an application program

    + RXER is immediately legible 立刻清晰可见
    + RXER's reason for existence is ease of legibility (no tools are needed) 易于辨认
    + But RXER uses significantly more bandwidth 使用更多带宽



## 12. Electronic Mail

**Basic Functionality of an Email System**

* Addressing
* Transfer
* Report
* Display
* Disposition



### Basic Interaction

**Simple Mail Transfer Protocol SMTP 简单邮件传输协议**

* a protocol for sending e-mail messages between servers
  + also used to send messages from a mail client to a mail server
  + uses a TCP connection to prot 25
* consists of
  + message format
  + data transfer protocol

**STMP - Message Format & Structure**

* an envelope

  + defined in RFC 821

* header fields

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-19 01.41.38_WFt7KN.jpg" alt="Screenshot_2024-02-19 01.41.38_WFt7KN" style="zoom:50%;" />

* one blank line

* message text

**SMTP - Data/Mail Transmission (steps)**

1. Sender: application

   generates the message in the correct format

2. Sender: transmission program

   distributes a copy of each message to each recipient

3. Receiver: email server

   receives message and files it in the appropriate mailbox

4. Receiver: application

   reads mailbox

### Post Office Protocol (POP) / Internet Message Access Protocol (IMAP)

**Protocol for remote mailbox access**

* user transfers mail for further processing
  + this transfer is defined in a protocol: Post Office Protocol POP 邮局协议
* POP uses Port 110, SSL encrypted Port 995
* POP goes through 3 states: authorization, transcation, and update

**IMAP - Internet Message Access Protocol 互联网消息访问协议**

* used to retrieve e-mail from a mail server 从邮件服务器检索电子邮件
* uses Port 143, SSL encrypted Prot 993

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-21 17.54.30_W7xUls.jpg" alt="Screenshot_2024-02-21 17.54.30_W7xUls" style="zoom:50%;" />



### MIME - Multipurpose Internet Mail Extensions

* Possibilities
  + messages may contain non ASCII character
    + accents or special characters ä, ö, ü, etc (e.g. French, German)
    + non-latin alphabets
    + languages that are not bound by an alphabet (e.g. Chinese, Japanese)
  + messages that may contain audio data, video data or general data

**Messages**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-19 14.04.44_TIxbxg.jpg" alt="Screenshot_2024-02-19 14.04.44_TIxbxg" style="zoom:50%;" />

* Content types

  + Text (subtypes: plain, richtext)
  + Image (subtypes: gif, jpeg)
  + Audio (subtypes: basic)
  + Video (subtypes: mpeg, h261)
  + Message (subtypes: partial, external-body)
  + Multipart (subtypes: mixed, alternative, parallel)
  + Application (subtypes: postscript, Octet-Stream)

* MIME Message must include:

  + data in multiple message parts
  + definition of content types of individual parts
  + boundaries 边界 between parts

* Header Fields

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-19 14.07.19_BefWNB.jpg" alt="Screenshot_2024-02-19 14.07.19_BefWNB" style="zoom:50%;" />
  
  + Content-Transfer-Encoding
  
    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-19 21.38.26_JAMP5z.jpg" alt="Screenshot_2024-02-19 21.38.26_JAMP5z" style="zoom:50%;" />



### Secure Electronic Mail & Pretty Good Privacy PGP

**PGP**

* based on "web of trust"
  + user decides which certification entity he can trust
* principle
  + sender and receiver have private and public keys
* complete email security package



## 13. Web

**Address - Uniform Resource Locators (URL) 统一资源定位符**

* URL is the "address" of a page
* Format: <SCHEME>:<SCHEME-SPECIFIC-PART>

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 13.23.14_Jd3psx.jpg" alt="Screenshot_2024-02-20 13.23.14_Jd3psx" style="zoom:50%;" />

### Hypertext Markup Language (HTML)

* Web pages are accessed using HyperText Transfer Protocol (HTTP) 使用超文本传输协议（HTTP）访问网页

* Browser interprets tags and generates page layout 浏览器解释标签并生成页面布局

* Exapmle HTML tags

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 13.27.21_tau3mE.jpg" alt="Screenshot_2024-02-20 13.27.21_tau3mE" style="zoom:50%;" />

  

### Hypertext Transfer Protocol (HTTP)

* Web's application layer protocol

* Client/Server model

  + Client: browser that requests (receives, "displays" web objects)
  + Server: web server sends objects (in response to requests)

* HTTP uses **TCP** and HTTP/3 as recent version uses QUIC

  + client intiates TCP connection to server **Port 80**
  + server accepts TCP connection
  + HTTP messages exchanged between browser (HTTP client) and web server (HTTP server)
  + TCP connection closed

* HTTP is a stateless protocol

* HTTP connections can be

  + Non-persistent (HTTP 1.0) 非持久性

    + at most one object sent over one TCP connection 通过一个TCP连接最多发送一个对象

      <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 13.38.58_QtWJn7.jpg" alt="Screenshot_2024-02-20 13.38.58_QtWJn7" style="zoom:50%;" />

      + Round Trip Time RTT 往返时间
        + one RTT to initiate TCP connection
        + one RTT for HTTP request
        + **File transmission time = 2RTT + transmission time**

  + Persisten (HTTP 1.1) 持久性

    + multiple objects can be sent over one TCP connection 通过一个TCP连接可以发送多个对象
    + server leaves connection open after sending response
    + overhead reduced to ~one RTT for all referenced objects 所有引用对象的开销减少到约一个RTT

**HTTP Request Messages**

* Two types: Request, Response
* HTTP method types
  + HTTP/1.0
    + GET, request file specified in URL field
    + POST, send request with additional info in entity body
    + HEAD, asks server to leave requested object out of response
  + HTTP/1.1
    + GET, POST, HEAD
    + PUT, uploads file in entity body to path specified in URL field
    + DELETED, delete file specified in the URL field

**HTTPS**

* HTTPS is HTTP over Transport Layer Security TLS in order to be encrypted
* and HTTPS was HTTP over Secure Sockets Layer SSL
* HTTPS provides
  + privacy
  + authentication of the accessed webserver
  + integrity of the exchanged data at the communication channel

**HTTP/2 - HTTP/3**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 13.56.37_nmLz9v.jpg" alt="Screenshot_2024-02-20 13.56.37_nmLz9v" style="zoom:50%;" />



### Cookies and Web Caches and Semantics

**Cookies**

* Cookies allow to maintain user state on server 允许维护用户服务器上的状态

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-20 13.59.11_HdmYIv.jpg" alt="Screenshot_2024-02-20 13.59.11_HdmYIv" style="zoom:50%;" />

**Web Caches (Proxy Servers) 网络缓存 代理服务器**

* to satisfy client request without involving orignin server  满足客户端请求而不涉及源服务器
* Total average delay = Internet delay + access delay + LAN delay



## Pingo

**Q4 Congestion control**

a) Packet dropping is the only and most efficient way to act against congestions at networks

b) In case of a congestion choke even increase the amount of traffic

c) Fairness means that packets from sources reducing their traffic shall have a higher probability to be delivered correctly

d) Random Early Detection (RED) need a feedback channel to the source

Answer: a, b, c, d





Protocol: two instances of the same layer handle a protocol

Service: serivce is used by the layer above

Physical: Signal representation of bits. Sending bit 1 is also recived as bit 1

data link: reliable data transfer between adjacent stations with frames

Network: connection end system to end system

Transport: connection from source to destination

Session: support a session for a longer period

presentation: data presentation independent from the end system

Application: application related services

Connect-oriented service: consists of 3 phases: connect, data transfer, disconnect, more reliable connection service, more bandwidth, telephone service

connectionless service: tansfer of isolated units, postal service

it's unusual that the header data of a layer is stored behind the header data of the layer above

FDM, split btween the users, each user is allocated one frequency band

TDM, using time slot. during the time slot, the user has the full bandwidth

data link layer service: reliable, efficient data transfer between adjacent stations

slotted aloha has hiher delay than pure aloha

when two stations want to send at the same time, and the channel at this time is not used, they both sense the channel available and send immediately, then occurs collision

minmum frame length: to distinguish the faulty from correct frames

Routing: to take a decision which route to use

Forwarding: to define what happens when a packet arrived

congestion avoidance, congestion repair/correction

leaky bucket: does not allow a burst larger than the maximal data rate, relieves the network from the burden to manage bursts

token bucket: the sender can accumulate tokens and send a very high rate for a short time, cause congestion control problem

due to the changing topology, it is impossible to equally distribute permits

packet from one network can be too large for another network

fragmented in every intermediate system

reassembled at destination

if one fragment gets lost, the wohle packet must be retransmitted, beacuse the sender can not know, if and how the packet was fragmented.

looks like the fragment of a new packet, store until timeout, then discard

ICMP is used to communicate network layer infromation

subnet mask is used to split the host part of an address to allow the subdivision of the network

CIDR, classless interdomain routing, allocate IP address in variable-size blocks

broadcast an ARP request datagram on LAN, every machine on this LAN receives ARP request and check address, replys by sending ARP response datagram (it's MAC address), send data

A will not receive a response for its ARP request, because Ethernet broadcasts are not rerouted over a router

Non-adaptive: current network state not taken into consideration, spanning tree, flooding

Adaptive: decisions are based on current network state, link state routing

Proactive: provide routes to each node in the network all the time. routes are readliy available when required, overhead generated due to update mechanism

Reactive: determine route on-demand only. no overhead due to update, routing has to be complete before the first packet can be sent

Uniform: all nodes have the same duties wrt routing

Non-uniform: some nodes have dedicated duties wrt routing

AODV: routes are stored at the routing time locally. each node is aware of the next hop

DSR: the complete route is attached to each message. even intermediate nodes are aware of the complete route

Network: responsible for the communication between systems

Transport: provides an end-to-end communication to process

transport layer isolates upper layers from the technology and improves Network Service Quality

Connect request: initiator sends a request with a sequence number selected by the sender

Connect confirmation: receiver responds with the transmitted number and with an own randomly selected number 

Acknowledgment: sender acknowleges these two sequence numbers. after receiving a valid ACK, receiver accpets data

symmetric disconnect: if one party says disconnect, it means that this party will no longer send but might still receive. the disconnect has to be done by both connected entities.

asymmetric disconnect: one of the entites sends a disconect TPDU, and both parties disconnect

TSAP known implicitly, initial connection protocol, name server





UDP is a simple transport protocol, which is unreliable, connectionless, message-oriented and boroadcast support. needs few resources, causes less overhead, no flow control, no erorr control or retransmission

TCP provides reliable end-to-end byte streams over an unreliable network. Two-way communication, point-to-point, no boadcast/multicast/QoS parameters/real-time support, reliable, efficient, connection set up and disconnect necessary, higher resources requirement

Form and Sender tell respectively who composed and sent the message.

Circuit switching: a path through the network is set up and maintained for the whole message exchange. telephone network

message switching: the whole message is routed through the network one hop at a time. Telegraphy network

Packet switching: is still used in todays internet, where the message is limited in size

DHCP, flexibility, automation in managing IP address for devices on a network

client broadcasts a DHCP Discover packet to obtain an IP address and other configuration, server answers with DHCP Offer, with available IP address, client accepts the offer and ask server for its configuration with DHCP Request, server answers with comitted IP address and other configuraion with DHCP ACK.

Iterative: the local name server queries various DNS servers and receives a result.

Recursive: the local name sercer sends a request to the DNS server, which in turn requests other DNS servers.

Scoping: is the way of specifying the sub-hierarchy of the Directory Information Tree where the search query should take place

Filtering: search criteria within the defined scope is specified by filtering

ISN, chooses during TCP connection handshake randomly

use temporarily TSAP numbers, which only valid for one connection. disallows "well-known" TSAPs

Identify all connections individually by assigning a new sequence number. requires connection-oriented system

identigy each packet by an individual sequence number. requires more bandwidht and memory

cwnd is increased 1 MSS for each received ACK

Fragment: IP packets are split into fragment, in oder to adapt them to underlying networks

Segment: TCP data stream is split into segment, segment sents as payload of IP packet

setting IDSN to a random value to improves security, avoid losing data in some special cases

A TCP connection is identifed by source to destination port and IP, once a handover between different networks happens, the IP address changes, then disconnct of TCP connection

MPTCP uses several IP at the same time for the same MPTCP connection

the switching of a connection between different network interfaces without establishment of a new connection

an increased fault tolerance by using one of the subflows as backup

increased throughput achieved by sending and receiving data on multiple IP-enabled interfaces in parallel

Strict: data transmission stalled if one stream is stalled

Partial: data transmission for non-stalled streams can continue

MPTCP options are exchanged encoded in a specified TCP option. some middleboxes might still remove any unknown TCP options, MPTCP automatically falls back to TCP

human readable, supported by many programming languages, text format is less efficient, limited set of datatypes

FTPS: an extension of FTP, which adds an addtional encryption

SFTP: an extension of SSH, retaining benifts from SSH while adding file transfer support

failure transparency: failure unknown to user

access transparency: the interface for local and remote method calls should be equal

all interactions are stateless, relies on simple point-to-point communication via HTTP

space decoupling: the interacting parties do not need to know each other

time decoupling: the interacting parties do not need to be actively participating in the interaction at the same time

synchronization decoupling: publishers are not blocked while producing events, and subscribers are not blocked while receiving events

Topic-based: messages sent to well-known topics and recipients are known a-priori

Content-based: subscribers describe their interest as filter experssions

subscription forwarding, reducing subscription propagation, matching notifications

distributed objects have more meta data, remote method invocations have much higher latency

RPC: processes can call procedures on other computers

RMI Registry, Server Stub, Server Skeleton

RTSP: used to control the media playback

RTP: the protocol used to actually transfer the media content

RTCP: provides out-of-band statistic and control information for RTP

compensate for jitter, compensate for delay

P2P: using less resources, content does no longer come from server/content provider and could be modified in transit

HLS is based on HTTP, this enables better compatibility and scalability for delivering video content over the internet, HLS typically has higher latency

boadcast, expanding ring, random walk, rendzvous idea

overlay network: allow for bootstrapping, do not have to deploy new equipment, higher complexity

The chord protocol achieves log(n) search time with the help of its finger table, which contains references to nodes that are exponentially spaced apart, enabling efficietn routing to the desired node in a distributed hash table network.





