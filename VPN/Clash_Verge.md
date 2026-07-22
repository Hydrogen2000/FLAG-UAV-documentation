# Clash_Verge

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

启动软件后，在**订阅**页卡填入订阅地址，点击**导入**。导入成功会显示添加的订阅：

<img src="/VPN/images/8.png" width="800">

在**代理**页卡，选择**规则**模式。可使用**延迟测试**功能，测速选择节点：

<img src="/VPN/images/9.png" width="800">

## 3. Clash Verge 开启代理

桌面右上角图标处展开，此时应显示“**规则模式**”。关闭**系统代理**：

<img src="/VPN/images/10.png" width="600">

此时，操作系统网路设置中的网络代理应自动为“**关**”，应用不使用代理。

通过 `env | grep -i proxy` 测试终端代理，应**无输出**。

通过 `curl -s https://api.ipify.org; echo` 测试代理公网IP，应**无输出**。

开启**系统代理**：

<img src="/VPN/images/11.png" width="600">

此时，操作系统网路设置中的网络代理应自动为“**手动**”，并且已填入所使用的**端口**，应用使用代理。

通过 `env | grep -i proxy` 测试终端代理，输出应如：

```bash
no_proxy=localhost,127.0.0.1,192.168.0.0/16,10.0.0.0/8,172.16.0.0/12,::1
https_proxy=http://127.0.0.1:7897/
NO_PROXY=localhost,127.0.0.1,192.168.0.0/16,10.0.0.0/8,172.16.0.0/12,::1
HTTPS_PROXY=http://127.0.0.1:7897/
HTTP_PROXY=http://127.0.0.1:7897/
http_proxy=http://127.0.0.1:7897/
ALL_PROXY=socks://127.0.0.1:7897/
all_proxy=socks://127.0.0.1:7897/
```

通过 `curl -s https://api.ipify.org; echo` 测试代理公网IP，应输出一个**区别于 192.168.x.x 的公网IP**。
