# 使用 WireGuard 组网实现内网穿透 | varkai
- URL: https://varkai.com/posts/operation/use-wireguard-networking-to-achieve-intranet-penetration/
- Added At: 2025-01-16 09:18:09
- [Link To Text](2025-01-16-使用-wireguard-组网实现内网穿透-varkai_raw.md)

## TL;DR
本文介绍了如何通过WireGuard实现内网穿透，使外部客户端能够安全访问家庭内网服务。文章详细描述了网络拓扑、前提条件、WireGuard的安装与配置步骤，包括中继服务器、内网服务器和客户端的设置。最终通过配置确保各节点之间的通信安全可靠，实现外部访问家庭内网服务的目标。

## Summary
1. **需求背景**：
   - 用户希望在公司或外部访问家庭网络服务（如文件共享、照片存储等），但由于家庭网络没有公网地址，无法直接访问。
   - 通过使用 WireGuard 组件，可以实现虚拟专用局域网的内网穿透，从而在外网访问家庭内网服务。

2. **WireGuard 简介**：
   - WireGuard 是一种简单、快速且现代的 VPN，利用先进的加密技术，旨在比 IPsec 和 OpenVPN 更快、更简单、更精简。
   - 支持跨平台（Windows、macOS、BSD、iOS、Android）部署，适用于多种环境。

3. **网络拓扑**：
   - **Peer1**：公网服务器（Debian 12），充当中转服务器。
   - **Peer2**：家庭内网服务器（Debian 12），负责内部局域网的地址转发。
   - **Peer3**：外部客户端（支持 WireGuard 的平台），通过 Peer1 访问家庭内网。

4. **前提条件**：
   - 一台具有公网 IP 的 Linux 服务器（Debian 12）。
   - 家庭内网中的一台 Linux 服务器。

5. **WireGuard 组网配置**：
   - **Peer1 中继服务器配置**：
     - 安装 WireGuard：`sudo apt install wireguard`。
     - 生成服务端密钥对：`wg genkey | sudo tee /etc/wireguard/privatekey | wg pubkey | sudo tee /etc/wireguard/publickey`。
     - 创建配置文件 `wg0.conf`，配置内容包括接口地址、监听端口、私钥、IP 转发规则等。
     - 设置文件权限：`sudo chmod 600 /etc/wireguard/*`。
     - 启动接口并设置开机自启动：`sudo systemctl enable wg-quick@wg0`。
     - 启用 IP 转发和防火墙配置：修改 `/etc/sysctl.conf` 并放行 UDP 端口 `51820`。

   - **Peer2 内网服务器配置**：
     - 开启 IP 地址转发：修改 `/etc/sysctl.conf`。
     - 安装 WireGuard：`sudo apt install wireguard`。
     - 生成客户端密钥对并创建配置文件 `wg0.conf`，配置内容包括客户端私钥、接口地址、IP 转发规则等。
     - 配置 Peer 节点，指定中继服务器的公钥、公网地址和监听端口。

   - **Peer3 客户端配置（以 Windows 为例）**：
     - 下载并安装 WireGuard Windows 客户端。
     - 创建新隧道，配置客户端私钥、接口地址、中继服务器公钥、公网地址和监听端口。
     - 保存配置并启动隧道。

6. **将客户端添加到中继服务器**：
   - 添加 Peer2 客户端：`sudo wg set wg0 peer ${Peer2 公钥} allowed-ips 10.0.0.2/32,192.168.1.0/24`。
   - 添加 Peer3 客户端：`sudo wg set wg0 peer ${Peer3 公钥} allowed-ips 10.0.0.3/32`。

7. **启动客户端并检查连接状态**：
   - 在 Peer2 服务器上启动接口并检查连接状态。
   - 在 Peer3 客户端上启动隧道并检查连接状态，确保可以访问家庭局域网。

8. **总结**：
   - 通过 WireGuard 组网，可以实现内网穿透，使外部客户端能够安全访问家庭内网服务。
   - 配置过程涉及中继服务器、内网服务器和客户端的安装与配置，确保各节点之间的通信安全可靠。
