# Mobile Networking

## Chapter 01, Module 01

### Frequencies for wireless communications  无线通信频率

**Wireless channel guide the signal from transmitter to receiver 无线通道将信号从发射器引导至接收器**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 16.53.46_TF6rTW.jpg" alt="Screenshot_2024-02-10 16.53.46_TF6rTW" style="zoom:50%;" />

**Electromagnetic spectrum (光谱) has variable wavelengths and frequencies 电磁波谱具有可变的波长和频率**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 16.55.46_78S4pn.jpg" alt="Screenshot_2024-02-10 16.55.46_78S4pn" style="zoom:50%;" />

**Frequencies for mobile communication is regulated by ITU-R**

* **VHF (Very high frequency, 30 - 300 GHz)** to **UHF (ultra-high frequency, 300 - 3000GHz)** -ranges for ==mobile radio== 

  + simple, small antennas for cars
  + good propagation characteristics, reliable connections

* **SHF (Super high frequency, 3 - 30GHz)** and higher for directed links, ==satellite== communication

  + small antenna, focusing the transmitted signal
  + high bandwidth available

* Wireless **LAN (local area network)** or **MAN (metropolitan area network)** use frequencies in UHF to SHF spectrum

  + some systems planned up to **EHF (extremely high frequency)**

  + limitations due to absorption by water and oxygen molecules (resonance frequencies)

    + weather dependent fading, sighnal loss caused by heavy rainfall etc.

      

### Radio propagation 无线电传播

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 17.09.17_Q9pcji.jpg" alt="Screenshot_2024-02-10 17.09.17_Q9pcji" style="zoom:50%;" />

**Singal propagation ranges 信号传播范围**

* Transmission range

  + communication possible
  + low error rate

* Detection range

  + detection of the signal possible
  + no communication possible

* Interference range 干扰范围

  + signal may not be detected
  + signal adds to the background noise

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 17.11.14_hrmHCz.jpg" alt="Screenshot_2024-02-10 17.11.14_hrmHCz" style="zoom:50%;" />

**Wave propagation modes**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 17.12.42_xeuJTz.jpg" alt="Screenshot_2024-02-10 17.12.42_xeuJTz" style="zoom:50%;" />

* Ground Waves (up to 2MHz) 地波
  + Radio transmission energy that travelling roughly follow (run parallel to) the earth's surface and is subject to surface attenuations 大致传播的无线电传输能量跟随 (平行于) 地球表面并受制于表面衰减
  + &rarr;  the lower the frequency, the less the attenuation (衰减)
* Sky Waves (3 - 30MHz) 天波
  + Radio transmission energy that is **reflected or refracted** by the ionosphere (电离层). 被电离层反射或折射的无线电传输能量
  + Sky waves will continue to reflect or refract between the earth's surface and the ionosphere until complete attenuation occurs
* Space Waves (VHF & UHF band) 空间波
  + Radio transmission energy that continues through the inonsphere (without reflection or refraction) into space
  + Space waves neither follow the curvature of the earth, nor bend around obstructions 空间波既不遵守地球曲率，也不绕障碍物弯曲

#### Signal: electromagnetic wave 电磁波

* In wireless communication, electromagnetic waves are used as a mean to transmit information

* Signal is a physical representation of data

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 17.27.44_uaKPEl.jpg" alt="Screenshot_2024-02-10 17.27.44_uaKPEl" style="zoom:50%;" />

* Radio Wave Cycle 周期

  + The interval between any two points that measures the completion of a single wave movement

* Wave Length 波长

  + The actual linear measurement, in meters, of one wave

* Amplitude 振幅

  + The strength or width of one wave &rarr;  the greater the distance from the transmitting site, the smaller this the amplitude
  + Signal strength decreases over time and distance

**Signal: Transmit Signal**

Sine wave (正弦波) is special periodic signal for a carrier 正弦波是一种特殊的载波周期信号

* Frequency is measured in Cycles/sec or Hertz
* The most important characteristic of a periodic signal, or the signal parameters are **amplitude 振幅, frequency 频率, and phase shift 相移**

$$
s(t)=A\sin(2\pi ft+\varphi)
$$

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 17.38.34_9tgx3o.jpg" alt="Screenshot_2024-02-10 17.38.34_9tgx3o" style="zoom:50%;" />

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 17.39.08_PWPaGQ.jpg" alt="Screenshot_2024-02-10 17.39.08_PWPaGQ" style="zoom:50%;" />

* Wavelength

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 17.41.09_LcqTty.jpg" alt="Screenshot_2024-02-10 17.41.09_LcqTty" style="zoom:50%;" />

  + Distance occupied by one cycle

  + Distance between two points of corresponding phase in two consecutive cycles

  + Assuming signal velocity *v* (速度)
    $$
    \lambda =vT, \lambda f=v,c=3\cdot10^8m/s
    $$

**The effects of signal propagation**

* Path loss
* Effects that causes multipath propagation
  + Shadowing
  + Reflection
  + Scattering
  + Diffraction
  + Penetration
  + Refraction



#### Path loss or path attenuation

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 17.48.06_ryI6qh.jpg" alt="Screenshot_2024-02-10 17.48.06_ryI6qh" style="zoom:50%;" />

* Strength of signal degrades with distance over transmission medium 信号强度随着距离的增加而减弱
  + The reduction of power density of an electromagnetic wave as it propagates through space
* Attenuation factors for unguided (wireless) media:
  + Received signal must have sufficient strength so that circitry in the receiver can interpret and decode the signal
  + Signal must maintain a level sufficiently higher than noise to be received without error
* Path loss is a function of frequency and distance
  + Attenuation is greater at higher frequencies 频率越高，衰减越大

**Free space path loss (FSPL) 自由空间路径损耗**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 17.57.18_KgkuBq.jpg" alt="Screenshot_2024-02-10 17.57.18_KgkuBq" style="zoom:50%;" />

* Propagation in free space:
  + FSPL for line-of-sight (LoS) communication 视距通信的自由空间路径损耗

$$
FSPL(dB)=P_t(dBm)-P_r(dBm)
$$

* If transmitter and receiver has transmit and receive antenna gain of G~t~ and G~r~, respectively, the path loss is computed using the Friis Formula
  $$
  \frac{P_r}{P_t}=G_tG_r\cdot\frac{1}{FSPL}=G_tG_r(\frac{\lambda}{4\pi d})^2=G_tG_r(\frac{c}{4\pi fd})^2
  $$

  $$
  P_r[dBm]=P_t[dBm]+G_t[dB]+G_r[dB]-FSPL[dB]
  $$

  

  + P~t~ = signal power at transmitting antenna

  + P~r~ = signal power at receiving antenna

  + d = distance between antennas

  + 入 = carrier wavelength

    + c = speed of light (~ 3x10^8^m/s)

    + f = frequency

    + $$
      \lambda=\frac{c}{f}
      $$

* FSPL for ideal isotropic antenna
  $$
  FSPL=\frac{P_t}{P_r}=(\frac{4\pi d}{\lambda})^2=(\frac{4\pi fd}{c})^2
  $$

  $$
  FSPL(dB)=20\log10(\frac{4\pi d}{\lambda})=20\log10(\frac{4\pi df}{c})
  $$

  

#### Channel capacity 通道容量

* Capacity refers to the maximum data rate for a channel
  + Data rate is the rate, in bits per second (bps), at which data can be communicated
* Channel capacity is the rate at which data can be transmitted over a given communication path, or channel, under given conditions
* Channel capacity is a function of
  + *B*: the bandwidth of the transmitted signal as constrained by the transmitter and the nature of the transmission medium, expressed in cycles per second, or Hertz
  + *S*: the average received signal power
  + *N*: the average level of noise over the communications path

**Shannon-Hartley theorem tells the maximum rate**

* Shannon-Hartley theorem computes the theoretical maximum channel capacity or rate that can be transmitted over a communication channel of specific bandwidth in the presence noise
  $$
  C[bps]=B[bps]\log_2(1+SNR)
  $$

  + C is the capacity of the channel in bits per second
  + B is the bandwidth in bits per second
  + SNR is the signal to noise ratio

* SNR (Signal-to-noise ratio) 信噪比

  + The ratio of the power in a signal to the power contained in the noise that is present at a particular point in the transmission:

    **SNR~dB~ = P~r~(dBm) - kTB(dBm)**

  + The above formula expresses the amount, in decibels, that the intended signal exceeds the noise level

  + A high SNR means high-quality signal

**Thermal Noise** 热噪声

* Also called white noise
* Due to agitation of electrons inside electrical conductor
  + Except at absolute zero temperature, the electrons in every conductor (resistor) are always in thermal motion
* Present in all electronic devices and transmission media
* Can not be eliminated
* Function of temperature of the components such as resistor
* Particularly significant for satellite communication
  + The sun contributes to the thermal noise at the receiver

**Computation of noise for SNR**

* SNR~dB~ = P~r~(dBm) - kTB(dBm)
* The amount of thermal noise to be found in a bandwidth of 1Hz in any device or conductor (导体) is:
  + **N~0~ = kT (W/Hz)**
  + N~0~ = noise power density in watts per 1 Hz of bandwidth
  + k = Boltzmann's constant = 1.3803 x 10^-23^ J/K
  + T = temperature, in kelvins (absolute temperature)
* Nosie depends on temperature and bandwidth
  + Noise is assumed to be independent of frequency
  + Noise depends on temperatue and bandwidth of the system
  + Thermal noise present in a bandwidth of B [Hz] when T = 300K is:
    + **N = kTB**
    + N[dBm] = 10log~10~(kT x 1000) + 10log~10~B
    + N[dBm] = -174[dBm] + 10log~10~B(Hz)    (when B = 1Hz)

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 19.28.38_TEPCoU.jpg" alt="Screenshot_2024-02-10 19.28.38_TEPCoU" style="zoom:50%;" />



#### Other factors that influence receive power

* Shadowing

  + power fluctuation due to objects obstructing the propagation path between the transmitter and receiver 由于物体阻碍发射器和接收器之间的传播路径而导致的功率波动

* Reflection at large obstacles

  + occurs when signal encounters a surface that is larger relative to the wavelength of the signal 当信号遇到相对于信号更大的表面时发生

* Scattering at small obstacles

  + occurs when the plane waves are incident upon an object whose dimensions are on the order of a wavelength or less and causes energy to be redirected in many directions 当平面波入射到物体上时发生尺寸约为波长或更小，导致能量在多个方向上重新定向

* Diffraction at edges

* Penetration loss

* Refraction

  

#### Multipath propagation

*  What is causing multipath propagation?
  + Signal from transmitter propagates through different paths due to reflection, scattering, diffraction
* What is the results of multipath propagation?
  + Signal arrives at the received via multiple paths, which include the line-of-sight (LoS) and the non-line-of-sight (Nlos) paths
  + Receiver receives multiple copies of different phases signal
* Advantages:
  + it allows Nlos transmitter and receiver to be able to communicate with each other

**Multipath Propagation causes ISI (inter symbol interference 符号间干扰)**

* The energy of a symbol spills over into succeeding (or adjacent) symbols, and causes interference
* The first symbol arrived at the received interfered with next symbol

**Multipath Propagation: Path loss and fading (衰退)**

* Fading is the variation in signal strength with respect to time as it is received at the antenna from the transmitter

* Two types of fading

  + **Fast fading** varies quickly with the frequency and it is a result of constructive and destructive interference patterns which is caused due to multipath 随频率快速变化，这是有多径引起的相长和相消干涉图案的结果
  + 
  + **Slow fading** varies slowly with the frequency and it is the result of signal path changes due to shadowing and obstructions such as trees or buildings 随频率缓慢变化，这是由于阴影和树木或建筑物等障碍物导致信号路径变化的结果
  
  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 23.28.01_A8O5io.jpg" alt="Screenshot_2024-02-10 23.28.01_A8O5io" style="zoom:50%;" />
  
  

### Antennas 天线



## Chapter 01, Module 02

### Modulation 调制

Modulation is a process of encoding information from a message source in a manner suitbale for transmission 调制是以适合传输的方式对来自消息源的信息进行编码的过程

**Basic types of digital modulation (keying)**

* ASK (Amplitude shift keying) 幅移键控

  + Advantage: very simple and low bandwidth requirements
  + Disadvantage: very susceptible to noise interference 非常容易受到噪音影响
  + Application: transmit digital data over optical fiber 通过光纤传输数字数据

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 23.35.39_kvZuMQ.jpg" alt="Screenshot_2024-02-10 23.35.39_kvZuMQ" style="zoom:50%;" />

* FSK (Frequency shift keying) 频移键控

  + Advantage: less susceptible to noise than ASK
  + Disadvantage: needs larger bandwidth (the bandwidth needed for FSK depends on the distance between the carrier frequencies)
  + Application: high-frequency radio transmission

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 23.39.21_0IQjFr.jpg" alt="Screenshot_2024-02-10 23.39.21_0IQjFr" style="zoom:50%;" />

* PSK (Phase shift keying) 相移键控

  + Advantage:

    + less susceptible to errors than ASK, but it uses the same bandwidth as ASK
    + more bandwidth efficient than FSK

  + Disadvantage: more complex signal detection / recovery process than ASK and FSK

  + Application: widely use in existing technologies (WLAN): **BPSK, QPSK**

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 23.42.20_hRQ7hv.jpg" alt="Screenshot_2024-02-10 23.42.20_hRQ7hv" style="zoom:50%;" />

**BPSK (Binary Phase Shift Keying) 二进制相移键控**

* The simplest modulation method

* Bit value 0: sine wave 正弦波

* Bit value 1: inverted sine wave 反正弦波

* Low spectral efficiency 频谱效率低

* Robust, used in satellite systems

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 23.46.01_y0tgmt.jpg" alt="Screenshot_2024-02-10 23.46.01_y0tgmt" style="zoom:50%;" />

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 23.46.07_usujWi.jpg" alt="Screenshot_2024-02-10 23.46.07_usujWi" style="zoom:50%;" />

**QPSK (Quadrature phase shift keying) 正交相移键控** 

* 2 bits coded as one symbol

* Symbol determines shift of sinewave

* Needs less bandwidth compared to BPSK

* Higher data rate than BPSK

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 23.47.40_OgbQWb.jpg" alt="Screenshot_2024-02-10 23.47.40_OgbQWb" style="zoom:50%;" />

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 23.47.43_b8Cmv6.jpg" alt="Screenshot_2024-02-10 23.47.43_b8Cmv6" style="zoom:50%;" />

**OFDM (Orthogonal Frequency Division Multiplexing) 正交频分复用**

* OFDM is a multi-carrier modulation

* Ten 100kHz channels are better than one 1MHz channel

* Frequency band is divided into 256 or more sub-bands

  + Orthogonal carrier is used: Peak of one at null of others

* Advantage

  + the ability to mitigate ISI
  + using this scheme, frequency selective fading only influences some subcarriers, and not the whole signal

* Eachcarrier is modulated with a BPSK, QPSK, 16-QAM etc. depending on the noise (Frequency selective fading)

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 23.53.59_Qn6l3u.jpg" alt="Screenshot_2024-02-10 23.53.59_Qn6l3u" style="zoom:50%;" />

  

### Multiplexing 多路复用

Multiplexing describes how several users can share a medium with minimum or no interference 多路复用描述了多个用户如何在最小干扰或无干扰的情况下共享媒体

**Multiplexing in 4 dimensions**

* SDM (Space Division Multiplex) 空分复用

  + Goal: multiple use of a shared medium

  + Can be achieved using

    + Beamforming 波束成形
    + Sectorization

  + The channels k1 to k3 can be mapped onto the 3 'spaces' s1 to s3 which clearly separate the channels and prevent the interference ranges from overlapping 通过k1至k3可以映射到三个通道空间s1至s3，清楚地分割通道并防止干扰范围重叠

    + Guard spaces is needed

      <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-11 00.01.28_XGrEf7.jpg" alt="Screenshot_2024-02-11 00.01.28_XGrEf7" style="zoom:50%;" />

* FDM (Frequency Division Multiplex) 频分复用

  + FDM subdivide the frequency dimension into several non-overlapping frequency bands 频分复用将频率维度细分为几个不重叠的频段

  + A channel gets a certain band of the spectrum for the whole time 信道获得特定频段的频谱全程

  + Advantages:

    + no dynamic coordination necessary 无需动态协调

  + Disadvantages:

    + waste of frequency resources if the traffic is distributed unevenly

    + the fixed frequency assignment to a sender makes the scheme very inflexible and limits the number of senders

    + Guard spaces is needed to avoid adjacent channel interference

      <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-11 00.04.49_fveNqV.jpg" alt="Screenshot_2024-02-11 00.04.49_fveNqV" style="zoom:50%;" />

* TDM (Time Division Multiplex) 时分复用

  + A channel gets the whole bandwidth for a certain amount of time 通道在一定时间内获取整个带宽

  + Advantages:

    + only one carrier in the medium at any time
    + High utilization and flexible

  + Disadvantages:

    + guard spaces, which represent time gaps, have to separate the different periods when then transmitters use the medium

    + If two transmission overlap in time, this is called co-channel interference. To avoid co-channel interference, precise synchronization is necessary

      <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-11 00.17.18_Am5uqr.jpg" alt="Screenshot_2024-02-11 00.17.18_Am5uqr" style="zoom:50%;" />

* CDM (Code Division Multiplex) 码分复用

  + Each transmitter has a unique code

  + All channels use the same spectrum (communication channel) at the same time

  + Advantages

    + bandwidth efficient
    + no coordination and synchronization necessary
    + provides good protection against interference and tapping: inherently secure

  + Disadvantages: requirements for a successful CDM

  + Implemented using spread spectrum technology

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-11 00.23.10_KW36e9.jpg" alt="Screenshot_2024-02-11 00.23.10_KW36e9" style="zoom:50%;" />

**Time and Frequency Multiplex**

* Combination of both methods
* A channel gets a certain frequency band for a certain amount of time
* Example: GSM
* Advantages
  + higher multiplexing degree
  + provides protection against tapping
  + more robust against frequency
* Disadvantages
  + precise coordination between different transmitters is required 需要不同发射机之间的精准协调

**Spread Spectrum 扩频**

Spread Spectrum techniques involve spreading the bandwidth needed to transmit data 扩频技术涉及扩展传输数据所需的带宽

**Two common types**

* FHSS (Frequency Hopping Spread Spectrum) 跳频扩频

  + The total available bandwidth is split into many channels of smaller bandwidth plus guard spaces between the channels

  + Two versions

    + Fast Hopping: multiple hops per symbol
    + Slow Hopping: more than one symbols per one frequency hop

  + Advantages 

    + frequency selective fading and interference limited to short period
    + simple implementation
    + uses only small portion of spectrum at any time

  + Disadvantages 

    + not as robust as DSSS

    + simpler to detect

    + coordination of all transmitter and their hopping sequences is required

      <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-11 00.43.47_YJc2pm.jpg" alt="Screenshot_2024-02-11 00.43.47_YJc2pm" style="zoom:50%;" />

* DSSS (Direct-Sequence Spread Spectrum) 直接序列扩频

  + XOR of the signal with pseudo-random number (chipping sequence)

    + many chips per bit results in higher bandwidth of the signal

  + Advantages 

    + reduces frequency selective fading 减少频率选择性衰落

  + Disadvantages 

    + precise power control necessary 需要精准的功率控制

      <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-11 00.46.59_twhtSh.jpg" alt="Screenshot_2024-02-11 00.46.59_twhtSh" style="zoom:50%;" />

**DSSS vs. FHSS**

* FHSS systems only use a portion of the total band, while DSSS systems always use the total bandwidth available
* DSSS systems are more resistant to fading and multi-path effects
* DSSS signals are much harder to detect (on needs to knwo the spreading code)



## Chapter 02, Module 01

### Motivation of MAC

### Contention-Free MAC

### Contention-Based MAC

### Hidden- & Exposed- Terminal Probles



## Chapter 03, Module 01

### IEEE 802 Families

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-11 23.00.54_cVpBN2.jpg" alt="Screenshot_2024-02-11 23.00.54_cVpBN2" style="zoom:50%;" />



### IEEE 802.11 Basics

* Technical standard for LAN (Local Area Networks) 局域网
* Original IEEE 802.11-1997 was at 1 and 2 Mbps
* All versions use "License-exempt" spectrum or band
* Need ways to share spectrum among **multiple users** and multiple LANs &rarr; Spread Spectrum (CDMA)
* **PHY Layer**
  + Single carrier
    + DSSS (Direct Sequence Spread Spectrum) using ISM band 
  + Multiple carriers
    + OFDM
    + OFDMA
* **MAC Layer**
  + CSMA (carrier sense multiple access)



### IEEE 802.11 Architecture

* BSA (Basic Service Area) 基本服务器
  + A cell. Each BSA may have several APs (Access Points) 每个BSA可能有多个接入点
* BSS (Basic Service Set) 基本服务集
  + Set of stations associated with one AP
* IBSS (Independent Basic Service Set) 独立基本服务集
  + Set of computers in ad-hoc mode. May not be connected to wired backbone
* DS (Distribution System) 分配系统
  + wired backbone
* ESA (Extended Service Area) 扩展服务区
  + Multiple BSAs interconnected via a distribution system 多个BSA通过分布互连系统
* ESS (Extended Service Set) 扩展服务集
  + = Set of stations in an ESA
  + Ad-hoc networks coexist and interoperate with infrastructure- based networks

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-11 23.09.56_D53m1d.jpg" alt="Screenshot_2024-02-11 23.09.56_D53m1d" style="zoom:50%;" />



## Chapter 03, Module 02

### 802.11 Medium Access Control

**Access Methods**

* DCF (Distributed Coordination Function) 分布式协调功能
  + CSMA/CA (mandatory)
    + collision avoidance via randomized "back-off" mechanism 通过随机“退避”机制避免碰撞
    + minimum distance between consecutive packets 连续数据包之间的最小距离
    + ACK packet for acknowledgment (not for broadcast) 用于确认的ACK数据包
  + DFC w/RTS/CTS (optional)
    + reduces hidden problem
* PCF (Point Coordination Function) 点协调功能
  + access point polls terminals according to a list
* HCF (Hybrid Coordination Function) 混合协调功能
  + EDCA (Enhanced Distributed Channel Access)
  + CCA (Controlled Channel Access)
    + improved polling 改进轮询

**IFS (Inter frame spacing) 帧间距**

* IFS is a time interval in which frames can not be transmitted by stations within a BSS

* This ensure that the frames do not overlap with each other

* IFS types:

  + SIFS (Short Inter Frame Spacing) 短帧间距

    + highest priority, for ACK, CTS, polling response

  + PIFS (PCF Inter Frame Spacing)

    + medium priority, for time-bounded service using PCF

  + DIFS (DCF Inter Frame Spacing)

    + lowest priority, for asynchronous data service

  + EIFS (Extended Inter Frame Spacing)

    + If a previously received frame contains an error then a station has to defer EIFS duration instead of DIFS before transmitting a frame

      <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-11 23.30.03_6UmtqM.jpg" alt="Screenshot_2024-02-11 23.30.03_6UmtqM" style="zoom:50%;" />

**Timing Intervals**

* Timing intervals are defined to control a station's access to the medium/channel
* Slot Time (A slot time)
  + 1
* SIFS (Short Inter Frame Spacing)
* PIFS (PCF Inter Frame Spacing)
* DIFS (DCF Inter Frame Spacing)

### Distributed Coordination Function (with and w/o RTS/CTS)

### Point Coordination Function

### Frame Types



## Chapter 04, Module 01

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

**Taxonomy**

* Uniform routing: all nodes behave equally
* Destination-based routing: distance vector principle
* Reactive routing:
  + Route is established on-demand
  + Source-initiated route discovery

**Route discovery cycle for route finding**

* Flood/broadcast Route Request (RREQ)
* Unicast Route Reply (RREP) along reverse path of RREQ
* Unicast Route Error (RERR)

**No overhead on data packets**

**Loop freedem is achieved through sequence numbers, also sloves "count to infinity" problem**

**AODV established the faster route, not the shortest**



**Route Discovery**

* Route discovery from source **S** to destination **D**
  + **S** broadcasts a Route Request (RREQ) &rarr; flooding
    + A RREQ must never be broadcast more than once by any node
    + Nodes set up a reverse path pointing towards the source S
  + **D** unicasts a Route Reply (RREP) to **S**
    + Nodes set up a forward path pointing to D

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-05 16.16.12_V2EoTl.jpg" alt="Screenshot_2024-02-05 16.16.12_V2EoTl" style="zoom:50%;" />

* Example Routing Table

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-05 16.17.09_XrJHyN.jpg" alt="Screenshot_2024-02-05 16.17.09_XrJHyN" style="zoom:50%;" />



**Route Maintenance**

* Timers to keep route alive
  + A routing table entry maintainging a reverse path is purged after a timeout interval
    + Timeout should be long enough to allow RREP to come back
  + A routing table entry maintaining a forward path is purged if not used for an active_route_timeout interval
    + If no data is being sent using a particular routing table entry, that entry will be deleted from the routing table (even if the route many actually still be valid)
* Destination sequence numbers (DSN): to determine fresh routes
  + To avoid using old/broken routes
  + To prevent formation of loops

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-05 16.21.50_yI3Gly.jpg" alt="Screenshot_2024-02-05 16.21.50_yI3Gly" style="zoom:50%;" />

* Movement along active path triggers action
  + If source moves, reinitiate route discovery
* When destination or intermediate node moves
  + Upstream node of the broken link broadcasts *Route Error (RERR)*
  + RERR contains list of all destinations no longer reachable due to link break
  + RERR propagated until node with no precursors for destination is reached



**Loop Formation**

* Assume that **A** does not know about failure of link **C-D** becasue Route Error (RERR) sent by **C** is lost
* Not **C** performs a route discovery for **D**, node **A** receives the RREQ (say, via path **C-E-A**)
* Node **A** will reply since **A** knows a route to **D** via node **B**
* Results in a loop (for instance, **C-E-A-B-C**)

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-05 16.57.54_icJo6d.jpg" alt="Screenshot_2024-02-05 16.57.54_icJo6d" style="zoom:50%;" />

**Loop Avoidance**

* Link failure reporting / repairing routes
  + When node **C** is unable to forward packt **P** (from node S to node D) on link (C-D), it generates a Route Error (RERR) message
  + Node **C** increments the destination sequence number for **D** cached at node **C**
  + The incremented sequence number *N* is included in the RERR, which is sent out based upon precursor lists
  + When node **S** reveives the RERR, it initiates a now route discovery for **D** using destination sequence number at least as large as *N*
* Example
  + Link failure increments the DSN at **C** (now is 10)
  + If **C** needs route to **D**, RREQ carries the DSN (10)
  + **A** does not reply as its own DSN is less than 10
  + S initiate new route discovery for D

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-05 17.14.00_PegL5w.jpg" alt="Screenshot_2024-02-05 17.14.00_PegL5w" style="zoom:50%;" />



**Other Features of AODV**

* Target networks
  + Where routing churn is high enough that proactively maintaining routes is unproductive, and that can absorb a network wide broadcast rate
  + The authors claim scalability up to 10,000 nodes
* Multiple optimizations
  + AODV-LR (Local Repair)
  + AODV-ESP (Expanding-Ring-Search)
  + Multi-path extension proposed (AODVM, AOMDV)
* Multiple open issues
  + Security
  + QoS
  + Protocol needs operational experience to discover further issues



**AODV Optimizations Gossiping**

* Flooding is very inefficient, esp. if node density is high
  + Probabilistic techniques are expected to deal better with the highly dynamic and mobile characteristics of the network
  + Probabilistic techniques may easily be adapted to network density without breaking symmetric conditions
* Gossiping as an example of epidemiological algorithm
  + Assume a large population of n people
  + A rumor is initially transmitted to one member of the population
  + This person passes (forwards) the rumor to a fixed number of confidants with probability p, the rumor is kept secret with probability 1-p (other modes possible)
* Other prominent networking applications of gossiping
  + Application level multicasting, content addressable networks
* Gossip-variants
  + General forwarding probability *p~1~*
  + Number of neighbors *n*; probability *p~2~* for *n < n~0~ , p~2~ > p~1~*
  + Hop count *k*; forwarding probability *p = 1 for k =<k~0~*
  + Number of overhead messages *m*, *p = 1 for m =< m~0~*
* Pseudo-Algorithm for Gossip (p~1~, k)
  + upon reception of message *m* at node *n*
  + if message *m* received for the first time then
    + if hop count *k* less or equal *k~0~* then
      + broadcast (m) with probability 1
    + else
      + broadcast (m) with probability *p~1~*
    + end if
  + end if
* Multiple variants implemented
  + Gossip (p~1~), Gossip (p~1~, k), Gossip (p~1~, k, m), Gossip(p~1~, k, p~2~, n) &rarr; proactive behavior, hello messages



**AODV Extension - Multipath (AODVM)**

* Multipath variants for multiple protocols
  + easy for source routing algorithms
  + not trival for optimized protocols like AODV
  + "Multipath" should not be mixed up with "Multicast"
* AODVM
  + Ad Hoc On-Demand Distance Vector Multipath (AODVM) Routing
  + Instead of dropping duplicate RREQ packets, AODVM uses an RREQ table to store the redundant RREQ information
* AODVM Explained (Path Discovery Procedure)
  + Destination initiates an RREP for each RREQ that is received (from different neighbors)
  + Nodes overhear the RREP packets
  + A node that is assigned to a route is deleted from its neighbor's RREQ tables

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-05 17.37.34_qtBh7u.jpg" alt="Screenshot_2024-02-05 17.37.34_qtBh7u" style="zoom:50%;" />



**Summary**

* At most one route per destination maintained at each node
  + After link break, all routes using the failed link are erased
* Expiration based on timeout
* Use of sequence numbers to prevent loops
* Optimizations
  + Routing tables instead of storing full routes
  + Control flooding (incrementally increase 'region')



### Dynamic Source Routing (DSR)

* Taxonomy
  + Uniform: all nodes behave equally
  + Topology-based: nodes maintain large-scale topology information
  + Reactive: establish routes on demand
* Shares some principles with AODV
  + When node **S** wants to send a packet to node **D**, but does not know a route to **D**, node **S** initiates a route discovery
  + Source node **S** floods Route Request (RREQ)
* Main differences from AODV
  + Each node appends its own identifier when forwarding RREQ
  + Nodes do not maintain routing tables



**Route Discovery in DSR**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-05 18.37.31_2buHSi.jpg" alt="Screenshot_2024-02-05 18.37.31_2buHSi" style="zoom:50%;" />

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-05 18.37.47_tDPZ3z.jpg" alt="Screenshot_2024-02-05 18.37.47_tDPZ3z" style="zoom:50%;" />



* Node H receives packet RREQ from two neighbors: potential for collision

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-05 18.37.58_Ek8sEW.jpg" alt="Screenshot_2024-02-05 18.37.58_Ek8sEW" style="zoom:50%;" />



* Node C receives RREQ from **G** and **H**, but does not forward it again, becasue node **C** has already forwarded RREQ once

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-05 18.38.06_qXX2vc.jpg" alt="Screenshot_2024-02-05 18.38.06_qXX2vc" style="zoom:50%;" />



* Node J and K both broadcast RREQ to node **D**
* Sine nodes J and K are hidden from each other, their transmissions may collide

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-05 18.38.13_uhtB8S.jpg" alt="Screenshot_2024-02-05 18.38.13_uhtB8S" style="zoom:50%;" />



* Node D does not forward RREQ, becasue node D is the intended target of the route discovery

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-05 18.38.23_mdNqZe.jpg" alt="Screenshot_2024-02-05 18.38.23_mdNqZe" style="zoom:50%;" />



**Route Discovery - Route Reply (RREP)**

* Destination **D** on receiving the first RREQ, sends a (RREP)
* RREP is sent on a route obtained by reversing the route appended to received RREQ
* RREP includes the route from **S** to **D** on which RREQ was received by node **D**
* Route Reply can be sent by reversing the route in Route Request (RREQ) only if links are guaranteed to be bi-directional
* If unidirectional (asymmetric) links are allowed, then RREP may need a route discovery for **S** from node **D**
  + unless node D already knows a route to node S
* Each node maintains a **Route Cache** which records routes it has learned and overhead over time



**Route Reply in DSR**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-05 21.19.41_rqi8fb.jpg" alt="Screenshot_2024-02-05 21.19.41_rqi8fb" style="zoom:50%;" />



**Data Delivery in DSR**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-05 21.20.38_mKwzyN.jpg" alt="Screenshot_2024-02-05 21.20.38_mKwzyN" style="zoom:50%;" />



**Route Maintenance**

* Route maintenance performed only while route is in use
* Error detection:
  + Monitors the validity of existing routes by passively listening to data packets transmitted at neighboring nodes
  + Lower level acknowledgements
* When problem detected, send Route Error packet to original sender to perform new route discovery
* Route Error is sent back to the sender the packet - original source

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-05 21.23.27_PTmpnk.jpg" alt="Screenshot_2024-02-05 21.23.27_PTmpnk" style="zoom:50%;" />



**Summary**

* Entirely on-demand, potentially zero control message overhead
* Trivially loop-free with source routing
* Conceptually supports unidirectional links as well as bidirectional links
* High packet delays/jitters associated with on-demand routing
* Space overhead in packets and route caches
* Promiscuous mode operations consume excessive amount of power



**AODV vs. DSR**

* Main common features
  + On-demand route requesting
    + Route discovery based on requesting and replying control packets
    + Broadcast route discovery mechanism
* Main differences
  + DSR can handle uni- and bi-directional links, AODV uses only bi-directional
  + In DSR, using a single RREQ-RREP cycle, source and intermediate nodes can learn routes to other nodes on the route
  + DSR maintains many alternate routes to the destination, instead of AODV that maintains at most one entry per destination
  + DSR does not contain any explicit mechanism to expire stale routes in the cache. In AODV if a routing table entry is not recently used, the entry is expired



### Location Aided Routing (LAR)

* Taxonomy
  + Non-uniform: nodes may behave differently / take distinguished roles
    + LAR: based on location &rarr; **reduces routing overhead** by limiting the number of nodes involved in network flooding
  + Geographical: utilizes geographical location in the pgysical world
* LAR exploits location information to limit scope of flooding for route discovery
  + Location information may be obtained using GPS
* **Expected Zone** is determined as a region that is expected to hold the current location of the destination node (D)
  +  Expected region determined based on previous location information, and knowledge of the destination's speed and direction
* Route requests limited to a **Request Zone** that contains the Expected Zone and location of the sender node (S)



**Expected Zone in LAR**

* S = Source node, D = Destination node
* X = last known location of node D, at time t0
* Y = location of node D at current time t1, unknown to sender S
* v = =estimated speed of D
* r = (t1 - t0) * v

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-05 22.25.19_DbR2fQ.jpg" alt="Screenshot_2024-02-05 22.25.19_DbR2fQ" style="zoom:50%;" />



**Request Zone in LAR**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-05 22.25.57_vQPuE4.jpg" alt="Screenshot_2024-02-05 22.25.57_vQPuE4" style="zoom:50%;" />



**Operation of LAR**

* Only nodes within the **request zone** forward route requestes
  + Node A does not forward RREQ, but node B does
  + Request zone explicitly specified in the route request
  + Each node must know its physical location to determine whether it is within the request zone
* If route discovery using the smaller request zone fails to find a route, the sender initiated another route discovery (after timeout) using a larger request zone
  + the largest request zone may be the entire network
* The rest of the route discovery protocols is similar to DSR
* Possible variations and optimizations
  + Loaction information is piggybacked on any message from Y to X
  + Y distributes its location information proactively



**LAR Variations - Adaptive Request Zone**

* Source explicitly specifies a request zone, but each node may modify the request zone included in the forwarded request
  + Modified request zone may be determined using more recent information and may differ from original request zone
* Implicit Request Zone
  + A node X forwards a route request received from Y if node X is deemed to be closer to the expected zone as compared to Y
  + The motivation is to attempt to bring the route request physically closer to the destination node after each forwarding

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-05 22.38.15_EL3hmo.jpg" alt="Screenshot_2024-02-05 22.38.15_EL3hmo" style="zoom:50%;" />



**LAR Variations - Query Localization**

* Limits route request flood without using physical information
  + Route requests are propagated only along paths that are close to the previously known route
  + The closeness property is defined without using physical location information
* Path locality heuristic: Look for a new path that contains at most **k** nodes that were not present in the previously known route
  + Old route is piggybacked on a Route Request
  + Route Request is forwarded only if the accumulated route in the Route Request contains at most k nodes that were absent in the old route
  + This limits propagation of the route request



**Location-Aided Routing**

* The basic proposal assumes that, initially, location information for node X becomes known to Y only furing a route discovery
  + This location information is used for a future route discovery
  + Each route discovery yields more updated information which is used for the next discovery
* LAR - Advantages
  + Reduces the scope of route request flooding
  + Reduces overhead of route discovery
* LAR - Disadvantages
  + Nodes need to know their physical locations
  + Does not take into account possible existence of obstrucitions for radio transmissions



### Optimized Link State Routing (OLSR)

* Taxonomy
  + Non-uniform: nodes nay take different roles
    + optimization aspect: reduce routing overhead by using relay node
  + Flat: non-hierarchical routing
  + Proactive: continuously maintain routing information
    + Local information is disseminated network-wide
  + Topology-based: nodes keep track of the network's topology
* Links state routing in general: Nodes ... 
  + ... periodlically flood status of their links
  + ... re-broadcast link state information received from other neighbors
  + ... keep track of link state information received from other nodes
  + ... use this information to determine next hops to destinations
* Optimization: Reduce overhead of flooding link state information
  + The broadcast from X is only forwarded by selected nodes, so-called **Multipoint relays (MPR)**
  + Usage of MPRs reduces global flooding overhead by optimizing it locally



**OLSR - Multipoint Relays**

* MPR Definitions
  + A node is selected with two rules
    + Any 2-hop neighbor must be covered by at least one multipoint relay
    + The number of multipoint relays should be minimized (per node)
  + A node forwards the flooding packets with the flollowing rules
    + Forward if the packet has not already been received
    + The node is multipoint relay of the last transmitter
* A simple heuristic for computing MPRs
  + Start with an **empty MPR set**
  + Add to the MPR set each neighbor that is the only one covering one or more 2-hop neighbor (must be an MPR anyway)
  + Until all 2-hop neighbors are covered repeat:
    + Add to the MPR set a neighbor that covers a maximum of still uncovered 2-hop neighbors



**OLSR - MPR Selection**

* Nodes E and K are multipoint relays for node H
  + Node K has forwarded the information received from H in the next step
  + E has already forwarded the same information once

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-05 23.09.39_B1ImPa.jpg" alt="Screenshot_2024-02-05 23.09.39_B1ImPa" style="zoom:50%;" />



**OLSR - Core Protocl Functionality**

* Link sensing
* MPR selection and MPR signaling
* Topology control message diffusion (Link State Message)
* Route calculation
* The OLSR standard specifies all messages + mechanisms



**Summary**

* Target networks
  + Large, dense networks
  + Low routing latency due to proactive routing
  + Various extensions exist, so-called auxiliary functions to complement the core functionality of OLSR
* Multipoint relays reduce the flooding overhead because:
  + only MPRs forward control messages
  + MPRs may flood partial link state, that is, only MPRs generate link state information including MPR Selector information
  + A MPR Selector of node X is a node which has selected its 1-hop neighbor, node X, as its multipoint relay





## Chapter 08, Module 01

### Introduction to Cellular Network (蜂窝网络)

**Basic Concept**

* AT&T Bell Labs designed a cellular structure to **reuse frequency**
* In Cellular Netowork, a **based station (BS)** transmits to and receives from mobiles station at the assigned spectrum
* When multiple base stations use the same spectrum, this scenario is known as **spectral / spatial / reuse / frequency reuse**
* The service area of each base station is called a cell typically represented by hexagonal shape
* Each mobile station is typically served by the closest base station
* When mobile station moves, it is handed over to another base station

**Cell Size**

* Macro: Sections of a city, more than 1km radius
* Micro: Neighborhoods, less than 1km
* Pico: Busy public areas, i.e., Malls airports, 200m
* Femto: Inside a home, 10m

**Why Cellular Network?**

* Sloves the problem of spectral congestion and increases user capacity &rarr; Frequency Reuse
* Offer very high capacity in a limited spectrum
* Reuse of radio channel in different cells
* Enable a fixed number of channels to serve an arbitrarily large number of users by reusing the channel throughout the coverage region



### Evolution to Cellular Network

**From 1G to 4G**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-09 01.38.21_O8IZuq.jpg" alt="Screenshot_2024-02-09 01.38.21_O8IZuq" style="zoom:50%;" />

**Evolution of Cellular Network**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-09 01.39.02_ydrrJn.jpg" alt="Screenshot_2024-02-09 01.39.02_ydrrJn" style="zoom:50%;" />

**GSM (2G)**

* GSM is European standard, adopted worldwide and increasingly in US
* Each voice band is 13kbps (versus 64kbps fiber)
* Standatd GSM has 124 channels
* Each channel is 270.8kbps carried in 200kHz
  + 8 users per channel
  + GSM can (re)use 1/3 of channels in each cell, due to good error correction
* GSM data is carried over GPRS (General Packet Radio Services), often considered 2.5G

**3G wireless**

* Worldwide standard, though frequency bands vary by region
  + Roaming phones must use different bands
  + There are a few common frequency bands worldwide
* Designed for many services
  + Real-time gaming
  + Voice
  + File download and upload
  + Video
  + Web and email
* 3G data protocols are WCDMA and HSPA
  + In broad use, continue to evolve new features
    + Supported for many years until full 4G usage
    + Data rates of 500kbps to 1Mbps typical

**4G (LTE)**

* 4G is also called LTE (long term evolution)
  + Standard is 3GPP
  + Not backward compatible with 3G
  + Entirely IP based; no voice switched traffic
  + Supports spectrum flexibility for worldwide operation
  + Handoffs at 350km/hr to support high speed rail
  + Data rates of up to 20Mbps typical
  + Scarcity of bandwidth resulting in throttling of use
* LTE appears to solve the last-mile problem for residences
  + (low / medium density) and low / medium density small business, but not high bandwidth users



### Frequency Reuse and Capacity

**Cell Structure**

* Implements **space divison multiplexing**: base station covers a certain transmission area (cell)
* Mobile stations communicate only via the base station
* Advantages of cell structures
  + higher capacity, higher number of users
  + less transmission power needed
  + more robust, decentralized
  + base station deals locally with interference, transmission area, ... 
* Characteristics
  + fixed network needed for the base stations
  + handover (changing from one cell to another) necessary
  + interference with other cells
* Cell sizes from **35km** on the country side (GSM) to some **100m** in cites - even less for higher frequencies
* Base station transmission areas overlap (safety margin to ensure full coverage). Standard model using 7 frequencies: *Cluster size, N = 7*
* Types of frequency allocation
  + **Fixed frequency allocation (FCA)**: aka Fixed frequency assignment
    + certain frequencies are assigned to a certain cell
    + Problem: different traffic load in different cells
  + **Dynamic frequency allocation (DCA)**: aka Dynamic frequency assignment
    + base station chooses frequencies depending on the frequencies already used in neighbor cells
    + more capacity in cells with more traffic
    + assignment can also be based on interference measurement
    + the allocation scheme is more complex
  + Hybrid channel allocation
    + give two sets of channels to each: a set of local channels and a set of borrowable channels
    + allow to dynamic allocate channels but with intermediate complexity



#### Cellular Frequency Reuse

**Characterizing Frequency Reuse**

* **D** = minimum distance between centers of cells that use the same frequency band (called co-channels) 使用相同频段（称为同信道）的中心之间的最小距离

* **R** = radius of a cell 半径

* **d** = distance between centers of adjacent calls: 相邻呼叫中心之间的距离
  $$
  d=R\sqrt{3}
  $$

* **N** = number of cells in repetitious pattern (Cluster) 重复模式中的细胞数

  + Reuse factor
  + Each cell in pattern uses unique band of frequencies

* Hexagonal cell pattern, following values of N possible

  + N = I^2^ + J^2^ + (I x J), I, J = 0, 1, 2, 3 &rarr; determine the relative location of co-channels

* Reuse Ratio = ReuseDistance / Radius:
  $$
  Reuse Ratio=D/R=\sqrt{3N}
  $$

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-09 19.47.17_qVK4OT.jpg" alt="Screenshot_2024-02-09 19.47.17_qVK4OT" style="zoom:50%;" />

**Frequency Reuse Notation**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-09 19.48.20_j5QmPl.jpg" alt="Screenshot_2024-02-09 19.48.20_j5QmPl" style="zoom:50%;" />

&rarr; N x S x K: 1 x 3 x 3

* N x S x K frequency reuse pattern

  + N = Number of cells per cluster 每个簇的单元数
  + S = Number of sectors in a cell 单元中的扇区数
  + K = Number of frequency allocations per cell 每个单元的频率分配数量

* Example: Capacity

  + Assume the total bandwidth, B = 25MHz and each user requires W = 30KHz, what is the number of supported users *n* if the cluster size, N = 7, and there are c = 20 cells ?

  + Answer:

    + A cluster can support 25000/30 = 833 users

    + In a cluster of seven cells each cell can support 833/7 = 119 users

    + If there are 20 cells, then the cluster can support 833/7 x 20 = 2380 users
      $$
      n=\frac{(\frac{B}{W})}{N}\cdot c
      $$
      

#### Capacity Enhancement

**Cell-splitting**

* To Accommodate a very high density of mobile subscribers, a cell can be divided into a smaller coverage area
  + This smaller cell is called microcell.
  + Microcells are traditionally used in convention centers, airports, and similar areas. 
  + A microcell can be further splitted into picocells
  + The number of handoffs is increased

**Sectorization**

* To further reduce inter-cluster interference, each cell is quite often sectored - i.e. directional antennas are used at the mobile base stations
  + A cell is normally partitioned into three 120-degree sector or six 60-degree sectors
  + The number of handoffs is increased



**Interference**

* Two types of interferences in cellular systems:
  + Co-channel interference results from the use of same frequencies in different clusters
  + Adjacent channel interference results due to usage of adjacent frequencies within a cluster
* Fractional frequency reuse
  + Users close to the BS use all subchannels
  + Users at the cell boundary use only a fraction of available subchannels



### Mobility Management

#### Handover

**Basic Principle**

* Handover: Change radio channel during communication 通信期间更改无线电频道
* Reasions for handover
  + User (mobile) is moving between cells while communicating
  + Current channel has bad radio conditions
  + Balance traffic load between cells
  + Minimize mobile power consumption and global interference level
* Handover techniques
  + Network Controlled Handoff (NCHO)
    + Link quality is only monitored by the serving BS and the surrounding BSs
    + The handoff decision is made under the centralized control of a mobile telephone switch
  + Mobile Assisted Handoff (MAHO): Network Control with MS assisting
    + Both the serving BS and MS measure link quality
    + Link quality measurements of the alternate BSs are only obtained by the MSs
    + The MS periodcally relays the link quality measurements back to the serving BS
  + Mobile Controlled Handoff (MCHO)
    + Link quality is measured by both BS and the MS
    + Like MAHO, the measurements of link quality for alternate BSs are done at the MS, and both inter and intracell handoffs are supported
    + Unlike MAHO, the link measurements at the serving BS are relayed to the MS, and the handoff decision is made by the MS



#### Handover Phases

1. Monitoring and lin (signal quality) measurement

   + Performed continuously
   + In GSM: done by mobile, data sent to network ~2x per second
   + Parameters:
     + RSSI - Reveived signal strength indication
     + BER - Bit error rate
     + Distance to base station
     + BS identity

2. Target cell determination and handover triggering

   + Handover triggering algorithms

     + a) Relative signal strength

       + Selects the strongest received BS at all times 始终选择最强的接收BS
       + The decision is based on a mean measurement of the received signal 该决定基于接收信号的平均测量
       + The handoff would occur at position A
       + Disadvantages: provode too many unnecessary handoffs

     + b) Relative signal strength with threshold 相对信号强度与阀值

       + Allows a MS to handoff only if the current signal is sufficiently weaker/lesser than the threshold and the other is the stronger of the two 仅当当前信号足够弱/小于阀值且另一个信号是两者中较强的信号时，才允许MS进行切换
         + If threshold is T1, the handoff occur immediately when the signal strenght of BS2 is larger, which is at position A
         + If the threshold is T2, handoff only occur when the signal is lower than T2, which is at position B
         + If the threshold is T3, handoff occurs when the signal is lower than T3, which is at position D
       + If threshold is set too low, handoff doesn't occur fast enough so call dropped may occur

     + c) Relative signal strength with hysteresis

       + If new signal > current signal + hysteresis margin *h*, select new BS pos. C

       <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 03.20.08_XhoP3y.jpg" alt="Screenshot_2024-02-10 03.20.08_XhoP3y" style="zoom:50%;" />

3. Handover execution procedures

   + Hard handover
     + Radio link to existing base station is released before radio link to new base station is established
     + Network link is established in advance (from switch/router to base station)
     + Interruption of data flow
     + Mobile only needs to support 1 radio channel
   + Seamless handover
     + Radio link to existing base station is released after radio link to new base station is established
     + For a short period, 2 radio links are available, during which network link is switched
     + No interruption of data flow
   + Soft handover
     + => 2 radio links are available and active for a relatively long period of time
     + Data is flowing over 2 (or more) radio links simultaneously
     + Improved Quality of Service

**Handover Failures**

In the link transfer procedure, there are several reasons why handoff hailures occur:

* No channel is available on the selected BS
* Handoff is denied by the network for reasons such as lack of resources, e.g., the MS has exceeded some limit on the number of handoffs that may be attempted in a period of time
* It takes the network too long to set up the handoff after it has been initiated
* The target links fails in some way during the execution of the handoff

**Types of Handover Flows**

1. Intra-cell handover

   + Same base station, different channel (e.g., to avoid interference between users within the same cell)

2. Inter-cell handover

   + Other base station (to avoid call drop due to coverage range)

3. Inter-system handover

   + Another technology (e.g., between 3G and LTE, to avoid call drop due to change of system)

     <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 03.32.49_a3Wm7F.jpg" alt="Screenshot_2024-02-10 03.32.49_a3Wm7F" style="zoom:50%;" />

**Layered cell structure**

* Small cells
  + High capacity
  + Many handover for fast-moving mobiles
* Large cells
  + Limited capacity
  + Fewer handover
* Solution
  + Layered Cell Structures



## Chapter 08, Module 02

### Towards LTE

In Nov. 2004, 3GPP began a project to define the long-term evolution (LTE) of Universal Mobile Telecommunications System (UMTS) cellular technology

* Higher performance
* Backwards compatible
* Wide application

**Network Solutions from GSM to LTE**

* GSM: developed to carry real time services, in a circuit switched manner
* GPRS: the first step towards an IP-based packet switched solution
  + Developing UTRAN and WCDMA to achieve higher data rates
* EPS (Evolved Packet System): Purely IP-based
  + A flat, all-IP architecture with separation of control plane and user plane traffic
  + Composed with E-UTRAN/LTE and packet-switched EPC (Evolved Packet Core)

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 14.10.40_KJ7HGN.jpg" alt="Screenshot_2024-02-10 14.10.40_KJ7HGN" style="zoom:50%;" />

**LTE Access Network**

* LTE access network is a network of base stations, evolved NodeB (eNB), generating a flat architecture
* No centralized intelligent controller
* eNBs are inter-connected via X2 interface
  + Speed up connection set-up
  + Reduce the time required for a handover
* Each eNB is connected to the core network via S1 interface

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 14.14.27_mc2hA3.jpg" alt="Screenshot_2024-02-10 14.14.27_mc2hA3" style="zoom:50%;" />

**IP-Based Flat Network Architecture**

* Flat - Less hierarchical and fewer nodes
* All services (Voice/multimedia) over IP
* For backward compatibility some non-IP protocols and services are still used in LTE network

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 14.28.57_KpOCfj.jpg" alt="Screenshot_2024-02-10 14.28.57_KpOCfj" style="zoom:50%;" />

**Evolved Packet Core (EPC)**

Four new elements:

* Serving Gateway (S-GW): Demarcation point between RAN and Core. Serves as mobility anchor when terminals move
* Packet Data Network Gateway (P-GW): Termination of EPC towards Internet or IMS network. IP services, address allocation, deep packet inspection, policy enforcement
* Mobility Management Entity (MME): Loaction tracking, paging, roaming, and handovers. All control plane functions related to subscriber and session management
* Policy and Charging Rules Function (PCRF): Manages QoS

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 14.39.53_YntQ27.jpg" alt="Screenshot_2024-02-10 14.39.53_YntQ27" style="zoom:50%;" />

**Evolved Packet System (EPS)**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 14.40.38_eC03dT.jpg" alt="Screenshot_2024-02-10 14.40.38_eC03dT" style="zoom:50%;" />



### LTE Key Features

* Long Term Evolution, 3GPP Release 8, 2009
* The Evolved Packet System (EPS) is purely IP based
* 3.9G (Pre-4G) cellular technology. Sold as 4G by some providers
* 4G = International Mobile Telecommunication (IMT) Advanced Requirements in ITU M. 2134-2008
* Many different bands: 700 / 1500 / 1700 / 2100 / 2600 MHz
* Flexible & large bandwidth: 1.4 / 3 / 5 / 10 / 15 / 20 MHz
* Frequency Division Duplexing (FDD) and Time Division Duplexing (TDD)
  + Both paired and unpaired spectrum
* 4x4 MIMO, Multi-user collaborative MIMO
* Beamforming in the downlink
* Data Rate: 326 Mbps/down 86 Mbps up (4x4 MIMO 20 MHz)
* Modulation: OFDM with QPSK, 16 QAM, 64 QAM
* OFDMA downlink, Single Carrier Frequency Division Multiple Access (SC-FDMA) uplink

* A multicarrier approach for multiple access that was chosen by 3GPP scheduling in both time and frequency domain
* Hybrid ARQ Transmission for rate adaptation
* Short Frame Sizes of 10ms and 1ms faster feedback and better efficiency at high speed
* Persistent scheduling to reduce control channel overhead for low bit rate voice transmission
* IP based flat network architecture

**OFMDA Downlink**

* Transmitter at based station: IFFT converts frequency to time

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 14.58.53_QsHeZw.jpg" alt="Screenshot_2024-02-10 14.58.53_QsHeZw" style="zoom:50%;" />

* Receiver at user terminal: FFT converts time to frequency

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 14.58.30_xjFTMN.jpg" alt="Screenshot_2024-02-10 14.58.30_xjFTMN" style="zoom:50%;" />

* OFDM

  + Each carrier modulated according to specific channel condition
  + High variation of power levels
  + has high peak-to-average power ratio (PAPR)
  + higher cost of amplifiers

* Amplifiers are linear only over a restricted region

  + costly amplifier or reduce average signal power significantly
  + can afford such amplifiers in base stations but not in mobiles

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 15.04.23_xgPiOh.jpg" alt="Screenshot_2024-02-10 15.04.23_xgPiOh" style="zoom:50%;" />

**SC-FDMA**

* Single-Carrier Frequency Division Multiple Access

* OFDMA causes high power consumption for signal generation but handheld devices have limited power capacity thus SC-FDMA is used at the receiver

* Each user get contiguous subset/part of the channel

* Uses single carrier modulation and adds a cyclic prefix

* Lower PAPR

  + Single carrier, therefore not much variation in amplitude

* Better for uplink because slight mis-synchronization among users does not affect the decoding significantly

* With OFDMA, each user's subcarriers are spread all over the band and may affect other users subcarriers all over the band

* Transmitter at the user termianl

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 15.08.42_IJIc1u.jpg" alt="Screenshot_2024-02-10 15.08.42_IJIc1u" style="zoom:50%;" />

* Receiver at the base station

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 15.08.19_xTT4Vm.jpg" alt="Screenshot_2024-02-10 15.08.19_xTT4Vm" style="zoom:50%;" />

**LTE Frame Structure**

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 15.45.50_uGJAYj.jpg" alt="Screenshot_2024-02-10 15.45.50_uGJAYj" style="zoom:50%;" />

* Subframe = 2 slots of 0.5ms for DL and 0.5ms for UL

* 1 Slot = 6 or 7 symbols of 66.7us each

* Normal Cyclic Prefix: 5.2us for 1^st^ symbol, 4.7us for others

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 15.47.50_4axBpV.jpg" alt="Screenshot_2024-02-10 15.47.50_4axBpV" style="zoom:50%;" />

* Extended Cyclic Prefix: for larger networks. 16.7us

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 15.47.40_v4HURp.jpg" alt="Screenshot_2024-02-10 15.47.40_v4HURp" style="zoom:50%;" />

**Resource Allocation**

* Time slot: 0.5ms 6 or 7 OFDM symbols
* Subcarrier: 15kHz
* Physical Resource Block: 12 subcarriers (180 kHz) over 1 time slot
* Minimum Allocation: 2PRBs per subframe

**LTE Resource Grid**

* Two slots form a subframe with a duration of 1 millisecond
* A subframe represents the LTE scheduling time, which means that at each millisecond the eNB decides as to which users (UEs) are to be scheduled and which RBs are assigned to which user
* The number of parallel RBs in each subframe depends on the system bandwidth
  + If a 10MHz carrier is used (15kHz for each subcarrier) &rarr; 600 subcarriers are available &rarr; 50RBs
* To enable mobile devices to detect LTE carriers during a network search and to estimate the channel quality later on, reference symbols are inserted with predefined pattern (there are 504 different patterns exists)

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 15.53.14_NNTfnC.jpg" alt="Screenshot_2024-02-10 15.53.14_NNTfnC" style="zoom:50%;" />

**ARQ (Automatic Repeat reQuest)**

* Retransmit a packet if it is received in error

* Previous (bad) bits are discarded

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 15.54.32_EqxSFy.jpg" alt="Screenshot_2024-02-10 15.54.32_EqxSFy" style="zoom:50%;" />

* Hybrid-ARQ

  + PHY and MAC layers work together &rarr; Hybrid

  + PHY layer sends some bits first (uses puncturing)

    + Sends additional bits only if necessary
    + Additional bits are sent until the decoding is successful (Incremental redundancy or Type II H-ARQ)
    + Another alternative is to combine the good bits of multiple transmissions (Chase combining or Type I H-ARQ)

    <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 15.57.00_Ju9ldK.jpg" alt="Screenshot_2024-02-10 15.57.00_Ju9ldK" style="zoom:50%;" />

    

## Chapter 09, Module 01

### WSN (Wireless Sensor Networks)

**Sensor Nodes: Common Architecture**

Sensor nodes usually contain a variation of these components:

* MCU: embedded processor, usually running a real-time OS, limited memory and processing power. Often low-power optimized

* Radio Module: Communication with the WSN, controlloed by the MCU

* Power Supply: Often USB for development, battery for deployment. Constaints energy budget. Supply of other components (sensors, radio) often can be cut off if not used

* Sensors: Strongly application-dependent, to gather data from the environment

  <img src="/Users/summer/Pictures/截屏/Screenshot_2024-02-10 16.33.52_wUEtZx.jpg" alt="Screenshot_2024-02-10 16.33.52_wUEtZx" style="zoom:50%;" />

**WSN Applications: GDI (Great Duck Island Project)**

WSNs offer a non-intrusive observation methodology

* Large spatial and temporal dataset
* Correlation with climate and occupancy data
* Near real-time data access

Result from the GDI Project

* High energy efficiency: 2% duty cycle
* Low throughput: reading every 20 min.
* Low reliability: 30% - 70%
* High latency



### IoT (Internet of Things)

* The idea behind this term:
  + take a physical, real-world object enable it with communication technology make it available on the Internet
* Focus: Make device available on the Internet, allow interaction with other Things or humans
  + "Internet" as main enabler for connectivity and interaction
  + Connecting to the Internet more important than direct communication
  + Spatial coverage not by devices themselves

**IoT: Network Architecture**

* WSNs make use of mesh topologies to cover larger areas, requiring multi-hop wireless protocols

* In the IoT, devices more often talk directly to the gateway/base station/...:

  + Cellular Netwokrs

  + LPWANs (LoRaWAN, Sigfox, NB-IoT, ...)

  + WiFi or ZigBee

    

### WSN vs. the IoT

* Same:

  + Embedded devices
  + Wireless communication (BTLE, 802.15.4, LoRa, ...)

* Different:

  + WSNs

    + Single & Special Purpose Network (Non-IP Network)
    + Homogeneous Sensor Devices
    + Mesh / Multi-Hop Networks
    + Measuring External Phenomena

  + IoT

    + General Network Infrastructure (Internet) (IP-Network)

    + Heterogeneous Devices

    + Often: Node-Gateway-Internet

    + Create Virtual Representation of Physical Device

      

## Chapter 09, Module 02

### The Glossy Protocol

* One-to-All Communication, Goals:

  + Network-wide flooding using constructive interference
  + Free network-wide time-sychronization with us precision
  + High packet reliability while maintaing low latency and low energy consumption

* Basic Protocol:

  + All nodes wake up simultaneously and periodcally for communication

  + Multiple nodes broadcast the same packet concurrently

  + Result: wave-like flooding

    

#### Propagation in Glossy



### Physical Layer Properties



### Outlook: Other WSN Protocols



## Chapter 09, Module 03

## Chapter 09, Module 04

## Chapter 09, Module 05



VHF, 30-300

UHF, 300-3000

for mobile radio, car

SHF, 3-30. 

for satellite communication

EHF, 30-300



transmission range, communication possible

detection range, detection of signal possible, no communication possible

interference range, signal may not be detected, signal only adds to the background noise

ground wave, the radio transmission energy that travelling roughly follow the earth's surface and it subject to surface attenuations.

sky wave, the radio transmission energy that is reflected or refracted by the ionosphere.

space wave, the radio transmission energy that continues through the ionosphere without reflection or refraction into space.

path loss, strength of signal degrades with distance over transmission medium.

impact FSPL, the distance between transmitter and receiver; the carrier frequency

Shadowing, power fluctuation due to objects obstructing the propagation path between the transmitter and receiver.

scattering, occurs when the signal encounters a surface that is larger relative to the wavelength of the signal.

slow fading, varies slowly with the frequency, it is the result of signal path changes due to shadowing and obstruction.

fast fading, varies quickly with the frequency, it is the result of constructive and destrucitve interference patterns.

Omni-directional antenna, radiates power in all directions

directional antenna, directs power in a specific, desired direction

isotropic antenna, radiates power in all directions equally.

ASK,amplitude, low bandwidth, susceptible to noise interference

FSK, less susceptible, larger bandwidth

PSK, less susceptible to error, more bandwidth efficient, more complex signal detection/ recovery process

SDM, multiple use a shared medium, guard spaces necessary

FDM, a channel gets a certain band of spectrum for the whole time, no dynamic coordination necessary, waste of frequency resources, guard spaces necessary

TDM, a channel gets the whole band of spectrum for a certain amout of time, high utilization and flexible, if two transmission overlap in time, it called "co-channel", to avoid this, precise synchronization is necessary.

CDM, all channels use the same band of spectrum for the same time, bandwidth efficient, requirements for a successful CDM

DSSS, robust against narrow-band interference, low data rate in terms of the used bandwidth

Pured ALOHA, use ACK, allows nodes to access the medium immediately.

Slotted ALOHA, a station may commence transmission only at predefined points in time, synchronization is necessary

mmWave can provide high-speed communication thus ensuring low delay. online gaming, smart home

large bandwidth, small antenna footprint, low interference

very high reflection on most surfaces, high scattering on rough surfaces, prone to blockage as it has high penetration loss, very low diffraction

device discovery, neighbor discovery, beam discovery, beam tracking

beam training, allows the device to use a fine directional beamforming mode with higher gain.

beam tracking, it ensures the optimality of the fine diectional beamforming mode. with this phase, the optimality of the fine diectional beamforming modes is checked over time to account for slow variations in the channel or device mobility.

divides the network into piconets with each piconet having a piconet controller. not suitable for large network, beacuse this would incur a high overhead at piconet controller to schedule the tansmission of all decives.

CBAP: is used for nodes that want to access using contention-free

SP: is used to enable the simultaneous communication of multiple scheduled links 

highly directional beam steering at mmWave frequencies is sensitive to blockage of the beam.

reinitialize the links by perfoming beam discovery.

multiple beams are maintained between transmitter and receiver

other nodes are used to route signals around blockages when the direct path is blocked.

either transmit or receive but not both at the same time

the relay can listen/recive and retransmit at the same time

continuous data streaming, wireless speakers, wireless headset

short burst data transmission, sport&fitness devices, health&wellness devices

Scatternet, increase the network throughput, consist of two or more interconnected piconets

joins more than one piconet

can only be active in one piconet at a time

timeshare and must be synchronize to the master of the current piconet

Frequency Hopping, shares channel with WiFi networks, which caused it to experience more interference, robust against narrow-band interference, co-existence

AFH, avoid interference in WiFi and similar environment to improve reliability.

BLE optimization: short packets, delay and piggybacked acknowledgements, low overhead in packets

Bluetooth mesh, many-to-many communication

ZigBee WPAN requirement, no infrastructure, battery power

FFD, a device that can become a coordinator if it starts a PAN

RFD, a device that can not become a coordinator

extended address 64bit

short address 16bit

beam-enabled mode, coordinator sends beacon periodically

non-beam mode, coordinator do not send beacons, therefore there's no superframe structure.

4 common topologies, star, tree, cluster tree, mesh

ZigBee Coordinator, selects channel, starts network, assigns short addresses to other nodes

ZigBee Router, nodes that can route packets to/from other nodes

ZigBee End-Device, can sleep to extend battery life, not capable of being coordinator, router, or leaf node.

Cskip address assignment, address is guaranteed conflict-free, a node can tell from the addres whether it's a descendant or not, does not support the tree with depth larger than 5.

stochastic scheme, parent draws a 16bit random number between 0 and 2^16^-1, a new number is drawn if the result is all-zero or all-one, parent then broadcasts the number to the network 4 times

ZigBee Routing: broadcast, tree routing, mesh routing, source routing

AODV, uniform, reactive, destination-based, established the faster route.

RREQ, Route Request (broadcast), RREP Route Reply (unicast), RERR, Route Error (unicast)

route discovery, node S broadcasts a Route Request, node D unicasts a Route Reply to node S

Timer to keep route alive

a routing table entry maintaining a reverse/forward path is purged after a timeout interval.

DSN, to prevent formation of loops, to avoid old/broken routes, to determine fresh routes

DSR, uniform, reactive, topology-based

route discovery, node S broadcasts a Route Request, each node appends its own identifier when forwarding RREQ, node D on receving the first RREQ, sends a RREP

error detection, when problem detected, send a Route Error packet to original sender to perform a new route discovery.

LAR, non-uniform, based on location, geographical, 

LAR exploits location information to limit scope of flooding, only nodes within the Request Zone forward Route Request, if route discovery using the smaller zone fails to find a route, the sender initiates another route discovery (after timeout) using a larger request zone.

reduce the scope of route request flooding, reduce overhead of route discovery, nodes need to know their physical location.

OLSR, non-uniform, proactive, topology-based

small cell, increase capacity and data rate, higher depolyment costs

handover to change radio channel during communication

why: current channel has bad radio conditions, user is moving between cells while communicating

NCHO: link quality is only monitored by the serving BS and surrounding BSs

MAHO: network control with MS assisting, both the serving BS and MS measure link quality

MCHO: link quality is measured by both BS and MS

A: if threshold is T1, the handoff occur immediately when the signal strength of BS2 is larger

B: if threshold is T2, the handoff only occur when the signal is lower than T2

D: if threshold is T3, the handofff only occur when the signal is lower than T3

C: if new signal > current signal + hysteresis margin h, select new BS

Antenna footprint at mmWave frequencies is very small. It's possible to implement high-data-rate mmWave communication using multiple antenna technology in mobile devices.

Due to the directional transmission, its coverage area is limited, thus mmWave systems need to perform beam training for device discovery. 









 
