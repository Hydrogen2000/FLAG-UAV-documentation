# v2rayA Ubuntu_20.04.6
Ubuntu 20.04.6 LTS 操作系统配置 v2rayA

## 一、v2rayA安装

由于 v2rayA 仓库的最新密钥已于2025年9月15日过期，截至2026年7月15日，未更新密钥，无法通过软件源添加密钥apt下载。

目前仅推荐使用官方安装脚本。

### 1. 下载官方安装脚本

```bash
wget -O /tmp/v2raya-installer.sh https://raw.githubusercontent.com/v2rayA/v2rayA-installer/main/installer.sh
```
参数 ‘-O’ 表示指定输出文件的位置和文件名。

‘/tmp’ 是 Linux 的临时文件目录，系统重启或定期清理时，这里的文件可能被删除。


