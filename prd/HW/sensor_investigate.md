# 传感器选型

| 任务名称 | MYY-12 调研-传感器选型       |     |
|------|-----------------------|-----|
| 提交作者 | gsq                   |     |
| 提交时间 | 2024-08-17            |     |
| 文件名  | sensor_investigate.md |     |

# 一、概述

## 1、相关背景

MY-T01是一个物联网终端硬件设备，用于监测园林植物（如罗汉松）的数据和自动化干预。
设备需要感知以下几种数据：

- 温度
- 湿度
- 光照
- 土壤温度
- 土壤水分
- 土壤氮磷钾
- 土壤EC

由于设备的三防需求，将传感器芯片集成在板上不是一个好方案，所有我们需要选择合适的外接传感器探头。

## 2、意义

- 传感器与控制器分离，方便维护和更换
- 传感器探头可以根据不同的需求选择不同的型号
- 外接设计可以更容易做到防水、防尘、防腐蚀

# 三、业内方案调研

针对我们需要的几种数据，可以将相似功能集成在一个探头中，具体来说有以下几种

- 温湿度探头
- 土壤探头
- 光照探头

### 1、温湿度探头

#### AHT2417C

[链接](https://item.taobao.com/item.htm?spm=a21n57.1.item.26.464a66aeXHpFxR&priceTId=2147826917237237103427300e994e&utparam=%7B%22aplus_abtest%22:%22552a1e85f7e36122e26cea1b60818701%22%7D&id=712622792060&ns=1&abbucket=8&skuId=4989875820559&pisk=fiIotoYWlIG6XOMLZix7JNXOCR4AibtBP6np9HdUuIRj2eRLP6Yh9sTF23BRiB5OtpIRvMbjxO6C28tLF36WAHPT6lIhFTtCPtkd-gmq0p6q4b-EZT-SUHPT6k0x3UNJYwU4DK9DuI9HLDJPTn-2dLxeLL-UnIJHC2lPTHyc3I9HT2urYol2LdvrCJlpsw7c07SqDJE5Vb3XFUANnPZ3Y2pI6BBroDnCmZ2v1TuIYDSDEUj3aS1dwH7PesYOr5mk5T71Od5raWACmtSP7srxqHXV7MxV0SkvaN6cx3Izpu-N5sjH7h4LFUWho6tR0Juy_aCJJgTmg8AC2_jHPGPtcQ7ccMxRk7m9Oe7AVFs8g0xN5TKR81PxyQ7MLgytuV-n8D94piuIRUJXnCiGAJhJ0evoW-2m5xYyhLwTn-0IeUJXnCe0nVgpzK97B)
电压：2V2~5V5
输出：数字，I2C
范围：-30~80°C，0~100%RH
分辨率：0.01°C，0.024%RH
响应时间：5~30S 温度，8S 湿度
防护性：防水透气膜
价格：15.8

#### VMS-3000-WS-*

[链接](https://detail.tmall.com/item.htm?spm=a21n57.1.item.8.464a66aeXHpFxR&priceTId=2147826917237237103427300e994e&utparam=%7B%22aplus_abtest%22:%22bbd57346156ed80d191b280e9b6d5408%22%7D&id=683507032556&ns=1&abbucket=8&xxc=taobaoSearch&skuId=4892042313829&pisk=fC5jtuaUWGCr8OQWjKUyFEqbKkO6BiNEcVTO-NhqWIdvXT_hfnzgnIWWfgIWDjz0ndK1mIpG3h-2fC_GAzrUTW7coCAYYkPEmWw9GBDxBnnw20LDnuzr4W7coh0jXyW8TA1KSU59WGpveULe2EKt6hUWee896jptMYnJqFd9XGpAyYL2kqnvDEd-aUMH5StflzeCrW2o52SeVfhI-ZpYiaDZOXMDkKKpekhZ_PYXhHQvVk_IZ-v1cK1zGDYfew_ylGVniIp1BsRRMuF9wwXPDUsTAAtRdsf6LsZIKnCDjg9FhkGfAiYO5FIbt2tRGN1WnTuEOa9CwsRcFkGevTbO1LQ0AvYPBw5VCiro6nWCyg9Fa0le99j51pdd4tGeAkCmC49n1UtUPzMiQGUfe3qbtvcMHUYXyzaScGvvrUTuPzMiIKLklH47PmsG.)
电压：5V~28V
输出：数字，RS485 + Modbus-RTU
范围：-40~80°C，0~100%RH
分辨率：0.1°C，0.1%RH
响应时间：？
防护性：PE外壳板有一定防水性
价格：34

#### RS-WS-N01

[链接](https://detail.tmall.com/item.htm?spm=a21n57.1.item.8.464a66aeXHpFxR&priceTId=2147826917237237103427300e994e&utparam=%7B%22aplus_abtest%22:%22bbd57346156ed80d191b280e9b6d5408%22%7D&id=683507032556&ns=1&abbucket=8&xxc=taobaoSearch&skuId=4892042313829&pisk=fC5jtuaUWGCr8OQWjKUyFEqbKkO6BiNEcVTO-NhqWIdvXT_hfnzgnIWWfgIWDjz0ndK1mIpG3h-2fC_GAzrUTW7coCAYYkPEmWw9GBDxBnnw20LDnuzr4W7coh0jXyW8TA1KSU59WGpveULe2EKt6hUWee896jptMYnJqFd9XGpAyYL2kqnvDEd-aUMH5StflzeCrW2o52SeVfhI-ZpYiaDZOXMDkKKpekhZ_PYXhHQvVk_IZ-v1cK1zGDYfew_ylGVniIp1BsRRMuF9wwXPDUsTAAtRdsf6LsZIKnCDjg9FhkGfAiYO5FIbt2tRGN1WnTuEOa9CwsRcFkGevTbO1LQ0AvYPBw5VCiro6nWCyg9Fa0le99j51pdd4tGeAkCmC49n1UtUPzMiQGUfe3qbtvcMHUYXyzaScGvvrUTuPzMiIKLklH47PmsG.)
电压：5V~28V
输出：数字，RS485 + Modbus-RTU
范围：-40~80°C，0~100%RH
分辨率：0.1°C，0.1%RH
响应时间：25S 温度，8S 湿度
防护性：PE外壳板有一定防水性
价格：44

### 2、土壤探头

可选方案：

- [型号1](https://item.taobao.com/item.htm?spm=a21n57.1.item.8.bc69632dgiDJxF&priceTId=2147818d17238187223005978eae4a&utparam=%7B%22aplus_abtest%22:%22cc3c81d00129dd77af619455442f7fb7%22%7D&id=565434368878&ns=1&abbucket=8&skuId=4625218304956)
- [型号2](https://detail.tmall.com/item.htm?spm=a21n57.1.item.2.bc69632dgiDJxF&priceTId=2147818d17238187223005978eae4a&utparam=%7B%22aplus_abtest%22:%226145fe332c1bf8c5ccdd344157108216%22%7D&id=641146249229&ns=1&abbucket=8&xxc=taobaoSearch&skuId=4784477903795&pisk=fNunTpZQfR6jUffJKV4B2mcxGIxTFya4zeD8e8hzUW2_LwhzezDoEY2L4paKrAcrnBNJd4CIfxhVJ2KQya4QPzJvHELAOXa7zeGN20XQ_SPvyaPFzphUy69vHELkY1zkKKnJ7363s72aT7SU4C4awSFUzuPE_CVzw9SP8Ylws7waT8PPY18ag7sUTAGRe-mrjVJE7NdJRm7VNor33fxjeYgwU5sIFRYkPVmM-8GFVa7rSWqnrpJsevUrYXHgDDvc-oGEcYNqL9JuFVcZ8mkwWw4o_muu7VJN6Jojs44K8QLUumMirozD2BZEZcD7JVRPY-oKpu3QjOR3F2Hnrkg2HNwEjVguJcphk8ZrX2ZjJd73umGLJ0k2BMeEm7SzXGS4rg77_Q3NVgZU152fo4ORpPrutidMsi1gY5NBMCAGV6EU152vsCjf2kP_OIC..)

需要考虑的参数：

- 供电电压
- 功耗
- 工作温度
- 防护等级
- 接口和协议

市面上土壤传感器大多是RS485接口，Modbus协议，在开发控制板时需考虑RS485的隔离问题，采用隔离DC-DC模块和收发器，或采用现成模组。

### 3、光照探头

市面暂无合适的光照探头，我们需要自己开发

**光照传感器芯片选型**

| 型号                     | 电压      | 输出方式   | 精度     | 范围           | 立创千片价格 |
|------------------------|---------|--------|--------|--------------|--------|
| BH1750FVI-TR           | 2V4~3V6 | 数字I2C  | 16位    | 1~65535 lx   | 3.2    |
| ALS-PT19-315C/L177/TR8 | 2V5~5V5 | 模拟（电流） | /      |              | 0.37   |
| LTR-303ALS-01          | 2V4~3V6 | 数字I2C  | 16位    | 0.01~64K lx  | 1.28   |
| LTR-308ALS-01          | 1V7~3V6 | 数字I2C  | 16~20位 | 0.01~157K lx | 1.43   |
|                        |         |        |        |              |        |

还有带接近传感器的型号

技术路线：
制作一个圆形小板，集成传感器芯片和外围电路，塑料外壳+透明树脂封装，杜邦线或屏蔽线引出，连接到控制板上

# 名词解释

# 附件及参考资料


