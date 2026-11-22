---
name: principle-normalize
description: "Apply when changing where repository facts are stored or how multiple consumers read them."
---

# Normalize the Repository

Give each independently changing fact one place to edit. If one logical update requires coordinated edits, trace each copy to its consumers.

- Prefer a reference, lookup, or derived view. A README can link to the skills directory instead of maintaining a second inventory.
- When consumers require separate files, generate them deterministically from the canonical source. Keep edits at the source and check committed outputs for drift.
- Share values that must change together. Equal values with independent meanings can evolve separately.
