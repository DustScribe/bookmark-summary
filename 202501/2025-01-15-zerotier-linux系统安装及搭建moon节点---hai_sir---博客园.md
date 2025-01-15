# ZeroTier Linux系统安装及搭建moon节点 - hai_sir - 博客园
- URL: https://www.cnblogs.com/z-h-q/p/18138653
- Added At: 2025-01-15 09:57:13
- [Link To Text](2025-01-15-zerotier-linux系统安装及搭建moon节点---hai_sir---博客园_raw.md)

## TL;DR
本文详细介绍了在Linux系统上安装ZeroTier并搭建moon节点的步骤，包括下载安装、加入网络、生成和编辑配置文件、创建moon文件、重启服务以及验证搭建成功的过程。

## Summary
1. **ZeroTier简介**：ZeroTier是一种用于创建虚拟局域网的网络工具，支持跨平台使用，适用于Linux系统。

2. **安装步骤**：
   - **下载安装**：通过curl命令下载并安装ZeroTier One。
     ```bash
     curl -s https://install.zerotier.com/ | sudo bash
     ```

3. **加入网络**：
   - **加入网络命令**：使用`zerotier-cli join`命令加入指定的网络ID。
     ```bash
     sudo zerotier-cli join （NetWork ID）
     ```
   - **后台信任设备**：在ZeroTier官网后台勾选信任新加入的设备。

4. **搭建moon节点**：
   - **进入安装目录**：默认路径为`/var/lib/zerotier-one`。
     ```bash
     cd /var/lib/zerotier-one
     ```
   - **生成配置文件**：使用`zerotier-idtool initmoon`生成`moon.json`配置文件。
     ```bash
     zerotier-idtool initmoon identity.public >> moon.json
     ```
   - **编辑配置文件**：修改`moon.json`中的`stableEndpoints`为云服务器的公网IP和端口。
     ```bash
     vim moon.json
     ```
   - **生成moon文件**：使用`zerotier-idtool genmoon`生成moon文件。
     ```bash
     zerotier-idtool genmoon moon.json
     ```
   - **开放端口**：在云服务商后台开放9993端口，协议为UDP。

5. **创建moon文件**：
   - **创建目录**：在`/var/lib/zerotier-one`目录下创建`moons.d`文件夹。
     ```bash
     mkdir moons.d
     ```
   - **移动moon文件**：将生成的moon文件移动到`moons.d`目录。
     ```bash
     mv 000000xxxxxxxxxx.moon moons.d/
     ```

6. **重启服务**：
   - **重启ZeroTier服务**：使用`systemctl restart`命令重启ZeroTier服务。
     ```bash
     systemctl restart zerotier-one
     ```

7. **查询节点信息**：
   - **查询本机节点地址**：使用`zerotier-cli info`命令查询本机的ZeroTier节点地址。
     ```bash
     zerotier-cli info
     ```
   - **列出节点信息**：使用`zerotier-cli listpeers`命令列出所有节点信息。
     ```bash
     zerotier-cli listpeers
     ```
   - **加入moon节点**：使用`zerotier-cli orbit`命令加入moon节点。
     ```bash
     zerotier-cli orbit ******** *******
     ```

8. **验证搭建成功**：
   - **查看节点信息**：使用`zerotier-cli listpeers`命令查看是否显示moon节点，确认搭建成功。

9. **总结**：本文详细介绍了在Linux系统上安装ZeroTier并搭建moon节点的步骤，包括下载安装、加入网络、生成和编辑配置文件、创建moon文件、重启服务以及验证搭建成功的过程。
