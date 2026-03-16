# requirement-to-delivery

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](./LICENSE)
[![Skill](https://img.shields.io/badge/Codex-Skill-blue)](./SKILL.md)
[![Language](https://img.shields.io/badge/README-Bilingual-orange)](./README.md)

> Turn vague requirements into approved drafts, tracked markdown todos, and real execution in the workspace.  
> 把模糊需求推进为已确认草案、可追踪 Markdown Todo，并最终在工作区执行落地。

---

## 中文说明

### 简介

`requirement-to-delivery` 是一个面向复杂任务交付的 Codex Skill。  
它的目标不是让代理直接跳进实现，而是让它先建立正确的执行节奏：

1. 理解需求
2. 调研上下文、可用 Skill 和 MCP 能力
3. 输出草案并与用户确认
4. 在工作区生成 `TASK_TODO.md`
5. 根据 Todo 分步执行
6. 随着真实完成进度更新 `- [ ]` 为 `- [x]`

这个 Skill 适合：

- 功能开发
- 代码重构
- 调查与排障
- 多步骤实现任务
- 需要先澄清、再规划、再执行的复杂工作

不适合：

- 纯聊天或头脑风暴
- 一次性的小回答
- 不需要计划与执行跟踪的微小任务

---

### 核心能力

- **需求澄清优先**：先明确目标、约束、交付物与成功标准
- **先调研后追问**：优先利用工作区、Skill、MCP 和现有上下文
- **草案确认闭环**：用户不满意时，回到调研与澄清阶段继续迭代
- **Todo 驱动执行**：确认后生成 `TASK_TODO.md`，作为执行真相源
- **真实进度同步**：只有任务真的完成后，才把 `- [ ]` 改成 `- [x]`
- **能力按需调度**：首次激活时盘点可用 Skill / MCP，并按相关性深入
- **语言跟随用户**：默认跟随用户语言进行讨论与落盘

---

### 工作流概览

#### 1. Session bootstrap
- 识别当前可用的 skills、MCP、工作区上下文
- 只按需深入，不一次性加载全部能力

#### 2. Understand the requirement
- 提炼目标、约束、交付物、成功标准、未知项

#### 3. Research and clarification loop
- 先看本地工作区
- 再复用相关 Skill / MCP
- 最后再向用户提出阻塞性问题

#### 4. Draft and approval loop
- 输出草案
- 如果用户不满意，返回上一阶段继续迭代

#### 5. Write the todo
- 在工作区根目录生成 `TASK_TODO.md`

#### 6. Execute from the todo
- 按 Todo 执行任务
- 完成一项，更新一项

---

### Todo 设计规则

Todo 文件采用以下结构：

- `## Part N:` 表示一个大部分
- `### N.M` 表示一个小部分
- 每个小部分有唯一的 checkbox 行

勾选规则：

- `- [ ] Task:` 表示未完成
- `- [x] Task:` 表示已完成

每个子任务通常应包含：

- `Task`
- `Goal`
- `Done when`
- `Deliverables`
- `Notes`

---

### 仓库结构

```text
.
├─ LICENSE
├─ README.md
├─ SKILL.md
├─ agents/
│  └─ openai.yaml
└─ assets/
   └─ TASK_TODO.template.md
```

---

### 文件说明

- `SKILL.md`  
  Skill 主说明文件，定义触发场景、工作流、守卫规则与执行方式。

- `agents/openai.yaml`  
  Skill 的 UI / 接口元数据。

- `assets/TASK_TODO.template.md`  
  推荐的 Todo 模板，用于快速生成 `TASK_TODO.md`。

- `LICENSE`  
  本仓库当前使用的开源许可证。

---

### 使用示例

```text
Use $requirement-to-delivery to clarify this request, draft a plan, create TASK_TODO.md, and execute it step by step.
```

---

### 设计原则

- 不跳过非简单任务的草案确认
- 不在批准前修改工作区文件，除非用户明确授权
- 不把部分完成标记为完成
- 不深度加载与当前任务无关的 Skill / MCP
- Todo 必须具体、可审计、可执行

---

## English

### Overview

`requirement-to-delivery` is a workflow-oriented Codex skill for non-trivial task delivery.

Its purpose is not to jump straight into implementation, but to move through a disciplined sequence:

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

- casual conversation or brainstorming only
- one-off quick answers
- tiny tasks that do not need planning or execution tracking

---

### Core capabilities

- **Clarification first**: capture goals, constraints, deliverables, and success criteria
- **Research before questioning**: inspect workspace context, existing skills, and MCP tools first
- **Draft approval loop**: return to clarification when the user wants revisions
- **Todo-driven execution**: create `TASK_TODO.md` as the execution source of truth
- **Honest progress tracking**: only mark items complete when they are actually done
- **Capability orchestration**: inspect available skills and MCP surfaces on first activation, then use them progressively
- **Language matching**: follow the user's language by default when practical

---

### Workflow summary

#### 1. Session bootstrap
- Inspect available skills, MCP surfaces, and relevant workspace context
- Load deeper details only when needed

#### 2. Understand the requirement
- Capture goals, constraints, deliverables, success criteria, and unknowns

#### 3. Research and clarification loop
- Inspect local context first
- Reuse relevant skills / MCP tools
- Ask the user only the minimum blocking questions

#### 4. Draft and approval loop
- Present a draft
- Return to clarification if the user requests revisions

#### 5. Write the todo
- Create `TASK_TODO.md` in the workspace root

#### 6. Execute from the todo
- Work from the todo
- Update checkbox state as work is actually completed

---

### Todo design rules

The todo file is structured with:

- `## Part N:` for major workstreams
- `### N.M` for concrete subtasks
- one checkbox line per subtask

Checkbox rules:

- `- [ ] Task:` means not completed
- `- [x] Task:` means completed

Each subtask should typically include:

- `Task`
- `Goal`
- `Done when`
- `Deliverables`
- `Notes`

---

### Repository structure

```text
.
├─ LICENSE
├─ README.md
├─ SKILL.md
├─ agents/
│  └─ openai.yaml
└─ assets/
   └─ TASK_TODO.template.md
```

---

### File overview

- `SKILL.md`  
  Main skill definition, including trigger conditions, workflow, guardrails, and execution behavior.

- `agents/openai.yaml`  
  UI / interface metadata for the skill.

- `assets/TASK_TODO.template.md`  
  Recommended starter template for generating `TASK_TODO.md`.

- `LICENSE`  
  The open-source license currently used by this repository.

---

### Example usage

```text
Use $requirement-to-delivery to clarify this request, draft a plan, create TASK_TODO.md, and execute it step by step.
```

---

### Design principles

- Do not skip draft approval for non-trivial work
- Do not modify workspace files before approval unless explicitly authorized
- Do not mark partial progress as complete
- Do not deeply load unrelated skills or tools
- Keep the todo concrete, auditable, and execution-friendly

---

## License

This repository is licensed under the **MIT License**. See [LICENSE](./LICENSE).
