# Photoprism教程：建立你的私人云相册
- URL: https://taoofcoding.tech/blogs/2024-01-07/the-tutor-of-build-your-photopri
- Added At: 2025-01-16 07:03:56
- [Link To Text](2025-01-16-photoprism教程：建立你的私人云相册_raw.md)

## TL;DR
Photoprism是一款开源的个人相册和视频管理软件，提供类似Google Photos的功能。安装需要一定的Linux和Docker知识，并准备服务器资源。通过Docker部署后，用户可以导入和索引照片，支持外网访问和定期备份。虽然需要技术投入，但Photoprism提供了安全可靠的数据管理解决方案。

## Summary
1. **Photoprism简介**：Photoprism是一款开源软件，用于管理和组织个人相册和视频，提供类似Google Photos的功能。

2. **安装前提**：
   - **折腾意愿**：使用Photoprism需要用户有学习和尝试新技术的意愿，这涉及到搜索资料、学习和实验。
   - **技术知识**：需要基本的Linux和Docker知识，这对于非程序员可能是一个门槛。
   - **服务器资源**：需要准备服务器资源，可以是云服务、家庭服务器或个人电脑。

3. **安装步骤**：
   - **准备服务器资源**：可以是云服务、家庭服务器或个人电脑，操作系统不限。
   - **安装Docker环境**：推荐使用Docker来部署Photoprism，对于MacOS和Windows用户，建议使用特定的Docker工具。
   - **选择数据库**：Photoprism支持SQLite和MariaDB，SQLite适合体验，MariaDB适合正式使用。
   - **配置docker-compose**：创建必要的目录和配置文件，编辑docker-compose.yml以设置环境变量和目录映射。

4. **导入和索引照片**：
   - **导入旧照片**：可以将旧照片放入`originals`或`import`目录，`originals`目录用于存放原始照片，`import`目录用于待处理的照片。
   - **索引操作**：在UI上触发全量索引操作，提取照片的元数据并生成缩略图。

5. **互联网访问和备份策略**：
   - **浏览器访问**：Photoprism支持通过浏览器在任何设备上访问。
   - **外网访问**：可以使用`tailscale`和阿里云服务器来映射外网访问。
   - **照片同步和备份**：使用`filestash`和`webdav`进行批量上传，使用`rsync`进行定期备份。

6. **总结**：Photoprism提供了一个强大且灵活的平台来管理和备份个人照片和视频，虽然需要一定的技术知识和时间投入，但能够提供更安全和可靠的数据管理解决方案。
