# LLM x 书签收藏：摘要 & 全文索引 - Nekonull's Garden
- URL: https://nekonull.me/posts/llm_x_bookmark/
- Added At: 2025-01-09 09:53:21
- [Link To Text](2025-01-09-llm-x-书签收藏：摘要-&-全文索引---nekonull's-garden_raw.md)

## TL;DR
作者为了解决书签管理中的死链接、查找困难和内容遗忘问题，开发了一个自动化系统`bookmark-summary`，通过Github Actions和LLM技术自动保存书签内容、生成摘要和总结。未来计划优化摘要质量、数据结构化、代码重构等。

## Summary
1. **背景介绍**：
   - 作者在网上冲浪时经常收藏有趣的文章或网站，但发现单独收藏效率低下。
   - 自2021年5月起，使用名为`osmos::memo`的书签插件，将收藏记录到公开的Github存储库中。
   - 插件通过Github token实现自动化，近三年半积累了800+条目。

2. **现有问题**：
   - **死链接问题**：书签指向的URL可能失效。
   - **查找困难**：记录项仅包含URL、标题和标签，查找效率低。
   - **内容遗忘**：长文章时间久了容易忘记内容，通读费时。

3. **解决方案**：
   - 建立新的存储库`bookmark-summary`，作为现有书签存储库的辅助数据。
   - 新增书签的Markdown格式全文、列表摘要、一句话总结。
   - 通过Github Actions实现自动化流程：
     1. 新增书签条目。
     2. 触发`summarize`工作流。
     3. 解析书签README.md，保存URL到Wayback Machine。
     4. 使用`jina reader` API获取Markdown全文。
     5. 使用LLM生成列表摘要和一句话总结。
     6. 更新摘要存储库的README.md。

4. **技术细节**：
   - 主要代码由Claude和GPT4o编写，人工进行小调整。
   - 使用深度求索的`deepseek-chat`生成摘要，成本低且效果尚可。

5. **未来优化方向**：
   - **列表摘要质量**：优化prompt或更换模型。
   - **数据结构化**：考虑在Markdown外维护JSON格式。
   - **代码整理和重构**：重构代码结构，改进存储库交互方式。
   - **向量搜索**：考虑使用embedding模型生成嵌入，存储到SQLite数据库。
   - **自动生成每周周报**：已完成，参见Github Releases。
   - **改用更现代的工具链**：例如`uv`和PEP 723。

6. **部署指南**：
   - 参考`osmos::memo`指引，初始化书签存储库。
   - 新建摘要存储库，添加`process_changes.py`。
   - 修改`BOOKMARK_COLLECTION_REPO_NAME`和`BOOKMARK_SUMMARY_REPO_NAME`。
   - 添加`bookmark_summary.yml`到书签存储库。
   - 新建PAT（Personal Access Token）。
   - 添加密钥到环境变量。
   - 配置完成后，使用`osmos::memo`扩展添加书签，观察工作流运行情况。

7. **勘误**：
   - 感谢评论区指出「我也想要一节」中的部分步骤错误，已在文中修复。
