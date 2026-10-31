# 大预言家 RSS

已收录文章：148 篇，配图资源：148 个。

RSS 文件：`feed.xml`

每个条目包含：

- 标题、分类、发布日期和稳定 GUID
- `poster` 主图字段，兼容只读取主图字段的下游
- `description` 中包含首图和摘要
- `content:encoded` 完整正文
- 正文中的图片以内嵌 HTML 形式提供，不输出 `media:content` 或 `enclosure` 节点，避免部分平台把图片 URL 当作视频链接
- `articles/` 下的原始 Markdown 备份
- `assets/` 下的配图资源（已用 sips 压缩为 JPEG）

## 内容采集规范

按既定规则，RSS 每条只采集三类内容，其余一律不进 Feed：

1. **标题**：只取文章首个一级标题（`# 标题`），即便文内有多个备选标题也只读一个。
2. **正文**：采集首个一级标题之后的正文，但遇到「参考资料 / 资料说明 / 参考来源 / 注释 / 来源 / 拓展阅读」等小节标题即停止（其后的引用、链接、说明不进 RSS）。
3. **图片**：只保留正文配图本身；图片说明（`figcaption` / 替代文字）不输出。

正文小节截断由 `rss_config.json` 的 `bodyExcludeHeadings` 控制，图片说明开关由 `image.caption` 控制，可按垂类调整。

## 给下游抓取

机器抓取场景（GitHub Pages / 静态 HTTPS）请设置 `RSS_PUBLIC_BASE_URL`，让 Feed、文章和图片全部使用绝对 HTTPS 地址：

`RSS_PUBLIC_BASE_URL=https://example.github.io/REPO node build_vertical_rss.mjs`

本机预览可在本目录启动静态服务：

`python3 -m http.server 8765`

然后把 `http://127.0.0.1:8765/feed.xml` 交给下游。

## 更新

把新文章放入已配置的来源目录后，在本目录运行：

`node build_vertical_rss.mjs`

脚本会扫描 `rss_config.json` 中的所有来源，重新排重并覆盖 `feed.xml`、`articles/` 和新增图片资源。原始文章目录不会被修改。
