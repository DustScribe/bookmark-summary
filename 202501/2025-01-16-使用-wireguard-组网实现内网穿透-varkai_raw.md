Title: 使用 WireGuard 组网实现内网穿透 | varkai

URL Source: https://varkai.com/posts/operation/use-wireguard-networking-to-achieve-intranet-penetration/

Markdown Content:
前言
--

最近有个需求，就是希望在公司或者外面的时候能够访问到家里提供的网络服务，例如：文件共享、照片存储等。但是我家里的网络没有提供公网地址，在外面是无法直接访问的，几经搜寻之后，发现可以使用 WireGurad 组件虚拟专用局域网实现内网的穿透，从而实现在外面访问家里的内网服务。

本文将介绍如何在 Debian 12 上安装和配置 WireGuard，它将充当中转服务器。还将展示如何在 Linux、Windows 和 macOS 上将 WireGuard 配置为客户端。客户端的流量将通过 Debian 12 服务器进行路由。

通过 WireGuard 组建虚拟专用网络，可用于防止中间人攻击、匿名上网、绕过受地理限制的内容或允许在家工作的同事安全地连接到公司网络。

下面是 WireGuard 官网的介绍：

> WireGuard 是一种极其简单但快速且现代的 VPN，它利用了最先进的加密技术。它的目标是比 IPsec 更快、更简单、更精简和更有用，同时避免令人头疼的问题。其旨在提供比 OpenVPN 更高的性能。WireGuard 被设计为在嵌入式接口和超级计算机等上运行的通用 VPN，适用于许多不同的环境。虽然最初仅支持 Linux，但现在可以跨平台（Windows、macOS、BSD、iOS、Android）广泛部署。

通过 WireGuard 可以将广域网上的主机连接起来，形成一个局域网。只需要有一台具有固定公网 IP 的服务器，就可以将其作为我们搭建的局域网的中心节点，让其他的主机（不论是否有公网IP，不论是否在NAT内），都通过这个中心节点和彼此相连。由此就构建了一个中心辐射型的局域网，实现了内网穿透等功能。

前提条件
----

1.  **公网服务器：** 一台具有公网 IP 地址的 Linux 服务器，我这里采用的是 Debian 12 系统，这台服务器充当中转站，负责将外部请求转发到相应的内部网络。
2.  **内网服务器：** 在家庭内网中，也需要准备一台 Linux 服务器做内部局域网的地址转发。

网络拓扑
----

![Image 11](https://varkai.com/posts/operation/use-wireguard-networking-to-achieve-intranet-penetration/images/1.png)

*   **Peer1** - 公网服务器（OS：Debian 12）
*   **Peer2** - 家庭内网服务器 （OS：Debian12）
*   **Peer3** - 需要访问家庭网络的外部客户端（OS：任意 WireGuard 支持的平台，有关 WireGuard 所有受支持平台的安装说明，请访问 [https://wireguard.com/install/](https://wireguard.com/install/)）

WireGuard 组网配置
--------------

### 配置 Peer1 中继服务器

#### 安装 WireGuard

```
$ sudo apt install wireguard
```

#### 配置 WireGuard

1.  生成服务端密钥对

执行以下命令后，将在 `/etc/wireguard` 目录下生成私钥文件 `privatekey` 和公钥文件 `publickey` ：

```
$ wg genkey | sudo tee /etc/wireguard/privatekey | wg pubkey | sudo tee /etc/wireguard/publickey
```

2.  创建配置文件

在 `/etc/wireguard` 目录下创建一个名为 `wg0.conf` 的配置文件，使用编辑器打开并编写配置：

```
$ sudo vim /etc/wireguard/wg0.conf
```

配置文件内容如下：

```
[Interface]
Address = 10.0.0.1/24
ListenPort = 51820
PrivateKey = YOUR_SERVER_PRIVATE_KEY
SaveConfig = true
PostUp = iptables -A FORWARD -i %i -j ACCEPT; iptables -A FORWARD -o %i -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i %i -j ACCEPT; iptables -D FORWARD -o %i -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE
```

配置文件中 `Interface` 节点的设置含义：

*   **Address** - WireGuard 的接口地址，可以从为专用网络保留的地址范围（10.0.0.0/8、172.16.0.0/12 或 192.168.0.0/16）中选择一个 IP 地址。
    
*   **ListenPort** - 服务的监听端口，这里使用的是 UDP 端口。
    
*   **PrivateKey** - 服务端私钥，可以通过 `sudo cat /etc/wireguard/privatekey` 查看。
    
*   **SaveConfig** - 当设置为 `true`，关闭 WireGuard 接口时，将当前状态保存到配置文件中。
    
*   **PostUp** - 在启动接口之前执行的命令或脚本。 注意：这里需要将 `POSTROUTING -o` 后面的网络接口名称 `eth0` 替换成你自己服务器的默认网络接口名称，可以通过下面的命令查看默认网络接口名称：
    
    ```
    $ ip -o -4 route show to default | awk '{print $5}'
    ```
    
*   **PostDown** - 在关闭接口之前执行的命令或脚本。一旦接口关闭，iptables 规则将被删除。这里同样的也需要将网络接口名称 `eth0` 替换成你自己服务器的默认网络接口名称。
    

设置 `/etc/wireguard` 目录下所有文件的权限为 `600`，确保服务的安全性。

```
$ sudo chmod 600 /etc/wireguard/*
```

完成以上步骤后，使用 `wg0` 配置文件中的设置启动接口：

要检查接口状态和配置，请运行：

还可以使用以下命令验证接口状态：

WireGuard 可以使用 Systemd 进行管理，运行以下命令设置 WireGuard 接口开机自启动：

```
$ sudo systemctl enable wg-quick@wg0
```

#### 网络和防火墙配置

必须启用 IP 转发才能使 NAT 正常工作。

打开 `/etc/sysctl.conf` 文件：

```
$ sudo vim /etc/sysctl.conf
```

添加或取消注释以下行：

保存文件后执行以下命应用更改：

如果系统启用了防火墙，则需要在防火墙放行 UDP 端口 `51820` 的流量，我使用的是 ufw 软件管理防火墙，相应的命令如下：

```
$ sudo ufw allow 51820/udp
```

到这里，WireGuard 的服务端就已经设置好了。

### 配置 Peer2 内网服务器

#### 开启 IP 地址转发

开启 IP 地址转发后，才能将其它客户端访问内部局域网的数据转发到相应的目标机器。

打开 `/etc/sysctl.conf` 文件：

```
$ sudo vim /etc/sysctl.conf
```

添加或取消注释以下行：

保存文件后执行以下命应用更改：

#### 安装 WireGuard

```
$ sudo apt install wireguard
```

#### 配置 WireGuard

配置过程与配置 **Peer1** 的过程几乎相同。首先，生成公钥和私钥：

```
$ wg genkey | sudo tee /etc/wireguard/privatekey | wg pubkey | sudo tee /etc/wireguard/publickey
```

在 `/etc/wireguard` 目录下创建一个名为 `wg0.conf` 的配置文件，使用编辑器打开并编写配置：

```
$ sudo vim /etc/wireguard/wg0.conf
```

配置文件内容如下：

```
[Interface]
PrivateKey = YOUR_CLIENT_PRIVATE_KEY
Address = 10.0.0.2/24
PostUp = iptables -A FORWARD -i %i -j ACCEPT; iptables -A FORWARD -o %i -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i %i -j ACCEPT; iptables -D FORWARD -o %i -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE

[Peer]
PublicKey = YOUR_SERVER_PUBLIC_KEY
Endpoint = 1.2.3.4:51820
AllowedIPs = 10.0.0.0/24
PersistentKeepalive = 25
```

配置文件中 `Interface` 节点的设置含义：

*   **PrivateKey** - 本机客户端的私钥，可以通过 `sudo cat /etc/wireguard/privatekey` 查看。
    
*   **Address** - 本机客户端的接口地址。
    
*   **PostUp** - 在启动接口之前执行的命令或脚本。 注意：这里需要将 `POSTROUTING -o` 后面的网络接口名称 `eth0` 替换成你自己服务器的默认网络接口名称，可以通过下面的命令查看默认网络接口名称：
    
    ```
    $ ip -o -4 route show to default | awk '{print $5}'
    ```
    
*   **PostDown** - 在关闭接口之前执行的命令或脚本。一旦接口关闭，iptables 规则将被删除。这里同样的也需要将网络接口名称 `eth0` 替换成你自己服务器的默认网络接口名称。
    

配置文件 `Peer` 节点的设置含义：

*   **PublicKey** - Peer1（中继服务器）的公钥，可以通过在 Peer1 服务器上运行 `sudo cat /etc/wireguard/publickey` 查看。
*   **Endpoint** - 指定远端 Peer1（中继服务器）的公网地址和监听端口。
*   **AllowedIPs** - 需要进行路由转发的目标网段，可以是以逗号分隔的 IPv4 或 IPv6 地址列表。
*   **PersistentKeepalive** - 表示每隔多少秒发送一次 ping 来检查连通性。

### 配置 Peer3 客户端

Peer3 做为需要访问家庭内部网络的客户端，这里主要以 Windows 为例进行配置演示。

从 [WireGuard 网站](https://download.wireguard.com/windows-client/) 下载并安装 Windows MSI 软件包。

安装完成后，打开 WireGuard 应用程序后，单击 `新建隧道` -\> `新建空隧道...` ，如下图所示：

![Image 12](https://varkai.com/posts/operation/use-wireguard-networking-to-achieve-intranet-penetration/images/2.png)

密钥对会自动创建并显示在弹出的编辑框中：

![Image 13](https://varkai.com/posts/operation/use-wireguard-networking-to-achieve-intranet-penetration/images/3.png)

输入隧道的名称后并编辑配置，如下所示：

```
[Interface]
PrivateKey = UKbdobnRCZlycBkHZQAD7hPVjicoKQCM1ktBZhGLfno=
Address = 10.0.0.3/24

[Peer]
PublicKey = YOUR_SERVER_PUBLIC_KEY
Endpoint = 1.2.3.4:51820
AllowedIPs = 10.0.0.0/24, 192.168.1.0/24
PersistentKeepalive = 25
```

在 `Interface` 节点添加：

*   **Address** - 本机客户端的接口地址。

在 `Peer` 节点添加：

*   **PublicKey** - Peer1（中继服务器）的公钥，可以通过在 Peer1 服务器上运行 `sudo cat /etc/wireguard/publickey` 查看。
*   **Endpoint** - 指定远端 Peer1（中继服务器）的公网地址和监听端口。
*   **AllowedIPs** - 需要进行路由转发的目标网段，这里需要额外添加需要访问的家庭内网网段。
*   **PersistentKeepalive** - 表示每隔多少秒发送一次 ping 来检查连通性。

完成后，点击 `保存` 按钮。

### 将客户端添加到中继服务器

最后一步是将所有客户端的公钥和 IP 地址添加到中继服务器。

#### 添加 Peer2 客户端

```
$ sudo wg set wg0 peer ${Peer2 公钥} allowed-ips 10.0.0.2/32,192.168.1.0/24
```

#### 添加 Peer3 客户端

```
$ sudo wg set wg0 peer ${Peer3 公钥} allowed-ips 10.0.0.3/32
```

完成后，返回客户端计算机并启动隧道接口。

### 启动客户端并检查连接状态

#### 启动 Peer2 客户端

在 Peer2 服务器上运行以下命令以启动接口：

现在，Peer2 服务器应该已连接到 Peer1 服务器，可以通过以下方式检查连接：

要停止隧道，允许如下命令关闭接口：

#### 启动 Peer3 客户端

打开 WireGuard 软件后，点击主界面的 `连接` 按钮，连接到中继服务器后，隧道状态将变更为 `已连接`。

此时就可以通过 Peer3 这台客户端访问家庭局域网了。
