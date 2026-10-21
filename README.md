# 小说创作工作台

将八个小说技能按用途整合为两个可独立安装的 Codex skill。每个技能包含自己的专项方法、参考文件与脚本，不依赖原八个技能目录，不需要先安装专用写作助手。

[下载版本包](https://github.com/lost-dream/story-workbenches/releases) · [长篇技能入口](skills/story-long-workbench/SKILL.md) · [短篇技能入口](skills/story-short-workbench/SKILL.md) · [版本记录](CHANGELOG.md) · [来源说明](NOTICE.md)

目前按 Codex 场景整理与验证；其他 Agent 的兼容性需要在对应环境验证。这里的“工作台”指统一的技能流程入口，使用对话和项目文件工作，不包含独立图形界面。

| 技能 | 主要用途 | 按需接入的功能 |
|---|---|---|
| `story-long-workbench`（长篇小说工作台） | 扫榜选题、深度拆文、设定、全书/卷纲/章节细纲、正文、日更与改稿 | 长篇导入、去 AI 味、审稿、封面 |
| `story-short-workbench`（短篇小说工作台） | 目标情绪、故事构思、小节大纲、正文与精修 | 短篇导入与分析适配、去 AI 味、审稿、封面 |

## 八个原技能的去向

| 原技能 | 长篇工作台 | 短篇工作台 |
|---|---|---|
| `story-long-scan` | 扫榜与选题模块，保留平台采集与聚合脚本 | 不将长篇榜单当成短篇市场数据 |
| `story-long-analyze` | 完整深度拆文、连续批次、续跑与可选灵感库 | 不加载长篇拆文管道；为短篇导入补齐包内分析适配 |
| `story-long-write` | 长篇规划、正文与权威追踪事务 | 不使用长篇工程结构 |
| `story-short-write` | 需要转短篇时提示另一个入口 | 短篇构思、成稿、题材资源与设计/交付验收 |
| `story-import` | 重建设定/大纲/正文/追踪的长篇工程 | 重建设定、小节大纲、正文三文件工程 |
| `story-cover` | 共同的封面模块 | 共同的封面模块 |
| `story-deslop` | 共同的检测与表达修改模块 | 同一流程，保留短篇声线与有功能的钩子 |
| `story-review` | 共同的证据审查模块，按容量分批 | 同一流程，按短篇平台标准审查 |

两个包均只有根目录的一份 `SKILL.md`。`modules/` 内为按需读取的流程资料，不会生成八个额外的可发现技能。

## 安装

### 让 Codex 安装

将下面这句话发送给支持从 GitHub 安装技能的 Codex：

```text
请安装 https://github.com/lost-dream/story-workbenches 中的两个 skill：
skills/story-long-workbench
skills/story-short-workbench
```

只需要其中一个时，指定对应子目录即可。

### 手动安装

从 [Releases](https://github.com/lost-dream/story-workbenches/releases) 下载完整版或单个技能包，也可用仓库页面的 Code → Download ZIP 下载源码。

将 `skills/story-long-workbench`、`skills/story-short-workbench` 分别完整复制到 Codex 的 skills 目录：`$CODEX_HOME/skills`，未设置时为用户目录下的 `.codex/skills`。单技能压缩包直接包含同名技能目录。保留目录结构，不只复制 `SKILL.md`。不要覆盖已有同名自定义技能；先比较差异。

安装后目录应为：

```text
skills/
├── story-long-workbench/
│   ├── SKILL.md
│   ├── LICENSE
│   ├── agents/
│   ├── modules/
│   └── references/
└── story-short-workbench/
    ├── SKILL.md
    ├── LICENSE
    ├── agents/
    ├── modules/
    └── references/
```

已装原技能可以保留，不影响新包资源完整性；两个新技能从下一轮对话起可用。调用新名字可明确使用整合版。

### 验证入口

安装后先尝试下面的请求，不需要开始创作：

```text
使用 $story-long-workbench，列出可用阶段，暂时不要创建小说文件。
使用 $story-short-workbench，说明短篇残稿导入与续写的衔接流程。
```

如找不到技能，先确认解压后没有多套一层目录，且两个 `SKILL.md` 位于各自技能目录的根部。

## 调用示例

```text
使用 $story-long-workbench，帮我定全书大纲，先不写正文。
使用 $story-long-workbench，只修改第8章细纲。
使用 $story-long-workbench，分析这本参考小说的黄金三章。
使用 $story-long-workbench，导入我的长篇旧稿。
使用 $story-short-workbench，先设计一篇悬疑短篇的小节大纲。
使用 $story-short-workbench，按已经确认的大纲写完整正文。
使用 $story-short-workbench，导入这篇残稿并准备续写。
使用 $story-short-workbench，只检测这篇文章的AI味，不改正文。
使用 $story-long-workbench，单人审查第1到3章，给出原文证据。
使用 $story-short-workbench，为这篇小说设计封面提示词。
```

## 工作边界

- 指定哪个阶段就完成哪个阶段；只规划不展开正文，审查不修改正文，导入不重写原稿。授权的必要前置可以连续完成，剧情上的实质新决定仍由作者确定。
- 默认当前会话执行，专用 agent 与 `.story-deployed` 不是前置。只有明确要求多助手且当前工具支持时才委派；不可用时直接执行同一标准。
- 生图方式沿用当前任务的选择。尚未选择时先问 Image2 API 或内置 image_gen；同一批次不自动切换。只交付方案/提示词不调用图像生成。
- 保留已有有效分析、原文备份和项目决定，不通过重拆全书修补无关字段。
- 短篇导入区分“工程导入完成”和“续写就绪”。从已有原文补齐设计交接后运行写作门禁；未写结局、付费点或目标篇幅未定时如实列出待定项，不杜撰字段假装可以直接续写。
- 短篇分析适配是依据现有导入映射与输出契约新增的实现，不是另外下载安装原 `story-short-analyze`。没有新增短篇榜单采集器。

## 运行依赖与验证

按任务使用 Python 3、Node.js、联网/浏览器能力或所选图片工具。各模块脚本使用同目录资源，跨包运行只需保持相对结构。本次基础检查使用 Python 3.12，其他 Python 版本未逐一验证。不会要求普通使用者先运行构建脚本。

| 场景 | 所需能力 |
|---|---|
| 流程说明、构思与文本讨论 | 能读取技能文件的 Codex |
| 章节索引、状态事务、部分任务包 | Python 3 |
| 正文/大纲检查、榜单聚合 | Node.js |
| 实时扫榜 | 可用网络与相应网页/浏览器能力 |
| 封面方案、封面提示词 | 文本能力即可 |
| 实际生图或改图 | 用户选择且当前环境可用的 Image2 API 或内置 image_gen 工具 |

技能包不附带 Image2 服务、账号或 API Key，也不会给宿主添加内置图片工具。没有图片能力时可以先交付提示词。浏览器采集脚本的 CDP/CLI 为可选采集路径；没有相应能力可使用可用网页工具或用户提供的数据，不能伪造实时榜单。

本次整合已执行两个入口的格式验证、资源链接检查、Python/JavaScript语法检查，并在临时目录中验证章节索引、三类规划任务包和榜单聚合。另按只改细纲、短篇残稿导入、封面方式选择、仅检测、单人审稿和全新环境开书做独立流程复核。未用这些检查代替真实平台抓取、完整小说创作或实际封面生成。

## 来源

原八个技能的 metadata 标记来源为 [zenstory-ai/oh-story-claudecode](https://github.com/zenstory-ai/oh-story-claudecode)，源技能 metadata 中的版本值为 `1.0.0`；这不是对上游整个项目版本号的声明。两个包的 `references/sources.json` 保留来源技能名、原文件名、原文件 SHA-256 及整合后文件位置，便于追溯。

本项目新增内容包括两个统一入口、模块内路径适配、独立运行约定、短篇导入分析及设计交接、封面方式选择。原项目采用 MIT 许可，原版权声明与许可全文保留在根目录及两个技能目录的 [LICENSE](LICENSE) 中。详细来源与变更范围见 [NOTICE.md](NOTICE.md)。

下载包和源码以发布标签对应的版本为准。更新前保留自己对技能的修改，再替换相应技能目录。
