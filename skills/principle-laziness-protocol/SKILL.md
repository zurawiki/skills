---
name: principle-laziness-protocol
description: "Use when choosing between refactors or considering a new abstraction."
disable-model-invocation: true
---

# Laziness Protocol

- Make each decision once. Pass its result to callers that need it.
- Choose the smallest complete change. Delete redundant code before introducing a helper or layer.
