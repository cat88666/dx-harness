# Ingest Standards

## Source Classes

| Class | Typical Inputs | Primary Outputs | Secondary Outputs |
| --- | --- | --- | --- |
| `project` | plans, tickets, meeting notes, milestones, scope docs | `wiki/entities/项目-<name>.md` or the nearest stable object page | `wiki/summaries/主题-<name>.md`, `wiki/changes/变更-<name>.md` |
| `product` | PRDs, feature briefs, UX flows, product decisions | `wiki/entities/产品-<name>.md` | `wiki/summaries/主题-<name>.md`, `wiki/synthesis/对比-<name>.md` |
| `codebase` | repository tree, README, `pom.xml`, configs, source code | `raw/repos/<repo>/` snapshots first, then `wiki/entities/仓库-<repo>.md` in a later pass | `wiki/entities/模块-<module>.md`, `wiki/entities/服务-<service>.md`, `wiki/entities/任务-<task>.md`, `wiki/runbooks/Runbook-<symptom>排查.md` |

## Required Fields

### Project page

- goal
- scope
- owners
- milestones
- risks
- current state

### Product page

- problem statement
- target users
- constraints
- decision points
- related features

### Codebase page

- repository path
- startup entry
- package tree
- dependency stack
- key protocols
- high-value entry points

## Raw Snapshot Naming

For `codebase`, keep raw snapshots under `raw/repos/<repo>/` with date-stamped names such as:

- `YYYY-MM-DD-readme.md`
- `YYYY-MM-DD-pom-snapshot.md`
- `YYYY-MM-DD-package-tree.md`
- `YYYY-MM-DD-entrypoints.md`
- `YYYY-MM-DD-config-snapshot.md`
- `YYYY-MM-DD-doc-<topic>.md`
- `YYYY-MM-DD-git-heatmap.md`
- `YYYY-MM-DD-external-deps.md`
- `YYYY-MM-DD-structure-judgment.md`

## Accept/Reject Rules

- Accept only stable facts that help locate, explain, or operate the source.
- Reject transient chat, duplicated notes, and speculative conclusions.
- If a detail cannot be sourced, leave it out.
- Every page must be reachable from `index.md`.
- Raw files must not contain wiki-level judgments; they may contain evidence and lightweight observations only.
