# IT Sicherheit

## Data Link and Network Layers Security

### 1. Network, subnetwork, networks of networks(Internet)

A network is a set of two or more connected computers

Connect more computers to broadcast channel with Hub/Switch

A network can have multiple subnets

Routers connect different networks

Routers connect networks to Internet

![Screenshot_2024-06-25 00.03.31_3X0Ksn](/Users/summer/Pictures/截屏/Screenshot_2024-06-25 00.03.31_3X0Ksn.jpg)



### 2. TCP/IP layers

**Physical Layer**

+ Delivery of individual **bits** over a medium(air, wire, ...)
+ Examples: Fast Ethernet(100BASE-*), Gigabit Ethernet(1000BASE- *), ...

**Data Link Layer**

+ Delivery of **frames**
+ Identified by media access address(MAC address)
+ Examples: Ethernet, IEEE-802.11, PPP

**Internet Layer**

* Delivery of **packets** from one host to another
* Hosts are now addressable over different Networks(if e.g. IPs are unique)
* Example: IP

**Transport Layer**

+ End-to-end communication of **segments** or **datagrams**
+ Congestion Control, Packet reordering/resending, ...(for TCP)
+ Add the concept of **ports**
+ Examples: TCP, UDP

**Each layer uses the lower and services the upper layer for data transmission. 每层均使用下层并为上层提供服务，以进行数据传输**

![Screenshot_2024-06-25 00.20.50_rlufe9](/Users/summer/Pictures/截屏/Screenshot_2024-06-25 00.20.50_rlufe9.jpg)

![Screenshot_2024-06-25 00.25.19_R9o0O0](/Users/summer/Pictures/截屏/Screenshot_2024-06-25 00.25.19_R9o0O0.jpg)

**Each lower layer creates a new data unit by adding additional header information. 每个较低层通过添加附加标头信息来创建新的数据单元**

**Encapsulation: 封装**

+ Each lower layer adds at least *header* information to create new *data unit*. 每个较低层至少添加标头信息以创建新的数据单元
+ Sometimes also *trailer* information is added. 有时还会添加尾部信息
+ If the previous data unit is too big, it can be *fragmented* (split into several smaller parts). 如果前一个数据单元太大，则可以将其碎片化（分成几个较小的部分）
+ Finally, a layer passes the newly created encapsulated data unit(s) to layer below. 最后，一层将新创建的封装数据单元传递给下一层

<img src="/Users/summer/Pictures/截屏/Screenshot_2024-06-25 00.30.58_MFtLXa.jpg" alt="Screenshot_2024-06-25 00.30.58_MFtLXa" style="zoom: 50%;" />

**Devices on the route do not implement the whole stack of layers. 路由上的设备没有实现整个堆栈层**

![Screenshot_2024-06-25 00.40.55_32j0KY](/Users/summer/Pictures/截屏/Screenshot_2024-06-25 00.40.55_32j0KY.jpg)



### 3. IP and MAC addresses



### 4. Address Resolution Protocol(ARP)

### 5. Dynamic Host Configuration(DHCP)

### 6. CIDR and IP addresses' allocation

### 7. IP security

### 8. Firewalls



