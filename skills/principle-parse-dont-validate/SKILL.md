---
name: principle-parse-dont-validate
description: "Apply when code receives data from outside the program: request bodies, config files, CLI args, API responses, env vars. Parse into a precise type instead of validating a loosely-typed one and passing it onward."
disable-model-invocation: true
---

# Parse, Don't Validate

Turn unstructured input into a precisely-typed value in one step, at the boundary, and let the type carry the guarantee from then on. Do not check a loose type (`any`, `dict`, `string`) and pass that same loose type onward hoping the check was enough.

**Why:** A validator that returns `true`/`false` (or throws) discards what it learned. Every later reader of the data has no way to know the check already happened, so either it re-checks (duplication) or it trusts blindly (the bug). A parser that returns a structured value or an error makes the guarantee visible in the type signature, so the compiler or type checker, not the reader's memory, enforces it everywhere downstream.

**Pattern:**
- Parse once, at the boundary where uncontrolled data enters (the HTTP handler, config loader, CLI arg parser, DB row mapper), using the ecosystem's parsing library instead of hand-rolled checks: Zod or `io-ts` in TypeScript, Pydantic or `attrs`/`cattrs` in Python, `serde` in Rust, Jackson/`kotlinx.serialization` on the JVM/Kotlin. Everything past that point works with the typed value and never sees the raw input.
- Make illegal states unrepresentable rather than checked. A `NonEmptyList`, a branded `UserId`, a sum type/discriminated union for mutually exclusive fields — encode the invariant in the shape of the type, not in a runtime `if`.
- Return the parsed value or a typed error (`Result`, `Either`, an exception carrying the validation detail) — never a bare boolean. The caller must be unable to reach the data without going through the success path.
- Do not re-validate a value whose type already proves the property. If a function takes a `PositiveInt`, it does not need to check `> 0` again.
- Resist passing raw `any`/`dict`/`JSON` deeper into the call stack "to validate later" — that defers the guarantee past the point where it's cheap to enforce.
