# 冷知识 RSS

已收录文章：24 篇，配图资源：24 个。

RSS 文件：feed.xml

发布基址：https://anliangsa79-sleepybear.github.io/wenshi-rss/cold-knowledge

本次只在本地生成文件，没有上传。部署到静态 HTTPS 站点后，上述绝对链接才会生效。栏目路径使用英文 cold-knowledge；文章文件名使用 article- 加哈希，不将中文标题转写为拼音；图片使用哈希文件名。

每个条目包含标题、分类、发布日期、稳定 GUID、摘要、正文和配图。正文到“参考资料”等小节为止；引用列表不进入 Feed。articles/ 保存清理元信息后的 Markdown 副本，assets/ 保存压缩后的 JPEG 配图。

## 本机预览

先在本目录重建本地链接：

    RSS_PUBLIC_BASE_URL=http://127.0.0.1:8765 node build_feed.mjs

再在另一个终端启动静态服务：

    python3 -m http.server 8765

然后订阅 http://127.0.0.1:8765/feed.xml。

## 更新

将新稿放入配置的来源目录后，在本目录运行：

    node build_feed.mjs

脚本读取 rss_config.json，重建 feed.xml、articles/、assets/ 和 index.html；源文章不受修改。
