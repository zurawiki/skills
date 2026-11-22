---
name: principle-illegal-states-unrepresentable
description: "Apply when designing a type, struct, or set of fields, especially several booleans or independently-optional fields that only make sense in certain combinations. Replace them with a discriminated union so the type checker rejects the impossible combinations."
disable-model-invocation: true
---

# Make Illegal States Unrepresentable

A struct with several booleans and optional fields encodes every combination of them, even the ones that should never happen. Replace it with a discriminated union (sum type, tagged union) that has exactly one shape per legal state, so the combinations that should never occur cannot be constructed.

**Why:** `{isLoading: bool, error?: Error, data?: T}` has four fields' worth of combinations, but only four are legal: idle, loading, error, success. Nothing stops `isLoading: true` with `data` already set, or `error` and `data` both present — the type checker is silent, and the only guard against those states is a comment, a runtime check, or whoever wrote the code remembering the rule. A discriminated union collapses the space down to the states that can occur; the type checker rejects the rest at compile time instead of a reviewer having to notice them in a diff.

**Pattern:**
- Spot fields that are coupled: `isLoading`/`error`/`data`, `isAdmin`/`role`, `startDate`/`endDate`/`isOngoing`. If some combination of their values should never happen, they are one state hiding in several variables.
- Replace them with a tag plus the data that tag's state needs: `type Fetch<T> = {status: "idle"} | {status: "loading"} | {status: "error", error: Error} | {status: "success", data: T}`. Each variant carries only the fields that are actually present in that state.
- Switch or match on the tag, not on a chain of `if (flag)`. Turn on exhaustiveness checking — TypeScript's `never` in a default case, Rust's non-exhaustive-match error, Kotlin/Scala sealed classes — so adding a new state without updating every call site is a compile error, not a runtime surprise.
- Resist bolting on a second boolean to patch a gap in the first (`isActive`, then `isArchived`, then `isPending`). Fold them into one tag with a variant per state instead of letting the flag count grow.
- Keep plain booleans for a true independent binary with no related fields (`isVisible`, `isChecked`). Reach for a union once a flag correlates with other fields or rules another flag out.
- Parse external input straight into the union rather than into loose optional fields reconciled later — pairs with the parse-don't-validate principle.
