# Requirements Discovery

Use this guide when a request arrives as a preferred implementation, when different actors have conflicting incentives, or when the actual constraint is unclear.

## Separate four things

Write down, mentally or explicitly:

1. **Observation** — What happened? Prefer a reproducible event, error, delay, or user behavior.
2. **Outcome** — What must become possible, safer, faster, or clearer?
3. **Constraints** — Which product, policy, time, data, device, accessibility, or compatibility limits are real?
4. **Proposal** — What implementation did the requester suggest?

The proposal is useful evidence, but it is not automatically the requirement.

## Reconstruct the operating context

Inspect the context that can change the design:

- actor, permissions, expertise, and frequency of use;
- device, network, environment, and accessibility needs;
- upstream inputs and downstream consumers;
- time pressure, handoffs, and recovery when the action fails;
- other actors who inherit cost, risk, or extra work.

Avoid theatrical detail. Only retain facts that affect the decision.

## Probe without interrogating

First use available evidence: code, product copy, schemas, tests, issue history, analytics, logs, and runtime behavior. If uncertainty remains, ask the smallest question that separates materially different solutions.

Useful prompts include:

- What is the user unable to complete today?
- What do they do immediately before and after the problem?
- How often does it occur, and what is the cost when it does?
- Is the requested result required, or is the proposed interaction required?
- Which source decides whether the action is valid?
- Who would be harmed if the action succeeds incorrectly?

Avoid repeatedly asking “why” when the answer is already observable or when it feels accusatory. Summarize the inferred need and invite correction.

## Detect common misdiagnoses

| Surface request | Possible underlying need | Evidence to inspect |
| --- | --- | --- |
| “Add a global override button” | The normal recovery path is too slow or unavailable | failure states, permissions, support workflow, audit requirements |
| “Export everything” | Users need a recurring summary or reconciliation view | filters, report consumers, dataset size, retention and privacy |
| “Make every label larger” | Critical information lacks hierarchy or contrast | task flow, viewport, accessibility checks, actual device |
| “Add a special mode” | A standard workflow lacks one legitimate variation | domain model, frequency, lifecycle, existing policy/configuration |
| “Add another status” | Two independent dimensions are being collapsed | state transitions, derived state, persistence and API contracts |

These are hypotheses, not canned answers.

## Define success before scope

A useful outcome statement names observable behavior and constraints without dictating implementation:

> An authorized operator can recover a failed submission without duplicating the external side effect, and the result remains auditable.

Then define what evidence would demonstrate success. This prevents both a symptom-only patch and an unnecessarily broad redesign.
