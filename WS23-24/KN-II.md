#Communication Networks II
## 1. Introduction

## 2. Naming and Addressing

## 3. Transport Layer

## 4. Advanced UDP and TCP

## 5. Multipath

## 6. SCTP

## 7. Advanced Application Layer

##8. Message Passing

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

## 11. Resilience and Adaptivity

## 12. Overlay Networks



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





