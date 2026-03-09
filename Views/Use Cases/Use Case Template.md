# Use Case Template

Use this template when writing a use case intended for Codex Coder or another implementation-focused agent.

The goal is to describe a real operable scenario, not just an idea. A good use case should make it clear what Spider is trying to do, what capabilities it needs, what decisions require human approval, and what success looks like.

## Writing Rules

- Write from the perspective of a deliverable system behavior.
- Prefer concrete workflows over abstract aspirations.
- Name the actors involved so responsibilities are visible.
- Separate required capabilities from optional enhancements.
- Include guardrails so unsafe automation is not mistaken for desired behavior.
- Define success in a way that can later become tests, demos, or acceptance criteria.

## Suggested Structure

```md
# <Use Case Name>

One paragraph describing what Spider is doing in this scenario and why it matters.

## Goal

- The main outcomes this use case should achieve

## Inputs

- Repositories, devices, accounts, goals, policies, or other context Spider needs before it can act

## Primary Actors

- User
- Spider primary brain
- Relevant sub-brains, services, or adapters

## Example Workflow

### Setup

1. Initial setup or onboarding steps

### Execution

1. The normal operating flow

### Exceptions or follow-up

1. How Spider handles failures, ambiguity, or later events

## Required Venoms / Capabilities

### <Capability name>

What this capability must allow Spider to do.

## Optional Capabilities

### <Capability name>

Useful but not required for the first usable version.

## Guardrails

- Safety limits
- Approval boundaries
- Scope limits

## Success Criteria

- Observable outcomes that show the use case is working

## Open Questions

- Unknowns that still need product or technical decisions
```

## Section Guidance

### Goal

State the outcome in user or project terms. Avoid writing only about internal mechanics.

### Inputs

List the minimum context Spider must be given or discover. This is the fastest way to reveal hidden dependencies.

### Primary Actors

Use this section to show how responsibility is split. If multiple Spider brains or external systems participate, name them.

### Example Workflow

Make the workflow operational. A reader should be able to imagine implementing each step.

Good workflow steps:

- detect a new PR
- fetch the branch
- run baseline checks
- write review comments

Weak workflow steps:

- be smart about code
- help the user
- improve quality

### Required Venoms / Capabilities

Describe capabilities in terms of what the system must do, not how the code will necessarily be organized.

### Guardrails

This section is mandatory for any use case that can change code, publish externally, touch personal data, or trigger real-world devices.

### Success Criteria

These should later map to acceptance tests, manual demos, or milestone checks.

## Hand-off To Codex Coder

When a use case is ready for implementation, Codex Coder should be able to extract:

- the actors and boundaries
- the main event flow
- the external systems involved
- the required capabilities
- the safety and approval rules
- the first thin slice that would count as usable

If any of those are missing, the use case is still too vague.
