<!--
Real-world example output generated with source-faithful-summary-skill.
Source: https://www.youtube.com/watch?v=-QFHIoCo-Ko
Published demo: https://geekinney.com/share/demo-matt-pocock-ai-coding-workflow-summary/
-->

# Matt Pocock《Workflow for AI Coding》：把 AI Coding 变成可控、可反馈、可审查的工程流程

来源：YouTube 视频《Workflow for AI Coding》：https://www.youtube.com/watch?v=-QFHIoCo-Ko  
材料说明：英文字幕 transcript，视频时长 `1:36:25`。

## Source type 与一句话概括

这是一场 **实践 / 工作流型 workshop**：Matt Pocock 一边讲解 LLM 的约束，一边演示他如何把一个模糊产品需求推进到 PRD、Kanban、agent implementation、QA / review、并行 sandbox agent loop。

一句话概括：

> Matt 的核心不是泛泛地说“AI 时代仍要软件工程基本功”，而是展示一套 AI coding 控制流程：先承认 LLM 会在长上下文里变笨、会失忆；再用 Grill Me、PRD、Kanban、vertical slice、fresh context review、feedback loop、deep modules 和 sandboxed parallel agents，把大任务拆成能让 AI 执行、又能让人类审查和纠偏的小闭环。

## 1. 开场判断：AI 是新范式，但它仍受工程约束支配

Matt 开场先提醒听众：AI 确实是新范式，但与人协作时重要的软件工程基本功，在与 AI 协作时同样有效。整场 workshop 后面所有演示都在展开这个判断：不是找到一个神奇 prompt，而是设计任务边界、上下文、反馈、文档和审查机制。

他很快把问题落到 LLM 的“奇怪约束”上。这里的约束不是背景知识，而是后面流程的起点：如果不知道模型什么时候变笨、什么时候遗忘，就很容易把 AI coding 想成“无限上下文里的自动程序员”。

## 2. 约束一：smart zone / dumb zone —— 任务要小到模型还没变笨

`03:21–05:00` 左右，Matt 引用 Dex Hardy / HumanLayer 的说法：LLM 有 **smart zone** 和 **dumb zone**。

他的解释是：一个新对话刚开始时，模型通常最聪明，因为 attention relationships 最不紧张。每增加 token，就像足球联赛里多加队伍，关系数量近似平方增长。上下文越长，模型越容易把重要信息淹没在噪声里，最后开始做愚蠢决策。

Matt 给了一个经验标记：大约 `100K` tokens 左右就要警惕；即便模型宣传 `200K` 或 `1M` context window，也不代表 coding 能一直保持质量。长上下文更适合 retrieval，不等于适合持续编码。

这个概念控制了后面多个动作：

- 不要让一个大任务在同一 session 里无限延展；
- 任务粒度要小到能停留在 smart zone；
- 不要过度依赖“不断 compact 然后继续”；
- 把关键状态外部化到 PRD、issue、Kanban；
- review 最好从 fresh context 开始，而不是让同一个已消耗大量上下文的 agent 自审。

## 3. 约束二：LLM 像《Memento》主角，会不断失忆

`07:49–11:03` 左右，Matt 画出一次 LLM session 的生命周期：system prompt → exploration → implementation → testing。clear context 之后，模型回到初始状态。

他不喜欢把所有历史都 compact 成沉积物继续塞回去。因为 compact 不是“完美记忆”，而是把一段长对话压缩成可能污染后续判断的摘要。Matt 更喜欢把 AI 当成《Memento》主角：它会不断忘记，所以流程要围绕“每次 fresh start 仍能工作”来设计。

这也是 PRD、Kanban、issue files 在他流程里的意义：它们不是文档洁癖，而是给一个会失忆的执行者准备外部记忆。

## 4. 他反对的默认路径：specs-to-code 会把不清楚的需求放大成代码偏差

`10:50–13:30` 左右，Matt 说明自己反对的隐含路径：先写 specification，再把 specs 交给 AI 生成代码；如果代码有问题，不看代码，只回头改 specs，再继续生成。

他把这种方式看作 vibe coding 的另一种形式，因为它容易让人忽略代码本身，也忽略需求澄清过程。真正的问题常常不是“spec 不够长”，而是人和 agent 没有形成共同理解。

所以他不是从“写代码”开始，而是先用一个很小的 skill 让 AI 追问人类。

## 5. 第一段动作：用 Grill Me 把模糊 brief 变成 shared design concept

`14:52–24:00` 左右，Matt 从一个模糊客户 brief 开始演示。假设 Sarah Chen 提了一个需求但已经休假，开发者需要接手。Matt 的第一步不是进入 plan mode，也不是直接让 Claude 写代码，而是 clear context，然后调用 **Grill Me skill**。

这个 skill 很短，核心指令是：

> relentless 地采访我，沿着决策树一支一支追问，直到我们形成 shared understanding；每次只问一个问题，并给出推荐答案。

这一步的分工很清楚：

- AI 负责追问、暴露遗漏、保持访谈节奏；
- 人类负责领域判断、边界取舍和最终确认；
- 输出不是代码，而是 shared design concept。

Matt 说，他几乎每次用 AI 开始工作都会这样做。原因是 plan mode 往往太急着产出计划，而他真正需要的是“和 agent 对齐”。在演示里，AI 会问点数经济、progression curve、retroactive backfill、哪些事件算积分、哪些 UI 行为算完成等问题；Matt 一边回答，一边删掉不必要范围、确认边界。

他还提到 sub agent：探索代码库的 sub agent 可以消耗大量 token，但只把重要摘要回传给 parent agent。这也是控制上下文的一种方式：让探索发生在隔离窗口里，而不是把所有原始信息塞进主上下文。

## 6. 第二段动作：把 Grill Me 产生的高价值上下文沉淀成 PRD

`30:00–36:30` 左右，Grill Me 之后上下文里已经有大量“gold tokens”。Matt 说这些内容需要进入某种 destination document，于是他让 AI 写 PRD。

PRD 的格式不是重点，公司已有模板也可以。重点是：它把刚才形成的 shared design concept 外部化，让后续 fresh context 或其他 agent 能接住项目状态。

他的 PRD 通常包含：问题陈述、用户面对的问题、解决方案、user stories、实现决策、测试决策，以及 out-of-scope 内容。这里还有一个容易被误解的细节：Matt 说自己通常不会过度 review 这个 PRD。不是因为 PRD 不重要，而是因为他认为 Grill Me 阶段已经达成同频，此时逐字 review PRD 测的主要是 LLM 的总结能力，而总结本来是 LLM 擅长的事。

这暴露出他的 review 判断模型：人类注意力要投向高风险 failure mode，而不是每个中间文档都机械审一遍。

## 7. 第三段动作：从 PRD 到 Kanban，而不是线性 multi-phase plan

`40:00–52:20` 左右，Matt 把 PRD 拆成 Kanban board。

他之前也用 multi-phase plan：phase 1、phase 2、phase 3。问题是，线性 phase plan 看起来清楚，却不擅长表达任务之间的 blocking relationships，也不方便并行。Kanban board 的优势是：

- 每个任务是一个 ticket；
- ticket 之间可以标注阻塞关系；
- 能区分 AFK task 和 human-in-the-loop task；
- 依赖关系形成 DAG；
- 独立任务可以交给多个 agent 并行处理。

但 Matt 没有把任务拆分完全交给 AI。他在现场看到 AI 生成的第一项偏向 “schema + gamification service”，立刻指出这太像 **horizontal slice**。AI 很喜欢一层一层横向写：先数据库，再 API，再前端。问题是这种方式要等到很晚才有端到端反馈。

他想要的是 **vertical slice / tracer bullet**：第一片就要跨过必要层次，形成最小可见行为，这样在早期就能测试整个 flow。这里的判断不是“任务越小越好”，而是：任务既要小到停留在 smart zone，又要垂直到能产生真实反馈。

## 8. 第四段动作：implementation 可以 AFK，但前面的 backlog 必须可观察、可调 prompt

`52:20–58:20` 左右，Matt 总结前半段流程：idea → Grill Me → PRD → Kanban。到这一步之前，人类一直在 loop 里；到了 implementation，才是人类可以暂时退出的阶段。

他把这比作 day shift 和 night shift：白天人类把问题澄清、任务拆好、依赖排好；夜班 agent 按 backlog 执行。

他展示了一个简单 implementer loop：

- 把 local issue files 注入上下文；
- 取最近 commits；
- 用 prompt 让 Claude Code 选择 AFK issue；
- 读取 codebase、实现、运行测试；
- 在更复杂版本里放进 Docker sandbox。

Matt 特别强调：先跑 human-in-the-loop 的 once loop 很重要。你需要观察 agent 实际做了什么，然后调 prompt。这不是一键自动驾驶，而是先用可观察循环把行为调顺，再进入 AFK loop。

这段现场细节值得保留：implementer loop 不是“给一个大 prompt 然后祈祷”。它会把 issue number、issue title、branch、recent commits、本地 issue files 等明确上下文交给 agent；agent 选择可执行 issue、读取 codebase、实现、运行测试。如果进入更复杂的版本，才放进 Docker sandbox 和独立 branch。这个细节说明 Matt 真正在控制的是 agent 的输入边界、执行隔离和可观察性，而不是只追求自动化。

## 9. QA / code review 不会消失：AI 写得越多，人类审查压力越真实

`58:58–65:00` 左右，有人问：agent 生成的代码比人能 review 的还多，怎么办？Matt 的回答很诚实：他不认为有办法完全避免这个问题。

他的流程里真正 AFK 的主要是 implementation。之后仍然需要 QA 和 code review，而且可能比以前更多。小 PR、stacked PR、agent 一次做多个 issue，这些都会带来新的 review 压力。Matt 没有把 AI coding 包装成“人类退出工程判断”，而是把人类位置重新分配：

- planning 阶段，人类深度参与；
- implementation 阶段，可以交给 agent AFK；
- QA / review 阶段，人类重新进入。

他也承认团队环境更混乱：idea、prototype、研究、领域专家反馈、PRD 都可能来回循环；在 PRD 之前的阶段尤其需要团队参与。Kanban implementation 只有在方向相对明确之后才适合启动。

## 10. Review 要用 fresh context：不要让 dumb zone 里的 agent 自审

`65:00–69:30` 左右，有人问为什么不用 AI QA 自己的代码。Matt 的回答是：当然可以，而且应该把 automated review 作为 implementation 的一部分，因为 tokens 便宜，AI 也擅长 review。

但他强调一个关键细节：如果让刚写完代码、已经消耗大量上下文的同一个 session 自审，那么 reviewer 可能已经处在 dumb zone。更好的做法是 clear context，用 fresh context 做 review。

到 `88:00–93:00` 左右，他又把 review 和 coding standards 联系起来，区分 **push** 和 **pull**：

- push：把指令直接塞进上下文，例如 Claude.md 中始终发送的规则；
- pull：让 agent 在需要时拉取 skills 或额外说明。

对 implementer，标准可以更多通过 pull 提供，避免上下文一开始就过重；对 reviewer，标准应当明确 push，因为 reviewer 的工作就是拿标准对照代码检查。

## 11. Feedback loops 决定 AI coding 的质量天花板

`70:00–74:00` 左右，Matt 明确说：如果代码库没有 feedback loops，AI 就是在 blind coding。AI 输出质量的上限，很大程度由反馈循环质量决定。

他展示 agent 运行 `npm run test`、`npm run typecheck`，发现 TypeScript 错误并修复。这里的测试、类型检查、可运行反馈不是附属工具，而是 AI coding 的导航系统。

他也承认前端更难，因为很多质量信号需要人眼判断，不是 service-level test 能完全覆盖。这意味着，越难自动反馈的部分，越需要谨慎的人类 QA 和更短的验证闭环。

## 12. Deep modules：用模块边界降低 AI 和人类共同迷路的概率

`74:00–83:20` 左右，Matt 转向代码结构。他引用 John Ousterhout《A Philosophy of Software Design》里的 **deep modules**。

他指出，很多代码库由大量 shallow modules 组成：小文件、小函数、复杂依赖图。AI 很难理解这种依赖关系，人类也很难决定测试边界。AI 还容易给每个小函数包一层测试，制造大量低价值测试：每个碎片单独看能工作，但系统行为并没有被真正验证。

Matt 更偏好的结构是 deep modules：接口小而清晰，内部承载较多功能。这样测试边界更自然，调用者面对的接口更简单，人类也能把注意力放在模块形状和接口设计上，而不是审查每个内部细节。

这不是为了架构美学，而是为了适应 AI coding 后的新压力：代码生成速度变快，但人类理解和 review 能力没有同比变强。模块边界越清晰，AI 越容易工作，人越容易审查。

## 13. 文档也会腐烂：外部 artifact 要服务流程，而不是污染未来 agent

`83:20–89:40` 左右，有人问：PRD、markdown plans、issues 是否要长期保存在 repo 里？Matt 的回答很实用：没有简单答案，但他担心 **doc rot**。

如果一个月后代码结构、命名、需求、用户反馈都变了，旧 PRD 或旧 issue 仍在 repo 里，未来 agent 可能把它误读成当前事实。这种 stale documentation 会影响模型判断。

所以他倾向于不保留临时执行文档；如果使用 GitHub issues，可以把它们 mark as closed，让 agent 能看到它们已完成。PRD 这类 destination document 是否保留，要看它是否承载长期语义；临时执行脚手架则应删除、关闭，或明确标记状态。

他把 database migrations 区分开：migration 更像确定性的变更记录，不完全等同于普通计划文档。

## 14. Sandcastle：把 Kanban DAG 扩展成 sandboxed parallel agent loop

`90:00–96:00` 左右，Matt 介绍自己写的 TypeScript library：**Sandcastle**。它的作用是运行 AFK agent loops：创建 worktree，把执行放进 Docker container，在独立 Git branch 中跑 prompt，之后再 merge。

Sandcastle 把前面 Kanban / DAG 的设计工程化：

- planner 读取 backlog 和 blocking relationships，选择可并行处理的 issues；
- 每个 implementer 在自己的 sandbox / branch 里处理 issue；
- 如果产生 commits，就进入 review；
- merger agent 合并分支，处理 merge、types、tests 等问题；
- reviewer 可以使用更强模型，例如 Matt 提到实现用 Sonnet、review 用 Opus。

这说明 Kanban 不是流程仪式。它为并行 agent 提供依赖边界；worktree / Docker sandbox 提供执行隔离；reviewer / merger 提供质量关口。

但 Matt 最后仍然说：当代码达到满意状态，还要 share with team，进入完整 review。AFK 不是最终交付，它只是把 implementation 阶段自动化。

## 15. 最后的总结：这不是 specs-to-code compiler，而是控制系统

`94:00–96:10` 左右，Matt 收束整场 workshop：整个流程始终要记住代码库形状。这不是 specs-to-code compiler，不是让 AI 盲目 churn out code。

他的完整流程是：

1. 用 Grill Me 对齐需求和设计概念；
2. 不过度迷信 PRD，但把高价值上下文沉淀为 destination document；
3. 把 PRD 转成可并行、可阻塞、可反馈的 Kanban issues；
4. 让 agent 在 sandbox 中实现；
5. 用 QA 和 code review 反复把新问题补回 Kanban；
6. 最后把满意的代码交给团队完整 review。

Matt 最后的建议也回到开场：去读那些 AI 之前的软件工程老书。他想强调的不是怀旧，而是这些关于任务切分、反馈、模块边界、设计概念和人类判断的位置，在 AI coding 中变得更重要了。

## Decision model map

### Constraint 1：LLM 会从 smart zone 滑向 dumb zone

- Failure：同一个上下文越塞越多，模型开始做差决策。
- Judgment：不要让大任务在一个 session 里无限延展。
- Action：切小任务、clear context、fresh context review、用外部 artifacts 承载状态。
- Tradeoff：需要更多前期拆分和中间文档。
- Evidence：`03:21–05:00`、`65:00–69:30`。

### Constraint 2：LLM 会失忆，compact 会产生沉积物

- Failure：依赖长对话历史会让后续状态不稳定。
- Judgment：与其追求永续上下文，不如优化每次 fresh start。
- Action：Grill Me → PRD → Kanban → issue files。
- Tradeoff：要管理 artifact 生命周期，避免 doc rot。
- Evidence：`07:49–11:03`、`30:00–36:30`、`83:20–89:40`。

### Constraint 3：模糊需求直接 specs-to-code 会放大错误

- Failure：需求未澄清时，代码生成越快，偏差越快固化。
- Judgment：人类判断必须前置到问题澄清阶段。
- Action：用 Grill Me 反复追问，形成 shared design concept。
- Tradeoff：前期看起来更慢，但减少后期错方向实现。
- Evidence：`10:50–24:00`。

### Constraint 4：线性 phase plan 不利于反馈和并行

- Failure：horizontal slice 要到很晚才有端到端反馈。
- Judgment：任务应该既小，又能产生垂直反馈，还能表达依赖。
- Action：PRD → Kanban / DAG；优先 vertical slice / tracer bullet。
- Tradeoff：Kanban 拆分需要人类 review。
- Evidence：`40:00–52:20`。

### Constraint 5：AI implementation 快，但 review / QA 不会消失

- Failure：agent 产出可能超过人类 review 能力；同一上下文自审也会掉进 dumb zone。
- Judgment：不能把 implementation 自动化误认为交付自动化。
- Action：implementation 可以 AFK；review 用 fresh context；human QA、code review、team review 仍保留。
- Tradeoff：人类 review 压力可能上升。
- Evidence：`58:58–69:30`、`94:00–96:00`。

### Constraint 6：反馈循环是质量天花板

- Failure：没有测试、typecheck、运行反馈时，AI 是 blind coding。
- Judgment：提升反馈循环比只换 prompt 更根本。
- Action：让 agent 跑 `npm run test`、`npm run typecheck`，用 vertical slice 提早获得端到端反馈。
- Tradeoff：前端和视觉质量仍需要人眼或更复杂反馈机制。
- Evidence：`70:00–74:00`。

### Constraint 7：代码结构决定人类能否承受 AI 速度

- Failure：shallow modules 和低价值测试让 AI 与人类都难以理解系统。
- Judgment：用清晰接口和 deep modules 保住系统理解。
- Action：人类设计模块边界和接口，AI 更多承担模块内部实现。
- Tradeoff：需要持续维护架构边界，不能放任 AI 生成碎片化结构。
- Evidence：`74:00–83:20`。

## 可复制的工作流清单

1. 不要一开始就让 AI 写代码。
2. 从 fresh context 开始，用 Grill Me 让 AI 追问需求。
3. 人类回答问题，做领域判断、范围裁剪和边界确认。
4. 把高价值对话沉淀成 PRD / destination document。
5. 不要把 PRD 当自动编译目标；始终保持代码库结构意识。
6. 从 PRD 生成 Kanban，而不是只生成线性 phase plan。
7. 人类 review Kanban，尤其检查是否 vertical slice / tracer bullet。
8. 用 blocking relationships 把任务变成 DAG。
9. 先 human-in-the-loop 跑 once loop，观察 agent 行为并调 prompt。
10. 再让 AFK agent loop 在 sandbox / worktree / branch 中执行。
11. 让 AI 做 automated review，但最好用 fresh context。
12. 对 implementer 允许 pull skills / coding standards；对 reviewer 明确 push standards。
13. 用测试、类型检查、运行反馈提升 AI coding 的质量上限。
14. 人类继续做 QA、code review，必要时让团队完整 review。
15. QA 阶段发现的新问题继续回填到 Kanban。
16. 用 deep modules 和清晰接口降低 review 与测试负担。
17. 保留有长期语义的文档；关闭、删除或标记容易腐烂的临时 issue / plan。
18. 用 Sandcastle 这类 sandbox/worktree 机制把 Kanban DAG 扩展成并行 agent loop。

## 不要误读这场 workshop

不要把它误读成：

- “有一个神奇 prompt 可以自动写完整个项目”；
- “AI coding 的关键只是多 agent 并行”；
- “PRD / Kanban 是流程仪式”；
- “人类只需要最后看一眼”；
- “1M context window 可以解决 coding 的上下文问题”；
- “旧软件工程基本功只是开场鸡汤”；
- “specs-to-code 可以替代代码理解和设计判断”。

更准确的理解是：

> Matt 在做的是 AI coding 的控制系统设计：用 smart zone / dumb zone 管上下文，用 Memento 模型管状态，用 Grill Me 管需求澄清，用 PRD / Kanban 管外部记忆和依赖，用 vertical slice 管反馈，用 fresh context review 管质量，用 deep modules 管人类认知负担，用 sandboxed parallel loop 扩大执行吞吐。

## Timestamp source notes

- `00:27–02:30`：开场；AI 是新范式，但软件工程基本功仍适用于 AI 协作。
- `03:21–05:00`：smart zone / dumb zone；上下文越长，attention relationships 越紧张。
- `05:00–07:20`：大任务拆小；multi-phase plan 与循环式执行的背景。
- `07:49–11:03`：LLM session 生命周期；clear context、compact、Memento 类比。
- `10:50–13:30`：反对 specs-to-code；需要 shared design concept，而不是只改规格不看代码。
- `14:52–24:00`：Grill Me skill 演示；从模糊 brief 到共同理解。
- `30:00–36:30`：把 grilling session 的 gold tokens 沉淀成 PRD；PRD 是 destination document。
- `40:00–52:20`：PRD → Kanban；blocking relationships、AFK task、vertical slice、tracer bullet、DAG。
- `52:20–58:20`：implementer once loop；local issue files、recent commits、Claude Code、Docker sandbox、human-in-the-loop 调 prompt。
- `58:58–65:00`：AI 产出增加带来的 code review 压力；team feedback 和 prototype 问题。
- `65:00–69:30`：AI automated review 可以做，但最好 fresh context。
- `70:00–74:00`：feedback loops 是质量上限；`npm run test`、`npm run typecheck` 示例。
- `74:00–83:20`：shallow modules、低价值测试、deep modules、模块接口和测试边界。
- `83:20–89:40`：doc rot；PRD / issue / migration 的保留边界；push / pull 规则。
- `90:00–96:00`：Sandcastle；planner、implementer、reviewer、merger、worktree、Docker、parallel agents、最终团队 review。

## 最终结论

这场 workshop 最有价值的不是某个工具，而是 Matt 的控制模型：他不把 AI 当无限聪明、无限记忆的程序员，而是把它当一个会变笨、会失忆、但在小任务和强反馈里很能干的执行者。于是整套流程都围绕一个目标展开：让 AI 始终在可控、可反馈、可审查的边界内工作。AI 可以扩大 implementation 吞吐，但不能替代人类对问题、边界、反馈、模块形状和最终质量的判断。
