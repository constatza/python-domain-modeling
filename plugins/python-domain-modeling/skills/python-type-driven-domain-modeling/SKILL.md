---
name: python-type-driven-domain-modeling
description: Encode Python domain invariants with unions, state-specific frozen dataclasses, semantic types, validated value objects, explicit transitions, exhaustive matching, and boundary-to-domain conversion. Use when designing or refactoring Python domain states, lifecycle APIs, validated values, result models, or boundary schemas; do not use for general Python style, tooling, tests, or documentation.
---

# Python Type-Driven Domain Modeling

Use Python's type system and runtime construction boundaries to make invalid
domain states difficult to represent. Read
[references/type-driven-domain-modeling.md](references/type-driven-domain-modeling.md)
before changing a domain model.

Apply the smallest pattern that prevents a plausible error:

- Use `A | B` variants when states are mutually exclusive or carry different data.
- Use separate `@dataclass(frozen=True, slots=True)` state types when operations
  are state-specific. Account for shallow immutability of mutable field values.
- Use `NewType` for zero-cost semantic distinctions without validation.
- Use an immutable value object when construction must validate an invariant.
- Use `Literal` or `StrEnum` for closed symbolic values only when variants do
  not require different data or operations.
- Handle closed unions with `match` and `typing.assert_never` when exhaustive
  checking matters.
- Validate untrusted input with the project's existing boundary mechanism,
  then convert it into domain types. Do not make framework schema models the
  domain by default.
- Keep `dict[str, Any]`, coupled flags and optionals, string statuses, and
  repeated invariant checks out of core domain logic when a stronger practical
  representation exists.
- Use explicit success/failure variants only for domain outcomes represented as
  data. Continue using exceptions for ordinary Python error transport.

Do not imitate stronger type systems mechanically. If the representation adds
ceremony without excluding a real invalid state, prefer the simpler Python
design.
