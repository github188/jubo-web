---
layout: docs
title: 设备驱动 
prev_section: iot-connector 
permalink: /docs/iot-driver/
---

jubo-iot通过设备驱动程序来识别和控制设备，根据物联网协议的不同，设备和驱动程序被分成不同的类别进行索引。
一个能够被jubo-iot运行的驱动程序应该实现以下功能:

* `init`，初始化函数，注册驱动程序到对应的连接器。
* `probe`，探测函数，当设备接入时，jubo-iot使用probe函数来判断设备是否可以被该驱动程序驱动。
* `handler`，消息处理函数，当接收到设备发出的消息时，消息中心使用该函数来处理接收到的消息。
* `properties`,设备属性组，提供设备的服务属性和属性方法。
	- device id, jubo-iot给设备分配的全局唯一标识，用来唯一标识某个设备。
	- service, 设备提供的服务，如LED灯提供了照明服务。
	- property, 服务属性，如LED灯的照明服务有亮度和颜色两种属性。
	- value, 属性值，如颜色属性值为白光。 
	- method, 属性方法，对属性进行操作。如颜色属性的属性方法为AdjustColor。
* `methods`，设备方法组，设备对外接口，jubo-iot通过这些接口操作设备。每个方法由设备ID、服务类型和属性方法组成。
	- device id, jubo-iot给设备分配的全局唯一标识，用来唯一标识某个设备。
	- service, 设备提供的服务
	- method, 属性方法，操作服务属性的方法，如AdjustColor方法提供了对颜色这个属性的操作方法。

> **PS: `methods`中服务和属性方法要与`properties`中服务和属性方法对应。**

* `observe`, 监测函数，监听和接收设备发出的消息而不经过消息中心。**该函数为可选的**。



