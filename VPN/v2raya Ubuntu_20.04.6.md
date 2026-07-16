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

很容易失败，需要**多尝试**运行几次，或者**科学上网**。*(鸡生蛋，蛋生鸡)*

## 二、v2rayA 配置使用

### 1. 启动服务

将 v2rayA 服务设置为开机自启动：

```bash
sudo systemctl enable --now v2raya
```

参数 `--now` 表示立即启动。

若想检查 v2rayA 运行状态，可以执行：

```bash
systemctl is-enabled v2raya
systemctl is-active v2raya
```

正常应该分别输出 "**enabled**" 和 "**active**"。

单次停止、启动、重启服务：*(应该用不到)*
```bash
sudo systemctl stop v2raya
sudo systemctl start v2raya
sudo systemctl restart v2raya
```

### 2. 网页配置代理

浏览器登入 `127.0.0.1:2017`，需要注册、登录账号：

<img src="/VPN/images/1.png" width="200">

按照对话框提示，或者右上角，`Import` 导入订阅链接，`Confirm` 确定：

<img src="/VPN/images/2.png" width="800">

<img src="/VPN/images/3.png" width="200">

成功订阅后，节点列表将显示在 "**SERVER**" 标签后；

`Update` 用于更新订阅：

<img src="/VPN/images/4.png" width="800">

选中节点后，左上角将出现 `PING` 用于测试连接；

未启动代理时，左上角状态显示为红色 "**Ready**"；

选择节点时 ***(最好只选一个)***，`Add to` 添加 `PROXY` 代理：

<img src="/VPN/images/5.png" width="800">

选中节点后，"**View**"、"**Share**" 标签变为蓝色，同时节点将显示在左上角 "**Proxy Groups: PROXY**"；

左上角 "**Ready**"，`Start` 开启，使其变为 "**Runing**"：

<img src="/VPN/images/6.png" width="800">

### 3. 开启代理

v2rayA 默认端口为：

127.0.0.1:20170 **SOCKS5**
127.0.0.1:20171 **HTTP 代理**
127.0.0.1:20172 **带分流规则的 HTTP 代理** *(一般用不到)*

系统应用使用代理：将Ubuntu操作吸引`设置`→


终端使用代理：

```bash
export http_proxy=http://127.0.0.1:20171;
export https_proxy=http://127.0.0.1:20171;
export all_proxy=socks5h://127.0.0.1:20170;
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





