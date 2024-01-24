#Communication Networks II
## 1. Introduction

##9. RTP & RTSP

### Real-Time

**Real-Time Process**

A process which delivers the results of the processing in a given time-span

**Deadlines in Real-Time (networked) Systems**

* Hard deadlines
  + should never be violated
  + result presented too late after deadline has no value for the user
* Soft deadlines
  + deadlines are not missed by much
  + In some cases, the deadlines may be missed, but not too many deadlines are missed



### Real-Time Transport Protocol (RTP)

#### RTP + RTCP Basics



#### Packet Format



### Real-Time Streaming Protocol (RTSP)



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





