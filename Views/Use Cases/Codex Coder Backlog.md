# Codex Coder Backlog

This backlog translates the current use cases into implementation-oriented epics for Codex Coder.

The aim is to give Spider a build order that produces usable slices early while still supporting the broader vision. The recommended sequence is:

1. Build the cross-cutting platform capabilities once.
2. Deliver `PR Review Project` as the first strong vertical slice.
3. Reuse that foundation for `Existing Development Project`.
4. Add `Project Promotion` and `Assistant` once the shared eventing, permissions, memory, and adapter patterns are stable.

## Cross-Cutting Foundation

These epics are shared by most or all use cases and should be treated as platform work rather than duplicated per scenario.

### F1. Project and workspace model

Spider needs a durable concept of a project, its repositories or devices, working directories, goals, policies, and active tasks.

Deliverables:

- project definition format
- workspace layout rules
- per-project state and status files
- attachment of multiple use cases to one project

### F2. Capability mounting and discovery

Spider needs to discover what venoms or mounted capabilities are available and whether they are usable for the current project.

Deliverables:

- capability registry or manifest
- capability health/state detection
- required vs optional capability checks during setup
- human-readable missing capability reports

### F3. Eventing, timers, and interrupts

Most use cases are event-driven and need to wake on external changes without losing context.

Deliverables:

- timer/wait primitive
- interrupt or notification primitive
- resumable task state
- project-scoped event subscriptions

### F4. Memory and context files

Spider needs persistent operational memory that is inspectable and can be shared between brains.

Deliverables:

- compact task summaries
- recent activity history
- project preferences and policies
- handoff files between primary brain and sub-brains

### F5. Human approval and policy gates

Spider needs a standard way to stop before high-impact actions.

Deliverables:

- approval policy model
- action classification by risk
- "safe to auto-execute" vs "requires approval" checks
- audit trail of approvals and blocked actions

### F6. Observability and reporting

The user needs to know what Spider is doing without reading raw logs.

Deliverables:

- project activity feed
- task outcome summaries
- failure reporting format
- long-running status updates

## Use Case Priority

### P1. PR Review Project

This is the best first vertical slice because it has a tight scope, strong external signals, and clear definitions of success.

See [PR Review Implementation Spec.md](D:/Projects/Spider/SpiderDocs/Views/Use%20Cases/PR%20Review%20Implementation%20Spec.md) for the detailed execution model.

#### Epic PR1. Repository onboarding

- register repos to watch
- clone or refresh local checkouts
- install toolchains and dependencies
- run and record a baseline validation pass

#### Epic PR2. GitHub monitoring

- detect new pull requests
- detect new review comments and threads
- detect CI state changes
- map GitHub events back to the correct local workspace

#### Epic PR3. Review execution engine

- fetch PR metadata and changed files
- run repo-specific review commands
- produce structured review findings
- publish review comments and approvals to GitHub

#### Epic PR4. Comment and thread resolution loop

- classify comment intent
- decide whether a reply, code change, or escalation is required
- apply fixes on the branch when allowed
- rerun relevant validation and resolve threads when appropriate

#### Epic PR5. Merge readiness and merge action

- evaluate branch protection and required checks
- confirm unresolved thread state
- merge using repo policy
- report merge outcome

#### First usable slice

One repo can be onboarded, one PR can be fetched locally, review checks can be run, and Spider can post a useful review summary back to GitHub.

### P2. Existing Development Project

This should reuse most of the PR review machinery plus a planning and coding loop.

#### Epic DEV1. Vision ingestion and planning

- ingest a project vision or roadmap
- summarize current codebase state
- propose the next small implementation steps
- persist the chosen plan

#### Epic DEV2. Worktree and branch orchestration

- create isolated work areas for planned steps
- link each work area to a task
- keep branch and PR metadata attached to the task

#### Epic DEV3. Coding worker delegation

- prepare bounded implementation briefs
- start and supervise the coding worker
- capture questions and decisions during implementation
- collect changed files and rationale

#### Epic DEV4. Validation orchestration

- define targeted checks for the current step
- run broad regression validation before PR creation
- capture failures and decide whether to fix, retry, or narrow scope

#### Epic DEV5. PR lifecycle integration

- open the PR with a useful summary
- hand off to PR review flow when configured
- address follow-up comments
- merge and advance the plan

#### First usable slice

Given one repo and one small approved step, Spider can create a branch, supervise implementation, run validation, and open a reviewable PR.

### P3. Project Promotion

This can follow once posting permissions, memory, and reporting are stable.

#### Epic PROMO1. Project understanding and positioning

- read docs, repo metadata, and roadmap
- extract value proposition, audience, and honest limitations
- create reusable messaging briefs

#### Epic PROMO2. Channel and community mapping

- identify candidate communities
- capture channel rules and norms
- record which communities have been contacted already

#### Epic PROMO3. Content drafting and approval

- generate channel-specific drafts
- adapt tone and length per platform
- route high-visibility posts through approval

#### Epic PROMO4. Publishing and response tracking

- publish through approved accounts
- monitor reactions and replies
- classify feedback into actionable categories

#### Epic PROMO5. Feedback to product loop

- turn repeated questions into docs tasks
- turn bug reports into issues
- report which channels and messages are working

#### First usable slice

Spider can read one project repo, draft channel-specific launch copy, and present a reviewable outreach package plus a simple feedback capture plan.

### P4. Assistant

This is strategically important but depends on broader adapter, identity, and permission work than the other use cases.

#### Epic ASST1. User identity and preference model

- identify household users and allowed devices
- store room, device, and service preferences
- persist approval and privacy settings

#### Epic ASST2. Device and service adapters

- connect calendars, email, streaming services, TVs, speakers, and lights
- expose available actions consistently
- detect current state and availability

#### Epic ASST3. Intent routing and execution

- interpret multi-step household requests
- resolve target users, rooms, devices, and services
- execute actions with confirmation when confidence is low

#### Epic ASST4. Voice interaction

- accept voice input
- generate spoken output
- support follow-up commands with shared context

#### Epic ASST5. Safety, privacy, and action history

- enforce consent rules for personal accounts
- log device-changing and account-changing actions
- expose why Spider took a given action

#### First usable slice

Spider can answer by voice or text, read a connected calendar, and perform one controlled device action such as playing media on a chosen TV or changing lights in a named room.

## Recommended Build Sequence

1. Finish the shared project model, capability discovery, eventing, and approval framework.
2. Deliver PR review for a single GitHub repo with local checkout, validation, and review publishing.
3. Add comment resolution and merge automation.
4. Layer in development planning and coding-worker orchestration for existing projects.
5. Add promotion workflow with approval-gated publishing.
6. Expand into the home assistant once adapter and privacy infrastructure are strong enough.

## Definition of Ready For An Epic

Before Codex Coder starts an epic, the project should provide:

- the target repositories, devices, or accounts
- the success criteria for that epic
- the approval policy for high-impact actions
- the external systems and credentials available
- the first demo scenario that must work

## Definition of Done For A Vertical Slice

A slice should count as done when:

- Spider can perform the workflow end-to-end in a real project context
- state survives interruptions or waiting
- the user can see what happened and why
- guardrails are enforced, not just documented
- the slice is narrow enough to be reliable, not a half-built version of every future feature
