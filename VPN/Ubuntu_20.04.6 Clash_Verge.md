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

## 2. Clash Verge 配置代理

启动软件后，在`订阅`页卡填入订阅地址，点击`导入`。导入成功会显示添加的订阅：



在`代理`页卡，选择`规则`模式。可使用`延迟测试`功能，测速选择节点：




右上角图标处展开，此时应显**规则模式**，并且`系统代理`未开启时，操作系统网路设置中的网络代理应显示为**关**：






开启`系统代理`，操作系统网路设置中的网络代理应显示为**手动**，并且已自动填入所使用的端口：




此时桌面软件已经可以使用代理。

