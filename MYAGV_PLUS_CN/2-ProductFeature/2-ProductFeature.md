# myAGV Plus参数说明

> 第一章中，我们探讨了产品的卖点及其设计理念，为您提供了对产品高层次理解的全景视角。现在，让我们进入第二章——机器人参数说明。这一章节将是您理解产品技术细节的关键。详细了解这些技术参数，不仅可以帮助您充分认识到我们产品的先进性和实用性，而且还能够确保您能够更有效地利用这些技术来满足您的具体需求。
> 重要说明：myAGV  Plus的具体参数会因所购版本不同而有所区别，最终请以实际交付版本的产品规格为准！！！

<img src="../resources/2-ProductFeature/2.1/JN-main.png " width="800" height="auto" />

## 1.产品规格参数

|       索引       |                  参数                  |
| :--------------: | :------------------------------------: |
|       名称       |               移动机器人               |
|       型号       |               myAGV Plus               |
|       电机       |          FOC行星无刷减速电机           |
|       车轮       |               麦克纳姆轮               |
|     有效载荷     |                  8Kg                   |
|       重量       |                  <5Kg                  |
| 激光雷达扫描范围 |                0.12-8M                 |
|   激光雷达角度   |                  360°                  |
|    内置摄像头    | 800万像素 <br> 拍摄视角77° 焦距2.96mm° |
|     待机时间     |                   --                   |
|     续航时间     |                   --                   |
|   最大移动速度   |                 1.6m/s                 |
|       电源       |              25.2V, 1.5A               |
|     工作温度     |               -5°C-45°C                |

## 2.控制核心参数

|     索引     |                             参数                             |
| :----------: | :----------------------------------------------------------: |
|    主控制    |                  Jetson orin nano Super 8GB                  |
|     CPU      | ARM架构 <br> Cortex-A57核心数：6个 <br> 最大主频：1.728 GHz <br>二级缓存(L2 Cache):1.5 MiB |
|     GPU      |              NVIDIA Ampere 架构，1024个CUDA核心              |
|     内存     |                             8 GB                             |
|     蓝牙     |          板载，可通过`rfkill unblock bluetooth`启用          |
|     无线     |             Realtek RTL8822CE 802.11ac 无线网卡              |
| 核心视频接口 |           HDMI接口\*1 <br> DisplayPort(DP)接口\*1            |
|     USB      |                         USB 3.0 \*2                          |
|    以太网    |                           RJ45\*1                            |
|      IO      | G7, G8, G9, G10, G11, G17, <br> G18, G22, G23, G24, G25, G27 |

## 3.机械结构参数

### 3.1规格和尺寸

<img src="../resources/2-ProductFeature/2.3/structure_param.png " width="800" height="auto" />

### 3.2通孔安装

<img src="../resources/2-ProductFeature/2.3/hole.jpg " width="800" height="auto" />

## 4.电气特性参数

### 4.1 表面电气接口概述

<img src="D:\xuniji\GitBook文档\myagvPlus_docs\MYAGV_PLUS_CN\resources\2-ProductFeature\2.4\dianqi_1.png" width="800" height="auto" />

| 序号 |       接口       |    定义    |              功能              |          备注           |
| :--: | :--------------: | :--------: | :----------------------------: | :---------------------: |
|  1   |       开关       |            |    控制输入电源的开启和关闭    | With lights (lights on) |
|  2   |  机械臂供电接口  |            | 为 my 系列机械臂供电（12V 5A） |                         |
|  3   |   DC/IO 接口组   |    3.3     |             DC3.3V             |                         |
|      |                  |     17     |            GPIO 17             |                         |
|      |                  |     27     |            GPIO 27             |                         |
|      |                  |     22     |            GPIO 22             |                         |
|      |                  |     10     |            GPIO 10             |                         |
|      |                  |     9      |             GPIO 9             |                         |
|      |                  |     11     |            GPIO 11             |                         |
|      |                  |     G      |              GND               |                         |
|      |                  |     10     |            GPIO 10             |                         |
|      |                  |     23     |            GPIO 23             |                         |
|      |                  |     24     |            GPIO 24             |                         |
|      |                  |     25     |            GPIO 25             |                         |
|      |                  |     8      |             GPIO 8             |                         |
|      |                  |     7      |             GPIO 7             |                         |
|  4   |      USB3.0      | USB3.0\*2  |    可与外部设备或 U 盘连接     |                         |
|  5   |       HDMI       |            |          用于连接屏幕          |                         |
|  6   |     网络端口     |  Ethereum  |         以太网端口通信         |                         |
|  7   | 电源直流输入接口 | 25.2V 1.5A |            电源输入            |                         |

#### 1.1 开关：电源开关用于控制主电源输入。如果电源开关关闭，控制器也将断电。

#### 1.2 机械臂电源接口：香蕉插头母头，型号 XT30UPB-F，为 my 系列机械臂供电（12V 5A）。

#### 1.3 DC/IO 接口：IO 接口组为 2.54 毫米杜邦接口，可从外部使用 2.54 毫米杜邦线。

| 标签 |  信号  | 类型 |  功能   | 说明 |
| :--: | :----: | :--: | :-----: | :--: |
| 3.3  |  3.3V  |  P   | DC 3.3V |      |
|  17  | GPIO17 | I/O  | GPIO17  |      |
|  27  | GPIO27 | I/O  | GPIO27  |      |
|  22  | GPIO22 | I/O  | GPIO22  |      |
|  10  | GPIO10 | I/O  | GPIO10  |      |
|  9   | GPIO9  | I/O  |  GPIO9  |      |
|  11  | GPIO11 | I/O  | GPIO11  |      |
|  G   |  GND   |  p   |   GND   |      |
|  18  | GPIO18 | I/O  | GPIO18  |      |
|  23  | GPIO23 | I/O  | GPIO23  |      |
|  24  | GPIO24 | I/O  | GPIO24  |      |
|  25  | GPIO25 | I/O  | GPIO25  |      |
|  08  | GPIO8  | I/O  |  GPIO8  |      |
|  07  | GPIO7  | I/O  |  GPIO7  |      |

> **注意：**
>
> 1. I: 仅作为输入
>
> 2. I/O: 该功能信号包括输入和输出组合。
>
> 3. 单管角设置为输出端时，将输出 3.3V 电压。
>
> 4. 单管角的源电流随着引脚数的增加而减小，从约 40mA 减小到 29mA。
>
> 5. 如果将某个 GPIO 设置为输出模式并输出高电平信号，与 LED 连接的电路如图 2 所示，LED 就会亮起。
>
> <img src="D:\xuniji\GitBook文档\myagvPlus_docs\MYAGV_PLUS_CN\resources\2-ProductFeature\2.4\IO.png" width="800" height="auto" />
>
> 6. 在使用其他功能的情况下，IO 功能不可用，功能界面的其他功能表如图 3 所示。
>
> 

#### 1.4 USB3.0：主线标准为 3.0 接口的串行端口。USB 端口用于复制程序文件和连接鼠标、键盘等外设。

#### 1.5 HDMI：HDMI D 型端口连接显示器。

#### 1.6 网络端口：用于网络数据连接的端口。以太网接口可用于 PC 与机器人系统之间的通信，或与其他设备进行以太网通信。

#### 1.7 电源 DC 输入接口：使用 DC 2.5\*5.1 电源接口；可使用厂家提供的 25.2V1.5A DC 电源适配器为 myAGV 充电。

---

### 4.2 弹仓电气接口概述

<img src="D:\xuniji\GitBook文档\myagvPlus_docs\MYAGV_PLUS_CN\resources\2-ProductFeature\2.4\Battery.png" width="800" height="auto" />

 <br>

<img src="D:\xuniji\GitBook文档\myagvPlus_docs\MYAGV_PLUS_CN\resources\2-ProductFeature\2.4\pump.png" width="800" height="auto" />

| 序号 |     接口     | 定义 |            功能            | 备注 |
| :--: | :----------: | :--: | :------------------------: | :--: |
|  8   | 备用电池端口 |      |        连接备用电池        |      |
|  9   |  抽吸泵接口  |      | 连接吸入泵，控制吸入泵工作 |      |

#### 1.8 待机电池接口：连接待机电池

#### 1.9 吸入泵接口：连接吸入泵，控制吸入泵工作

---

[← 上一章](../1-ProductIntroduction/1-ProductIntroduction.md) | [下一章 →](../3-UserNotes/README.md)
