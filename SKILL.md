---
name: requirement-to-delivery
description: Use this skill when the user wants to turn a vague, evolving, or multi-step requirement into an approved execution plan and then have Codex carry it out in the workspace. Best for feature work, refactors, investigations, implementation projects, or other tasks that benefit from iterative clarification, a markdown todo file, and progress tracking. Do not use it for tiny one-shot answers or purely conversational brainstorming with no intent to execute.
---

# Requirement to Delivery

## Overview

Use this skill to move a task from rough intent to approved draft, then to a tracked markdown todo, and finally to execution in the workspace. The skill should act like a disciplined operator: clarify the request, research what is already available, ask only the minimum necessary questions, create a concrete plan, and then execute while keeping progress synchronized in a todo file.

## When to use

Use this skill when:
- The user has a real task to complete, not just a question to answer.
- The request is ambiguous, incomplete, or likely to evolve during discussion.
- The work is large enough to benefit from a written plan and progress tracking.
- The task may require combining workspace files, existing skills, MCP tools, and iterative user feedback.

Do not use this skill when:
- The user only wants a quick answer, explanation, or brainstorming.
- The task is so small that a todo file would add more ceremony than value.
- The user explicitly wants discussion only and does not want planning or execution.

## Session bootstrap

On the first activation for a task, or the first conversation where this skill becomes relevant:
1. Inspect what skills, MCP servers, and relevant workspace context are available.
2. Build a lightweight mental map of those capabilities.
3. Read deeper instructions or invoke tools only when they are relevant to the current task.
4. Prefer reusing existing capabilities before inventing a custom process.

Do not fully load every available skill or tool specification just because it exists.

### Capability discovery

During bootstrap:
1. List available skills by name and short description when that information is available.
2. Identify what MCP servers or tool surfaces are available in the current session.
3. Match the current task against those capabilities.
4. Read detailed instructions only for the skills that are materially relevant.
5. Invoke MCP tools only when they help the active stage move forward faster or more reliably.

Use a progressive loading strategy:
- First inspect names, summaries, and obvious capability signals.
- Then narrow to the few skills or tools most relevant to the user's task.
- Only then load deeper instructions or perform tool calls.

## Workflow

### Stage 1: Understand the requirement

Turn the user's request into a concrete task definition.

Capture:
- Goal
- Constraints
- Expected deliverable
- Success criteria
- Important unknowns

If key information is already discoverable from the workspace, existing skills, or available tools, inspect that first before asking the user.

### Stage 2: Research and clarification loop

Fill missing context before proposing a final execution path.

Preferred order:
1. Inspect workspace files and local context.
2. Reuse relevant skills and MCP capabilities.
3. Ask the user only the blocking questions that cannot be resolved locally.

Rules for questioning:
- Ask the fewest questions needed to unblock the next decision.
- Prefer high-value questions over exhaustive questionnaires.
- If uncertainty does not block progress, proceed with explicit assumptions.

### Stage 3: Draft and approval loop

Before writing a todo file or executing, provide a draft that the user can review.

The draft should include:
- Proposed approach
- Scope boundaries
- Assumptions
- Key deliverables
- Risks or open questions

If the user is not satisfied, return to Stage 2 and refine the draft.

Do not create the todo file and do not start implementation until the user clearly approves the draft or clearly asks to continue.
Do not modify workspace files before approval unless the user explicitly asks for exploratory file creation or the task itself is to produce the draft as a file.

### Stage 4: Write the todo file

After approval, create `TASK_TODO.md` in the workspace root.

The file is the source of truth for the implementation plan and execution status.

If `assets/TASK_TODO.template.md` exists in this skill, use it as the preferred starting structure and adapt it to the task.

Use this structure:

```md
# Task Todo

## Part 1: High-level area
### 1.1 Subtask title
- [ ] Task: Concrete action to perform
- Goal: Why this subtask exists
- Done when: Observable completion condition
- Deliverables: Files, outputs, or decisions produced
- Notes: Assumptions, risks, dependencies, or blockers
```

Formatting rules:
- Use multiple `## Part N:` sections for major workstreams.
- Use multiple `### N.M` subsections for concrete subtasks.
- Each subtask must have exactly one checkbox line that represents completion.
- The checkbox line starts as `- [ ] Task:`.
- Keep descriptions specific enough that progress can be audited later.

## Stage 5: Execute from the todo file

Use `TASK_TODO.md` as the live execution plan.

Execution rules:
1. Work from the todo file rather than from memory.
2. If the plan changes materially, update the todo file before continuing.
3. Only change `- [ ]` to `- [x]` after the subtask is truly completed.
4. Completion means the work is done and any necessary validation for that subtask has been performed.
5. If something is blocked, keep the task unchecked and explain the blocker in `Notes:`.

Never mark a task as complete for partial progress.

## Tool and skill orchestration policy

When this skill is active:
- Prefer existing workspace artifacts before creating new ones.
- Prefer relevant existing skills before re-deriving specialized workflows.
- Prefer MCP tools when they provide faster or more reliable access to the needed information.
- Choose tools in service of the current stage rather than using them performatively.
- Load detailed instructions only when they are relevant to the active task.

## Response behavior

During discussion phases:
- Be concise, structured, and explicit about assumptions.
- Distinguish confirmed facts from inferred assumptions.
- Tell the user when you are still in clarification or draft mode.
- Match the user's language by default unless the user requests another language.

During execution phases:
- Mention when `TASK_TODO.md` is created.
- Mention when a task is completed and the checkbox is updated.
- Keep progress synchronized with actual work performed.
- Keep `TASK_TODO.md` in the user's preferred working language when practical.

## Guardrails

- Do not skip the approval loop for non-trivial work.
- Do not create a bloated todo file full of vague tasks.
- Do not ask redundant questions when the answer can be found locally.
- Do not mark work complete unless it is actually complete.
- Do not overuse tools or load unrelated skill instructions.
- Do not modify workspace files before approval unless the user has clearly authorized that behavior.
- Stay aligned with the user's requested scope; if scope expands, say so and update the plan.

## Default posture

Act as an execution-oriented project operator:
- First understand
- Then research
- Then propose
- Then plan
- Then execute
- Then keep the plan honest
