# 数据库调研（阿里云RDS、Influx、自建）

| 任务名称                                                   | MYY-25 调研-阿里云RDS数据库        | 
|--------------------------------------------------------|----------------------------|
| 提交作者<input type="checkbox" class="rowselector hidden"> | gsq                        | 
| 提交时间<input type="checkbox" class="rowselector hidden"> | 2024-08-13                 | 
| 文件名                                                    | aly_rds_investigate.md<br> | 

# 一、概述

## 1、相关背景

MYY的CDP需要数据库存储边缘硬件的传感器、执行器、控制器的原始数据，也需要在原始数据上进行加工。
IoT设备产生的本质上是时序数据，时序数据有专用的时序数据库，例如InfuxDB、TimescaleDB等。
但是我们的应用中需要考虑到数据量的大小、数据类型、数据源的多样性、数据处理的复杂度、数据安全性等因素，因此需要选择合适的数据库。

## 2、意义

- 选择合适的数据库能够提高数据处理的效率、降低成本、提高数据安全性、提高数据可靠性。
- 选择合适的数据库能够降低开发和维护的难度。
- 选择合适的数据库能够提高数据的可用性、可扩展性、可维护性。

# 三、业内方案调研

描述业内一般如何实现此功能，包括与此功能相关的现状、未来趋势；

对调研的方案进行对比**评价**和**对比分析**，论述各种方案的优劣势。
tbd

## 1、阿里云RDS数据库

阿里云关系型数据库RDS（Relational Database Service）是一种安全稳定可靠、高性价比、可弹性伸缩的在线数据库服务。RDS支持MySQL、SQL
Server、PostgreSQL和MariaDB引擎，并且提供了容灾、备份、恢复、监控、迁移等方面的全套解决方案，帮助您解决数据库运维的烦恼。

特点：

- 是关系型数据库，支持SQL语言。
- 支持多种数据库引擎
- 不需要关心物理机和组网层面的问题，开箱即用
- 有severless模式，可以根据业务需求自动伸缩

评论：

- 适合关系型数据，不适合时序数据
- 我们的数据量是否适合RDS？
- 对于大量的硬件实例，如何设计库表结构？
- 最丐版的香港serverless实例价格是2块钱/小时

## 2、阿里云InfluxDB

云数据库 InfluxDB 版是一款专门处理高写入和查询负载的时序数据库，完全兼容开源InfluxDB
1.8版本，用于存储大规模的时序数据并进行实时分析，包括来自DevOps监控、应用指标和IoT传感器上的数据。

特点：

- InfluxDB®是您处理时序数据的一个绝佳选择，目前有以下特点：
- 专为时间序列数据量身打造的高性能数据存储。TSM引擎提供数据高速读写和压缩等功能。
- 简单高效的HTTP API写入和查询接口。
- 针对时序数据，量身打造类似SQL的查询语言，轻松查询聚合数据。
- 允许对tag建索引，实现快速有效的查询。
- 数据保留策略（Retention policies）能够有效地使旧数据自动失效。

评论：

- 4v16g起步，只能包年包月，港区丐版878元/月，北京区丐版是591元/月。
- 成本比较高，不知道当数据规模大到什么程度时，成本对比RDS会有优势。
- 存储桶的抽象模式，不像库表，在设计数据架构时和关系型数据库有很大不同。
- 时序数据的查询和分析，需要学习新的查询语言。

## 3、自建数据库

自建数据库是指自己搭建数据库服务器，自己管理数据库的运维、备份、恢复、监控等工作。
可以考虑购买物理机、虚拟机、容器等资源，安装数据库软件，自己管理数据库。
但是购买虚拟机的价格比较高，买二手物理服务器自行搭建也是一种低成本的方案。

自行购买物理机有以下几点需要注意：

- 机器的配置，CPU、内存、硬盘、网卡等
- 一般3-4代之前的服务器会在价格上有较大优势，如果买最新代或次新代服务器还不如买虚拟机
- 自己买物理机最大的问题是网络，要搞定防火墙、路由器等网络设备，还需要公网ip、带宽、上下行流量等
- 不知道是否需要ICP备案，如果需要备案，还需要备案域名，这里需要公司身份或个人身份。
- 一个好处是如果自己买老款服务器，可以把更多的服务也跑在上面，比如youtrack、teamcity、存储等

# 名词解释

# 附件及参考资料

- [阿里云RDS数据库](https://help.aliyun.com/zh/rds/product-overview/what-is-apsaradb-rds?spm=5176.yaochi_portal_overview.0.0.42034d7ey0BXr2)
- [时序数据库 InfluxDB® 版](https://help.aliyun.com/document_detail/113093.html?spm=a2c4g.440789.0.i0)
- [淘宝-浦东服务器](https://shop33284911.taobao.com/)
- [Dell R730](https://www.dell.com/support/home/zh-cn/product-support/product/poweredge-r730/overview)
- [Dell R740](https://www.dell.com/support/home/zh-cn/product-support/product/poweredge-r740/overview)
- [二手R730](https://item.taobao.com/item.htm?spm=a1z10.1-c-s.w4004-22887490630.2.60322f69bEbGxt&id=561411204824&pisk=fj7eypTPPUX17d2Icp8y__CsbU8pJEebUa9WZ_fkOpvHda6PZQAJZYvoxFYMQsVpduEdUGWlBH9hz_3yZ_X89LNLf6CpyU2bhazf96EnIefl8p4iI1dJt0Y--Y8wyU2bUWS-3BLRhPqyxQ-g_QOS-XXkKCcMBQJotTvHjAAJwUvkrFWsPPu9mSf2Ig-LE8fn6mpir4b3yHJ2q0grzKRHYafvQCO17B-enhwBnWbVi6bvaaFm4L5lx9OOUrywoiBNznYzzVLCgGXebMyr7hIGMaxNX-oAM_fAqh7rKW6cIgWk6Ger4KSlOiQ6fbmMxiBCmh7_LVpcj15WbGF-ALsvZg-seCvm8aIEE0-H6CJb_5SdL6RX8-Jz90nJjKRwhWpK20KHhCJb_5o-2hA6_KNpp)
- [二手R740](https://item.taobao.com/item.htm?spm=a1z10.5-c-s.w4002-22887490653.21.816a1472TnTzuu&id=741950888850&pisk=fPqndEgI5fObpFRnhNmCyk3veR7ORBiSh7K-w0hP7flsweCSvzAui-ApJ2ULSYP81T6Iv8luZ5h_v9GRdQVuEJ0ELYkrQckre3RE88JoU5nEPyh-9bmuFSXOMiIYdJiSYsCADdBjaAmXLpuywVoZnO0UqAsYdJGSi8NNMiLlgVV2rYPr8VlZ3fkyYYPrbckK_HkyY0lNIYTzAeBsbBZRtqlDtSGTuQSbZjyETJeLbdgeRJci40qZKRm3Laty4lDn-up6FELt4yyLsqUhiHm4LrNS3WRFZbZgQkz4_GKnqRz4qcrN_dhUlRqovkWRYmzbsu0qmaBI884gNDENUel4JW38AVANKbZLtu0Q0sKsTPq_qDUOtnhSzglH7Eokz3MNel8WP2ksIjK0VTdK-4G1jOXMld0ECv6AIOYWp2ksIjBGIET-8AMCH)