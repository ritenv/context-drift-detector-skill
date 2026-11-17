# Context Drift Detector

A portable Agent Skill for checking whether an AI agent's current plan, output, or code changes conflict with previously confirmed project decisions.

## What it does
- Read-only **audit mode** by default
- Optional **strict mode** requiring user confirmation before material deviations
- Evidence-backed findings and explicit uncertainty
- Optional persistent decision ledger for long-running projects

## Install
Use the folder containing `SKILL.md` as a skill in a compatible Agent Skills host. Import/upload the ZIP where supported, or copy the folder to the host's supported skills directory. Exact installation and automatic activation depend on the host and version.

## Example prompts
- "Use context-drift-detector to audit this implementation plan against our prior decisions."
- "Run a context drift audit on the current Git diff."
- "Enable strict mode for this task and flag any deviation from our agreed architecture before coding."
- "Create a proposed context ledger from the available project docs; ask me to confirm it."

## Limitations
The skill can only compare context available to the agent. For long-running work, maintain a version-controlled decision ledger. Strict mode is instruction-level unless the host supports enforcement hooks.

## Test cases
1. Explicit PostgreSQL commitment, silent MongoDB replacement => confirmed drift.
2. REST replaced by GraphQL after explicit user approval => authorized change.
3. Earlier conversation unavailable, no ledger => unknown, not confirmed drift.
4. Internal refactor preserving API/constraints => aligned.
5. Vague preference for fewer dependencies, one justified new dependency => potential drift at most.
