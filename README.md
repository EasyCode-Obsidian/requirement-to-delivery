# requirement-to-delivery

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](./LICENSE)
[![Skill](https://img.shields.io/badge/Codex-Skill-blue)](./SKILL.md)
[![Language](https://img.shields.io/badge/README-Bilingual-orange)](./README.md)

> Turn requirements — from small bug fixes to multi-phase projects — into tracked execution with automatic complexity routing.
> 把需求——从小 Bug 修复到多阶段项目——自动分流为对应深度的可追踪执行。

---

## 中文说明

### 简介

`requirement-to-delivery` 是一个面向任务交付的 Codex Skill。
它会根据任务复杂度自动选择执行深度，从小 Bug 直接修复到多阶段项目的完整规划执行，无需用户手动切换：

1. 理解需求
2. 自动分类：quick-fix / 单阶段 / 多阶段
3. **Quick-fix**：直接研究、修复、报告，跳过规划流程
4. **单阶段**：草案确认后生成双 Todo 并执行
5. **多阶段**：识别模块、输出阶段路线图、逐阶段循环推进
6. 如果执行中发现复杂度超出预期，自动升级到更高档位

这个 Skill 适合：

- 小 Bug 修复与微调
- 功能开发
- 代码重构
- 调查与排障
- 多步骤实现任务
- 需要先澄清、再规划、再执行的复杂工作
- 由多个模块和阶段组成、需要持续推进的项目

不适合：

- 纯聊天或头脑风暴
- 一次性的小回答

---

### 核心能力

- **自动复杂度分流**：根据任务信号自动选择 quick-fix、单阶段或多阶段模式，无需用户干预
- **无感升级**：执行中发现复杂度超预期时，自动从轻量模式升级到完整规划流程
- **需求澄清优先**：先明确目标、约束、交付物与成功标准
- **单阶段 / 多阶段判断**：识别当前工作是一次性任务还是需要多轮推进的项目
- **阶段路线图规划**：对于多阶段项目，先识别模块，再产出粗粒度阶段表
- **当前阶段草案确认**：每一个阶段都要有草案与用户确认，而不是只在项目最开始确认一次
- **项目级路线图持久化**：多阶段项目会维护 `PROJECT_PHASE_ROADMAP.md`，用于保存完整阶段表、模块划分与当前阶段定位
- **双 Todo 驱动执行**：`TASK_TODO_MEDIUM.md` 和 `TASK_TODO_FINE.md` 始终表示“当前阶段”的计划与执行状态
- **阶段完成后刷新 Todo**：当当前阶段完成后，双 Todo 会更新为下一阶段目标，而不是把整个项目误判为结束
- **阶段历史可审计**：进入下一阶段前，上一阶段的双 Todo 会先归档，避免历史执行痕迹丢失
- **真实进度同步**：只有任务真的完成后，才把 `- [ ]` 改成 `- [x]`
- **能力按需调度**：首次激活时盘点可用 Skill / MCP，并按相关性深入
- **语言跟随用户**：默认跟随用户语言进行讨论与落盘

---

### 三档执行模式

#### Quick-fix（快速修复）
适用于：
- 明确的小 Bug、拼写错误、小行为缺陷
- 改动范围限于单个文件或少量相关行
- 修复方案清晰，无设计歧义
- 无明显副作用风险

此时：
- 跳过草案审批和 Todo 文件生成
- 直接研究、修复、报告
- 如果发现问题比预期复杂，自动升级到单阶段或多阶段

#### 单阶段任务
适用于：
- 交付物边界清晰
- 预期能在一个连续执行周期内完成
- 不需要阶段性路线图

此时：
- 项目级流程与阶段级流程几乎重合
- 双 Todo 表示整个任务

#### 多阶段项目
适用于：
- 存在多个模块或工作流，例如前端、后端、管理后台、测试、部署、文档等
- 阶段之间有明显依赖关系或里程碑
- 当前阶段完成后，还需要继续推进下一阶段

此时：
- Skill 会先识别项目模块
- 再产出粗粒度阶段表
- 然后只把“当前阶段”展开为中细粒度双 Todo
- 当前阶段完成后，再进入下一阶段循环

---

### 粗粒度阶段表（Phase Roadmap）

对于多阶段项目，Skill 会先输出粗粒度阶段表。  
这个阶段表不是直接执行清单，而是项目级路线图，并且应持久化到 `PROJECT_PHASE_ROADMAP.md`。

通常每个阶段会描述：

- 阶段名称
- 主要目标
- 范围边界
- 涉及模块
- 主要交付物
- 进入条件
- 完成条件
- 与下一阶段的衔接说明

例如一个项目可以被拆成：

- Phase 1：需求梳理与架构设计
- Phase 2：后端核心能力建设
- Phase 3：前端主流程实现
- Phase 4：管理后台与配置能力
- Phase 5：联调、测试与发布准备

---

### 双 Todo 的新语义

本 Skill 会生成两份 Todo：

- `PROJECT_PHASE_ROADMAP.md`：多阶段项目的项目级路线图与阶段状态文件
- `TASK_TODO_MEDIUM.md`：当前阶段的中粒度计划与沟通视图
- `TASK_TODO_FINE.md`：当前阶段的细粒度执行蓝图

也就是说：

- 对于单阶段任务，它们表示整个任务
- 对于多阶段项目，它们只表示当前阶段

当当前阶段完成后：

- Skill 会先做阶段回顾
- 更新 `PROJECT_PHASE_ROADMAP.md`，标记当前阶段状态并指向下一阶段
- 将当前阶段的双 Todo 归档到 `archive/` 目录中
- 明确已完成、延期项、风险变化与下一阶段重点
- 然后刷新两份 Todo，使其对准下一阶段目标

---

### 工作流概览

#### 1. Session bootstrap
- 识别当前可用的 skills、MCP、工作区上下文
- 只按需深入，不一次性加载全部能力

#### 2. Understand the requirement
- 提炼目标、约束、交付物、成功标准、未知项
- 初步识别这是单阶段还是多阶段工作

#### 3. Classify project mode
- 自动判断为 quick-fix、single-phase 或 multi-phase
- 如有必要，记录判断依据

#### 3a. Quick-fix abbreviated path（仅 quick-fix）
- 简要研究相关文件，确认问题根因
- 直接执行修复
- 报告改动内容、位置和验证方式
- 如发现复杂度超预期，自动升级并继续完整流程

#### 4. For multi-phase work, map modules and phases
- 识别项目模块（如前端、后端、管理、数据、测试、部署等）
- 输出粗粒度阶段路线图
- 确定当前活跃阶段

#### 5. Research and clarification loop
- 先看本地工作区
- 再复用相关 Skill / MCP
- 最后再向用户提出阻塞性问题
- 对多阶段项目，优先围绕“当前阶段”收集信息

#### 6. Draft and approval loop
- 输出草案
- 对多阶段项目，草案同时包含：
  - 项目级粗粒度阶段表
  - 当前阶段的详细执行方案
- 如果用户不满意，返回上一阶段继续迭代

#### 7. Write or refresh the todo
- 在工作区根目录生成或刷新：
  - `PROJECT_PHASE_ROADMAP.md`（多阶段项目）
  - `TASK_TODO_MEDIUM.md`
  - `TASK_TODO_FINE.md`
- 多阶段项目下，roadmap 文件保存项目级阶段表，双 Todo 始终表示“当前阶段”

#### 8. Execute from the todo
- 用中粒度 Todo 跟踪当前阶段整体进度
- 用细粒度 Todo 驱动当前阶段具体执行
- 完成一项，更新一项，并保持两份 Todo 同步

#### 9. Phase completion review and transition loop
- 判断当前完成的是整个任务，还是仅完成了当前阶段
- 如果只是完成当前阶段：
  - 回顾结果
  - 更新 `PROJECT_PHASE_ROADMAP.md`
  - 归档上一阶段双 Todo 到 `archive/`
  - 收集下一阶段所需上下文
  - 再次输出草案并确认
  - 刷新双 Todo
  - 进入下一轮执行
- 如此循环，直到项目真正结束

---

### Todo 设计规则

两份 Todo 都采用以下层次结构：

- `## Part N:` 表示一个大部分
- `### N.M` 表示一个小部分
- 每个小部分有唯一的 checkbox 行

勾选规则：

- `- [ ] Task:` 表示未完成
- `- [x] Task:` 表示已完成

中粒度任务通常包含：

- `Task`
- `Goal`
- `Done when`
- `Deliverables`
- `Notes`

细粒度任务通常包含：

- `Task`
- `Goal`
- `Inputs / Dependencies`
- `Procedure / Implementation notes`
- `Output / Artifact`
- `Done when`
- `Verification`
- `Notes`

在多阶段项目中，模板还应尽量包含：

- Roadmap File / Reference
- Project Mode
- Current Phase
- Phase Goal
- Phase Scope
- Exit Criteria / Done Definition
- Next Phase Trigger / Transition Notes
- Previous Phase Archive Reference

细粒度模板不限于软件开发任务。  
对于软件任务，它可以细到包结构、文件路径、类职责、接口、测试等；  
对于文档、研究、流程、运营类任务，则应细到该领域自然适用的执行单元、输入、输出、验证方式与交接点。

---

### 仓库结构

```text
.
├─ LICENSE
├─ README.md
├─ SKILL.md
├─ PROJECT_PHASE_ROADMAP.md           # 多阶段项目生成 / 维护的项目级阶段路线图
├─ TASK_TODO_MEDIUM.md                # 运行中任务生成 / 刷新的当前阶段中粒度 Todo
├─ TASK_TODO_FINE.md                  # 运行中任务生成 / 刷新的当前阶段细粒度 Todo
├─ archive/                           # 多阶段切换时归档历史 Todo（按需创建）
├─ agents/
│  └─ openai.yaml
└─ assets/
   ├─ PROJECT_PHASE_ROADMAP.template.md
   ├─ TASK_TODO_MEDIUM.template.md
   └─ TASK_TODO_FINE.template.md
```

---

### 文件说明

- `SKILL.md`  
  Skill 主说明文件，定义触发场景、项目级 / 阶段级工作流、守卫规则与执行方式。

- `agents/openai.yaml`  
  Skill 的 UI / 接口元数据。

- `assets/PROJECT_PHASE_ROADMAP.template.md`  
  项目级路线图模板，用于生成多阶段项目的持久化阶段表与状态视图。

- `assets/TASK_TODO_MEDIUM.template.md`  
  中粒度 Todo 模板，用于生成“当前阶段”的可审阅、可沟通计划视图。

- `assets/TASK_TODO_FINE.template.md`  
  细粒度 Todo 模板，用于生成“当前阶段”的可直接执行、可追踪、可核验执行蓝图。

- `LICENSE`  
  本仓库当前使用的开源许可证。

---

### 使用示例

```text
Use $requirement-to-delivery to handle this request. Automatically classify it as quick-fix, single-phase, or multi-phase, then follow the appropriate execution depth.
```

---

### 设计原则

- 自动选择最轻量的执行模式，复杂度超预期时无感升级
- 不用 quick-fix 模式回避真正需要规划的任务
- 不跳过非简单任务的草案确认
- 不在批准前修改工作区文件，除非用户明确授权
- 不把部分完成标记为完成
- 不深度加载与当前任务无关的 Skill / MCP
- 中粒度 Todo 必须便于快速审阅
- 细粒度 Todo 必须便于直接执行
- 多阶段项目下，阶段完成不等于项目完成
- `PROJECT_PHASE_ROADMAP.md` 必须作为多阶段项目的稳定项目级视图
- 进入新阶段前，必须重新经过澄清、草案、确认和 Todo 刷新流程
- 进入新阶段前，应先归档上一阶段双 Todo，保留执行与验证历史
- 两份 Todo 必须保持同步且都可审计

---

## English

### Overview

`requirement-to-delivery` is a workflow-oriented Codex skill for task and project delivery.

It automatically selects the right execution depth based on task complexity — from direct bug fixes to multi-phase project management — without requiring the user to choose a mode:

1. Understand the requirement
2. Automatically classify: quick-fix / single-phase / multi-phase
3. **Quick-fix**: research, fix, and report directly — skip the planning ceremony
4. **Single-phase**: get draft approval, generate dual todos, and execute
5. **Multi-phase**: identify modules, define a phase roadmap, and loop through phases
6. If complexity exceeds the initial classification during execution, seamlessly escalate to a higher mode

This skill is a good fit for:

- small bug fixes and tweaks
- feature work
- refactors
- investigations
- multi-step implementation tasks
- any task that benefits from clarification, planning, and tracked execution
- broader initiatives that should be advanced phase by phase

This skill is not a good fit for:

- casual conversation or brainstorming only
- one-off quick answers

---

### Core capabilities

- **Automatic complexity routing**: automatically selects quick-fix, single-phase, or multi-phase mode based on task signals — no user intervention needed
- **Seamless escalation**: if complexity exceeds the initial classification during execution, the skill upgrades to the appropriate full workflow automatically
- **Clarification first**: capture goals, constraints, deliverables, and success criteria
- **Single-phase / multi-phase classification**: identify whether the work is a bounded task or a broader initiative
- **Phase roadmap planning**: for multi-phase work, identify the main modules and define a coarse roadmap
- **Per-phase draft approval**: every phase gets its own draft/approval loop, not just the first one
- **Persistent project-level roadmap**: multi-phase work maintains `PROJECT_PHASE_ROADMAP.md` so the full roadmap and current phase remain visible across loops
- **Dual-todo execution**: `TASK_TODO_MEDIUM.md` and `TASK_TODO_FINE.md` always describe the **current active phase**
- **Todo refresh after phase completion**: when one phase finishes, the todo files are refreshed for the next phase instead of implying the whole project is done
- **Auditable phase history**: before entering the next phase, the finished phase todos are archived so execution evidence is not lost
- **Honest progress tracking**: only mark items complete when they are actually done
- **Capability orchestration**: inspect available skills and MCP surfaces on first activation, then use them progressively
- **Language matching**: follow the user's language by default when practical

---

### Three execution modes

#### Quick-fix
Use this mode when:
- there is an obvious bug, typo, or small behavioral defect
- the change is scoped to one file or a handful of closely related lines
- the fix is clear or can be determined with brief inspection — no design ambiguity
- there is no meaningful risk of side effects

In this case:
- skip draft approval and todo file generation entirely
- research, fix, and report directly
- if the issue turns out to be more complex than expected, seamlessly escalate to single-phase or multi-phase

#### Single-phase work
Use this mode when:
- there is one bounded deliverable
- the work can reasonably complete in one execution cycle
- there is no strong need for a roadmap beyond the immediate task

In this case:
- project-level planning and phase-level planning mostly collapse into one
- the todo files represent the whole task

#### Multi-phase work
Use this mode when:
- the project spans multiple modules or workstreams such as frontend, backend, admin, data, QA, deployment, or documentation
- milestone-based sequencing or dependencies matter
- completion of the current phase should lead into planning and execution of the next phase

In this case:
- the skill first identifies major modules
- then defines a coarse roadmap
- then expands only the **current active phase** into the medium/fine todo files
- when that phase completes, it loops forward into the next phase

---

### Coarse phase roadmap

For multi-phase work, the skill should first create a coarse phase roadmap.  
This roadmap is not the execution checklist. It is the project-level view, and it should be persisted in `PROJECT_PHASE_ROADMAP.md`.

Each phase should usually describe:

- phase name
- primary objective
- scope boundary
- modules involved
- main deliverables
- entry conditions
- completion conditions
- transition notes to the next phase

A project might, for example, be broken into:

- Phase 1: Requirement clarification and architecture
- Phase 2: Backend core capabilities
- Phase 3: Frontend primary flows
- Phase 4: Admin and configuration capabilities
- Phase 5: Integration, testing, and release readiness

---

### Updated meaning of the dual todo files

This skill uses a three-layer artifact model for multi-phase work:

- `PROJECT_PHASE_ROADMAP.md` for the durable project-level roadmap
- `TASK_TODO_MEDIUM.md` for the medium-granularity review and communication view of the **current phase**
- `TASK_TODO_FINE.md` for the fine-granularity execution blueprint of the **current phase**

That means:

- for single-phase work, they represent the whole task
- for multi-phase work, they represent only the current phase

When a phase completes, the skill should:

- review what was completed and what was deferred
- update `PROJECT_PHASE_ROADMAP.md` with the finished phase status and next active phase
- archive the finished phase todo files under `archive/` using phase-aware names when practical
- capture changes in assumptions, risks, and dependencies
- refresh both todo files for the next phase target

---

### Workflow summary

#### 1. Session bootstrap
- Inspect available skills, MCP surfaces, and relevant workspace context
- Load deeper details only when needed

#### 2. Understand the requirement
- Capture goals, constraints, deliverables, success criteria, and unknowns
- Form an initial view of whether the work is single-phase or multi-phase

#### 3. Classify project mode
- Automatically decide whether the work should be treated as quick-fix, single-phase, or multi-phase
- Record the reasoning when helpful

#### 3a. Quick-fix abbreviated path (quick-fix only)
- Briefly inspect the relevant files and confirm the root cause
- Apply the fix directly
- Report what was changed, where, and how to verify
- If complexity exceeds expectations, escalate seamlessly and continue with the full workflow

#### 4. For multi-phase work, map modules and phases
- Identify the project modules (for example frontend, backend, admin, data, QA, deployment)
- Create a coarse phase roadmap
- Identify the current active phase

#### 5. Research and clarification loop
- Inspect local context first
- Reuse relevant skills / MCP tools
- Ask the user only the minimum blocking questions
- For multi-phase work, focus the deeper clarification on the current phase unless roadmap uncertainty is blocking

#### 6. Draft and approval loop
- Present a draft
- For multi-phase work, include both:
  - a project-level roadmap
  - a detailed current-phase approach
- Return to clarification if the user requests revisions

#### 7. Write or refresh the todo
- Create or refresh:
  - `PROJECT_PHASE_ROADMAP.md` for multi-phase work
  - `TASK_TODO_MEDIUM.md`
  - `TASK_TODO_FINE.md`
- In multi-phase work, the roadmap file keeps the durable project view, while the todo files always represent the **current active phase**

#### 8. Execute from the todo
- Use the medium todo for current-phase scope tracking and review
- Use the fine todo as the current-phase execution blueprint
- Keep both files synchronized as work progresses

#### 9. Phase completion review and transition loop
- Decide whether the work itself is complete or whether only the current phase is complete
- If only the phase is complete:
  - review the result
  - update `PROJECT_PHASE_ROADMAP.md`
  - archive the previous phase todo files under `archive/`
  - gather context for the next phase
  - draft the next phase and get approval
  - refresh the dual todo files
  - execute the next phase
- Repeat until the project is actually complete

---

### Todo design rules

Both todo files use:

- `## Part N:` for major workstreams
- `### N.M` for concrete subtasks
- one checkbox line per subtask

Checkbox rules:

- `- [ ] Task:` means not completed
- `- [x] Task:` means completed

Medium-granularity subtasks should typically include:

- `Task`
- `Goal`
- `Done when`
- `Deliverables`
- `Notes`

Fine-granularity subtasks should typically include:

- `Task`
- `Goal`
- `Inputs / Dependencies`
- `Procedure / Implementation notes`
- `Output / Artifact`
- `Done when`
- `Verification`
- `Notes`

For multi-phase work, the templates should also include phase-aware context such as:

- Roadmap File / Reference
- Project Mode
- Current Phase
- Phase Goal
- Phase Scope
- Exit Criteria / Done Definition
- Next Phase Trigger / Transition Notes
- Previous Phase Archive Reference

The fine-granularity todo is not limited to software work.  
For software tasks it may include package layout, file paths, class responsibilities, interfaces, tests, and validation steps.  
For research, document, operational, or process tasks, it should become equally concrete in the natural units of that domain.

---

### Repository structure

```text
.
├─ LICENSE
├─ README.md
├─ SKILL.md
├─ PROJECT_PHASE_ROADMAP.md           # generated/maintained project-level roadmap for multi-phase work
├─ TASK_TODO_MEDIUM.md                # generated/refreshed current-phase medium todo during execution
├─ TASK_TODO_FINE.md                  # generated/refreshed current-phase fine todo during execution
├─ archive/                           # archived prior-phase todos for multi-phase work (created as needed)
├─ agents/
│  └─ openai.yaml
└─ assets/
   ├─ PROJECT_PHASE_ROADMAP.template.md
   ├─ TASK_TODO_MEDIUM.template.md
   └─ TASK_TODO_FINE.template.md
```

---

### File overview

- `SKILL.md`  
  Main skill definition, including trigger conditions, project-level / phase-level workflow, guardrails, and execution behavior.

- `agents/openai.yaml`  
  UI / interface metadata for the skill.

- `assets/PROJECT_PHASE_ROADMAP.template.md`  
  Recommended starter template for the durable project-level roadmap in multi-phase work.

- `assets/TASK_TODO_MEDIUM.template.md`  
  Recommended starter template for the medium-granularity plan view of the **current phase**.

- `assets/TASK_TODO_FINE.template.md`  
  Recommended starter template for the fine-granularity execution blueprint of the **current phase**.

- `LICENSE`  
  The open-source license currently used by this repository.

---

### Example usage

```text
Use $requirement-to-delivery to handle this request. Automatically classify it as quick-fix, single-phase, or multi-phase, then follow the appropriate execution depth.
```

---

### Design principles

- Always select the lightest execution mode that fits the task; escalate seamlessly when complexity exceeds expectations
- Do not use quick-fix mode to avoid planning on tasks that genuinely need it
- Do not skip draft approval for non-trivial work
- Do not modify workspace files before approval unless explicitly authorized
- Do not mark partial progress as complete
- Do not deeply load unrelated skills or tools
- Keep the medium todo reviewable and concise
- Keep the fine todo concrete, auditable, and execution-friendly
- In multi-phase work, phase completion is not the same as project completion
- `PROJECT_PHASE_ROADMAP.md` should remain the stable project-level view for multi-phase work
- Before entering a new phase, go through clarification, draft, approval, and todo refresh again
- Archive the completed phase todos before refreshing them for the next phase
- Keep both todo files synchronized

---

## License

This repository is licensed under the **MIT License**. See [LICENSE](./LICENSE).
