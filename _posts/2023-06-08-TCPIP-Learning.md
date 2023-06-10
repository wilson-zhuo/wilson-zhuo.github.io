---
layout: post
title: TCP/IP协议学习
subtitle: TCP/IP协议簇
gh-repo: NA
gh-badge: [star, fork, follow]
tags: [互联网技术]
comments: false
---
* content
{:toc}
TCP (Transmission Control Protocol)和UDP(User Datagram Protocol)协议属于传输层协议。其中TCP提供IP环境下的数据可靠传输，它提供的服务包括数据流传送、可靠性、有效流控、全双工操作和多路复 用。通过面向连接、端到端和可靠的数据包发送。通俗说，它是事先为所发送的数据开辟出连接好的通道，然后再进行数据发送；而UDP则不为IP提供可靠性、 流控或差错恢复功能。一般来说，TCP对应的是可靠性要求高的应用，而UDP对应的则是可靠性要求低、传输经济的应用。 TCP支持的应用协议主要有：Telnet、FTP、SMTP等； UDP支持的应用层协议主要有：NFS（网络文件系统）、SNMP（简单网络管理协议）、DNS（主域名称系统）、TFTP（通用文件传输协议）等。 TCP/IP协议与低层的数据链路层和物理层无关，这也是TCP/IP的重要特点




# 网际互联协议模型
|OSI七层参考模型|TCP/IP五层模型|主要协议|各层解释|
|--------------|-------|-------|-----------|
|应用层|应用层|HTTP,TFTP,NFS,WAIS,SMTP|为应用程序提供服务|
|表示层|应用层|Telnet,Rlogin,SNMP,Gopher|数据格式转化,数据加密|
|会话层|应用层|SMTP,DNS|建立,管理和维护会话|
|传输层|传输层|TCP,UDP|建立,管理和维护端到端的连接|
|网络层|网络层|IP,ICMP,IGMP,UUCP,ARP,RARP,AKP|IP地址及路由选择|
|数据链路层|链路层|FDDI,Ethernet,Arpanet,PDN,SLIP,PPP|提供介质访问和链路管理|
|物理层|物理层|IEEE 802.1A,IEEE 802.2到IEEE 802.11|提供物理链路|
![OSI网络参考模型_20230608](https://cdn.staticaly.com/gh/wilson-zhuo/pic_public@main/OSI网络参考模型_20230608.tpmpvppeodc.webp)
## 物理层
作用：定义一些电器，机械，过程和规范，如集线器;  
PDU(协议数据单元)：bit/比特  
设备：集线器HUB;  
注意：没有寻址的概念;  
## 数据链路层
作用：定义如何格式化数据，支持错误检测;  
典型协议：以太网，帧中继(古董级VPN) 
PDU：MAC frame（帧）设备：以太网交换机;  
备注：交换机通过MAC地址转发数据，逻辑链路控制;  
## 网络层
作用：定义一个逻辑的寻址，选择最佳路径传输，路由数据包;  
典型协议：IP，IPX，ICMP,ARP(IP->MAC),IARP;  
PDU:IP packet/IP数据包;  
设备：路由器;  
备注：实现寻址;  
## 传输层
作用：提供可靠和尽力而为的传输  
典型协议：TCP,UDP,SPX,port(65535个端口),EIGRP,OSPF  
PDU:fragment 段  
无典型设备  
备注：负责网络传输和会话建立,建立应用程序间的通信管道;  
## 会话层
作用：控制会话，建立管理终止应用程序会话  
典型协议: RSVP(资源预留协议)  
备注：负责会话建立;  
## 表示层
作用：格式化数据；
典型协议：ASCII, JPEG. PNG, MP3. WAV, AVI  
备注：可以提供加密服务  
## 应用层
作用：控制应用程序  
典型协议：telnet, ssh, http, ftp, smtp, rip, BGP...   
备注：为应用程序提供网络服务;  
## 物联网应用层协议(base TCP/IP)
### IOT网络模型
![IOT拓扑_20230608](https://cdn.staticaly.com/gh/wilson-zhuo/pic_public@main/IOT拓扑_20230608.3ltew2jhhue0.webp)
### MQTT(Message Queuing Telemetry Transport)
消息队列遥测传输协议（MQTT : Message Queuing Telemetry Transport）是为大量计算能力有限，工作带宽有限、网络环境不可靠的传感器或控制器而设计的协议。  
　　MQTT是IBM针对物联网推出的一种轻量级协议，建立于TCP/IP层协议之上。其是物联网的重要组成部分，可能会成为物联网的事实标准。其具有QoS，能够缓冲消息，并通过重传机制保证终端设备收到消息；其消息格式极其简化，最短是两个字节；其提供订阅和发布模式，高效推送消息。  
　　MQTT协议原来是IBM开发的一个即时通讯协议，基于TCP协议实现，相比来说比较适合物联网场景的通讯协议。MQTT客户端需要通过消息代理（MQTT Broker）来进行消息的发布和订阅。  
　　MQTT协议采用发布/订阅模式，所有的物联网终端都通过TCP连接到云端，云端通过主题的方式管理各个设备关注的通讯内容，负责将设备与设备之间消息的转发。  
　　MQTT协议的兼容性非常好，几乎支持所有平台，可以把各种物联网设备都连接起来。所以MQTT协议也是目前应用最广泛的物联网应用层协议。  
　　MQTT有三个角色，包括服务器代理、订阅者和发布者。  

　　（1）启动服务器代理。  

　　（2）订阅者向服务器代理订阅相关主题。  

　　（3）发布者向服务器代理发布主题信息。  

　　（4）服务器代理想所有订阅该主题的订阅者推送消息。  

　　MQTT有C/C++语言和JAVA包实现。需要明确的是，MQTT更适用于设备终端和手机APP socket通信，而不能支持浏览器使用。如果要支持微信浏览器应用，还需要增加类似WebsocketServlet技术给浏览器提供支持，这时MQTT以JS接口进行封装，并被调用完成消息推送。  
　　适用范围：在低带宽、不可靠的网络下提供基于云平台的远程设备的数据传输和监控。MQTT协议一般适用于设备数据采集到端（Device-》Server，Device-》Gateway），集中星型网络架构（hub-and-spoke），不适用设备与设备之间通信，设备控制能力弱，另外实时性较差，一般都在秒级.  
![MQTT_20230608](https://cdn.staticaly.com/gh/wilson-zhuo/pic_public@main/MQTT_20230608.saq3ui2x70g.webp)
### AMQP(Advanced Message Queuing Protocol)
　　高级消息队列协议（AMQP：Advanced Message Queuing Protocol）是一个提供统一消息服务的应用层标准高级消息队列协议，为面向消息的中间件设计，这是OASIS组织提出的，该组织曾提出OSLC（Open Source Lifecyle）标准，用于业务系统例如PLM，ERP，MES等进行数据交换。  
　　AMQP的工作原理与MQTT类似，也是基于发布-订阅机制。消息代理Broker的交换机组件（Exchange）会把接收到的消息，根据消息的主题，分配到不同的队列中，以便订阅者接收。  
　　RabbitMQ就是在AMQP协议基础上实现的一个消息系统，遵循Mozilla Public License开源协议。RabbitMQ在互联网应用中常被用作消息服务器。  
　　适用范围：最早应用于金融系统之间的交易消息传递，在物联网应用中，主要适用于移动手持设备与后台数据中心的通信和分析。  
