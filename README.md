# OnePlus Ace 6 刷入 LineageOS 教程

本文将指引您将 OnePlus 刷入 [NullCode](https://t.me/nullcode1337) 适配的 LineageOS 系统，本文将涵盖一些常见问题的 workaround。

> 本文内容遵循 署名-非商业性使用-相同方式共享 4.0 国际 (CC BY-NC-SA 4.0) 协议
> 
> 本文永久链接是: [https://github.com/ericclose/Install-LineageOS-on-OnePlus-Ace-6/blob/main/README.md](https://github.com/ericclose/Install-LineageOS-on-OnePlus-Ace-6/blob/main/README.md)

## 目录

- [OnePlus Ace 6 刷入 LineageOS 教程](#oneplus-ace-6-刷入-lineageos-教程)
  - [目录](#目录)
  - [前情提要](#前情提要)
    - [USB 驱动的安装](#usb-驱动的安装)
    - [配置 ADB 的环境变量](#配置-adb-的环境变量)
    - [基础常识](#基础常识)
    - [解锁 bootloader](#解锁-bootloader)
  - [固件的下载及刷写](#固件的下载及刷写)
  - [FAQ](#faq)
  - [参考资料](#参考资料)

## 前情提要

### USB 驱动的安装

<details>
    <summary>点击以展开</summary>

* 请确保已正确**安装 Google USB 驱动**
  
  * [官网下载链接](https://dl.google.com/android/repository/usb_driver_r13-windows.zip) 

  > 手动安装驱动可以参考[How to Fix "Waiting for any device" - Fastboot not detecting your device](https://www.youtube.com/watch?v=e4Y2YX8MV4I)
  
  > **通过命令安装需确保 Windows 10 v1607 及以上版本**。首先将下载的 `usb_driver_r13-windows.zip` 文件全部解压至方便的目录（如本例 `D:\Downloads\`），通过**以管理员模式运行** 下列命令，即可完成驱动的安装：

```bash
# 请将下列命令中的路径 D:\Downloads\usb_driver 改为你实际解压的路径
pnputil /add-driver "D:\Downloads\usb_driver\*.inf" /subdirs /install
```

</details>

---

### 配置 ADB 的环境变量

<details>
    <summary>点击以展开</summary>

* 配置 ADB 的环境变量的步骤
  
  * [ADB 下载](https://dl.google.com/android/repository/platform-tools-latest-windows.zip)
  
  * ADB 环境变量的配置方法：
    
    > Windows 10 及以上版本：按下 Win 键，键入 「environment variables」或『环境变量』，搜索预览结果选择**编辑系统环境变量**；『环境变量』→ 双击「系统变量」中的『PATH』→ 『新建』，在文本框输入 `adb.exe` **所在目录的绝对路径**，如『`D:\Program Files\platform-tools`』，最后保存即可。

</details>

---

### 基础常识

<details>
    <summary>点击以展开</summary>

* 知悉**启用 USB 调试**的方法
  
  > 『*Settings*』设置 →『*About Phone*』关于手机 → 版本信息 → 快速连续点击『*Build number*』版本号，直至提示已启用开发者选项；
  > 
  > 『*Settings*』设置 →『*System*』系统 →『*Developer options*』开发者选项 →『*USB debugging*』USB 调试

* 知悉**启用 OEM 解锁**的方法
  
  > 『*Settings*』设置 →『*About Phone*』关于手机 → 版本信息 → 快速连续点击『*Build number*』版本号，直至提示已启用开发者选项；
  > 
  > 『*Settings*』设置 →『*System*』系统 →『*Developer options*』开发者选项 → OEM 解锁


* 知悉如何将手机**启动至 bootloader 模式**
  
  > * 方法 1：设备处于关机状态下，长按『电源键』&『音量 -』，直至设备启动至 bootloader 模式后即可松开按键
  > 
  > * 方法 2：设备启用 USB 调试之后，用数据线将手机与电脑连接，通过 cmd 执行命令 `adb reboot bootloader` 重启至 bootloader 模式

* 知悉如何将手机**启动至 recovery 模式**
  
  > * 方法 1：设备处于关机状态下，长按『电源键』&『音量 +』，直至设备启动至 recovery 模式后即可松开按键
  > 
  > * 方法 2：设备启用 USB 调试之后，用数据线将手机与电脑连接，通过 cmd 执行命令 `adb reboot recovery` 重启至 recovery 模式

</details>

---

### 解锁 bootloader

<details>
    <summary>点击以展开</summary>

* 请确保设备已经**解锁 bootloader**
  
  > 解锁 OnePlus 设备的 bootloader 有以下影响，请自行决定是否解锁：
  > 
  > * 解锁操作将会**清除设备数据**
  > 
  > * 解锁后**设备启动**将会提示“**设备已解锁 bootloader**”
  
  * [一加深度测试公告&QA / 解锁 bootloader - OnePlus 官方社区](https://bbs.oneplus.com/thread/1926504022886318086)

从官方社区下载好[深度测试.apk](https://bbsstatic.oneplus.com/public/apk/%E6%B7%B1%E5%BA%A6%E6%B5%8B%E8%AF%95.apk)，**提交深度测试申请通过审核后**，记得在开发者选项**已启用 OEM 解锁**。

请将设备启动至 bootloader 模式，执行命令即可解锁 bootloader：

```bash
fastboot flashing unlock
```

</details>

---

## 固件的下载及刷写

要想刷入第三方固件，**请确保您的设备已解锁 bootloader**

* OnePlus Ace 6 非官方 LineagOS 刷机包和 recovery（recovery 为 LineageOS 包里提取而来）下载链接如下：
  
  * [LineageOS 链接](https://drive.google.com/drive/u/3/folders/18h7izlH_RPC5JURUA8oXUgQxQbKZk_Os)
  * [Lineage recovery 链接](https://github.com/ericclose/ktm/raw/refs/heads/main/lineage-recovery-ktm.img)
  
  > 下载 `lineage-*-ktm.zip`、和 `lineage-recovery-ktm.img` 即可。

* LineageOS 的刷写：

```bash
# 为确保 A/B 分区一致（分区不一致容易出错，甚至变砖），建议刷入两遍官方镜像
# 官方镜像 “SuperHybrid Flasher A6 COS 16.x.x.xxx.zip” 下载地址：https://roms.danielspringer.at/index.php?dir=Oneplus+Ace+6%2FSuper+Flashers
# 解压“SuperHybrid Flasher A6 COS 16.x.x.xxx.zip”的所有文件，将手机重启进入 bootloader 模式，执行两遍解压出来的 *.bat 文件即可

# 刷入 recovery（将会替换官方 recovery 为 Lineage recovery）
fastboot flash recovery lineage-recovery-ktm.img

# 重启设备至 recovery 模式
fastboot reboot recovery

# 「Apply Update 应用更新」→「Apply from ADB 通过adb侧载更新」
# 电脑执行命令刷入 LineageOS：
adb sideload lineage-*-ktm.zip

# 刷入系统之后，清进行格式化操作，完成后设备就可以开机进系统了
# 「Factory Reset 工厂格式化」→「Format data/factory reset 格式化数据/工厂格式化」

# ------------------------------------------以下为可选操作--------------------------------------------------

# Gapps
# 如果需要刷入 Gapps，建议刷入 MindTheGapps
# MindTheGapps Wiki 链接（请根据您刷入系统的 Android 版本和处理器架构进行选择）： 
# https://wiki.lineageos.org/gapps/
# 如本文 LineageOS 23.2 对应 Android 16，现在的设备均是 ARM 架构 64 位。下载路径为：
# https://github.com/MindTheGapps/16.0.0-arm64/releases/latest
# 刚刷完 LineageOS 刷机包，得再先重启至 recovery 一次（否则可能遇到分区挂载失败，刷写报错）
# 刷入方法一样是通过 adb sideload：
adb sideload MindTheGapps-16.0.0-arm64-*.zip

# Magisk
# 下载链接: https://github.com/topjohnwu/Magisk/releases
# 建议至少开机一次，设置密码等保护后再刷入，这样才能保证设备处于加密状态
# 刷入方式选择其中一种即可
## 刷入方式①（ADB 侧载）：
adb sideload Magisk*.apk
# -------------------------------------------------------------------
## 刷入方式②（fastboot 刷入修补后的 init_boot.img）：
# 手机先安装 Magisk*.apk，打开后「Install 安装」→「Select and Patch a File 选择并修补文件」,
# 选择 LineageOS 提取得到的 init_boot.img，选择修补，完成后得到 magisk_patched*.img，将文件传至电脑
# 手机重启至 fastboot 模式，通过命令刷入 magisk_patched*.img：
fastboot flash init_boot magisk_patched*.img
```

---

## FAQ

<details open>
    <summary>本设备 LineageOS Unofficial 目前存在的问题（点击以收起）</summary>

> 到目前为止，在最新的非官方 LineageOS 构建 `lineage-23.2-20260304-VANILLA-UNOFFICIAL-ktm.zip` 中发现了以下问题：
> 
> 1. 默认设定的情况下锁屏，**双击唤醒屏幕暂不可用**，暂时的处理方式是：启用 AOD（熄屏显示）后即可使用该功能

</details>

## 参考资料

* [[ROM] [UNOFFICIAL] LineageOS 23.2 for OnePlus Ace 6 (ktm)](https://xdaforums.com/t/rom-unofficial-lineageos-23-2-for-oneplus-ace-6-ktm.4781127/)
