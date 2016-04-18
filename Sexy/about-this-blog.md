#博客简介
##方案
- 使用 VS Code + Github 管理的博客。
- 全部文章使用 Markdown 书写，访问时由 Github 执行 GFM Markdown 渲染。
##原因
- 我觉得 Hexo, Jekyll 难用的很，直接GFW渲染md文件足够用，迅速，而且不是静态网站，可以利用自带的仓库内搜索。
- VS Code 和 Git 的搭配极佳，编写后直接publish。
##缺陷
- 缺点是目录README.md需要手动编写。
##同步方案
- 整个仓库使用 BitTorrent Sync 在设备间备份。在有同局域网下的NAS时，备份飞快。
- 草稿或私密日志文件命名为"s-*.*"，并添加到 .gitignore，不会同步到 Github。