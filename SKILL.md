---
name: context-drift-detector
description: Detect and report contradictions between current agent plans, code changes, or answers and previously agreed requirements, constraints, decisions, and rejected approaches. Use for long-running projects, handoffs, and before major implementation changes. Default to read-only audit; strict mode requires confirmation for material deviations.
---

# Context Drift Detector

Identify **unintentional changes to established project intent**, not merely changes in implementation. Never claim to remember context that is not available.

## Modes

- **Audit (default):** inspect and report; do not edit project files or change plans.
- **Strict (opt-in):** before executing a material departure from a confirmed decision, explain the conflict and ask for explicit user approval. This is an instruction-level checkpoint, not a guaranteed platform-enforced block.

## Sources of truth (highest priority first)

1. Current explicit user instructions, including explicit revisions.
2. Confirmed project decisions and constraints in a maintained decision ledger.
3. Original requirements and acceptance criteria.
4. Prior conversation and repository artifacts that are actually available.
5. Agent assumptions, proposals, and inferred preferences (not binding).

A newer explicit user decision can supersede an older one. Do not flag authorized changes as drift. Never override higher-priority platform instructions.

## Workflow

1. **Establish baseline.** Read the relevant request, available conversation/project documents, and `context-ledger.md` if present. If none exists, construct a *provisional* baseline from available evidence. Do not fabricate missing history.
2. **Extract commitments.** Identify requirements, non-goals, constraints, accepted architectural decisions, rejected alternatives, and unresolved questions. Distinguish confirmed from inferred or proposed items.
3. **Inspect current direction.** Review the proposed plan, output, or Git diff. Compare material changes to the baseline; cite file paths, line ranges, diff hunks, or quotes when available.
4. **Classify findings:**
   - **Aligned:** consistent with the baseline.
   - **Authorized change:** explicit newer decision supersedes older intent.
   - **Potential drift:** plausible contradiction, but baseline or intent is ambiguous.
   - **Confirmed drift:** contradicts an explicit, still-active commitment.
   - **Unknown:** insufficient context to assess.
5. **Assess impact.** Explain what changes for users, architecture, security, cost, compatibility, or project goals. Prioritize consequential contradictions; ignore stylistic differences unless explicitly constrained.
6. **Recommend resolution.** Suggest the smallest correction, or ask one precise question if the conflict cannot be resolved from evidence. In strict mode, request approval before proceeding with confirmed material drift.
7. **Maintain ledger only when requested or explicitly authorized.** Propose entries and supersession links; do not silently rewrite decisions. Use `templates/context-ledger.md`.

## Output format

Keep reports concise, especially when there are no findings.

```markdown
## Context Drift Audit
Baseline: [sources and coverage]
Mode: Audit | Strict

### Findings
- [Confirmed drift | Potential drift | Authorized change | Unknown] [severity]
  - Earlier commitment: ... (source)
  - Current direction: ... (source)
  - Why it matters: ...
  - Recommendation: ...

### Verdict
Aligned | Drift detected | Insufficient context
### Next action
[One actionable step, if any]
```

Only label something **confirmed drift** with evidence of both a confirmed earlier commitment and a conflicting current action. If history is truncated, explicitly state the coverage gap. Do not equate scope expansion, refactoring, or different wording with context drift by itself.

For examples and edge cases, read `references/classification-guide.md`. For persistence, see `templates/context-ledger.md`.
