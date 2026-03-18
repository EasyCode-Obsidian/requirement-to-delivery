---
name: requirement-to-delivery
description: Use this skill when the user wants to turn a requirement — from a small bug fix to a multi-phase project — into tracked execution. The skill automatically classifies the task as quick-fix, single-phase, or multi-phase and selects the appropriate execution depth without user intervention.
---

# Requirement to Delivery

## Overview

Use this skill to move a task from rough intent to execution in the workspace. The skill automatically selects the right execution depth based on task complexity.

This skill should act like a disciplined operator with adaptive control:
- **Quick-fix**: for small, well-defined changes — understand, inspect, fix, report. No planning artifacts needed.
- **Project level**: for larger work — understand the overall intent, decide whether the work is single-phase or multi-phase, define a durable roadmap when needed, and keep the project-level view current across phases.
- **Phase level**: for each execution cycle — clarify the current active phase, get approval, create or refresh the medium-granularity and fine-granularity todo files, execute, verify, archive the finished phase, and then decide whether to move into the next phase.

The skill seamlessly routes between these levels. For multi-phase work, it must keep re-entering the clarification -> draft -> approval -> execution -> archive -> refresh loop until the project is complete.

## When to use

Use this skill when:
- The user has a real task or project to complete, not just a question to answer.
- The request is ambiguous, incomplete, or likely to evolve during discussion.
- The work benefits from structured planning, progress tracking, or layered task decomposition.
- The task may require combining workspace files, existing skills, MCP tools, and iterative user feedback.
- The work may range from a small bug fix to a multi-phase initiative — the skill automatically selects the appropriate execution depth.

Do not use this skill when:
- The user only wants a quick answer, explanation, or brainstorming.
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

## Operating model

This skill operates on up to two levels, depending on the classified mode:

### Quick-fix level
For quick-fix tasks, the skill operates as a lightweight executor:
- understand the defect or change
- inspect the relevant context
- apply the fix directly
- report the result

No project-level or phase-level planning is needed.

### Project level
At the project level, determine:
- the user's overall goal
- whether the work is single-phase or multi-phase
- the major modules or domains involved
- the coarse roadmap if the work spans multiple phases
- where that roadmap is persisted
- which phase is currently active

### Phase level
At the phase level, determine:
- the current phase objective
- the phase boundaries and success criteria
- the context needed for this phase
- the approved approach for this phase
- the medium and fine todo for this phase
- the completion result and transition path to the next phase

For single-phase work, the project level and phase level effectively collapse into one phase.
For multi-phase work, the project-level roadmap remains coarse while the todo files always represent the **current active phase**.
For quick-fix work, neither level applies — the skill operates as a direct executor.

## Workflow

### Stage 1: Understand the requirement

Turn the user's request into a concrete task definition.

Capture:
- Goal
- Constraints
- Expected deliverable
- Success criteria
- Important unknowns
- Whether the user appears to be describing a bounded task or an ongoing project

If key information is already discoverable from the workspace, existing skills, or available tools, inspect that first before asking the user.

### Stage 2: Classify project mode

Before proposing execution, decide which execution depth the work requires:

- **Quick-fix**: a small, well-defined change that can be understood and executed directly without formal planning artifacts
- **Single-phase**: a bounded task that can reasonably be planned and completed within one continuous execution cycle
- **Multi-phase**: a broader project that spans multiple modules, milestones, or handoff points and should be advanced one phase at a time

Signals for **quick-fix** work:
- an obvious bug, typo, or small behavioral defect
- a change scoped to one file or a handful of closely related lines
- the fix is clear or can be determined with brief inspection — no design ambiguity
- no meaningful risk of side effects beyond the immediate change
- the user's description itself implies a small, bounded correction (e.g. "fix this error", "this button doesn't work", "update this value")

Signals for **single-phase** work:
- one main deliverable
- one bounded implementation window
- little need for roadmap-level sequencing beyond the immediate task
- enough complexity that a written plan helps track progress and communicate scope

Signals for **multi-phase** work:
- multiple modules or workstreams (for example frontend, backend, admin, data, QA, deployment, documentation)
- milestone-based delivery or dependency chains
- the need to finish one stage before planning the next in detail
- a likely need to refresh the todo files after one stage finishes

Classification is automatic. The skill selects the lightest mode that fits the task. If the task turns out to be more complex than initially classified, the skill escalates seamlessly: a quick-fix that reveals deeper issues becomes single-phase; a single-phase task that uncovers multi-module scope becomes multi-phase. Escalation does not require user intervention — the skill announces the reclassification and proceeds with the appropriate workflow.

If uncertainty does not block progress, proceed with an explicit classification assumption.

### Stage 3: For multi-phase work, map modules and define the phase roadmap

If the work is multi-phase, identify the major project modules and create a coarse phase roadmap before writing execution todos. That roadmap should be treated as a durable project artifact rather than a one-time chat-only summary.

Capture, when relevant:
- Major modules or domains involved
- What each module is responsible for
- A rough sequence of phases
- What each phase is intended to accomplish
- What is intentionally out of scope for the current phase
- Which phase is currently active

The roadmap should stay coarse and reviewable. It is not meant to replace the phase todo files. Instead, it provides the stable project-level reference that survives phase-to-phase todo refreshes.

A multi-phase roadmap should typically describe each phase with:
- Phase name
- Primary objective
- Scope boundary
- Modules involved
- Main deliverables
- Entry conditions
- Completion conditions
- Transition notes to the next phase

### Quick-fix abbreviated path

When the task is classified as **quick-fix**, the skill bypasses Stages 3, 5, and 6 entirely and follows this abbreviated path:

1. **Understand** (Stage 1): Capture the defect or change request. Inspect the relevant code or context to confirm the scope is genuinely small.
2. **Classify** (Stage 2): Confirm quick-fix mode. If inspection reveals the issue is more complex than it appeared, escalate to single-phase or multi-phase immediately.
3. **Research** (Stage 4, abbreviated): Inspect the relevant files, reproduce or confirm the issue, identify the root cause. No user questions unless truly blocking.
4. **Execute directly**: Apply the fix. No draft approval, no todo files.
5. **Report**: Briefly state what was changed, where, why, and how to verify. If the change has any non-obvious implications, mention them.

Quick-fix guardrails:
- Do not use quick-fix mode as an excuse to skip understanding. Always inspect before changing.
- If the fix touches more than a handful of lines across multiple unrelated files, escalate.
- If the root cause is unclear after brief inspection, escalate.
- If the fix could have non-trivial side effects, escalate.
- Escalation is seamless — announce the reclassification and continue with the appropriate full workflow.

### Stage 4: Research and clarification loop

Fill missing context before proposing the current execution path.

Preferred order:
1. Inspect workspace files and local context.
2. Reuse relevant skills and MCP capabilities.
3. Ask the user only the blocking questions that cannot be resolved locally.

Rules for questioning:
- Ask the fewest questions needed to unblock the next decision.
- Prefer high-value questions over exhaustive questionnaires.
- If uncertainty does not block progress, proceed with explicit assumptions.
- For multi-phase work, focus questions on the **current active phase** unless roadmap uncertainty is itself blocking.

### Stage 5: Draft and approval loop

This stage applies to **single-phase** and **multi-phase** work only. Quick-fix tasks skip this stage entirely.

For **single-phase** work, the draft should include:
- Proposed approach
- Scope boundaries
- Assumptions
- Key deliverables
- Risks or open questions

For **multi-phase** work, the draft should include both:
1. A coarse roadmap view of the project, and
2. A detailed approach for the **current active phase**

The current-phase draft should include:
- Current phase objective
- Current phase boundaries
- Current phase deliverables
- Assumptions
- Risks or open questions
- What will happen after this phase completes

If the user is not satisfied, return to Stage 4 and refine the draft.

Do not create or refresh the todo files and do not start implementation until the user clearly approves the draft or clearly asks to continue.
Do not modify workspace files before approval unless the user explicitly asks for exploratory file creation or the task itself is to produce the draft as a file.

### Stage 6: Write or refresh the todo files

This stage applies to **single-phase** and **multi-phase** work only. Quick-fix tasks skip this stage entirely.

After approval, create or update the workspace artifacts needed for the active mode.

For **single-phase** work, create or update:
- `TASK_TODO_MEDIUM.md`
- `TASK_TODO_FINE.md`

For **multi-phase** work, create or update:
- `PROJECT_PHASE_ROADMAP.md` as the durable project-level roadmap
- `TASK_TODO_MEDIUM.md` as the planning and communication view for the **current active phase**
- `TASK_TODO_FINE.md` as the execution and traceability view for the **current active phase**

If `assets/TASK_TODO_MEDIUM.template.md`, `assets/TASK_TODO_FINE.template.md`, or `assets/PROJECT_PHASE_ROADMAP.template.md` exist in this skill, use them as the preferred starting structures and adapt them to the task.

For **single-phase** work:
- The todo files represent the whole task.

For **multi-phase** work:
- `PROJECT_PHASE_ROADMAP.md` stores the stable coarse roadmap, the module map, the current active phase, and the remaining planned phases.
- The todo files represent only the **current active phase**.
- When the current phase changes materially, update `PROJECT_PHASE_ROADMAP.md` first or alongside the phase refresh.
- When a phase completes, archive the current todo files before refreshing them for the next phase. Use phase-identifying archive names when practical, for example `archive/TASK_TODO_MEDIUM.phase-2-backend.md` and `archive/TASK_TODO_FINE.phase-2-backend.md`.
- Preserve enough transition context so the next phase starts with a clear handoff and the prior phase remains auditable.

Use this structure for the medium-granularity todo:

```md
# Task Todo - Medium

## Part 1: High-level area
### 1.1 Subtask title
- [ ] Task: Concrete action to perform
- Goal: Why this subtask exists
- Done when: Observable completion condition
- Deliverables: Files, outputs, or decisions produced
- Notes: Assumptions, risks, dependencies, or blockers
```

Use this structure for the fine-granularity todo:

```md
# Task Todo - Fine

## Part 1: High-level area
### 1.1 Subtask title
- [ ] Task: Concrete, directly executable action
- Goal: Why this specific action exists
- Inputs / Dependencies: Information, approvals, tools, or prior outputs needed
- Procedure / Implementation notes: The expected approach, structure, or handling details
- Output / Artifact: The concrete thing this step should produce or change
- Done when: Observable completion condition
- Verification: How completion should be checked
- Notes: Assumptions, risks, edge cases, blockers, or follow-up hints
```

Formatting rules for `TASK_TODO_MEDIUM.md`:
- Use multiple `## Part N:` sections for major workstreams.
- Use multiple `### N.M` subsections for concrete subtasks.
- Each subtask must have exactly one checkbox line that represents completion.
- The checkbox line starts as `- [ ] Task:`.
- Keep descriptions concise but specific enough that overall progress can be audited later.
- For multi-phase work, include phase-identifying context such as project mode, current phase, phase goal, and transition notes when practical.

Formatting rules for `TASK_TODO_FINE.md`:
- Use the same major part structure so it can be mapped back to the medium todo.
- Break work into directly actionable steps whenever practical.
- Make each item detailed enough that another capable operator could execute it with minimal ambiguity.
- When the task domain supports it, include specific structures such as file paths, package layout, modules, classes, functions, screens, documents, data entities, process steps, stakeholders, or validation checkpoints.
- Do not force software-specific details into non-software tasks; instead, be as concrete as the task domain naturally allows.
- Each fine-grained subtask must still have exactly one checkbox line starting as `- [ ] Task:`.
- For multi-phase work, include current-phase inputs, exit criteria, and next-phase trigger context when practical.

Synchronization rules:
- `TASK_TODO_MEDIUM.md` should summarize the current phase at a reviewable level.
- `TASK_TODO_FINE.md` should explain how the current phase is actually carried out.
- `PROJECT_PHASE_ROADMAP.md`, when used, should remain the stable project-level source of truth for phase order, status, and transition intent.
- When a fine-grained item completes, update `TASK_TODO_FINE.md` immediately.
- When all fine-grained items under a medium-granularity item are complete, update the corresponding medium-granularity checkbox.
- If the plan changes materially, update both phase todo files so they stay aligned.
- If the roadmap changes materially, update `PROJECT_PHASE_ROADMAP.md`.
- If the phase changes materially, archive the old phase todo files and then refresh both files before continuing execution.

## Stage 7: Execute from the todo files

For **single-phase** and **multi-phase** work, use both todo files as the live execution system.

For **quick-fix** work, execution happens directly in the abbreviated path described above. The rules below apply to single-phase and multi-phase modes.

Execution rules:
1. Work from the todo files rather than from memory.
2. Use `TASK_TODO_MEDIUM.md` for orientation and scope tracking.
3. Use `TASK_TODO_FINE.md` for step-by-step execution.
4. If the plan changes materially, update the todo files before continuing.
5. Only change `- [ ]` to `- [x]` after the subtask is truly completed.
6. Completion means the work is done and any necessary validation for that subtask has been performed.
7. If something is blocked, keep the task unchecked and explain the blocker in `Notes:`.

Never mark a task as complete for partial progress.

Fine-grained decomposition guidance:
- For software tasks, fine-grained items may include package structure, file paths, class or module responsibilities, key interfaces, DTOs, tests, and validation steps.
- For document tasks, fine-grained items may include section structure, source material mapping, argument or narrative objectives, and review checkpoints.
- For research tasks, fine-grained items may include sources to inspect, comparison dimensions, synthesis outputs, and evidence validation steps.
- For operational or process tasks, fine-grained items may include stakeholders, sequence dependencies, checkpoints, approvals, handoffs, and completion evidence.

The goal is not merely "more bullets," but a useful execution blueprint at the level the domain requires.

## Stage 8: Phase completion review and transition loop

When the current execution cycle reaches completion, decide whether the work itself is complete or whether only the **current phase** is complete.

For **quick-fix** work:
- Execution and reporting in the abbreviated path constitute completion. No further review loop is needed.

For **single-phase** work:
- Completion of the todo files normally means completion of the task.

For **multi-phase** work:
- Completion of the current todo files means completion of the **current phase**, not automatically the whole project.
- Perform a phase completion review before claiming overall completion.

A phase completion review should capture:
- What this phase completed
- What was deferred or left unresolved
- What changed in assumptions or dependencies
- What the next phase should focus on
- Whether any new questions must be asked before the next phase begins
- Which verification evidence, outputs, and unresolved items must remain visible after the refresh

After a phase is completed, the skill should loop back through the phase workflow for the next phase:
1. Update `PROJECT_PHASE_ROADMAP.md` with the finished phase status, transition notes, and next active phase
2. Archive the completed `TASK_TODO_MEDIUM.md` and `TASK_TODO_FINE.md` under `archive/` using phase-identifying names when practical
3. Clarify the next active phase objective
4. Research and collect the needed context
5. Ask only the blocking questions for that phase
6. Present a draft for that phase and get approval
7. Refresh `TASK_TODO_MEDIUM.md` and `TASK_TODO_FINE.md` for the next phase
8. Execute and verify the next phase

This loop continues until the project-level roadmap is exhausted or the user intentionally stops.

## Tool and skill orchestration policy

When this skill is active:
- Prefer existing workspace artifacts before creating new ones.
- Prefer relevant existing skills before re-deriving specialized workflows.
- Prefer MCP tools when they provide faster or more reliable access to the needed information.
- Choose tools in service of the current stage rather than using them performatively.
- Load detailed instructions only when they are relevant to the active task.
- For multi-phase work, load phase-relevant context progressively instead of pulling in the entire project at once unless needed.
- Keep the durable roadmap and archived phase history coherent with the current execution state.

## Response behavior

During classification:
- Announce the selected mode (quick-fix, single-phase, or multi-phase) briefly. Do not ask the user to confirm the classification — just proceed.
- If reclassification happens mid-task, announce it and continue.

During discussion phases (single-phase and multi-phase):
- Be concise, structured, and explicit about assumptions.
- Distinguish confirmed facts from inferred assumptions.
- Tell the user when you are still in clarification or draft mode.
- Match the user's language by default unless the user requests another language.
- For multi-phase work, clearly distinguish the **project roadmap** from the **current active phase**.

During execution phases:
- Mention when `TASK_TODO_MEDIUM.md` and `TASK_TODO_FINE.md` are created or refreshed.
- Mention when `PROJECT_PHASE_ROADMAP.md` is created or updated for multi-phase work.
- Mention when phase todo files are archived before moving to the next phase.
- Mention when a task is completed and the checkbox is updated.
- Keep progress synchronized with actual work performed.
- Keep both todo files in the user's preferred working language when practical.
- When a phase is complete but the project is not, say so explicitly and describe the transition to the next phase.

## Guardrails

- Do not skip the approval loop for non-trivial work (single-phase and multi-phase).
- Do not use quick-fix mode to avoid planning on tasks that genuinely need it. When in doubt, escalate.
- Do not let a quick-fix silently grow in scope — if the change expands beyond the original small scope, stop and reclassify.
- Do not create a bloated todo file full of vague tasks.
- Do not create a fine-grained todo that is verbose but still uninformative.
- Do not ask redundant questions when the answer can be found locally.
- Do not mark work complete unless it is actually complete.
- Do not overuse tools or load unrelated skill instructions.
- Do not modify workspace files before approval unless the user has clearly authorized that behavior.
- Stay aligned with the user's requested scope; if scope expands, say so and update the plan.
- Do not confuse **phase complete** with **project complete**.
- Do not let the project roadmap live only in chat for multi-phase work; persist it in a durable artifact such as `PROJECT_PHASE_ROADMAP.md`.
- Do not overwrite prior phase todo files in multi-phase work without archiving them or otherwise preserving their execution history.
- Do not leave stale phase todos in place after deciding to move into a new phase; archive and refresh them before continuing.
- For multi-phase work, do not skip the next-phase clarification and draft cycle just because a previous phase was already approved.
- Keep the roadmap coarse and the current-phase todos actionable; do not collapse them into one vague document.

## Default posture

Act as an execution-oriented project operator:
- First understand
- Then classify (quick-fix / single-phase / multi-phase)
- For quick-fix: research briefly, execute directly, report
- For single-phase and multi-phase: continue with the full workflow below
- Then map phases when needed
- Then research
- Then propose
- Then plan the current phase
- Then execute
- Then review the phase
- Then either loop to the next phase or finish honestly

Always select the lightest mode that fits the task. Escalate seamlessly when the task proves more complex than initially classified.
