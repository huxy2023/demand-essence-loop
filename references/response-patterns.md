# Response Patterns

Use structure only when it helps people make or review a decision. Do not force every response into every section.

## Concise recommendation

For a localized change:

```markdown
The underlying need is [outcome], while the proposed [implementation] is only one possible route.

Evidence: [current behavior or source of truth].

Recommendation: [smallest complete change]. This preserves [invariant].

Scope: include [items]; defer [adjacent items] because [reason].

Verification: [performed checks or required evidence].
```

## Decision memo

For cross-boundary or contested work:

```markdown
## Need and success condition
[Observed problem, affected actors, and observable outcome.]

## Current system and evidence
[Relevant capabilities, owner, source of truth, and actual gap.]

## Options and tradeoffs
- Option A: [benefit, cost, risk, reversibility]
- Option B: [benefit, cost, risk, reversibility]

## Recommendation and scope
[Chosen option, why it best meets the outcome, what is in and out.]

## Impact and evolution
[Only material UX, state, contract, data, security, operational, and compatibility effects.]

## Verification and open questions
[Evidence collected, tests/runtime checks, assumptions, gaps, and one focused decision if needed.]
```

## When the proposed solution is unsafe

Lead with the shared goal, then make the conflict concrete:

```markdown
The goal—[desired outcome]—is valid. Implementing it through [proposal] would violate [specific invariant] by [mechanism], creating [concrete consequence].

I recommend [alternative], which achieves the same outcome while keeping [invariant]. The narrow scope is [items], verified by [evidence].
```

Avoid dismissive language such as “the architecture does not support it” without explaining the ownership boundary, risk, and viable path.

## When no new capability is needed

Be explicit that the gap is in experience rather than capability:

```markdown
The system already supports [outcome] through [current path]. The observed problem is [discoverability, friction, feedback, or defect], so adding a second implementation would create competing sources of truth. Improve [specific interaction or guidance] instead.
```

## Completion language

Separate implementation and verification. When either is incomplete, name:

- what is complete;
- what remains;
- what has not been verified;
- why it is blocked or deferred;
- the next concrete action.

Do not use a confident completion claim when evidence covers only a narrow path.
