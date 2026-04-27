---
name: ingest-source
description: Ingest project materials, product materials, and codebases into the Work Harness by classifying the source, extracting stable objects, and writing indexed wiki pages plus log entries.
---

# Ingest Source

Use this skill when the user wants to ingest one or more sources into the Work Harness, especially:

- project materials: plans, tickets, meeting notes, milestones, scope docs
- product materials: PRDs, feature briefs, UX flows, product decisions
- codebases: repository trees, README, `pom.xml`, configs, source code, run paths

## Standard

Read [standards.md](references/standards.md) first. It defines the source classes, target page types, and required fields.

## Workflow

1. Classify the source as `project`, `product`, or `codebase`.
2. Identify the stable object names that should be indexed.
3. Extract only durable facts. Drop transient chatter.
4. Write or update the minimal set of wiki pages.
5. Update `index.md` so the object is directly locatable.
6. Append `log.md` with the ingest result.

## Guardrails

1. If the user instruction, scope, file count, or boundary conflicts with earlier instructions or the skill standard, stop and ask for confirmation before proceeding.
2. Decide the source class before producing any artifacts.
3. For `codebase`, produce raw snapshots first; do not write `wiki/` in the same first pass.
4. Raw snapshots must record facts only; do not write wiki-level judgments into `raw/`.
5. For `codebase`, create dedicated structure, heatmap, and dependency snapshots when those facts are available.
6. Keep stage boundaries explicit in `log.md`: `raw` ingest and `wiki` ingest are separate events.

## Rules

- Treat `raw/` as read-only.
- Prefer updating existing pages over creating new ones.
- Every new page must use a type prefix.
- Every conclusion must point back to source evidence.
- Do not write rules or prompts into `wiki/`.

## Output by class

- `project`: capture scope, owners, milestones, risks, and current state.
- `product`: capture problem statement, audience, constraints, and decision points.
- `codebase`: capture repository identity, structure, entry points, dependencies, and high-value runbooks.

If the source is mixed, choose the dominant class and split the rest into secondary pages only when it adds stable value.
