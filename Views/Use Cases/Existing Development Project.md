# Existing Development Project

This use case defines Spider as an autonomous development partner for one or more existing GitHub repositories.

The goal is to move a real software project forward from its current state toward a stated vision, with the user staying informed and approving major decisions while Spider handles the routine execution work.

## Goal

Allow one or more Spider Monkeys to:

- understand the current state of an existing codebase
- break a product vision into small implementation steps
- implement and test those steps
- open and iterate on pull requests
- continue progressing until the agreed scope is complete

## Inputs

Spider needs:

- the repository or repositories to work in
- the product vision, roadmap, or outcome being pursued
- coding standards, branch rules, and deployment constraints
- the available toolchain and test commands for each repo

## Primary Actors

- User: defines the vision, priorities, and approval boundaries
- Spider primary brain: keeps global context, reports progress, and escalates decisions
- Project Manager sub-brain: turns the vision into a prioritized sequence of small steps
- Code Manager sub-brain: supervises implementation work and coordinates an AI coding worker when appropriate
- Test sub-brain: prepares and runs validation for each step

## Example Workflow

### Bootstrap

1. User defines the project vision and identifies the target repositories.
2. Spider clones or updates the repositories, installs dependencies, and validates a clean baseline build and test run.
3. Spider summarizes the current state of the codebase, architecture, and open work.

### Planning

1. Project Manager proposes the next small batch of steps, ideally fewer than five and each independently reviewable.
2. Spider identifies dependencies, risks, and whether work should happen in a single repo or across multiple repos.
3. User approves or adjusts the proposed direction when the change is significant.

### Implementation loop

1. Spider creates the required branch or worktree for the selected step.
2. Code Manager prepares an implementation brief for the coding worker.
3. The coding worker makes changes while Code Manager answers questions and keeps the work aligned with the plan.
4. Test sub-brain runs targeted checks, then broader validation as the step stabilizes.
5. Spider fixes failures or narrows the scope if the step was too large.

### Integration

1. Spider opens a pull request with a clear summary of what changed and why.
2. If a PR review use case is attached, Spider waits for or coordinates that review flow.
3. Spider addresses review comments, updates the branch, and merges when policy allows.
4. Project Manager selects the next step and repeats until the planned outcome is complete.

## Required Venoms / Capabilities

### Git and GitHub

Clone, branch, diff, commit, push, open PRs, inspect reviews, and merge according to project policy.

### Terminal execution

Install dependencies, run builds, run tests, and execute project tooling in the correct environment.

### Filesystem and workspace management

Create worktrees, manage generated files, persist plans, and keep project context accessible to all participating agents.

### Timers and interrupts

Wait on long-running work while still responding to new events such as review comments, failed CI runs, or user requests.

### AI coding worker integration

Delegate bounded implementation tasks to a coding agent while preserving supervision and review.

### Package and tool installer

Install missing compilers, CLIs, SDKs, and related tooling when the environment is incomplete.

## Guardrails

- Start from a known-good baseline before making forward changes.
- Prefer small, reviewable steps over broad speculative rewrites.
- Do not merge to protected branches without satisfying the repository's review and CI rules.
- Escalate architectural changes, production-impacting decisions, and unclear product calls to the user.
- Keep the user informed of progress, blockers, and any manual test or deployment handoff.

## Success Criteria

- Spider can repeatedly move the repository closer to the stated vision without needing a fresh prompt for every task.
- Each completed step leaves the project in a testable, reviewable state.
- Work is visible through branches, pull requests, and progress summaries rather than hidden agent activity.
- Human attention is reserved for direction, approval, and edge cases instead of routine implementation.
