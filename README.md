# MSI-B460M-10700-5500XT
hackintosh: OpenCore + MSI B460M Mortar + i7 10700 + 5500XT

UPDATE:
- 2022-12-19：升级 macOS 13.1 & OpenCore 0.8.7，尚未发现问题
- 2022-11-09：升级 macOS 13.0 & OpenCore 0.8.5，更新 kext 到最新版本,尚未发现问题
- 2022-09-24：升级 macOS 12.6 & OpenCore 0.8.4，尚未发现问题
- 2022-06-10：升级 macOS 12.4 & OpenCore 0.8.1，尚未发现问题
- 2022-03-16：升级 macOS 12.3 & OpenCore 0.7.9，尚未发现问题, universal control 使用正常
- 2022-02-26：升级 macOS 12.2.1 & OpenCore 0.7.8，尚未发现问题
- 2021-11-13：升级 macOS 12.0.1 & OpenCore 0.7.5，更新驱动版本到最新，尚未发现问题
- 2021-09-14：升级 macOS 11.6 & OpenCore 0.7.3，尚未发现问题
- 2021-08-15：升级 macOS 11.5.2 & OpenCore 0.7.2，尚未发现问题
- 2021-06-12：升级 macOS 11.4 & OpenCore 0.7.0，尚未发现问题
- 2021-05-04：升级 macOS 11.3.1 & OpenCore 0.6.9，尚未发现问题
- 2021-04-17：升级 macOS 11.2.3 & OpenCore 0.6.8。遇到了 USB 引导启动之后 hackintool 无法识别 OpenCore 新版本；用硬盘系统引导黑屏的情况。reset NVRAM 之后就好了。
- 2021-02-16：升级 macOS 11.2.1，尚未发现问题
- 2021-02-06：升级 OpenCore 0.6.6 和 macOS 11.2，尚未发现问题
- 2020-12-30：升级 OpenCore 0.6.4 和 macOS 11.1，尚未发现问题
- 2020-11-13：升级 macOS 11 Big Sur 正式版（11.0.1）一次成功，尚未发现问题

以下基于 OpenCore 0.6.3 版本。

## 硬件配置

| 配置 | 型号 | 价格 | 渠道 |
| ---- | ---- | --- | --- | 
| CPU | Intel i7 10700 | 2126 | 京东：英特尔解决方案官方旗舰店 |
| 主板 | 微星 MSI MAG B460M MORTAR（无 WiFi）| 673 | 京东自营 |
| 显卡 | 蓝宝石 RX 5500XT 8G 白金版 | 1572 | 京东：蓝宝石旗舰店 |
| 内存 | 美商海盗船(复仇者LPX系列) 3200MHz 16G * 2 | 869 | 京东自营 |
| SSD | 致钛 PC005 Active 1T | 819 | 京东自营 |
| 机箱 | 长城 商逸R41 | 99 | 京东自营 |
| 电源 | 酷冷至尊 V550 550W 全模组 | 399 | 京东自营 |
| CPU 风扇 | 利民 AS120 Plus | 129 | 京东自营 |
| WiFi + 蓝牙 | Fenvi FV-T919 BCM94360CD | 288 | 京东：优勃数码专营店 |

2020 年 11 月 1 号，双十一第一波活动，总计 6974 元。

## 配置过程

基本上完全参考了 [OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)

少量参考了 up 主司波图的[CometLake十代Intel平台台式机Opencore黑苹果通用配置教程（附安装包）](https://www.bilibili.com/video/BV1uf4y1X7MT)

对于详细的过程就不一一介绍了。不过非常强调的一点是，一定要仔仔细细的看好 OpenCore 官方教程的每一句话，正确理解每一句话的意思。有些 kext 扩展是某些特定平台特定硬件需要的，**你要是弄多了，反而会造成问题**。我的 efi 里基本上算是非常干净的了，都是必要的驱动。

### 第一步：硬件选购以及装机

选择正确的硬件配置，黑苹果基本就成功了一大半了。

#### CPU

CPU 选择 Intel 的平台没得说。虽说[tonymacx86](https://www.tonymacx86.com/buyersguide/building-a-customac-hackintosh-the-ultimate-buyers-guide/)的 Buyer's Guide 目前还是推荐 9 代 Coffee Lake，但是 10 代 Comet Lake 已经（2020.11）发售半年了，实际黑苹果并没有什么问题。

CPU 最好选择带核显的型号，macOS 的各种硬件加速会用上。

AMD 其实也能搞，就是实际搞起来会有点麻烦，并且 Adobe 之类的软件可能优化不是很好。不建议新手头铁硬刚。

#### 主板

主板选择 MSI、技嘉之类的市场主流就好了。之前思考配置的时候，刚开始搞的是 i7-10700K + Z490M，后来发现 10700 和 10700K 的性能差距在 5% 以内，但是整体配置降低到 10700 + B460M 能少花 1000+，还是降低了配置。反正也不搞什么超频。

#### 显卡

显卡选择 AMD 就对了，N 卡就别想了。

上一代的 RX 500 系列，RX 580、RX 590 其实都是可以用的。但是要注意的是，目前市场上卖的 580 都是 RX 580 2048SP，这玩意是不行的，非要搞，得刷 vBIOS 降级伪装成 RX570。市场上卖的 RX 590 GME 也是马甲阉割卡，也不行。

现在这个时间点，最好也就是选择 RX 5000 系列。RX 5500XT 虽然有点智商检测卡，但是确实没得选了。

品牌最好选 AMD 亲儿子蓝宝石，最多迪兰恒进。别买 XFX 之类的，会有问题。

#### 内存

这个好像比较无所谓，差别不大。

#### SSD

SSD 也差别不大，只是有个别型号的三星 PM981、PM991 会有兼容性问题。不过听说新版固件是修好了，可以用的。不过最好还是避开。

我自己选了国产 NVMe 致钛的 1T，双十一新品发售，算是支持一把国产吧。

#### 机箱 & 电源

这个比较无所谓，看个人喜好了。

我对机箱没啥要求，便宜皮实就行了。所以选了个傻大黑粗的便宜机箱。装起来倒是没啥问题。

电源在我这个配置下，550W 够用了，是否要全模组也看个人吧。我只是看这款双十一折扣价比较实在，399 就能买个 550W 金牌全模组，就买了。

#### CPU 风扇

我对水冷比较怵，还是买了风冷。而且 10700 65W 的 TDP，利民 AS120 Plus 足够压的住了。

#### Wi-Fi + 蓝牙

这个比较挑，要么淘宝买原装的苹果拆机网卡，要么买博通类似我这个 BCM94360CD 芯片的网卡 Fenvi FV-T919，四天线，算是我这里的顶配了。

不过实际到手质感一般，天线不紧，容易倒。准备买个天线延长线，接天线底座。毕竟放机箱后面，信号是有点够呛。

不过这个网卡确实免驱，啥驱动都不要放。放了反而可能有问题。

这个网卡的蓝牙是单独一根线插到了主板的 USB Header 上。所以刚装好的时候蓝牙用不了，这时候需要正确配置 USB mapping 才行。

#### 有线网卡

有线网卡是板载的 2.5G Realtek® RTL8125B，苹果用不了 2.5G 口，得在装好系统之后，手工在系统设置里，有线网卡从自动改成 1000baseT，强制用千兆就可以了。

#### 装机

装机就不说了。先各种插上，然后开始配置黑苹果，别上来就组装好，装箱的。

哪方面不好使，最好先用 U盘装一个 Ubuntu LiveCD，引导启动起来看看，看是不是硬件有问题。

### 第二步：创建 USB 镜像

我是在白苹果 macOS 下配置的，准备好一个应该是 16G 以上的 U 盘。

按照[教程](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)配置就好了。

把 OpenCorePkg 的底包里的 EFI 目录丢到 U盘的 EFI 挂载分区下，然后删除一些没用的文件就好了。

### 第三步：收集驱动文件

这一步是最关键的，搜集自己需要的各种驱动丢到对应目录里。然后配置 config.plist 文件。

展示以下我的最终文件目录树：

```
.
├── EFI
│   ├── BOOT
│   │   └── BOOTx64.efi
│   └── OC
│       ├── ACPI
│       │   ├── SSDT-AWAC.aml
│       │   ├── SSDT-EC-USBX-DESKTOP.aml
│       │   ├── SSDT-PLUG.aml
│       │   └── SSDT-RX\ 5500\ XT.aml
│       ├── Bootstrap
│       │   └── Bootstrap.efi
│       ├── Drivers
│       │   ├── HfsPlus.efi
│       │   └── OpenRuntime.efi
│       ├── Kexts
│       │   ├── AppleALC.kext
│       │   ├── Lilu.kext
│       │   ├── LucyRTL8125Ethernet.kext
│       │   ├── NVMeFix.kext
│       │   ├── SMCProcessor.kext
│       │   ├── SMCSuperIO.kext
│       │   ├── USBPorts.kext
│       │   ├── VirtualSMC.kext
│       │   ├── WhateverGreen.kext
│       │   ├── XHCI-unsupported.kext
│       │   └── dAGPM.kext
│       ├── OpenCore.efi
│       ├── Tools
│       │   └── OpenShell.efi
│       └── config.plist
└── README.md
```

逐个文件介绍一下：

| 文件 | 用途 |
| --- | --- |
| BOOT/BOOTx64.efi | OpenCore 底包自带，不管，不动它 |
| OC/ACPI/SSDT-AWAC.aml | ACPI 介绍见下方 |
| OC/ACPI/SSDT-EC-USBX-DESKTOP.aml | ACPI 介绍见下方 |
| OC/ACPI/SSDT-PLUG.aml | ACPI 介绍见下方 |
| OC/ACPI/SSDT-RX\ 5500\ XT.aml | 这个文件是参考司波图弄来的，据说释放显卡性能用的，[网上](https://www.tonymacx86.com/threads/amd-radeon-performance-enhanced-ssdt.296555/)确实有这个说法。所以就放了进来。 |
| OC/Bootstrap/Bootstrap.efi | OpenCore 底包自带，不管，不动它 |
| OC/Drivers/HfsPlus.efi | 底包里其他驱动都可以删掉，这两个是必须的。 |
| OC/Drivers/OpenRuntime.efi | 同上，必须的驱动 |
| OC/Kexts/AppleALC.kext | 声卡相关驱动，基本都需要，不过后续需要一些配置 |
| OC/Kexts/Lilu.kext | 基础驱动，必须的 |
| OC/Kexts/LucyRTL8125Ethernet.kext | 有线网卡驱动 |
| OC/Kexts/NVMeFix.kext | 其他驱动，也基本都是必须的 |
| OC/Kexts/SMCProcessor.kext | VirtualSMC 的相关插件驱动，基本必须 |
| OC/Kexts/SMCSuperIO.kext | 同上 |
| OC/Kexts/USBPorts.kext| 自己生成的正确配置的 USB Map 文件（其实我是从[别的地方](https://github.com/szc188/MSI-B460M-MORTAR-10700K-5500XT-OC/tree/main/EFI/OC/Kexts)抄的，我按照文档教程和司波图教程，都没配置成功) |
| OC/Kexts/VirtualSMC.kext| 基础驱动，必须 |
| OC/Kexts/WhateverGreen.kext| 显卡相关必须驱动 |
| OC/Kexts/XHCI-unsupported.kext| 配合解决 USB 问题的驱动 |
| OC/Kexts/dAGPM.kext| 配合上面 RX 5500XT 显卡性能提升的驱动 |
| OC/OpenCore.efi | 自带，不动它 |
| OC/Tools/OpenShell.efi | Tools 里面其实都删差不多了 |
| OC/config.plist | **重点编辑文件** | 

#### ACPI

ACPI 其实在教程里是在 kext 后面配置的，不过目录树排前面，就先介绍了。

按照 [OpenCore 教程](https://dortania.github.io/Getting-Started-With-ACPI/ssdt-platform.html#desktop)，Comet Lake 平台基本上只需要`SSDT-PLUG`、`SSDT-EC-USBX`、`SSDT-AWAC` 这三个文件。

`SSDT-RHUB` 这个文件是解决部分主板的 USB 问题的。不是所有都必须的。但是，刚开始我也没加这个文件。装完之后，整个 USB 设备里只有 USB 3.0 Bus。但是蓝牙的线接在主板内部的 USB Header 上是 USB 2.0 的，所以蓝牙并不工作。后来加了这个文件之后，USB 2.0 确实工作了。蓝牙也就有了。不过这时候，USB 还是不完美的，USB 2.0 工作了，USB 3.0 就不工作了。这时候还需要后来单独自己配置 USBPorts.kext 来正确处理 USB Map 的问题。所以，对于这个文件，可以一半解决问题，并不完美。

#### kext

按照教程，看清楚，自己需要什么，不需要什么。

比如在 [Wi-Fi 这里](https://dortania.github.io/OpenCore-Install-Guide/ktext.html#wifi-and-bluetooth)，挺多网上的 efi 都会放的`AirportBrcmFixup`、`BrcmPatchRAM`，其实我们是不需要的，我们是免驱的网卡。

### 第四步：配置 config.plist

从 0 开始的配置应该是复制 OpenCorePkg 底包里面的 Sample.plist 进行修改。如果是直接用我的 EFI 的话，最好还是按照教程都走一遍。比如里面配置 PlatformInfo 的地方，是需要每个人自己生成的，PlatformInfo 里面的 ROM 是 en0 的 MAC 地址，每个人的硬件不一样，也需要自己配置的。这个 ROM 是后面 Post-Install fix iService 阶段改的，安装的时候其实不改就能用。

这一步就按照[教程](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html)一个一个改就行了。

用 ProperTree 打开 config.plist 配置文件，cmd + shift + R 选择 OC 的目录，就可以自动加载修改了的 ACPI、kext 文件的对应配置。

然后就逐个参数修改就好了。

`AAPL,ig-platform-id` 这里说一下，十代平台目前对于纯核显支持还有点问题，最好是核显 iGPU + 独显 dGPU 一起用，使用`0300C89B`这个参数。在司波图的视频里也有说明。

`XhciPortLimit` 这个改为 True 是在还没有自定义 USB Map 的时候需要改的。自定义 USB Map 完成之后，是可以改回去的。

上面 config.plist 改完之后，保存就可以了，基本就可以用了。建议去 [Sanity Checker](https://opencore.slowgeek.com/) 检查一下配置正确性。

### 第五步：修改 BIOS

OpenCore 给了要开启和关闭的选项，但是不是每个主板都有全部选项的。

MSI B460M 这个改了大概这些：

* Fast Boot
* Secure Boot
* CFG lock
* Intel SGX
* VT-x
* Above 4G decoding
* Hyper-Threading
* EHCI/XHCI Hand-off
* SATA Mode: AHCI

其中有些默认值就是我们需要的，找到看一眼，也不用特意改他。


### 第六步：安装系统

> 如果使用有线网卡，没有无线网卡安装时，可以通过命令行工具设置网卡参数以启用(具体网卡名可通过命令行查看): <br> ifconfig en0 media 1000baseT mediaopt full-duplex

这一步没啥好说的。选择 U 盘引导启动，选择 macOS 安装程序。

全新硬盘安装的话，先去分区，然后安装。

安装过程看情况把，大概 20 来分钟的样子。然后就配置 iCloud、账户之类的，也没啥特别的。

OpenCore 也给出了一些安装前后可能遇到的问题，比如我就遇到了，最后发现还是自己应该配置的 ScanPolicy = 0 没配置导致的。正确的 config.plist 配置，安装就很顺畅了，没啥问题。

### 第七步：Post-Install

这就是系统安装后的小问题的修复过程。大部分问题其实我没遇到。就主要遇到一个 USB 的问题。

通常常做的 Fix Audio 过程，可以看文档，也可以看司波图的视频教程，都挺清晰的。我的板载声卡直接用 layout = 1 就可以，所以没改啥就可以用。

小 tips：系统安装好了之后，会让你把 U 盘里的 efi 复制到主机硬盘的 EFI 分区里。之后修改各种细节配置，还是在 USB 的 efi 里改，然后系统引导从 U 盘启动就可以使用新的配置。确定修改正确之后，再覆盖主机 SSD 的 EFI 分区的文件。

小系统升级没啥问题，装完之后，自动提示我升级 macOS 10.15.7 的补充更新，我就直接在线更新了，就没啥问题。

Fixing DRM 那一块我也搞了半天。最后发现，人家根本还不支持 Safari 14，所以整了半天没啥用。

USB Map 这个，有点麻烦，建议看看司波图的视频，说实话，我也没能实践成功。因为起手 USB 2.0 不可用，加了 SSDT-RHUB 之后，USB 3.0 就不可用，有点鬼畜。最后大概摸清楚原理，找了一份可用的 USBPorts.kext 文件。司波图的那种改 SSDT 的方式，我是没实践成功的。还是用了改 kext 的方式解决了问题。

### 总结

搞到这里就没啥了，各种东西都可用了。

+ [x] 睡眠 唤醒
+ [x] 所有USB端口、USB3.0
+ [x] 独显免驱
+ [x] 板载声卡
+ [x] 板载网卡（需要手动设置）
+ [x] Airdrop（需要苹果网卡）

主要参考对象：

- https://dortania.github.io/OpenCore-Install-Guide/
- https://github.com/abner-xu/efi
- https://github.com/szc188/MSI-B460M-MORTAR-10700K-5500XT-OC
- https://www.bilibili.com/video/BV1uf4y1X7MT 
