# Task Todo - Fine

> Use this file as the execution blueprint.
> It should be concrete enough that another capable operator could pick up the work with minimal ambiguity.

## Part 1: Requirement and scope
### 1.1 Capture the executable objective
- [ ] Task: Rewrite the approved request into a directly executable objective
- Goal: Remove ambiguity before execution begins
- Inputs / Dependencies: Approved draft, user constraints, prior context
- Procedure / Implementation notes: Separate confirmed requirements from assumptions; note domain-specific structure if relevant
- Output / Artifact: Executable objective statement
- Done when: Objective, boundaries, constraints, and success criteria are explicit
- Verification: Check that the task could be started without reinterpreting the request
- Notes: Record assumptions, open edge cases, and any ambiguity that remains acceptable

### 1.2 Enumerate dependencies and prerequisites
- [ ] Task: List the concrete inputs, approvals, tools, context, or prior outputs needed before execution
- Goal: Expose blockers before work starts
- Inputs / Dependencies: Workspace context, available tools, user direction
- Procedure / Implementation notes: Include the practical order of dependency resolution; use domain-specific detail when helpful
- Output / Artifact: Dependency and prerequisite list
- Done when: Execution prerequisites are explicit and usable
- Verification: Confirm that each major action in later parts has required inputs identified
- Notes: Include blockers, missing approvals, unavailable tools, or uncertain context

## Part 2: Research and decomposition
### 2.1 Inspect relevant context in detail
- [ ] Task: Identify the specific materials, components, sources, files, stakeholders, systems, or references that directly affect execution
- Goal: Ground the work in concrete context
- Inputs / Dependencies: Workspace files, tools, external references, approved draft
- Procedure / Implementation notes: Name the exact context units that matter; for software tasks, this may include file paths, modules, packages, classes, APIs, schemas, or tests
- Output / Artifact: Detailed context map
- Done when: The execution-relevant context has been identified at an actionable level
- Verification: Check that later tasks can reference this context without needing another broad discovery pass
- Notes: Distinguish mandatory context from optional context

### 2.2 Break the work into executable units
- [ ] Task: Split the approved plan into concrete steps that can be performed, checked, and updated individually
- Goal: Create a reliable execution blueprint
- Inputs / Dependencies: Approved plan, context map, constraints
- Procedure / Implementation notes: Prefer actions that are domain-specific and auditable; for software, include concrete file or module work; for research, include source review and synthesis steps; for documents, include section and revision steps
- Output / Artifact: Executable step breakdown
- Done when: Each major workstream has actionable child steps with clear completion criteria
- Verification: Check that another capable operator could begin from the list with minimal ambiguity
- Notes: Avoid vague items like “finish everything” or “do implementation”

## Part 3: Execution
### 3.1 Complete the first executable slice
- [ ] Task: Perform the first concrete execution slice from the approved breakdown
- Goal: Convert planning into real progress with traceable outputs
- Inputs / Dependencies: Required context, tools, approvals, and prior outputs
- Procedure / Implementation notes: Document the expected structure of the work; for software this may include package layout, files to add or change, class responsibilities, interfaces, tests, or validation steps; for non-software, adapt to the natural unit of work
- Output / Artifact: The first completed execution slice
- Done when: The slice is completed and any required validation is performed
- Verification: Run or record the domain-appropriate validation for this slice
- Notes: Capture implementation choices, blockers, or follow-up work

### 3.2 Complete remaining executable slices
- [ ] Task: Perform the remaining execution slices in the approved order or revised order
- Goal: Complete the requested work without losing traceability
- Inputs / Dependencies: Outputs from prior slices, updated context, active blockers
- Procedure / Implementation notes: Keep the order explicit; update details as the plan evolves; preserve a clear mapping back to the medium-granularity todo
- Output / Artifact: Completed work across the remaining slices
- Done when: Remaining slices are completed or explicitly deferred with reason
- Verification: Confirm that each completed slice has corresponding evidence or validation
- Notes: Record scope changes, tradeoffs, deferrals, and new follow-up items

## Part 4: Verification and completion
### 4.1 Verify completed outputs
- [ ] Task: Run or document the checks needed to confirm that completed work actually satisfies the intended result
- Goal: Prevent premature completion marking
- Inputs / Dependencies: Completed outputs, validation tools, review criteria
- Procedure / Implementation notes: Use domain-appropriate checks such as tests, reviews, inspections, comparisons, sign-offs, or acceptance checks
- Output / Artifact: Verification record
- Done when: There is sufficient evidence to support completion claims
- Verification: Confirm that each completed task has supporting validation
- Notes: Keep unchecked when evidence is partial, blocked, or missing

### 4.2 Reconcile and report completion
- [ ] Task: Update fine-grained status, reconcile the medium-granularity plan, and summarize final outcomes
- Goal: Leave a complete and honest execution trail
- Inputs / Dependencies: Final outputs, verification record, current todo state
- Procedure / Implementation notes: Mark medium items complete only when the corresponding fine-grained work is complete; summarize deferred or incomplete items explicitly
- Output / Artifact: Final synchronized todo state and outcome summary
- Done when: Fine and medium todos are aligned and the final summary is ready
- Verification: Check that status across both todo files is consistent
- Notes: Record known limitations, deferred items, and recommended next steps
