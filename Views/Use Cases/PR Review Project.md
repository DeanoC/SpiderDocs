# PR Review Project

This use case defines Spider as an always-on pull request reviewer for one or more GitHub repositories.

The objective is to monitor incoming pull requests, review them with project-specific standards, handle follow-up discussion, apply fixes when appropriate, and merge once the branch is truly ready.

Implementation detail and milestones are captured in [[PR Review Implementation Spec]].

## Goal

Provide a Spider Monkey that can:

- watch selected repositories for new pull requests and review activity
- prepare each repository so reviews are grounded in a working local checkout
- produce useful review feedback instead of shallow summaries
- implement straightforward fixes in response to review threads or failing checks
- merge ready pull requests without human babysitting when policy allows

## Inputs

Spider needs:

- the repositories to monitor
- the default branch and merge policy for each repo
- review standards, coding standards, and any repo-specific rules
- setup steps needed to build and test the repository locally

## Example Workflow

### Initial setup

1. User tells Spider which GitHub repositories belong to the project.
2. Spider clones each repository at the default branch into the workspace.
3. Spider installs the required dependencies and toolchain.
4. Spider runs a baseline build and test pass so future failures can be attributed to the PR rather than a broken local environment.
5. Spider starts monitoring for new pull requests and new review activity. Existing open PRs can be treated as new on first import.

### When a new pull request appears

1. Spider reads the PR description, linked issues, changed files, and current CI state.
2. Spider fetches and checks out the PR branch locally.
3. Spider runs targeted review checks such as tests, linting, static analysis, and any repo-specific review scripts.
4. Spider performs a code review focused on correctness, regressions, security, maintainability, and missing validation.
5. Spider publishes review feedback to GitHub in the appropriate form: approval, request changes, or line comments.

### When a new review thread or comment appears

1. Spider classifies the comment as informational, a question, or an actionable change request.
2. If code changes are required, Spider creates or updates a local branch, applies the fix, reruns the relevant checks, and pushes the update.
3. Spider replies in the thread with the outcome or asks for clarification if the request is ambiguous.
4. Spider resolves the thread when the underlying issue is actually addressed.
5. Spider performs another pass over the PR to ensure the new change did not create follow-on problems.

### When CI fails

1. Spider inspects the failing check output and identifies whether the issue is environmental, flaky, or caused by the branch.
2. If the failure is actionable and within scope, Spider applies a fix and reruns the relevant validation.
3. If the failure is external or blocked, Spider reports the issue clearly instead of guessing.

### When the PR is ready

1. Spider verifies that required reviews are satisfied, CI is green, and no unresolved threads remain.
2. Spider checks branch protection and merge policy.
3. Spider merges the PR into the default branch when allowed, then reports the result.

## Required Venoms / Capabilities

### Timers

Wait for new PRs, CI completion, and external responses without losing task state.

### Interrupts and notifications

Wake the Spider Monkey when GitHub events occur and surface important changes even if it is waiting on something else.

### GitHub access

Read pull requests, review threads, comments, commit statuses, and branch protection rules, then write reviews and replies back.

### Git access

Clone repositories, fetch branches, create commits, push fixes, and merge according to policy.

### Terminal execution

Run project setup, tests, linting, build steps, and any review-specific tooling.

### AI coding worker integration

Optionally delegate bounded coding tasks needed to address review comments or CI failures.

### Package and tool installer

Install compilers, SDKs, and CLI tools needed to review the repository correctly.

## Guardrails

- Do not merge if required reviews, required checks, or branch protections are not satisfied.
- Do not resolve review threads unless the underlying issue has actually been addressed.
- Prefer specific actionable feedback over generic praise or noise.
- Escalate ambiguous product decisions and large design disputes instead of forcing a code change.
- Avoid self-reinforcing loops where Spider both authors major changes and silently approves them without an explicit policy allowing that.

## Success Criteria

- New PRs receive timely, technically useful review feedback.
- Review conversations progress toward resolution without human coordination for every step.
- Straightforward fixes and CI issues are handled automatically.
- Ready PRs merge cleanly while unsafe or unclear PRs remain blocked with an explicit reason.
