# 来源与整合说明

本项目基于 [zenstory-ai/oh-story-claudecode](https://github.com/zenstory-ai/oh-story-claudecode) 的以下八个技能整理而成：

- story-long-scan
- story-cover
- story-long-analyze
- story-long-write
- story-short-write
- story-import
- story-deslop
- story-review

原作者的版权声明与 MIT 许可全文保留在仓库根目录的 LICENSE，以及各个技能目录的 LICENSE 中。原版权行为 `Copyright (c) 2025-2026 oh-story-claudecode`。

本次整合由 lost-dream 维护，主要变更包括：

- 按长篇与短篇用途提供两个统一入口。
- 将专项流程和资源收纳到各技能的 modules 中，并适配引用路径。
- 保留各技能所需资源，实现无需原八个技能目录的独立安装。
- 默认由当前会话执行，不将专用助手部署作为运行前置。
- 补齐短篇导入的分析适配与设计交接，区分工程导入完成和续写就绪。
- 将封面生成方式改为沿用用户当前任务选择，不自动切换生成通路。

这不是上游项目的官方发布，也不宣称全部内容为本项目原创。两个技能的 references/sources.json 分别记录原文件名、来源技能、源文件 SHA-256 与整合后位置。这里的源技能版本值来自原 metadata，不代表与某个上游完整发行版逐字一致。

本次发布补齐许可证时核对的上游文件为：

https://github.com/zenstory-ai/oh-story-claudecode/blob/74080143dd1ac9a39a930fafd99a0dbbe61b946a/LICENSE

上述提交仅用于固定许可证的核对来源；技能原文的身份以 sources.json 的源文件校验值为准。
