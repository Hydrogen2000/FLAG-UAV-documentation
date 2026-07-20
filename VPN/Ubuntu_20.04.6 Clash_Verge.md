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

<img src="/VPN/images/8.png" width="800">

在`代理`页卡，选择`规则`模式。可使用`延迟测试`功能，测速选择节点：

<img src="/VPN/images/9.png" width="800">

## 3. Clash Verge 开启代理

桌面右上角图标处展开，此时应显示**规则模式**。开启`系统代理`，操作系统网路设置中的网络代理应显示**手动**，并且已自动填入所使用的端口：

<img src="/VPN/images/11.png" width="600">

此时应用已经可以使用代理。

关闭`系统代理`，操作系统网路设置中的网络代理应显示为**关**：

<img src="/VPN/images/10.png" width="600">

终端使用代理：

```bash
export http_proxy=http://127.0.0.1:20171
export https_proxy=http://127.0.0.1:20171
export all_proxy=socks5h://127.0.0.1:20170
export HTTP_PROXY="$http_proxy"
export HTTPS_PROXY="$https_proxy"
export ALL_PROXY="$all_proxy"
```
**注意**：仅对当前终端有效，新开启终端需要重新输入指令。

终端清除代理：

```bash
unset http_proxy https_proxy all_proxy
unset HTTP_PROXY HTTPS_PROXY ALL_PROXY
```

为了简化输入，可以编辑 **bashrc** 添加指令：
```bash
sudo gedit ~/.bashrc
```

在文件末尾写入：
```bash
proxy_on()
{
    export http_proxy=http://127.0.0.1:20171
    export https_proxy=http://127.0.0.1:20171
    export all_proxy=socks5h://127.0.0.1:20170

    export HTTP_PROXY="$http_proxy"
    export HTTPS_PROXY="$https_proxy"
    export ALL_PROXY="$all_proxy"

    echo "Terminal proxy enabled"
}

proxy_off()
{
    unset http_proxy https_proxy all_proxy
    unset HTTP_PROXY HTTPS_PROXY ALL_PROXY

    echo "Terminal proxy disabled"
}
```

使配置立即生效：
```bash
source ~/.bashrc
```

此后，只需输入 `proxy_on` 和 `proxy_off` 使用、清除代理。




此时桌面软件已经可以使用代理。

