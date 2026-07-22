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

下载内核软件包：

```bash
while IFS= read -r file; do
  wget -c "${BASE}/${file}"
  done < files.txt
```

检查下载结果：

```bash
ls -lh *.deb
```

应输出**同上的两个文件**。

## 3. 安装并应用内核

安装内核：

```bash
sudo apt install ./*.deb
```

更新 GRUB 并检查已安装内核：

```bash
sudo update-grub
grep -E "menuentry 'Ubuntu, with Linux (6\.1|5\.15)" \
  /boot/grub/grub.cfg
```

应输出新旧两个内核版本：

```bash
menuentry 'Ubuntu, with Linux 6.1.177-0601177-generic (recovery mode)' --class ubuntu --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-6.1.177-0601177-generic-recovery-47d2fbc9-4109-48a7-a4af-b6869f23db28' {
menuentry 'Ubuntu, with Linux 5.15.0-67-generic (recovery mode)' --class ubuntu --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-5.15.0-67-generic-recovery-47d2fbc9-4109-48a7-a4af-b6869f23db28' {
```

检查无误后，重启系统，会自动选择更新的 6.1.177 版本内核：

```bash
sudo reboot
```

重启完成后，Wi-Fi 驱动应已经正常加载，此时 `uname -r` 检查内核版本，输出应为 `6.1.177-0601177-generic`。















