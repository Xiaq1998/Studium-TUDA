#Communication Networks II
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



## 2. Naming and Addressing

## 3. Transport Layer

## 4. Advanced UDP and TCP

## 5. Multipath

## 6. SCTP

## 7. Advanced Application Layer

##8. Message Passing

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 01.47.08_NmphOX.jpg" alt="Screenshot_2024-02-18 01.47.08_NmphOX" style="zoom:50%;" />

### Basic Operations

**Send Operation**

* Non-Blocking
  + the sender is delayed only for the duration of the copy operation
* Blocking
  + the sender is delayed until the corresponding receive operation is complete 发送方被延迟，直到相应的接收操作完成

**Receive Operation**

* Blocking
  + a precess calling receive is blocked until a message arrives 调用receive的进程将被阻塞，直到消息到达
* Non-Blocking
  + a process calling receive is never blocked 调用receive的进程永远不会被阻塞

**Synchronous Message Passing**

* If sender uses blocking send and receiver uses blocking receive
* No buffering needed
* Pros:
  + simpler (and verifiable) programs
  + no buffering needed
* Cons:
  + less parallelism
  + less flexibility

**Asynchronous Message Passing**

* If at least one process uses a non-blocking send or receive operation
* In principle, this needs unlimited buffer space for reliable transfer
  + Variant: buffer-blocking send for reliable transfer 缓冲区阻塞发送以实现可靠传输
* Pros:
  + maximum flexibility
  + maximum parallelism
* Cons:
  + buffering needed
  + complex programs, difficult to test



### Asynchronous: Message Queueing

**Message queues 消息队列** 

* the sender and receiver of the message do not need to interact with the message queue at the same time 消息的发送者和接收者不需要同时与消息队列交互

**Destination of a Message**

* IP address + (receiver's) local port

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 16.50.05_a2CGMs.jpg" alt="Screenshot_2024-02-18 16.50.05_a2CGMs" style="zoom:50%;" />

  

### Asynchronous: Publish/Subscribe - PubSub 发布/订阅

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 16.52.22_DQuyGV.jpg" alt="Screenshot_2024-02-18 16.52.22_DQuyGV" style="zoom:50%;" />

**Fundamentals of PubSub (Messaging Domain)**

* Point-to-Point
* Publish/Subscribe
  + applications post messages explicitly to specific channels
  + each message may have multiple receivers
* Advertisements
  + publisher advertises topic before publishing 发布者在发布前宣传主题
  + subscribers can get a list of advertised topics 订阅者可以获得广告主题列表

**Space and Time Decoupling 空间和时间解耦**

* Space Decoupling
  + the interacting parties do not need to knwo each other 交互双方不需要互相认识
  + producers publish messages through an event service 生产者通过事件服务发布消息
  + subscribers indirectly receive messages from event service 订阅者间接从事件服务接收消息
  + one-to-many communication patterns possible
* Time Decoupling
  + the interacting parties do not need to be actively participating in the interaction at the same time 互动双方无需积极参与同时互动
  + reducing space and time dependencies 减少空间和时间依赖性
  + greatly reduces the need for coordination between systems 减少了系统之间协调的需要

**Classification 分类 of Publish-Subscribe Systems**

* Subscription Model
  + topic-based / channel-based
  + content-based
  + attribute-based
* Routing
  + filter-based 基于过滤器
  + rendezvous-based 基于集合点
* Topology
  + centralized
  + decentralized

**Subscription Model**

* Topic-based subscriptions
* Content-based subscriptions

**Routing of Subscriptions and Publications**

* Two extreme cases

  + Event flooding

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 17.14.12_KmMgBJ.jpg" alt="Screenshot_2024-02-18 17.14.12_KmMgBJ" style="zoom:50%;" />

  + Subscription flooding

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 17.14.17_JxBw7x.jpg" alt="Screenshot_2024-02-18 17.14.17_JxBw7x" style="zoom:50%;" />

* More efficient cases

  + Filtering-based (Conten-based)

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 17.14.22_zmY90k.jpg" alt="Screenshot_2024-02-18 17.14.22_zmY90k" style="zoom:50%;" />

  + Rendezvous-based (Topic-based)

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 17.14.26_n8O0c7.jpg" alt="Screenshot_2024-02-18 17.14.26_n8O0c7" style="zoom:50%;" />

**==Filtering-based Routing (Conten-based)== P31-35**

* Identifying as soon as possible events that are not interesting for any subscriber and stop their diffusion 尽快识别任何订阅者不感兴趣的事件并阻止起扩散

* Creating "diffusion paths" 创建“扩散路径”

* Routing information consists of a set of FILTERS (aggregate of subscriptions) that are reachable through that broker 路由信息由一组可通过该代理访问的FILTERS（订阅聚合）组成

* Three main phases

  1. Subscribe - Subscription forwarding 订阅转发

     subscriptions are propagated to every broker leaving state along the path 订阅被传播到沿路径离开状态的每个代理

  2. Event(s) by publisher 发布者的事件

     by matching filters at brokers being adequately forwarded 匹配过滤器进行充分转发

  3. Reducing subscription propagation 减少订阅传播

     avoiding subscription propagation when a filter including the subscription has been already forwarded 当包含订阅的过滤器已被转发时避免订阅传播

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 17.27.26_51oj1M.jpg" alt="Screenshot_2024-02-18 17.27.26_51oj1M" style="zoom:50%;" />

**Case Study: Message Queue Telemetry Transport (MQTT) 消息队列遥测传输**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 17.31.52_3KKX7Z.jpg" alt="Screenshot_2024-02-18 17.31.52_3KKX7Z" style="zoom:50%;" />

* MQTT
  + is a messaging protocol
  + lightweight broker-based publish/subscribe messaging protocol
* Features
  + reliable messaging
  + minimal the on-the-wire footprint 最小化在线占用空间
  + expect and cater for frequent network disruption 预期并应对频繁的网络中断

**Some Protocol Details**

* Message Format: <Fixed Header>[<Variable Header>]<PayLoad>



### Synchronous: Remote Precedure Call - RPC 远程过程调用

**Processes can call procedures on other computers**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 17.43.27_rl6XqX.jpg" alt="Screenshot_2024-02-18 17.43.27_rl6XqX" style="zoom:50%;" />

**Principle**

* Code in client
  + set out-parameters
  + call X (out-parameters, result)
  + use result
* Code on server
  + proc X (parameters)
  + do stuff
  + return (result)

**Properties**

* Synchronous communication
* Only 1 call needed to access remote procedure 只需1次调用即可访问远程过程
* System takes care of all "small details" 
* Complexity same as normal procedure call 复杂性与普通过程调用相同
  + only one call in progress at a time
* Transparent to distribution 分配透明度
  + as long as client can find server, it does not matter where it is

**RPC Error: Request Omission 请求遗漏**

* If no answer within timeout, re-send request

* Four possible error cases in this case

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 17.52.12_Vbvrdc.jpg" alt="Screenshot_2024-02-18 17.52.12_Vbvrdc" style="zoom:50%;" />

**RPC Error: Reply Omission**

* Same countermeasure as for request omission (timeout)
* For client, indistinguishable from request omission & delays
* For server, means to memorize results for potential 2nd reply
  + more states, more memory

**RPC: Failure Semantics 失败语义**

* Maybe-Semantics
  + no repeated requests
* At-Least-Once-Semantics
  + infinite retry
* At-Most-Once-Semantics
  + tolerate omissions
* Exactly-Once
  + tolerate crashes

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 17.58.19_uIn5vF.jpg" alt="Screenshot_2024-02-18 17.58.19_uIn5vF" style="zoom:50%;" />



### Synchronous: Objects - Remote Method Invocation - RMI 远程方法调用

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 18.05.50_craX5A.jpg" alt="Screenshot_2024-02-18 18.05.50_craX5A" style="zoom:50%;" />

**RMI Components**

* Server Stub  (automatically generated) 服务器存根
  + provide an interface to call the remote method
* RMMI Registry 注册表
  + provides a name service for server objects
* Server Skeleton (automatically generated) 服务器骨架
  + unpack remote method call parameters
  + transfer the result to the client host

**RMI Interaction**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 18.05.55_CXugnO.jpg" alt="Screenshot_2024-02-18 18.05.55_CXugnO" style="zoom:50%;" />

* Workflow (remote method call)
  1. Client calls the Server stub (which is a local method)
  2. server stub serializes the arguments and writes them to the network stream
  3. server skeleton reads the network stream, unpacks the arguments and calls the server object method
  4. server object method performs the computation
  5. server skeleton packs the result and writes them to the network stream
  6. server stub reads the response from the network stream unpacks it and returns it to the caller

**Local vs. Distributed Objects**

* Distributed objects have more meta data 分布式对象有更多的元数据
* Remote method invocations have much higher latency 远程方法调用的延迟要高得多



##9. RTP & RTSP

### Real-Time

**Real-Time Process**

A process which delivers the results of the processing in a given time-span

**Deadlines in Real-Time (networked) Systems**

* Hard deadlines
  + should never be violated
  + result presented too late after deadline has no value for the user
  + violation means: severe (potentially catastrophic) system failure
  + Emample:
    + fly by wire
    + nuclear power plant
* Soft deadlines
  + deadlines are not missed by much
  + In some cases, the deadlines may be missed, but not too many deadlines are missed
  + violation: results(s) has/have still some value for the user/application
  + Example:
    + Train/plane arrival-departure



### Real-Time Transport Protocol (RTP) 实时传输协议

#### RTP + RTCP Basics

**Transport Layer**

* Real-Time Transport Protocol RTP 实时传输协议
* Real-Time Transport Control Protocol RTCP 实时传输控制协议

**Real-Time Transport Control Protocol (RTCP)**

* Functions
  + To monitor QoS
  + to convey information about
    + participants
    + session relationships
* Typically
  + "RTP does ..." means "RTP with RTCP does ..."

**RTP with RTCP Functions**

* RTP with RTCP provides:
  + support for transmission of real-time data
  + over multicast or unicast network services
* functional basis
  + sequence numbering
  + determination of media encoding
    + i.e. payload type identification
  + source identification (process)
  + synchronization
  + framing i.e. follows principle of
    + application level framing and integrated layer processing
  + error detection
    + i.e. delivery monitoring
  + encryption
  + timing
    + i.e. time stamping
  + unicast and multicast support
  + support for stream "translation" and "mixing"

**RTP + RTCP: Quality Control**

Component interoperations for control of quality:

* evaluation of sender and receiver reports
* modification or encoding schemes and parameters
* adaptation of transmission rates

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 18.08.48_2Yx4vn.jpg" alt="Screenshot_2024-01-29 18.08.48_2Yx4vn" style="zoom:50%;" />



#### Packet Format: RTP + RTCP

* Header structure

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 18.13.13_JvezKP.jpg" alt="Screenshot_2024-01-29 18.13.13_JvezKP" style="zoom:50%;" />

* RTP and RTCP uses (most commonly) **UDP**
  + simple
  + unreliable
  + connectionless
  + multicast
* RTCP to control the stream (Payload Type)
  + media encoding with profiles

* RTP Header

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 18.14.43_PkZ7Aw.jpg" alt="Screenshot_2024-01-29 18.14.43_PkZ7Aw" style="zoom:50%;" />

* RTCP Packets
  + Characteristics
    + periodic control packets
    + quality control
    + participants list
    + occupies only a fraction of the used bandwidth



#### Further Details: Mixer & Translator

**Mixer Functions**

* Reconstructs
* Translates
* Mixes
* Resynchronizes
* Forwards



### Real-Time Streaming Protocol (RTSP) 实时流协议

The Real Time Streaming Protocol (RTSP) is an application-level protocol for control over the delivery of data with real-time properties.

**Goal of RTSP**

* Signaling and control of multimedia streams
* Being independent from transport of media content

**Supported functions**

* To request streams from server (unicast, multicast)
* To invite a server to a conference
* To add media to a stream (record)



#### Properties of RTSP

**Supported operations**

* Play, Pause, Resume
* Reset
* Fast forward, Fast backward
* Record

Text-based, in the style of HTTPS 1.1

**Differences to HTTPS**

* RTSP assumes a state-full server, HTTPS is stateless

**What RTSP not does**

* To define compression méthodes for audio/video
* To define hoe media streams are split up in packets
* To make assumptions about the transport layer protocol being used
* To define how buffering is done by the media player



#### RTSP Session

**RTSP - Client-side Requests**

As in traditional client/server protocol

* Client, initiates session and sendz requests to server
* Server executes commands and replies

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 20.38.48_UdbxLp.jpg" alt="Screenshot_2024-01-29 20.38.48_UdbxLp" style="zoom:50%;" />

**RTSP - Server-side**

Server replies with status code similar to https

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 20.39.51_PqsulP.jpg" alt="Screenshot_2024-01-29 20.39.51_PqsulP" style="zoom:50%;" />

**RTSP - Session Example**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 20.41.03_PYAepO.jpg" alt="Screenshot_2024-01-29 20.41.03_PYAepO" style="zoom:50%;" />

* Options Command
  + Client request (CSeq)
    + Sequence number for request/response pair
    + Assigning responses to requests 
  + Server response
    + Reply contains supported commands
    + Server does not change its state
* Describe Command
  + Client request
    + Accept
      + Type of data that can be handled
      + Session ID
      + Bandwidth information
  + Server response
    + Reply contains
      + Content type
      + Content length
* Setup Command
  + Client request
    + Provide several possibilities for transporting content to client
      + TCP
      + RDT: Real Data Transport (similar to RTP)
  + Server response
    + Server decides about which possibility to use
      + (in this example) Transmit content via TCP over the same connection used by RTSP
* Play Command
  + Client request
    + Range to be played is requested
    + Allows to jump to an arbitrary position within the content
    + Pause playback with PAUSE
* Media Session
  + Transmission of media stream within RTP Session
    + Stream ID
    + Sequence Number
    + Timestamp
* Teardown Command
  + Client request
    + Playback is stopped
    + All resources are released
    + Restart requires: SETUP and PLAY
  + Server response
    + Successful stopping of playback
      + acknowledged



#### RTSP State Diagram

* State is maintained per Stream &rarr; Session-ID

* State Transition triggered at the reception of a request
  + OPTIONS, DESCRIBE, SET_PARAMETER request do not trigger any state transitions

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-01-29 20.52.46_9WU940.jpg" alt="Screenshot_2024-01-29 20.52.46_9WU940" style="zoom:50%;" />



## 10. Streaming

### Fundamentals

**Streaming Approach to Access Media Content**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 13.30.37_duwYO2.jpg" alt="Screenshot_2024-02-18 13.30.37_duwYO2" style="zoom:50%;" />

* Pros:
  + Playback starts as soon as playout buffer is filled with data (1 - 10 sec) 播放缓冲区充满数据后立即开始播放
  + Continuous stream of data 连续的数据流



### Streaming Media

 **Streaming**

* Continuous flow of media data from sender to receiver(s)
* Client starts playback directly after couple of seconds (1 - 10 sec)
* Server sends data with speed
* Type of streaming
  + Video on Demand VoD
  + Live-Streaming

**Classification of Streaming Approaches**

* Streaming protocol
  + HTTP
  + RTSP ... RTP-RTCP
  + Flash Streaming
* Data delivery
  + UDP
  + TCP
* Distribution
  + Client/Server
  + P2P-Streaming
* Type of Media
  + Audio
  + Video
* Client/Device
  + PC laptop
  + Mobile Device
  + Dedicated system Set-Top-Box
* Two basic types of streaming
  + (Video)-on demand-streaming
    + Complete media already available at the source
    + Spooling possible
    + Unicast-based communication
  + Live-Streaming
    + Data generated in real-time
    + No spooling possible
    + Multicast-based communication possible

**Alternatives for the Delivery of Streaming Data**

* via UDP with constant sending rate = playback speed
* via UDP with buffer time of 2-5s
* Via TCP



### HTTP Streaming

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 14.13.09_Rm5YZk.jpg" alt="Screenshot_2024-02-18 14.13.09_Rm5YZk" style="zoom:50%;" />

**Properties**

* Delivery of media stream via HTTP
* Cheap streaming alternative
* Stream played within browser plugin 在浏览器插件中播放的流
* Meida data delivered via TCP
  + using the open HTTP connection

**Streaming in HTML5**

* since version 5 HTML supports streaming of media content
  + added <video> tage
  + additional optional fields
* no further plugin required, codec integration in browser needed 不需要进一步插件，需要在浏览器中集成编解码器

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-18 14.19.05_sngwbL.jpg" alt="Screenshot_2024-02-18 14.19.05_sngwbL" style="zoom:50%;" />



### HTTP Live Streaming

**Problem: normal HTTP streaming not suitable for Live Streaming**

* Data rate can not be adjusted to meet requirements of devices
  + might lead to starving peers
  + no automatic fallback
* Quality level has to be selected manually at the beginning

**Solution**

* Adaptive streaming solution over HTTP



### P2P Streaming

* P2P video streaming has become increasingly popular approach for streaming (live) content
* many receivers, similar to IPTV
* Two approaches for P2P video streaming
  + Tree-based overlay
  + Mesh-shaped overlay



### Flash Streaming

**Real-Time Messaging Protocol (RTMP) 实时消息传递协议**

* used for communication between Flash-Player and Flash-Server
* transport of media content done like in HTTP streaming
* enables adaptive streaming like RTP/RTCP

**Advantages**

* better support for live streaming
* browser-independent due to the use as a plugin
* support for user interactions
* embedded audio- and video codecs

**Drawbacks**

* flash plugin needs to be installed
* proprietary (adobe) but specification publicly available sine 2008

**Flash Video - FLV**

* Audio Tags
  + Audio-Stream
  + Codecs: MP3, Speex, Nellymoser, G.711, AAC (MP4), PCM
  + Up to 44 kHz, 16 Bit
* Video Tags
  + Video-Stream
  + Codecs: On2 VP6, AVC (H.264), Screen Video, Sorensen H.263
* Data Tags (Script)
  + Flash ActionScript
* Meta Data
  + duration, widht, height, videodatarate, framerate



### Case Study: Adaptive Streaming of 360^0^ Videos and Point Cloulds

**Adaptive Streaming of 360^0^ Videos**

* During playback, only a small section of the cideo is actually visible
* Viewpoint Prediction Based Streaming
  + Adapts to current viewer's viewing behavior
  + But prone to prediction errors
* Popularity Based Streaming
  + Does not consider current viewer's viewing behavior
  + Utilize data from measurements movement of actual and previous viewers

**Point Clouds Streaming**

* Point clouds consist of 3D points
  + each with multiple attributes, such as coordinates and color 
* Can be divided into two components
  + the geometry 几何学
  + the attributes
* In a point cloud, each point has
  + a position (X, Y, Z)
  + optionally:
    + color (R, G, B)
    + time of acquistion 获取时间
    + transparency, reflectance, etc.



## 11. Resilience and Adaptivity

## 12. Overlay Networks

### Introduction

**Peer-to-Peer**

* A distributed system and a communication paradigm
* 9 Features
  1. Relevant resources located at nodes (“peers”) at the edges of a network
  2. Peers share their resources
  3. Resource locations
     + widely distributed
     + most often largely replicated
  4. Variable connectivity is the norm
  5. Combined Client and Server functionality (“Servent”)
  6. Direct interaction (provision of services, e.g. file transfer) between peers (= “peer-to-peer”)
  7. Peers have significant autonomy and mostly similar rights
  8. No central control or centralized usage/provisioning of a service
  9. Self-organizing system

**Client/Server Model vs. P2P Technology**

* Features of a client/server model:
  + in principle, 1 server and N clients
  + clear distinction between server and client functionalities
  + simple search mechanism
* Pros: reliable, well known behavior
* Cons: server needs to provide (almost) all resources



### Fundamentals of Overlay Networks

### Overlay Networks: Layer Model

### Unstructured P2P Networks

### Structured Overlay Networks

### Case Study Chord



##Pingo

**Q2**: Which of the following statements is true? (at least one answer is correct)

a) A body area network is based on broadcasting; a storage area network is based on point-to-point communications.

b) A communications system structured in a few(e.g., 3) layers is less complex(e.g., difficult to implement) than the same system structured by more(e.g., 9) layers.

c) The interface to a service is defined independently from the specific operating system.

d) Connectionless protocols are much easier to conceive and implement as connection-oriented protocols.

Answer: a, b, c, d.



**Q3**: An Address identifies communication entities/components. Which of the following statement/s is/are in general true?

a) an Address is the NAME of a resource indicating WHAT we seek.

b) an Address indicates WHERE it is.

c) an Address is needed in order to find out a ROUTE which tells HOW TO GET THERE.

d) an Address in an abbreviation in order to remember "something" it better.

f) ideally one Address is sufficient for a communication device/end system.



**Q1**： A typical connection oriented service comprises (at least one answer is correct)

a) less than 4 states at each entity

b) at most 4 states at each entity

c) exactly 4 states at each entity

d) at least 4 states at each entity

e) more than 4 states at each entity

Answer: d, e



**Q2**: Duplicates at the transport layer (multiple correct answers are possible)

a) occur if the IP communication does not work properly between a transport sender and a receiver

b) occur if there are not any errors but, at the initialization phase

c) do never occur in a proper system design

d) are difficult to detected

e) may easily be detected

Answer: a, e



**Q3**：Which of the following statements is true? (just one correct answer is possible)

a) If reliable message delivery is most important, you should use UDP instead of TCP

b) Regarding protocol overhead, TCP is more complex compared tu UDP due to e.g. connection setup

c) When using TCP, more or less 100% of the network bandwidth is used for message delivery

d) None of the other statements are true

Answer: b



**Q4**：What is the difference between fragments and segments?

a) Fragments are used to split TCP data if required by max. fragment size.

​    Segments are used when IP packets must be split according to maximum transfer unit of the underlying network.

b) Segments are used to split TCP data if required by max. segment size.

​     Fragments are used when IP packets must be split according to maximum transfer unit of the underlying network.

c) There is no difference between them. Just two names for the same.

Answer: b



**Q6**: What is correct for the Retransmission Timeout (i. e. timeout) compared the round trip time RTT ?

a) Very many duplicate packets are sent if timeout > 1*Round Trip Time

b) Very many duplicate packets are sent if timeout < 1*Round Trip Time

c) Timeout > 1*Round Trip Time

d) In case of packtes being dropped a very high timeout adds latency to the communication

Answer: b, c, d



**Q1**: The establishment of an association in SCTP allows...(multiple correct answers are possible)

a) to address one end system over different networks and network addresses

b) to set-up multiple TCP connections at the same time

c) to use stream to combine data of different media to be transmitted

d) to interconnect more than two end systems

Answer: a, c



**Q1:** What is/are the reason(s) for the usage of RTP (over UDP) for streaming applications instead of using traditional TCP?

a) RTP is more reliable than TCP

b) TCPs slow-start phase is detrimental to (i.e., is harmful for) real-time streaming applications

c) RTP provides better error detection than TCP

d) TCP does not support multicast

e) RTP can handle jitter better than traditional TCP

Answer: b, d, e





