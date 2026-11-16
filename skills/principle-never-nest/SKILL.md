---
name: principle-never-nest
description: "Apply whenever writing or changing code. Exit early on the unhappy cases so the main logic stays flat and comes last."
disable-model-invocation: true
---

# Never Nest

Exit early. Handle each unhappy case at the top and leave, so the main logic runs flat, unindented, and last.

**Why:** Each level of nesting is one more condition the reader must hold in their head to understand the line in front of them. An early exit settles that condition and lets the reader forget it.

**Pattern:**
- Invert the condition. Instead of wrapping the work in `if (ok) { ... }`, write `if (!ok) return` and continue below it.
- Use the exit that fits: `return` in a function, `continue` or `break` in a loop, a throw for an error.
- Drop the `else` after a branch that exits.
- When several checks answer one question, extract them into a named function and guard on it: `if not is_processable(order): continue`.
- Do not pack unrelated checks into one long compound condition.
- An early exit is for a state the function may legitimately receive. Do not add guards for states that should never exist.
- Apply this to code you write or change. Leave unrelated nested code alone.
