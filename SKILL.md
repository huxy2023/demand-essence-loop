---
name: demand-essence-loop
description: Analyze ambiguous feature requests, tester feedback, and proposed solutions to uncover the underlying need, inspect existing capabilities, assess system-wide impact, and recommend the smallest safe change. Use when a request may be an XY problem, spans multiple roles or system boundaries, or creates meaningful product, data, workflow, security, or compatibility tradeoffs. Do not use for straightforward, already-specified edits with no material design decision.
---

# Demand Essence Loop

Turn a proposed solution into an evidence-based change decision. Preserve the user's goal without treating their first implementation idea as the requirement.

## Core invariant

The delivered change must solve the underlying need, respect the system's source of truth and ownership boundaries, and avoid both speculative machinery and short-term choices that force unnecessary breaking changes later.

## Workflow

Use only the depth justified by the request's uncertainty and risk.

1. **Reconstruct the need**
   - Separate the observed problem, desired outcome, constraints, and proposed solution.
   - Identify affected actors and who bears the cost or risk of the change.
   - Ask a focused question only when repository evidence cannot resolve a decision that changes behavior, scope, data, security, or compatibility.
   - For detailed probing techniques, read [requirements discovery](references/requirements-discovery.md).

2. **Inspect the current system**
   - Locate the authoritative source of truth: code, schemas, contracts, tests, product requirements, logs, or observed runtime behavior.
   - Search for existing capabilities and the owning abstraction before proposing new concepts.
   - Distinguish a missing capability from discoverability, workflow friction, weak feedback, or an incorrect implementation.

3. **Map the impact**
   - Trace only relevant boundaries: user experience and accessibility, domain state, API contracts, data and migrations, permissions and privacy, concurrency and side effects, operations and observability.
   - Include reverse paths and failure paths when they matter, such as cancellation, retry, rollback, duplicate action, stale state, and partial success.
   - For a risk-scaled checklist, read [impact and evolution](references/impact-and-evolution.md).

4. **Choose the smallest complete solution**
   - Prefer reuse, clearer workflow, or a focused extension of the owning abstraction.
   - Make the smallest change that closes the real user journey and preserves relevant invariants.
   - State what is deliberately out of scope when adjacent ideas could blur the boundary.
   - Do not add generic engines, configuration layers, compatibility shims, extension fields, or fallback paths without present evidence.

5. **Preserve credible evolution paths**
   - Separate reversible decisions from expensive-to-reverse contracts, persisted data, identifiers, state transitions, and external side effects.
   - Preserve compatibility where a demonstrated evolution path requires it; otherwise keep the model explicit and narrow.
   - Prefer semantic names and additive contracts. Do not use speculative `metadata`, boolean flags, or reserved fields as automatic "future-proofing."

6. **Close the loop**
   - Match verification to the impact and completion claim.
   - Communicate the real need, evidence, recommendation, scope, tradeoffs, and verification or remaining uncertainty.
   - Adapt the response length to the decision. Use [response patterns](references/response-patterns.md) when a structured recommendation will help stakeholders align.

## Decision rules

- If the existing system already satisfies the need, improve guidance or discoverability instead of duplicating the capability.
- If the proposed solution violates an invariant, explain the conflict and recommend an alternative that achieves the goal.
- If the request is valid and localized, implement it directly without manufacturing a larger strategy exercise.
- If evidence is incomplete but the decision is reversible and low risk, state the assumption and proceed conservatively.
- If uncertainty affects security, money, permissions, irreversible data, public contracts, or acceptance criteria, stop and ask one focused question.
- Treat "not now" as a scope decision, not as a reason to design unused infrastructure.

## Guardrails

- Do not reject a request merely because the proposed implementation is imperfect.
- Do not universalize one project's architecture, tooling, domain language, thresholds, or release process.
- Do not invent existing capabilities, user research, constraints, or future requirements.
- Do not force a fixed report template onto simple work.
- Do not claim completion when implementation or risk-relevant verification is missing.

## Completion check

- The underlying outcome and affected actors are clear.
- The recommendation is grounded in repository or runtime evidence.
- Existing ownership and reusable capabilities were considered.
- Relevant happy, failure, reverse, and repeated-action paths were assessed.
- The chosen scope is complete but not speculative.
- Compatibility decisions are intentional and justified.
- Verification supports the claim, with gaps disclosed.
