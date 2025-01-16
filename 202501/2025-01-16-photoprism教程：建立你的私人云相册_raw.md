Title: Photoprism教程：建立你的私人云相册

URL Source: https://taoofcoding.tech/blogs/2024-01-07/the-tutor-of-build-your-photopri

Markdown Content:
几周前我讲了photoprism这个开源的软件, 可以帮助你很好的管理你的相册及视频. 在那篇文章中我对photoprism做了大致的介绍与说明.

如果你想了解photoprism, 可以参阅[用开源的photoprism来打造你个人的专属Google Photo](https://taoofcoding.tech/blogs/2023-12-03/open-source-replacement-of-google-photo)

这篇文章主要是再简单的说下如何安装与使用它. 主要包括

*   前提条件
*   安装photoprism
*   导入及索引你的相片
*   互联网访问策略
*   相册及视频的同步与备份策略

前提条件
----

其实我认为最重要的前提条件是**折腾的意愿**

> 折腾的意愿

使用一款开源软件,而不是现成的阿里云盘等现成的免费或SAAS服务, 最重要的是你有这种折腾的意愿. 而折腾则意味着你要去搜索资料,去学习,去尝试等.

折腾有好有坏, 好处在于你能学到很多, 而折腾一个自己的相册管理程序, 更能让你更安全,更可靠的管理你自己的相册数据, 不用担心哪一天某个云服务不提供服务了或要收费了.

当然坏处就是你需要付出时间与成本. 不过付出才有可能会有收获.

> 懂一点Linux及Docker相关的知识

安装photoprism等一系列操作, 都需要你懂一点Linux与Docker.

当然对于程序员来说, 这可能不是个大问题. 但对于非程序员来说, 这个门槛足够高了. 当然如果你愿意学习, 问题也不大.

> 服务器资源

部署自己的私有的东西, 你得准备自己的服务器资源. 可以是:

*   云服务资源 (如阿里云服务器等)
*   家庭私有服务器
*   自己的电脑或笔记本

我就是用的一个2014年的旧款Mac Mini搭建了一个家庭私有Linux服务器, 虽然这个8G的旧Mac很老了,但在上面装个Debian, 搭建一堆自己的东西的确非常方便.

当然,你没有的话,就考虑使用自己的电脑或笔记本吧. 安装在上面, 有需要再启动及使用, 毕竟相片并不是时时需要在线的.

> 1.  准备一个服务资源

如上面所说的, 可以是云服务,你自己的家庭服务或自己的电脑都可以.

操作系统不限, Windows, MacOS以及Linux都支持

最低资源需求: **2 cores**, **3 GB**

> 2.  准备好Docker环境

photoprism是基于GO语言的一款工具. 你当然可以选择在本地安装GO, 在运行它.

但相比这种方式,我个人更偏好Docker的方式来部署. 简单,方便,易于迁移.在这篇文章中, 我也只介绍基于Docker的方式来安装photoprism. 如果你想原生GO来使用photoprism, 建议访问官网来了解.

关于Docker环境, 这个东西Linux还好说, 对于Windows与MacOS, 我建议

*   MacOS: 考虑使用orbstack(商业软件,对个人免费)或lima(开源软件)
*   Windows: 使用WSL Linux子系统

不是非常建议使用Docker Desktop这个软件, 特别是在Windows下, 体验非常不好, 而且镜像体积巨大.

另外, 安装好docker-compose工具, 我会使用docker-compose来部署. 因为docker-compose的配置是写在yml中, 这样比较容易修改与查看部署的各种配置信息.

关于如何安装Docker以及Docker Compose不再这篇文章的范围之内. 建议参阅官网.

> 3.  确定你的数据库

photoprism支持几种不同的数据库, 主要是SQLite 3以及MariaDB 10.5.12 +. 确定你想使用的数据库, 其中SQLite是一个嵌入式简单的数据库.

如果只是想体验或尝试,使用SQLite就可. 如果想把它做为正式使用, 当然就得选择MariaDB了.

另外, MySQL已不再被支持了, photoprism官网说是MySQL新版本缺失了一些特性.

> 4.  docker-compose配置

**创建一个空目录**

在合适的地方创建一个空目录, 比如名为`photo`, 我们会把配置以及数据存储在这个目录下.

同时,在这个目录下创建三个子目录,分别是`import`,`originals`,`storage`,以及一个空文件`docker-compose.yml`

目录的整体结构大致如下:

```
photo
├── docker-compose.yml
├── import
├── originals
└── storage
```

三个子目录后面会解释具体用处

**编辑docker-compose.yml**

编辑docker-compose.yml文件,在里面写入如入内容

```
version: '3.5'

services:
  photoprism:
    image: photoprism/photoprism:latest
    container_name: photoprism
    stop_grace_period: 10s
    restart: always
    security_opt:
      - seccomp:unconfined
      - apparmor:unconfined
    ports:
      - "2342:2342"
    environment:
      PHOTOPRISM_ADMIN_USER: "admin"                 # 用户名
      PHOTOPRISM_ADMIN_PASSWORD: "admin1234"         # 用户密码(不少于8位)
      PHOTOPRISM_AUTH_MODE: "password"               # 授权模式, public 或 password

      # 数据库配置, 这里配置了sql
      PHOTOPRISM_DATABASE_DRIVER: "sqlite"         # 使用内置的SQLite数据库

      # 正式使用,建议使用mariadb数据库
      
      #PHOTOPRISM_DATABASE_DRIVER: "mysql"                # 使用MariaDB 10.5 以上的数据库
      #PHOTOPRISM_DATABASE_SERVER: "192.168.50.16:3306"   # MariaDB数据库地址 (hostname:port)
      #PHOTOPRISM_DATABASE_NAME: "photoprism"             # MariaDB数据库名称
      #PHOTOPRISM_DATABASE_USER: "photoprism"             # MariaDB用户名
      #PHOTOPRISM_DATABASE_PASSWORD: "photoprism"         # MariaDB密码

      # 网站标题
      PHOTOPRISM_SITE_CAPTION: "我的相册"
      
    working_dir: "/photoprism" # 不要改动这一项
    
    volumes:
      - "./originals:/photoprism/originals"               # 原始照片目录
      - "./import/Z:/photoprism/import"                   # 待导入照片目录
      - "./storage:/photoprism/storage"                   # photoprism程序产生的各种缓存,文件,索引等目录
```

如果你使用过docker-compose, 上面这些就非常你应该能很快读懂.

其中,最主要的是几个环境变量设置

*   `PHOTOPRISM_ADMIN_USER`, `PHOTOPRISM_ADMIN_PASSWORD`,`PHOTOPRISM_AUTH_MODE`: 这三项是设置基本的登录方式及初始用户名密码 (后续可进入系统修改密码)
*   `PHOTOPRISM_DATABASE_DRIVER`: 数据库模式, sqlite或mysql. 这份配置中使用了sqlite
*   `PHOTOPRISM_DATABASE_DRIVER`等: MariaDB数据库地址设置 (请注意, photoprism不再支持mysql), 如果要使用mysql, 请取消这些参数前面的`#`注释符号并把`PHOTOPRISM_DATABASE_DRIVER`值改为`mysql`
*   `PHOTOPRISM_SITE_CAPTION`: 自定义网站标题

关于三个目录

*   `originals`: 原始照片目录, 你可以把你存在的照片放在这个目录
*   `import`: 待导入照片, 这个目录的照片会等待导入并被photoprism处理 (处理是指对照片做分析与索引,存入原始目录等)
*   `storage`: 这个目录是photoprism程序产生的各种文件,比如索引照片缩略图,缓存等

需要注意,这份配置中只列出了最基本必须的一些设置项, photoprism可以配置的项非常多, 建议参考官网文档了以解.

**启动服务**

进入`photo`目录,使用如下命令启动

```
docker-compose up -d
```

第一次启动会下载镜像需要一些时间, 启动完成没有问题就可以使用了.

访问 [http://127.0.0.1:2342](http://127.0.0.1:2342/) , 如果没有意外,你就能看到登录页面了

![Image 12: 登录页面](https://images.fosstea.com/2024/01/login-photoprism.png)

使用刚刚配置中的用户名密码登录就可以了. 登录进去会发现什么都没有, 当然, 这是因为我们没有还没有导入照片.

第一次导入及索引
--------

基于Docker来安装photoprism其实非常简单. 这也是我推荐大多数情况下都用Docker的原因. 不用操心各种环境, 依赖等问题.

但你现在会发现,你还没有任何照片视频. 你现在的需求其实是两个:

*   导入旧有的存在的相片
*   后续如何同步新的相片

先讲下如何导入旧的存在的相片并完成索引. 所谓索引是指对照片的信息元数据,比如地点,大小,拍摄时间等做提取, 同时对照片生成各种大小的缩略图照片. (你在UI上看到的小图,其实是缩略图,而不是原照片)

_**那如何导入你存在的相片并完成索引呢?**_

前面的配置文件中,提及了两个目录, 一个是`originals`,另一个是`import`. 旧有的相片可以放在`import`目录下, 也可以放在`originals`目录下.

那究竟放在哪个目录?

> `originals`

`originals`是photoprism存放相片原文件的地方. 所有photoprism的相片最终的原文件,都在这个目录下.

你可以把已有的旧相片直接放到这个目录下.

但是, 由于photoprism没有对你这些已存在的相片做**索引**, 所以你需要在UI上触发一个全量索引操作.

![Image 13: 全量索引](https://images.fosstea.com/2024/01/photoprism-full-index.webp)

进入**资料库**, 然后点击**索引**页

在这里,你可以做一次**完全重新扫描**

> `import`

你也可以把存在的照片放到`import`目录下.

然后在**资料库**的**导入**页中, 选择你的目录, 导入你的照片.

![Image 14: 导入相片](https://images.fosstea.com/2024/01/photoprism-import-photo.webp)

> 区别与选择

好吧,你可能会有点困惑, 似乎随便放哪一个目录都可以. 其实不是的, 它们是有区别的.

它们之间的共同点是:

*   都会对照片做索引, 也就是提取照片的元数据及生成缩略图等

不同点在于

*   `import`目录下的照片,会按照日期重新进入命名,并将其存入`originals`目录下.
*   `import`相当于一个待处理的临时目录, 而`originals`则是你原始照片存放的真正目录

_**建议**_

所以, 你的已有照片究竟是放`import`还是`originals`, 关键点在于你是否希望photoprismt重新命名你的照片.

*   如果你的照片是已经有规则存放好的, 就把它放在`originals`,
    
*   否则把它放`import`中, 让程序按照日期重新整理你的照片,是个非常不错的选择.
    

_**需要注意的是, 索引是非常耗时的操作**_, 我当时7-8千张照片,索引花费了几个小时.

重新整理后的效果目录如下:

```
2000
└── 01
    ├── 20000101_090020_04FF387A.jpg
    ├── 20000101_090026_E7546984.jpg
    ├── 20000101_090027_4B306DB8.jpg
    ├── 20000101_090050_63B2D167.jpg
    ├── 20000101_090100_D17AE19A.jpg
    ├── 20000101_090111_D8648B18.jpg
    ├── 20000101_090131_FDA5E957.jpg
    ├── 20000101_090146_245BDD02.jpg
    ├── 20000101_090200_07FE3819.jpg
    ├── 20000101_090224_F0190680.jpg
    ├── 20000101_090341_3F2E89A5.jpg
    └── 20000101_090712_7D9EAF39.jpg
```

上面这个就是,2000年,01月份的相片, 每个相片都以时间 + 随机码来命名.

我迁移相片时, 本来非常杂乱, 经过photoprismt这么一处理, 变成了按日期存储的非常有规律的文件了.

待续
--

到上面这步完成后, 你已完全拥有了一个自己的相片程序了. 自己管理自己所有相片.

但这并不是一个完结, 事实上, 你可能还有很多问题或有待完善的地方, 比如:

*   如何在各种设备上浏览这个服务?
*   如果是在家里服务器部署的,如何映射外网访问?
*   如何同步设备上的相片?
*   如何备份我的相片以保证相片数据的安全?

受篇幅所限, 我这里只能简单讲下我的策略:

*   photoprism对浏览器的支持非常好,在任何设备上都可以用浏览器访问.
*   结合`tailscale` + 最便宜的`阿里云服务器`来映射外网访问
*   使用`filestash` + `webdav`来做到批量上传相片
*   用`rsync`来定期同步与备份原始相片数据到移动硬盘

这里面涉及一些开源的服务或工具, 后续有机会再分享.

但还是最开始那个话, 你得去**折腾**. 折腾是学习必不可少的一个部分.
