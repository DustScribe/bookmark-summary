Title: ZeroTier 创建私有服务器节点(Moon节点)

URL Source: https://wang.mx/posts/zerotier-creating-moons

Markdown Content:
没有公网 IP 的 NAS 无异于被阉割的太监。现在各运营商对公网 IP 管理政策来看怕是不会再有了，所以还是另寻它路。

目前常见的有 FRP、NPS、 ZeroTier 等方案。

FRP 是自己搭建一个公网服务器，所有流量经过公网服务器中转。ZeroTier 默认使用官方的一组根服务器进行节点查找。

ZeroTier 也允许自己在服务器上搭建自己的节点，这种节点称之为 `moon` 节点。 （官方根节点称之为行星节点，自建节点叫月球节点，很合情合理是吧 ）

首先使用官方脚本安装 ZeroTier：

```
curl -s https://install.zerotier.com/ | sudo bash
```

安装完成后会自动创建服务，并且显示节点 ID:

```

Created symlink /etc/systemd/system/multi-user.target.wants/zerotier-one.service → /lib/systemd/system/zerotier-one.service.

*** Enabling and starting ZeroTier service...
Synchronizing state of zerotier-one.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable zerotier-one

*** Waiting for identity generation...

*** Success! You are ZeroTier address [ abcxxxxx123 ].
```

ZeroTier 将被安装在 `/var/lib/zerotier-one/` 位置，该目录下包含自己的身份信息文件 `identity.public` 和 `identity.secret` （相当于公钥和私钥）。

使用 `zerotier-idtool` 工具从 `identity.public` 生成 moon 配置文件 `moon.json` ：

```
zerotier-idtool initmoon /var/lib/zerotier-one/identity.public >> moon.json
```

生成的 `moon.json` 文件结构如下：

```
{
 "id": "3f80270f25",
 "objtype": "world",
 "roots": [
  {
   "identity": "xxxx",
   "stableEndpoints": []
  }
 ],
 "signingKey": "xxxx",
 "signingKey_SECRET": "xxxx",
 "updatesMustBeSignedBy": "xxxx",
 "worldType": "moon"
}
```

编辑上一步生成的 `moon.json` 文件中的 `roots` 部份，向 `roots.stableEndpoints` 部份添加稳定节点信息：

```
{
  "stableEndpoints": [ "服务器IP:9993" ]
}
```

使用 `zerotier-idtool genmoon moon.json` 命令得到一个签名后的文件(使用 `moon.json` 中定义的密钥签名)，文件名类似于： `000000<nodeID>.moon` 。

加入自己的 moon
----------

在各节点，安装完 ZeroTier 后， 在程序安装目录（Linux:`/var/lib/zerotier-one`、 Mac: `/Library/Application Support/ZeroTier/One` ）内创建名为 `moons.d` 的目录，将上一步在服务器节点生成的类似于 `000000<nodeID>.moon` 的文件复制到 `moons.d` 目录内。

在其它节点，可以通过2种方式加入到 moon 节点： - 将上面创建的世界定义文件 `000000<nodeID>.moon` 复制到节点自己的 `moons.d` 目录，并重启服务； - 使用命令 `sudo zerotier-cli orbit 000000<nodeID> 000000<nodeID>` 加入 moon， `orbit` 命令的第1个参数是 Moon 节点ID(`moon.json` 文件的 `id` 字段)， 第2个参数是 `moon.json` 文件中 `roots` 字段定义的任意节点，可以与第1个参数相同。

验证
--

然后在常规节点使用 sudo zerotier-cli listpeers 查看节点时，就能看到 moon 节点的类型已经从 LEAF 变成了 MOON
