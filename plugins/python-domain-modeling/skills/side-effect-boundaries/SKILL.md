---
name: side-effect-boundaries
description: Use when Python domain decisions read clocks, randomness, environment or global state, mutate caller-owned values, or perform I/O, and when deciding where those effects belong.
---

# Side-Effect Boundaries

Keep domain decisions predictable: supply observed facts as inputs and make deliberate effects visible at the operation that owns them. A functional core and imperative shell can live inside one cohesive module; they do not require separate public layers or interfaces.

## Decide what crosses the boundary

- Read time, configuration, process state, and external data where the workflow owns them. Pass the **observed value** into a domain decision. Passing a mutable random generator makes the dependency visible but does not make the decision pure; pass a sampled value or seed when repeatability matters.
- Return a decision or new domain state when the caller should own the resulting mutation or I/O. Return an event or command only when it represents a real domain outcome or supports a required workflow.
- Keep intentional persistence, network calls, logging, and notifications in the operation responsible for them. Name effectful operations clearly; avoid surprising I/O in value constructors, getters, or imports.
- Preserve ownership contracts. Mutation of local scratch data is fine. Mutate caller-owned data only when the API explicitly promises it; a shallow copy does not isolate nested mutable values.
- Remove an unnecessary dependency before injecting it. Use a callback or `Protocol` when execution truly needs a capability. Keep decisions and their effects together when splitting them would obscure ordering or transaction guarantees.

```python
from datetime import datetime, timezone


def is_expired(deadline: datetime, *, now: datetime) -> bool:
    return now >= deadline


def report_if_expired(deadline: datetime) -> None:
    if is_expired(deadline, now=datetime.now(timezone.utc)):
        print("expired")
```

The workflow reads the clock and prints; the domain decision can be checked with a fixed `now`. If saving a transition and notifying must succeed together, design that delivery guarantee explicitly rather than splitting the calls merely to make the decision pure.

When a domain test needs clock freezing, global-state cleanup, or patches of external services, inspect the production boundary before adding test scaffolding. Test real effect ordering and failure behavior at the owning operation.
