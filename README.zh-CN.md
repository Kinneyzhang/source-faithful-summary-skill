# Source-Faithful Summary Skill

[English](README.md) | [简体中文](README.zh-CN.md)

一个面向 Agent 的原始材料忠实总结技能，适用于文本、视频 transcript、音频 transcript、播客、访谈、讲座、demo、workshop 和会议记录。

很多 AI 总结会优化“好读”和“高级概括”，最后产出一篇漂亮文章，但读者已经看不到原材料真正花时间讲了什么。这个 skill 优先保护原材料的主线、注意力权重、具体例子、动作链、失败模式、证据和讲者/作者的决策模型。

## 为什么需要它

长内容总结经常有一些隐蔽失败：

- 用总结者自己的漂亮框架替换原材料的真实推进；
- 提到了概念，但没解释这些概念为什么支配后续动作；
- 把例子压缩成口号；
- 还没忠实复原原材料，就先加入自己的启发和引申；
- 事实上没明显错误，但熟悉原材料的人会觉得“这不是它真正讲的东西”。

这个包给 Agent 一套可重复执行的 source-grounded summary 方法。

## 支持什么材料

- **文本**：文章、论文/报告、访谈稿、会议纪要、讲座笔记。
- **视频**：YouTube、Bilibili、会议演讲、课程、workshop、demo——前提是先拿到 transcript。
- **音频/语音**：播客、访谈录音、会议录音、语音笔记、讲座音频——前提是先转写。

这个包本身不做语音转文字，也不下载视频。先用你自己的工具获得 transcript，再使用这个 skill 总结。

## 包含内容

- `SKILL.md`：Hermes skill / 核心工作流。
- `AGENTS.md`：给 Codex、OpenCode、Gemini 风格 agent 的通用说明。
- `CLAUDE.md`：Claude Code 适配说明。
- `.cursor/rules/source-faithful-summary.mdc`：Cursor/Windsurf 规则。
- `templates/source-map.md`：source map 和 decision model worksheet。
- `templates/summary-outline.md`：忠实总结大纲模板。
- `templates/evaluation-rubric.md`：多场景评估评分标准。
- `templates/long-source-plan.md`：长 transcript、长播客、panel 和长文章的处理计划模板。
- `examples/workflow-talk-mini.md`：工作流/视频风格小型示例。
- `examples/text-article-mini.md`：文本文章示例。
- `examples/audio-podcast-mini.md`：多说话人音频/播客 transcript 示例。
- `examples/meeting-mini.md`：会议 transcript 示例。

## 核心原则

```text
忠实于原材料 > 文章优雅
叙事权重 > 概念密度
具体动作/问题链 > 抽象框架
证据 > 感觉
讲者/作者的决策模型 > 零散建议
```

对于实践/工作流型材料，默认抽取这条链：

```text
失败模式 → 底层约束 → 讲者/作者判断 → 具体动作 → 代价/限制
```

## 快速开始

克隆仓库：

```bash
git clone https://github.com/Kinneyzhang/source-faithful-summary-skill.git
cd source-faithful-summary-skill
```

在任意 Agent 中使用时，先让 Agent 阅读 `SKILL.md`，再开始总结原材料。

在 Hermes Agent 中，可以按你的 Hermes setup 复制或软链接到 skills 目录。

示例：

```bash
mkdir -p ~/.hermes/skills/research
ln -s "$(pwd)" ~/.hermes/skills/research/source-faithful-summary-skill
```

新会话中加载：

```bash
hermes -s source-faithful-summary-skill
```

## 使用方式

写正文之前，先让 Agent 产出这些中间物：

1. source type 分类；
2. source map：时间戳或章节引用 + 段落角色；
3. 命名概念和角色分类；
4. 失败模式或核心张力；
5. 动作链或论证链；
6. decision-model map；
7. main-thread audit；
8. reverse-summary audit。

然后再写最终总结。

如果产物是可发布/可阅读文章，使用**面向读者的文章模式**：source map 和审计材料放到附录或评估报告里，正文开头应是贴合原材料的标题、source type、一句话忠实总结、编号叙事段落、可复制工作流清单、不要误读、timestamp source notes 和最终结论。

## 最小提示词

```text
Use the Source-Faithful Summary Skill.
First classify the source type, build a source map, list named concepts, extract failure modes/tensions, action or argument chain, and decision-model map.
Then write a summary that preserves the source's main thread and attention weight.
Do not turn the source into a polished concept essay.
```

## 适合场景

- 对文章、报告、访谈稿、transcript 做忠实总结；
- YouTube/Bilibili/Vimeo 视频 transcript 总结；
- 播客和音频访谈转写后的总结；
- 技术 demo、workshop、课程、会议演讲；
- 需要公开发布且必须忠实代表单一来源的文章；
- 审计已有总结是否偏离原材料。

## 不适合场景

不要把它作为这些任务的主流程：

- 受原材料启发的自由观点文；
- 营销文案；
- 不要求 source fidelity 的普通摘要；
- 一上来就综合很多来源的研究文章。

如果要写分析和启发，先完成忠实总结，再单独加“分析/启发/我的看法”一节。

## 长材料支持

对于超过约 50k 字符或 60 分钟的材料，写正文前先使用 `templates/long-source-plan.md`。它要求 Agent 明确分块/抽样策略、章节覆盖、概念复现检查、说话人覆盖和证据预算。长播客、panel、长 workshop，以及可能丢图表/表格的网页抽取文本尤其需要这一步。

## 限制

- 本 skill 不负责抓取 transcript 或 STT。
- 自动字幕质量差时，需要明确标注限制。
- 它优先保证忠实，不优先追求文章最漂亮；如果要观点文章，应该作为第二阶段。

## License

MIT
