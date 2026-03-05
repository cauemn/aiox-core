# AIOX Agent Command Pocket Guide

> **EN** | [PT](../pt/guides/agent-commands-cheat-sheet.md) | [ES](../es/guides/agent-commands-cheat-sheet.md)

Practical quick-reference: which agent to activate and which command to run.

## 30-second use

1. Activate an agent: `@dev`, `@qa`, `@po`, etc.
2. Run `*help` to list agent commands.
3. Execute the task command.
4. Switch agents when stage changes.
5. End with `*exit`.

```text
@dev
*develop
```

## Important rules

- `@devops` is the authority for `*push`, `*create-pr`, and `*release`.
- Standard flow: story first (`@sm` / `@po`), implementation (`@dev`), validation (`@qa`), delivery (`@devops`).
- If in doubt, run `*help`.

## One-screen matrix: objective -> agent -> command

| Objective | Agent | Start command | Closing command |
| --- | --- | --- | --- |
| Shape idea | `@analyst` | `*create-project-brief` | handoff to `@pm` |
| Define product | `@pm` | `*create-prd` | `*create-epic` |
| Define architecture | `@architect` | `*create-full-stack-architecture` | `*create-plan` |
| Draft story | `@sm` | `*draft` | handoff to `@po` |
| Validate story | `@po` | `*validate-story-draft` | handoff to `@dev` |
| Implement | `@dev` | `*develop` | `*run-tests` |
| Validate quality | `@qa` | `*review` | `*gate` |
| Deliver | `@devops` | `*pre-push` | `*push` + `*create-pr` |
| Close cycle | `@po` | `*close-story` | backlog updated |

## Flow 1: Idea to deploy (end-to-end)

```text
@analyst
*create-project-brief

@pm
*create-prd
*create-epic

@architect
*create-full-stack-architecture

@sm
*draft

@po
*validate-story-draft

@dev
*develop
*run-tests

@qa
*review
*gate

@devops
*pre-push
*push
*create-pr
```

After merge:

```text
@devops
*release

@po
*close-story
```

## Flow 2: Simple implementation (story already ready)

```text
@dev
*develop
*run-tests

@qa
*review

@devops
*pre-push
*push
*create-pr
```

## Flow 3: Bug fix

```text
@qa
*review
*create-fix-request

@dev
*fix-qa-issues
*run-tests

@qa
*review
*gate

@devops
*pre-push
*push
*create-pr
```

Quick shortcut:

```text
@dev
*apply-qa-fixes
```

## Flow 4: New feature with database changes

```text
@architect
*assess-complexity
*create-plan

@data-engineer
*snapshot pre-feature
*dry-run path/to/migration.sql
*apply-migration path/to/migration.sql
*security-audit schema

@dev
*develop
*run-tests

@qa
*validate-migrations
*security-check
*review

@devops
*pre-push
*push
*create-pr
```

## Flow 5: New UI/design-system feature

```text
@ux-design-expert
*research
*wireframe high
*create-front-end-spec

@dev
*develop

@qa
*review

@devops
*pre-push
*create-pr
```

## Incident mode: production hotfix

```text
@qa
*risk-profile
*review

@dev
*develop
*run-tests

@qa
*gate

@devops
*pre-push
*push
*create-pr
```

If immediate release is required:

```text
@devops
*release
```

## Activation shortcuts

- `@aiox-master`
- `@analyst`
- `@architect`
- `@data-engineer`
- `@dev`
- `@devops`
- `@pm`
- `@po`
- `@qa`
- `@sm`
- `@squad-creator`
- `@ux-design-expert`

## Full reference

Use `*help` inside the active agent and read `.aiox-core/development/agents/*.md`.