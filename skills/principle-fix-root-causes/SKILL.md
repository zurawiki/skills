---
name: principle-fix-root-causes
description: "Trace debugging symptoms to the first faulty decision or missing handler."
disable-model-invocation: true
---

# Fix Root Causes

- Reproduce the failure. Trace the error and state backward. Instrument the first step you cannot explain.
- If the input is valid, fix the code that mishandles it. If it violates an invariant, fix the producer. Check whether a guard, retry, or workaround masks that fault.
- For restart-only failures, inspect persisted configuration, caches, locks, and serialized state first.
- Find and fix other instances of the same fault. If diagnosis was costly, propose a cheap signal that would have exposed it.
