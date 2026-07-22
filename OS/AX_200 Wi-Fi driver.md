# AX_200 Wi-Fi driver

NUC13ANKi7-1360P 在 Ubuntu 20.04.6 LTS 操作系统下 AX 200 系列无线网卡掉驱动解决方案

经测试，原因为原生的 **5.15.0** 内核太旧，不包含无线网卡的设备识别号 **51F1**，导致 **iwlwifi** 驱动无法绑定设备。更新至 **6.1.177** 内核可以支持。

***注意：太新的内核，如 6.4.7，更新后发生图形化界面无法启动的问题，未通过测试***

## 1. 系统检查

检查当前内核版本：

```bash
uname -r
```

应输出当前内核版本 `5.15.0-139-generic`。

```bash
sudo apt install dkms
dkms status
```

应**无输出**，说明没有第三方模块需要随新内核重编译。

## 2. 下载内核

下载内核软件包目录索引：

```bash
mkdir -p ~/kernel-6.1.177
cd ~/kernel-6.1.177
BASE="https://kernel.ubuntu.com/mainline/v6.1.177/amd64"
wget -O index.html "${BASE}/"
grep -oP 'href="\K[^"]+\.deb' index.html | grep -E '^linux-(image-unsigned|modules)-.*-generic_.*_amd64\.deb$' | sort -u > files.txt
```

检查下载结果：

```bash
cat files.txt
```

应输出两个文件，如下：

```bash
linux-image-unsigned-6.1.177-0601177-generic_6.1.177-0601177.202607041520_amd64.deb
linux-modules-6.1.177-0601177-generic_6.1.177-0601177.202607041520_amd64.deb
```





















