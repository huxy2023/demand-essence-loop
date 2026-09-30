# Impact and Evolution

Use this guide for changes that touch shared behavior, persisted data, workflows, integrations, permissions, or other expensive-to-reverse boundaries.

## Scale analysis to risk

### Low risk

For copy, documentation, isolated styling, or an internal rename, inspect the touched surface and verify it directly. Stop when the request is satisfied.

### Medium risk

For localized behavior or a limited-caller abstraction, identify the owner and invariant, inspect direct callers and tests, and verify the main path plus the most relevant edge or failure path.

### High risk

For authentication, authorization, money, personal data, public APIs, persistence, migrations, concurrency, retries, external side effects, or shared state machines, map entry points, ownership, failure modes, compatibility, rollout, and rollback. Static tests alone may not support a runtime claim.

## Impact map

Check only relevant dimensions:

- **User journey:** entry point, feedback, accessibility, cancellation, recovery, and repeated action.
- **Domain state:** valid transitions, derived versus stored state, reverse flows, and impossible combinations.
- **Contracts:** request and response semantics, error behavior, versioning, and downstream consumers.
- **Data:** source of truth, constraints, migration, backfill, deletion, retention, and stale records.
- **Identity and policy:** authentication, authorization, tenant boundaries, privacy, and auditability.
- **Concurrency:** idempotency, duplicate submission, ordering, races, locks, retries, and partial success.
- **Integrations:** timeouts, rate limits, cancellation, reconciliation, and ownership of side effects.
- **Operations:** diagnostics, rollout, rollback, monitoring, and support recovery.

## Decide where evolution matters

Future-proofing is valuable only where a credible future change meets a costly-to-reverse boundary.

### Prefer explicit current models

- Model known domain concepts directly.
- Use semantic identifiers and state names.
- Keep ownership clear and dependencies narrow.
- Prefer additive contract evolution when consumers cannot change together.

### Avoid speculative flexibility

Do not automatically add:

- generic `metadata` or “extra” fields;
- boolean flags whose meaning depends on context;
- unowned compatibility layers or silent fallbacks;
- configurable rule engines for one confirmed rule;
- reserved tables, columns, states, or endpoints with no present consumer;
- abstractions that combine concepts only because they look similar.

An extension field can be appropriate for genuinely open-ended, non-critical attributes, but it needs ownership, validation, privacy rules, lifecycle expectations, and a promotion path for data that becomes first-class. It is not a substitute for domain modeling.

## Reversibility test

For each consequential choice, ask:

1. If the assumption is wrong, can the change be removed without data repair or consumer coordination?
2. Does the choice narrow a public contract, persistent representation, or state machine?
3. Is compatibility required by a known consumer or merely imagined?
4. Does the proposed abstraction reduce coordinated future changes, or only hide uncertainty?
5. Can rollout or migration fail halfway, and what state remains?

Invest design effort in the least reversible decisions. Keep reversible implementation details simple.

## Verification prompts

Depending on risk, cover the happy path and relevant combinations of:

- empty, null, missing, malformed, and stale inputs;
- failure, timeout, retry, cancellation, and offline behavior;
- duplicate and concurrent actions;
- permission denial and tenant/user switching;
- restart, reload, migration, and rollback;
- downstream compatibility and observable diagnostics.

Report the environment and gaps when runtime validation is not feasible.
