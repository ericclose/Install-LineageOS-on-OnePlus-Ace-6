# OnePlus Ace 6 刷入 LineageOS 教程

本文将指引您将 OnePlus 刷入 [NullCode](https://t.me/nullcode1337) 维护适配的 LineageOS Official 系统。

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
  
  * [一加深度测试公告&QA / 解锁 bootloader - OnePlus 官方社区](https://bbs.oneplus.com/thread/2175833961601695750)

从官方社区下载好[深度测试.apk](https://oxygenos.oneplus.com/DeepTesting-bcf3709-all-all-domestic-all-release.apk)，**提交深度测试申请通过审核后**，记得在开发者选项**已启用 OEM 解锁**。

请将设备启动至 bootloader 模式，执行命令即可解锁 bootloader：

```bash
fastboot flashing unlock
```

</details>

---

## 固件的下载及刷写

要想刷入第三方固件，**请确保您的设备已解锁 bootloader**

* OnePlus Ace 6 非官方 LineagOS 刷机包和 recovery（recovery 为 LineageOS 包里提取而来）下载链接如下：
  
  * [LineageOS 链接](https://download.lineageos.org/devices/ktm/builds)
  
  > 下载以下文件： 
  * `boot.img`
  * `dtbo.img`
  * `init_boot.img`
  * `vbmeta.img`
  * `vendor_boot.img`
  * `recovery.img`
  * `lineage-*-nightly-ktm-signed.zip`

* LineageOS 的刷写：

```bash
# 为确保 A/B 分区一致（分区不一致容易出错，甚至变砖），建议刷入两遍官方镜像
# 官方镜像 “SuperHybrid Flasher A6 COS 16.x.x.xxx.zip” 下载地址：https://roms.danielspringer.at/index.php?dir=Oneplus+Ace+6%2FSuper+Flashers
# 解压“SuperHybrid Flasher A6 COS 16.x.x.xxx.zip”的所有文件，将手机重启进入 bootloader 模式，执行两遍解压出来的 *.bat 文件即可

# 刷入启动 lineage recovery 所需的镜像
fastboot flash boot boot.img
fastboot flash dtbo dtbo.img
fastboot flash init_boot init_boot.img
fastboot flash vbmeta vbmeta.img
fastboot flash vendor_boot vendor_boot.img

# 重启进入 bootloader 模式
fastboot reboot bootloader

# 刷入 lineage recovery
fastboot flash recovery recovery.img

# 重启设备至 recovery 模式
fastboot reboot recovery

# 「Apply Update 应用更新」→「Apply from ADB 通过adb侧载更新」
# 电脑执行命令刷入 LineageOS：
adb sideload lineage-*-nightly-ktm-signed.zip

# 刷入系统之后，清进行格式化操作，完成后设备就可以开机进系统了
# 「Factory Reset 工厂格式化」→「Format data/factory reset 格式化数据/工厂格式化」

# ------------------------------------------以下为可选操作--------------------------------------------------

# Gapps
# 如果需要刷入 Gapps，建议刷入 MindTheGapps
# MindTheGapps Wiki 链接（请根据您刷入系统的 Android 版本和处理器架构进行选择）： 
# https://wiki.lineageos.org/gapps/
# 如本文 LineageOS 24 对应 Android 17，现在的设备均是 ARM 架构 64 位。下载路径为：
# https://github.com/MindTheGapps/17.0.0-arm64/releases/latest
# 刚刷完 LineageOS 刷机包，得再先重启至 recovery 一次（因为需要先切换到刚刷完 lineage 所在的新 slot，否则刷写失败）
# 刷入方法一样是通过 adb sideload：
adb sideload MindTheGapps-17.0.0-arm64-*.zip

# Magisk
# 下载链接: https://github.com/topjohnwu/Magisk/releases
# 建议至少开机一次，设置密码等保护后再刷入，这样才能保证设备处于加密状态
# 刷入方式选择其中一种即可
## 刷入方式 ①（ADB 侧载）：
adb sideload Magisk*.apk
# -------------------------------------------------------------------
## 刷入方式 ②（fastboot 刷入修补后的 init_boot.img）：
# 手机先安装 Magisk*.apk，打开后「Install 安装」→「Select and Patch a File 选择并修补文件」,
# 选择 LineageOS 提取得到的 init_boot.img，选择修补，完成后得到 magisk_patched*.img，将文件传至电脑
# 手机重启至 fastboot 模式，通过命令刷入 magisk_patched*.img：
fastboot flash init_boot magisk_patched*.img
```

---

## FAQ

<details open>
    <summary>如果本设备 LineageOS Official 存在问题，如何反馈（点击以收起）</summary>

> 在首次构建发布的官方 LineageOS 构建 `lineage-24.0-20261030-nightly-ktm-signed.zip` 中暂未发现问题。
> 
> 若发现问题或 bug，可抓取 adb logcat 日志，于官方 [issues](https://github.com/LineageOS/issues/issues) 区域或联系 [NullCode](https://t.me/nullcode1337) 反馈

</details>

## 参考资料

* [Install LineageOS on ktm | LineageOS Wiki](https://wiki.lineageos.org/devices/ktm/install)
