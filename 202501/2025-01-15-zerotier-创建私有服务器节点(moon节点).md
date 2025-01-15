# ZeroTier 创建私有服务器节点(Moon节点)
- URL: https://wang.mx/posts/zerotier-creating-moons
- Added At: 2025-01-15 10:23:03
- [Link To Text](2025-01-15-zerotier-创建私有服务器节点(moon节点)_raw.md)

## TL;DR
文章介绍了如何通过自建ZeroTier的`moon`节点来解决NAS设备因公网IP受限的问题。内容包括ZeroTier的安装、生成和编辑`moon`配置文件、签名配置文件、加入`moon`节点以及验证节点类型等步骤。通过自建`moon`节点，用户可以提升ZeroTier网络的稳定性和性能。

## Summary
1. **背景介绍**：
   - **公网IP问题**：由于运营商对公网IP的严格管理，NAS设备无法直接获取公网IP，导致其功能受限。
   - **解决方案**：常见的解决方案包括FRP、NPS和ZeroTier等。

2. **ZeroTier简介**：
   - **默认配置**：ZeroTier默认使用官方的一组根服务器进行节点查找。
   - **自建节点**：ZeroTier允许用户自建节点，称为`moon`节点，与官方的`行星`节点相对应。

3. **安装ZeroTier**：
   - **安装命令**：使用官方脚本安装ZeroTier，命令为`curl -s https://install.zerotier.com/ | sudo bash`。
   - **安装结果**：安装完成后，系统会自动创建服务并显示节点ID。

4. **生成moon配置文件**：
   - **工具使用**：使用`zerotier-idtool`工具从`identity.public`生成`moon.json`配置文件。
   - **文件结构**：生成的`moon.json`文件包含节点ID、根节点信息、签名密钥等。

5. **编辑moon配置文件**：
   - **添加稳定节点**：编辑`moon.json`文件，向`roots.stableEndpoints`部分添加服务器的IP和端口信息。

6. **签名moon配置文件**：
   - **生成签名文件**：使用`zerotier-idtool genmoon moon.json`命令生成签名后的文件，文件名类似于`000000<nodeID>.moon`。

7. **加入moon节点**：
   - **创建目录**：在各节点的ZeroTier安装目录下创建`moons.d`目录。
   - **复制文件**：将生成的`000000<nodeID>.moon`文件复制到`moons.d`目录。
   - **加入方式**：
     - **文件复制**：将`000000<nodeID>.moon`文件复制到节点的`moons.d`目录并重启服务。
     - **命令加入**：使用`sudo zerotier-cli orbit 000000<nodeID> 000000<nodeID>`命令加入moon节点。

8. **验证**：
   - **查看节点类型**：在常规节点使用`sudo zerotier-cli listpeers`命令查看节点时，可以看到moon节点的类型已经从`LEAF`变成了`MOON`。
