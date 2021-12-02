# 实验1：模拟智慧农业场景

利用Wio Terminal和温湿度传感器，土壤湿度传感器,紫外线传感器，Wio Terminal内置光线传感器实时监测温室大棚温湿度，光线强度，紫外线强度及土壤湿度，将传感器数据传至Azure IoT Central。Azure IoT Central设置定时任务，模拟智慧农场定时浇灌。Azure IoT Central设置阈值，当土壤湿度过低时，紫外线强度或光线强度异常时，Azure IoT Central发出提示消息。Wio Terminal屏幕显示浇水（模拟浇水系统），内置蜂鸣器报警(模拟报警系统)，调节光线（模拟光线调节系统）。

![](https://files.seeedstudio.com/wiki/github_weiruanexample/weiruan27.png)

## 目录
- [实验1：模拟智慧农业场景](#实验1：模拟智慧农业场景)
  - [目录](#目录)
  - [准备1：硬件需求](#准备1：硬件需求)
  - [准备2：软件需求](#准备2：软件需求)
  - [实验1-1：采集并显示传感器数据](#实验1-1：采集并显示传感器数据)
    - [实验目的:](#实验目的)
    - [实验步骤：](#实验步骤)
  - [实验1-2：实验1-2：连接到Azure IoT Central平台并D2C Message发送时序数据](#实验1-2连接到azure-iot-hub并使用d2c-message发送时序数据)
    - [实验目的:](#实验目的-1)
    - [实验步骤：](#实验步骤-1)
  - [实验1-3：Azure IoT Central设置任务，使用C2D Message通道向设备发送指令，模拟智慧农场定时浇灌](#实验1-3：azure-iot-central设置任务，使用c2d-Message通道向设备发送指令，模拟智慧农场定时浇灌)
    - [实验目的:](#实验目的-2)
    - [实验步骤：](#实验步骤-2)
  - [实验1-4：Wio Terminal模拟自动控制中心](#实验1-4：Wio-terminal模拟自动控制中心)
    - [实验目的:](#实验目的-3)
    - [实验步骤：](#实验步骤-3)
  - [实验1-5：Azure IoT Central设置阈值，异常提示](#实验1-5：azure-ioT-central设置阈值，异常提示)
    - [实验目的:](#实验目的-4)
    - [实验步骤：](#实验步骤-4)

## 准备1：硬件需求

- [Wio Terminal](https://www.seeedstudio.com/Wio-Terminal-p-4509.html)
- [Grove - 温湿度传感器 (DHT20)](https://www.seeedstudio.com/Grove-Temperature-Humidity-Sensor-V2-0-DHT20-p-4967.html)
- [Grove - 土壤湿度传感器](https://www.seeedstudio.com/Grove-Moisture-Sensor.html)
- [Grove - 紫外线传感器](https://www.seeedstudio.com/Grove-UV-Sensor.html)
- [Grove - LED 彩灯](https://www.seeedstudio.com/Grove-Multi-Color-Flash-LED-5mm.html)
- 杜邦线

## 准备2：软件需求

1. 用电脑连接 Wio Terminal

2. 打开要运行智慧农业的[代码](https://files.seeedstudio.com/wiki/github_weiruanexample/Smart_Farm_Azure.ino)并添加运行所需要的[库](https://files.seeedstudio.com/wiki/github_weiruanexample/libraries.rar)到 Arduino IDE

3. 注册 [Azure IoT Central](https://lab1.azureiotcentral.com/dashboards/)

!!! note
    如果您刚开始使用 Wio Terminal 或者不知道怎么上传代码和添加库，可以查看[这里]

## 实验1-1：采集并显示传感器数据

### 实验目的:

实时监测温室大棚温湿度，光线强度，紫外线强度及土壤湿度

### 实验步骤：

1. 连接传感器，土壤湿度传感器在 右边 Grove 口，温湿度传感器 DHT20 在左边 Grove 口

![](https://files.seeedstudio.com/wiki/github_weiruanexample/connect.png)

2. 在 Wio Terminal 后面连接紫外线传感器，这里我们连接的是 A2 口，即分别用三条杜邦线连接传感器的 VCC（3.3V）），GND，SIG 口到 Wio Terminal 的编号 1，39，16接口。

![](https://files.seeedstudio.com/wiki/github_weiruanexample/weiruan28.png)

设计师作图中，后续补充

3. 下载[代码](https://files.seeedstudio.com/wiki/github_weiruanexample/Smart_Farm_Azure.zip)并上传到 Wio Terminal。如果您不知道如何连接 Wio Terminal，可以参考这里的[入门教程](https://wiki.seeedstudio.com/cn/Wio-Terminal-Getting-Started/)

4. 最后观察设备Wio Terminal界面上参数变化。

![](https://files.seeedstudio.com/wiki/github_weiruanexample/connect3.jpg)

## 实验1-2：连接到Azure IoT Central平台并D2C Message发送时序数据

### 实验目的:

实时监测温室大棚温湿度，光线强度，紫外线强度及土壤湿度，将传感器数据传至Azure IoT Central。可Azure IoT Central分析近期数据。

### 实验步骤：

1. 注册好后打开[Azure IoT Central](https://apps.azureiotcentral.com/)

a. 在左侧菜单栏点击“My apps”来建造一个app，也可以在这里管理你的已经建造的app

![](https://files.seeedstudio.com/wiki/github_weiruanexample/weiruan2.png)

b. 在左侧点击进入“Build”界面

![](https://files.seeedstudio.com/wiki/github_weiruanexample/weiruan3.png)

c. 输入你想要的“Application name”和“URL”，Azure IoT Central提供了 7 天的免费试用机会

![](https://files.seeedstudio.com/wiki/github_weiruanexample/weiruan4.png)

d. 当建造到 app 之后，在左侧菜单栏最下面选择“Administration” 接着选择“Device connection” 来连接我们的 Wio Terminal。名字是“SAS-IoT-Devices”

![](https://files.seeedstudio.com/wiki/github_weiruanexample/weiruan5.png)

e. 拷贝下“ID scope”和“Primary key”，两个参数使我们要填在我们的代码上进行网页和机器的认证连接。

![](https://files.seeedstudio.com/wiki/github_weiruanexample/weiruan6.png)

2. 修改 Arduino 代码并上传，需要改的内容为之前保存的 ID_scope 和 primary_key 以确保网页和设备相连

![](https://files.seeedstudio.com/wiki/github_weiruanexample/weiruan15.png)

3. 打开 Azure IoT Central ，选择已连接的设备即可观察数据

![](https://files.seeedstudio.com/wiki/github_weiruanexample/weiruan16.png)

![](https://files.seeedstudio.com/wiki/github_weiruanexample/weiruan17.jpg)

## 实验1-3：Azure IoT Central设置任务，使用C2D Message通道向设备发送指令，模拟智慧农场定时浇灌

### 实验目的：

通过设置指令以模拟智慧农场定时浇灌

### 实验步骤：

1. 在 Azure IoT Central 左侧栏选择“Jobs”进行设置

![](https://files.seeedstudio.com/wiki/github_weiruanexample/weiruan18.png)

输入名字，选择最开始设置的 template 名字，可以看到有“1 device”，选择在设置参数值的“command”浇水命令，让命令开始“on”

![](https://files.seeedstudio.com/wiki/github_weiruanexample/weiruan19.png)

选择“enable”，设置循环灌溉时间，设置开始和结束时间

![](https://files.seeedstudio.com/wiki/github_weiruanexample/weiruan20.png)

最后点击“Schedule”保存

![](https://files.seeedstudio.com/wiki/github_weiruanexample/weiruan21.png)

2. 在指定时间，观察任务是否被执行。

## 实验1-4：Wio Terminal模拟自动控制中心

### 实验目的：

设置阈值，当土壤湿度过低时，紫外线强度或光线强度异常时，做出对应操作。Wio Terminal屏幕显示浇水（模拟浇水系统），内置蜂鸣器报警(模拟报警系统)，调节光线（模拟光线调节系统）。

### 实验步骤：

实验1-1中上传的代码已实现该功能，此处模拟环境变化观察 Wio Terminal 变化即可。

## 实验1-5：Azure IoT Central设置阈值，异常提示

### 实验目的：

Azure IoT Central设置阈值，当土壤湿度过低时，紫外线强度或光线强度异常时，Azure IoT Central发出提示消息。

### 实验步骤：

1. 点击“Create a rule”

![](https://files.seeedstudio.com/wiki/github_weiruanexample/weiruan22.png)

2. 选择刚开始设置的 template 的名字，设置想要的参数和实行动作的参数值

![](https://files.seeedstudio.com/wiki/github_weiruanexample/weiruan23.png)

最后填写提醒信息和选择要接收信息的邮箱

![](https://files.seeedstudio.com/wiki/github_weiruanexample/weiruan24.png)

3. 到时间后查看是否收到提醒

![](https://files.seeedstudio.com/wiki/github_weiruanexample/weiruan25.png)