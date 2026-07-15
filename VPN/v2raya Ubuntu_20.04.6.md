# v2rayA Ubuntu_20.04.6
Ubuntu 20.04.6 LTS 操作系统安装、配置 v2rayA

## 一、v2rayA 安装

由于 v2rayA 仓库的最新密钥已于2025年9月15日过期，截至2026年7月15日，未更新密钥，无法通过软件源添加密钥apt下载。

目前仅推荐使用官方安装脚本。

### 1. 下载官方安装脚本

```bash
wget -O /tmp/v2raya-installer.sh https://raw.githubusercontent.com/v2rayA/v2rayA-installer/main/installer.sh
```
参数 `-O` 表示指定输出文件的位置和文件名。

`/tmp` 是 Linux 的临时文件目录，系统重启或定期清理时，这里的文件可能被删除。

### 2. 运行官方安装脚本

```bash
sudo sh /tmp/v2raya-installer.sh
```

很容易失败，需要**多尝试**运行几次，或者**科学上网**。(鸡生蛋，蛋生鸡)

## 一、v2rayA 配置使用

### 1. 启动服务

```bash
sudo systemctl enable --now v2raya
```

将 v2rayA 服务设置为开机自启动。

参数 `--now` 表示立即启动。

若想检查 v2rayA 运行状态，可以执行：

```bash
systemctl is-enabled v2raya
systemctl is-active v2raya
```

正常应该分别输出 "enabled" 和 "active"。

单次停止、启动、重启服务：(应该用不到)
```bash
sudo systemctl stop v2raya
sudo systemctl start v2raya
sudo systemctl restart v2raya
```


