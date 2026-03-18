# Task Todo - Fine

> Use this file as the detailed execution blueprint for the **current active phase**.
> For single-phase work, this file may represent the whole task.
> For multi-phase work, refresh this file when a new phase becomes active, but archive the finished phase first.

## Project / Phase Context
- Roadmap File / Reference: `PROJECT_PHASE_ROADMAP.md` for multi-phase work
- Previous Phase Archive Reference: Optional path to archived prior-phase medium/fine todos
- Project Mode: Single-phase / Multi-phase
- Project Modules: List the major modules or domains when relevant
- Phase Roadmap Summary: Briefly describe the overall sequence if this is multi-phase work
- Current Phase: Name the active phase, or mark it as the whole task if single-phase
- Current Phase Inputs: The specific inputs already available to this phase
- Phase Goal: The main objective of the active phase
- Phase Scope: What is included and excluded in this phase
- Phase Deliverables: Concrete outputs expected from this phase
- Entry Criteria: What must already be true before this phase starts
- Phase Exit Criteria: What must be true before this phase is marked complete
- Next Phase Trigger / Transition Notes: What should happen after this phase is completed
- Previous Phase Summary: Required brief handoff summary when this file is refreshed for a new phase

## Part 1: Current phase requirement and scope
### 1.1 Capture the executable objective for this phase
- [ ] Task: Rewrite the approved current-phase request into a directly executable objective
- Goal: Remove ambiguity before the active phase begins
- Inputs / Dependencies: Approved phase draft, user constraints, prior context, roadmap when applicable
- Procedure / Implementation notes: Separate confirmed requirements from assumptions; note domain-specific structure if relevant
- Output / Artifact: Executable current-phase objective statement
- Done when: Objective, boundaries, constraints, and success criteria are explicit for the active phase
- Verification: Check that the phase could be started without reinterpreting the request
- Notes: Record assumptions, open edge cases, and any ambiguity that remains acceptable

### 1.2 Enumerate current-phase dependencies and prerequisites
- [ ] Task: List the concrete inputs, approvals, tools, context, or prior outputs needed before execution of this phase
- Goal: Expose blockers before the active phase starts
- Inputs / Dependencies: Workspace context, available tools, user direction, prior phase outputs
- Procedure / Implementation notes: Include the practical order of dependency resolution; use domain-specific detail when helpful
- Output / Artifact: Current-phase dependency and prerequisite list
- Done when: Execution prerequisites for this phase are explicit and usable
- Verification: Confirm that each major action later in this file has its required inputs identified
- Notes: Include blockers, missing approvals, unavailable tools, or uncertain context

## Part 2: Current phase research and decomposition
### 2.1 Inspect relevant context in detail for this phase
- [ ] Task: Identify the specific materials, components, sources, files, stakeholders, systems, or references that directly affect current-phase execution
- Goal: Ground the work in concrete phase-relevant context
- Inputs / Dependencies: Workspace files, tools, external references, approved draft, roadmap when applicable
- Procedure / Implementation notes: Name the exact context units that matter; for software tasks, this may include file paths, modules, packages, classes, APIs, schemas, or tests
- Output / Artifact: Detailed current-phase context map
- Done when: The execution-relevant context for this phase has been identified at an actionable level
- Verification: Check that later tasks can reference this context without another broad discovery pass
- Notes: Distinguish mandatory context from optional context

### 2.2 Break the current phase into executable units
- [ ] Task: Split the approved current-phase plan into concrete steps that can be performed, checked, and updated individually
- Goal: Create a reliable execution blueprint for the active phase
- Inputs / Dependencies: Approved phase plan, context map, constraints
- Procedure / Implementation notes: Prefer actions that are domain-specific and auditable; for software, include concrete file or module work; for research, include source review and synthesis steps; for documents, include section and revision steps
- Output / Artifact: Executable current-phase step breakdown
- Done when: Each major workstream in this phase has actionable child steps with clear completion criteria
- Verification: Check that another capable operator could begin from the list with minimal ambiguity
- Notes: Avoid vague items like “finish everything” or “do implementation”

## Part 3: Current phase execution
### 3.1 Complete the first executable slice of this phase
- [ ] Task: Perform the first concrete execution slice from the approved current-phase breakdown
- Goal: Convert current-phase planning into real progress with traceable outputs
- Inputs / Dependencies: Required context, tools, approvals, and prior outputs
- Procedure / Implementation notes: Document the expected structure of the work; for software this may include package layout, files to add or change, class responsibilities, interfaces, tests, or validation steps; for non-software, adapt to the natural unit of work
- Output / Artifact: The first completed execution slice of the phase
- Done when: The slice is completed and any required validation is performed
- Verification: Run or record the domain-appropriate validation for this slice
- Notes: Capture implementation choices, blockers, or follow-up work

### 3.2 Complete remaining executable slices of this phase
- [ ] Task: Perform the remaining execution slices in the approved order or revised order for the active phase
- Goal: Complete the phase without losing traceability
- Inputs / Dependencies: Outputs from prior slices, updated context, active blockers
- Procedure / Implementation notes: Keep the order explicit; update details as the plan evolves; preserve a clear mapping back to the medium-granularity todo
- Output / Artifact: Completed work across the remaining slices of this phase
- Done when: Remaining slices are completed or explicitly deferred with reason
- Verification: Confirm that each completed slice has corresponding evidence or validation
- Notes: Record scope changes, tradeoffs, deferrals, and new follow-up items

## Part 4: Verification and transition
### 4.1 Verify completed outputs for this phase
- [ ] Task: Run or document the checks needed to confirm that completed work actually satisfies the intended result of the active phase
- Goal: Prevent premature completion marking
- Inputs / Dependencies: Completed outputs, validation tools, review criteria
- Procedure / Implementation notes: Use domain-appropriate checks such as tests, reviews, inspections, comparisons, sign-offs, or acceptance checks
- Output / Artifact: Current-phase verification record
- Done when: There is sufficient evidence to support completion claims for the active phase
- Verification: Confirm that each completed task has supporting validation
- Notes: Keep unchecked when evidence is partial, blocked, or missing

### 4.2 Reconcile phase completion and prepare the next step
- [ ] Task: Update fine-grained status, reconcile the medium-granularity plan, document the phase handoff, record archive references, and determine whether to refresh for the next phase or finish the project
- Goal: Leave a complete and honest execution trail for the active phase
- Inputs / Dependencies: Final outputs, verification record, current todo state, roadmap when applicable
- Procedure / Implementation notes: Mark medium items complete only when the corresponding fine-grained work is complete; summarize deferred or incomplete items explicitly; if another phase remains, capture the next-phase trigger before refreshing the todo files and archive the finished phase files first
- Output / Artifact: Final synchronized todo state, archive references, and phase transition decision
- Done when: Fine and medium todos are aligned and the next-step decision is explicit
- Verification: Check that status across both todo files is consistent and the transition path is understandable
- Notes: Record known limitations, deferred items, and recommended next steps
