# requirement-to-delivery

> A Codex skill for turning vague requirements into approved drafts, tracked markdown todos, and real execution in the workspace.  
> 一个用于把模糊需求推进为已确认草案、可追踪 Markdown Todo，并最终在工作区执行落地的 Codex Skill。

---

## 中文说明

### 这是什么

`requirement-to-delivery` 是一个面向复杂任务交付的工作流型 Skill。  
它的目标不是直接“跳进实现”，而是帮助 Codex 按照更稳定的节奏推进任务：

1. 理解用户需求  
2. 调研现有上下文、Skill、MCP 与工作区信息  
3. 提出草案并与用户确认  
4. 在工作区生成 `TASK_TODO.md`  
5. 根据 Todo 执行任务  
6. 随任务进度把 `- [ ]` 更新为 `- [x]`

这个 Skill 适用于：

- 功能开发
- 重构任务
- 调查/排障
- 多步骤实现任务
- 需要先澄清、再规划、再执行的工作

不适用于：

- 纯聊天
- 一次性小回答
- 完全不需要计划或执行的简单任务

### 核心特性

- **需求澄清优先**：先把目标、约束、交付物和成功标准搞清楚
- **调研后追问**：优先从工作区、Skill、MCP 获取信息，再问用户阻塞性问题
- **草案确认机制**：用户不满意时，回到调研与澄清阶段继续迭代
- **Todo 驱动执行**：经确认后生成 `TASK_TODO.md` 作为执行真相源
- **进度实时同步**：只有真实完成后，才把 `- [ ]` 改为 `- [x]`
- **能力按需调度**：首次激活时盘点可用 Skill 与 MCP，并按需深入使用
- **语言跟随用户**：默认跟随用户语言进行讨论与落盘

### 仓库结构

```text
.
├─ SKILL.md
├─ README.md
├─ agents/
│  └─ openai.yaml
└─ assets/
   └─ TASK_TODO.template.md
```

### 文件说明

- `SKILL.md`  
  Skill 主体说明，定义触发场景、工作流、守卫规则与执行方式。

- `agents/openai.yaml`  
  Skill 的 UI / 接口元数据。

- `assets/TASK_TODO.template.md`  
  `TASK_TODO.md` 的推荐模板，用于在执行前快速生成可追踪计划。

### 使用方式

当用户提出一个较大、较模糊、或需要多阶段推进的任务时，可以调用这个 Skill。

示例：

```text
Use $requirement-to-delivery to clarify this request, draft a plan, create TASK_TODO.md, and execute it step by step.
```

### 典型工作流

1. **Session bootstrap**
   - 盘点当前可用 skills、MCP、工作区上下文
   - 只按需深入，不一次性加载全部能力

2. **Understand the requirement**
   - 提炼目标、约束、交付物、成功标准、未知项

3. **Research and clarification loop**
   - 先看本地
   - 再复用 skill / MCP
   - 最后再问用户

4. **Draft and approval loop**
   - 输出草案
   - 用户不满意则返回上一阶段继续迭代

5. **Write the todo**
   - 在工作区根目录创建 `TASK_TODO.md`

6. **Execute from the todo**
   - 按 Todo 实施
   - 完成即更新勾选状态

### Todo 设计原则

Todo 文件使用以下结构：

- `## Part N:` 表示一个大部分
- `### N.M` 表示一个小部分
- 每个小部分有唯一的 checkbox 行
- 使用：
  - `- [ ] Task:` 表示未完成
  - `- [x] Task:` 表示已完成

并补充：

- `Goal:`
- `Done when:`
- `Deliverables:`
- `Notes:`

### 设计原则

- 不跳过草案确认
- 不在批准前修改工作区文件（除非用户明确允许）
- 不为部分完成而打勾
- 不做与当前任务无关的 Skill / MCP 深度加载
- Todo 必须具体、可核验、可追踪

---

## English

### What this is

`requirement-to-delivery` is a workflow-oriented Codex skill for handling non-trivial tasks from vague intent to real delivery.

Instead of jumping straight into implementation, it helps Codex move through a disciplined sequence:

1. Understand the requirement  
2. Research relevant workspace context, skills, and MCP capabilities  
3. Present a draft and get user approval  
4. Create `TASK_TODO.md` in the workspace  
5. Execute from the todo  
6. Update `- [ ]` to `- [x]` only when work is truly complete

This skill is a good fit for:

- feature work
- refactors
- investigations
- multi-step implementation tasks
- any task that benefits from clarification, planning, and tracked execution

This skill is not a good fit for:

- casual conversation
- one-off quick answers
- tiny tasks that do not need a plan or execution tracking

### Core capabilities

- **Requirement clarification first**: extract goals, constraints, deliverables, and success criteria
- **Research before questioning**: inspect the workspace, skills, and MCP tools before asking the user blocking questions
- **Draft approval loop**: refine the draft when the user is not satisfied
- **Todo-driven execution**: create `TASK_TODO.md` as the source of truth after approval
- **Honest progress tracking**: only mark tasks complete when they are actually done
- **Capability orchestration**: inspect available skills and MCP surfaces on first activation, then use them progressively
- **Language matching**: follow the user's language by default when practical

### Repository structure

```text
.
├─ SKILL.md
├─ README.md
├─ agents/
│  └─ openai.yaml
└─ assets/
   └─ TASK_TODO.template.md
```

### File overview

- `SKILL.md`  
  The main skill definition, including trigger conditions, workflow, guardrails, and execution behavior.

- `agents/openai.yaml`  
  UI / interface metadata for the skill.

- `assets/TASK_TODO.template.md`  
  A recommended starting template for generating `TASK_TODO.md`.

### Usage

Use this skill when a task is large enough to require clarification, a plan, and step-by-step execution.

Example prompt:

```text
Use $requirement-to-delivery to clarify this request, draft a plan, create TASK_TODO.md, and execute it step by step.
```

### Typical workflow

1. **Session bootstrap**
   - Inspect available skills, MCP surfaces, and relevant workspace context
   - Load deeper details only when needed

2. **Understand the requirement**
   - Capture goals, constraints, deliverables, success criteria, and unknowns

3. **Research and clarification loop**
   - Inspect local context first
   - Reuse skills / MCP when relevant
   - Ask the user only the minimum blocking questions

4. **Draft and approval loop**
   - Present a draft
   - Return to clarification if the user wants revisions

5. **Write the todo**
   - Create `TASK_TODO.md` in the workspace root

6. **Execute from the todo**
   - Work from the todo
   - Update checkbox status honestly as work completes

### Todo design rules

The todo file is structured as:

- `## Part N:` for major workstreams
- `### N.M` for concrete subtasks
- one checkbox line per subtask

Each subtask should include:

- `Task`
- `Goal`
- `Done when`
- `Deliverables`
- `Notes`

### Design principles

- Do not skip draft approval for non-trivial work
- Do not modify workspace files before approval unless explicitly authorized
- Do not mark partial progress as complete
- Do not deeply load unrelated skills or tools
- Keep the todo concrete, auditable, and execution-friendly

---

## License

Add a license if you want to distribute or reuse this repository publicly.
