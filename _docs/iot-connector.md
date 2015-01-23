---
layout: docs
title: 连接器 
prev_section: iot-architecture 
next_section: iot-driver 
permalink: /docs/iot-connector/
---

一个连接器(connector)就是某种物联网协议的具体实现，例如为了支持Alljoyn协议，那么jubo-iot就需要一个实现alljoyn协议的连接器。
连接器的主要职责就是把JuBo与使用特定物联网协议的设备连接起来，为了实现这个目的，连接器需要实现以下功能:

* 设备接入，需要发现设备并获取设备信息，在找到设备匹配驱动的条件下，添加设备。
* 驱动注册，提供该协议下的驱动程序注册接口。
* 消息监测，监听该协议下设备发出的消息，收取消息后交由消息中心处理。

在设备接入时，连接器获取设备信息并保存在device.about中，about应该至少包含以下信息：

* 设备ID
* 生产厂家
* 设备描述，设备的功能描述，方便用户了解设备功能。

设备还可以通告其他任何信息给连接器，由于JuBo是根据about信息来匹配设备驱动的，因此设备通告的信息中需要包含匹配设备驱动的数据。



