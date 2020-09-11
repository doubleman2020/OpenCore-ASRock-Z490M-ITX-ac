# OpenCore-ASRock-Z490M-ITX-ac
ASRock Z490M-ITX/ac Hackintosh OpenCore

| 硬件配置 ||
|---|----------------------------------|
| 主板  | 华擎（ASRock）Z490M-ITX/ac |
|CPU|Intel i5-10500                      |
|内存|英睿达 DDR4 3200 8G X 2 （OC 4000）|
|显卡|蓝宝石（Sapphire）RX 5500XT|
|SSD|英睿达 1TB MX500|
|Wifi/蓝牙|Broadcom DW1560|


macOS Catalina 10.15.6 + macOS Big Sur 10.16 beta6

按照官方指引 Comet Lake 做的引导

OpenCore 0.6.1

https://dortania.github.io/OpenCore-Desktop-Guide/

* 官方文档中在 “Creating the USB” --- "Windows install" 中创建的安装U盘是恢复镜像，安装过程中必须要有网络，我这里没有安装黑苹果免驱的无线网卡，板载2.5G网卡驱动需要手工配置才可使用，安装界面无法修改，打开“终端”执行命令：
    `ifconfig en0 media 1000baseT ` 


-------
2020.09.11

## 目前已知问题：
* 唤醒需要多按几次键盘
* iStat menu不显示CPU温度，Intel Power Gadget显示正常
* GPU加速未优化，Intel Power Gadget显示不正常

-------
## 相关配置说明：
### ACPI

1. SSDT-AWAC.aml
2. SSDT-EC-USBX.aml
4. SSDT-PLUG.aml
5. SSDT-PM.aml （修正节能第5项，如果不加默认是4项，非强迫症可忽略）

### Kexts

1. Lilu.kext
2. AppleALC.kext
3. LucyRTL8125Ethernet.kext   板载2.5G网卡驱动（网卡设置“高级-硬件”中将速率改为1000baseT）
4. SMCProcessor.kext
5. SMCSuperIO.kext
6. USBPorts.kext
7. VirtualSMC.kext
8. WhateverGreen.kext
9. NVMeFix.kext
10. AirportBrcmFixup.kext
11. CPUFriend.kext

* 在使用USBInjectAll.kext的时候发现系统USB设备HS13被识别为LED Controller 应该和主板的LED光效有关，重启进入Bios后会造成Bios中的主板LED光效开关失效，只能重新定制USBPort.kext，将HS13设备排除

### PlatformInfo
 iMac20,1

-------
CPU，内存，显卡识别正常

![screenshot-1](https://raw.githubusercontent.com/zhkong/OpenCore-ASRock-Z490M-ITX-ac/master/ScreenShot/screenshot-1.png)


