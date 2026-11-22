---
name: principle-never-nest
description: "Apply when writing or changing control flow. Use early exits, eliminate redundant state, and remove unnecessary branches."
---

# Never Nest

Keep the main path flat. Apply this principle to code you write or change.

- Return as soon as a case is settled. In loops, use `continue` to skip an item or `break` when the work is complete. Drop the `else` after an exit.
- Eliminate flags that merely record a decision for later. Derive state from an existing value or return the result directly.
- Reduce cyclomatic complexity by deleting redundant decisions. Guard clauses flatten nesting even when the number of paths stays the same.
- Guard only for reachable cases. Preserve evaluation order, side effects, and cleanup when moving an exit.
