# Ubuntu_20.04.6 Clash_Verge

Ubuntu 20.04.6 操作系统安装配置 Clash Verge

## 1. Clash Verge 软件下载

安装软件包依赖：

```bash
sudo add-apt-repository universe
sudo apt update
sudo apt install libayatana-appindicator3-1 libwebkit2gtk-4.0-37 libgtk-3-0
```

需要先添加由开源社区维护的 `universe` 软件源分区，区别于由官方维护的 `main` 软件源分区。

由于所依赖软件包的版本限制，Clash Verge 在 Ubuntu 20.04.6 上支持的最新版为 1.7.7。对应 Releases 仓库地址如下，下载 **amd64** 版 **.deb** 安装包：

https://github.com/clash-verge-rev/clash-verge-rev/releases/tag/v1.7.7

