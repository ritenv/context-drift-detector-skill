# Classification Guide

## Confirmed drift
- Earlier confirmed: "Use PostgreSQL for the persistence layer." Current plan silently replaces it with MongoDB. No later authorization exists.
- Earlier confirmed: "The app must work offline." Current implementation requires a network request to open saved records.
- Earlier confirmed: "Do not store user-uploaded documents." Current code adds permanent object storage for them.

## Potential drift
- Earlier discussion favored REST but never finalized it; current plan proposes GraphQL. Ask whether REST was a firm decision.
- A project summary says "minimal dependencies," while a new package is added for a specialized function. Need necessity and meaning of 'minimal'.

## Authorized change
- Earlier decision chose REST; user later explicitly requests GraphQL. Record REST as superseded, not as a contradiction.
- A new security requirement requires changing a previously agreed implementation detail.

## Aligned
- Refactoring internal modules while preserving an agreed public API and constraints.
- Changing variable names or test organization with no impact on confirmed decisions.

## Unknown
- The earlier discussion is unavailable and there is no ledger. Do not assert what was previously agreed.

## Severity
- **High:** breaks core goal, user-facing requirement, security/privacy constraint, data integrity, or critical compatibility.
- **Medium:** changes confirmed architecture, interfaces, operating cost, or delivery commitments.
- **Low:** minor deviation from an explicit preference with limited impact.

## False-positive prevention
- A suggestion is not a decision.
- Silence is not approval.
- More recent explicit user direction supersedes older direction.
- Unavailable context is not evidence of drift.
- Distinguish a requirement change from a change in technique used to meet the requirement.
- Cite exact available evidence; do not invent file paths or quotes.
