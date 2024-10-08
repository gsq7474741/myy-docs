# IoT平台横向调研

| 任务名称 | MYY-43 调研-IoT平台横评           | 
|------|-----------------------------|
| 提交作者 | gsq                         | 
| 提交时间 | 2024-08-14                  | 
| 文件名  | iot_platform_investigate.md | 

# 一、概述

## 1、相关背景

MYY项目的CDP需要接收边缘硬件上报的数据，但是硬件的上报数据具有量大、高并发、连接不可靠等特点。
而且我们希望CDP与硬件解耦，不去处理具体的连接、协议、数据格式等问题，而是通过IoT平台来接收硬件数据。

因此需要选择合适的IoT平台，来处理硬件的接入、注册、管理；接收硬件上报的数据，做初步的校验、处理和转发等步骤。

## 2、意义

- 解耦CDP与硬件，降低开发复杂度
- 规避复杂的网络编程
- 不用自己搭建IoT基础设施

# 三、业内方案调研

IoT平台提供的能力可以划分为以下几个层级：

- 设备接入与管理
- 数据转发与集成
- 产品结构化建模
- 监控运维

## 1、阿里云IoT平台

阿里云物联网平台提供全托管的企业级实例服务，具有低成本、高可靠、高性能、高安全的优势，
无需自建物联网基础设施即可接入各种主流协议设备，管理运维亿级规模设备，
存储备份和处理分析EB量级的设备数据，帮助企业快速实现设备数据和应用数据的融合，
实现设备智能化升级。

使用物联网平台实现设备完整的通信链接，需要自行完成设备端的设备开发、云端服务器的开发（云端SDK的配置）、
数据库的创建、手机App的开发。在设备和服务器开发中，您需完成设备消息的定义和处理逻辑。

![架构](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5171340271/CAEQORiBgMCjo7Sz5xgiIGY5Y2Q1NWEyNjU5ZjRhNGY4ZjVmMzVhMzNmYTg3MTFj3768084_20230630102432.227.svg)

特点：

- 全套服务，涵盖从接入层到应用层之前的所有功能
- 支持多种接入方式
- 提供设备端sdk、服务端sdk和操作实例的阿里云api

评论：

- 最丐版（1000设备，上下行TPS100，转发TPS100）大陆价格866元/月（
  同时在线设备数 ¥140.00
  消息上下行TPS ¥653.00
  消息转发TPS ¥73.00）
- 功能全面，可以减少开发工作量
- 很多管理、运维、产品设计的工作可以在网页端图形化操作

## 2、EMQX

EMQX Platform 是 EMQ 推出的一款面向物联网领域的 MQTT 消息中间件产品。作为全球首个 MQTT 5.0 消息云服务，EMQX Platform
提供了一站式运维代管、独有隔离环境的 MQTT 消息服务。在万物互联的时代，EMQX Platform
可以帮助您快速构建面向物联网领域的行业应用，轻松实现物联网数据的采集、传输、计算和持久化。

![架构](https://docs.emqx.com/assets/model_3.MbJ1d4YP.png)

特点：

- 纯MQTT消息中间件，支持MQTT 5.0
- 支持规则引擎，类SQL语句处理消息
- 支持面向数据库和消息队列的数据转发

评论：

- 免费版： 100 万连接分钟、1GB流量、100万规则动作每月，支持1000 TPS、1000设备
- 产品定义和建模的工作可能需要自己做
- 只是一个转发消息处理数据的组件，需要自己搭建其他服务

## 3、Jetlinks

JetLinks物联网平台 基于Java8,Spring Boot 2.x,WebFlux,Netty,Vert.x,Reactor等开发,
是一个开源的企业级物联网基础开发平台，实现了物联网相关以及相关业务开发的众多基础功能, 能帮助你快速建立物联网相关业务系统。

在线演示地址: https://demo.jetlinks.cn (opens new window)用户名:test 密码: test123456。
测试用户未开放全部权限,建议本地运行社区版体验。

![架构](http://doc.jetlinks.cn/assets/img/platform.31731347.png)

特点：

- 开放源代码
  全部源代码开放,可自由拓展功能,不再受制于人.前后端分离,接口全开放。

- 统一设备接入,海量设备管理
  TCP/UDP/MQTT/HTTP、TLS/DTLS、不同厂商、不同设备、不同报文、统一接入，统一管理。

- 规则引擎
  灵活的规则模型配置,支持多种规则模型以及自定义规则模型. 设备告警,场景联动,均由统一的规则引擎管理。

- 数据权限控制
  灵活的非侵入数据权限控制。可实现菜单、按钮、数据三维维度的数据权限控制。可控制单条数据的操作权限。

评论：

- 支持self host，可以部署在自己的服务器上
- 开源有社区版，可以自由定制
- 还没有试用过，不知道具体的使用体验
- 转发到MQ需要付费版

# 名词解释

# 附件及参考资料

- [阿里云IoT](https://www.aliyun.com/product/iot/iot_instc_public_cn?spm=5176.29125882.J_XmGx2FZCDAeIy2ZCWL7sW.50.7ae02868K6Fmyv&scm=20140722.S_product@@%E4%BA%91%E4%BA%A7%E5%93%81@@355110._.RL_%E7%89%A9%E8%81%94%E7%BD%91-LOC_topbar~UND~product-OR_ser-V_3-RE_productNew-P0_0)
- [EMQX](https://www.emqx.com/zh/cloud/serverless-mqtt)
- [JetLinks](https://www.jetlinks.cn/#/)
