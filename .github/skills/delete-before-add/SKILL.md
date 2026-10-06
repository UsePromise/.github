---
name: delete-before-add
description: Search for code, concepts, infrastructure, settings, workflows, or operational steps that can be removed when introducing a change.
---

# Delete Before Add

Before adding durable structure, identify what can disappear.

Inspect the affected area for duplicated concepts, compatibility shims, obsolete flags, dead code, redundant abstractions, parallel workflows, stale docs, unused provider paths, repeated transforms, and manual procedures made unnecessary by the change.

Ask:
- Does the new capability supersede an old path?
- Can two concepts collapse into one?
- Can a setting become a safe default?
- Can a cache/projection be derived instead of stored?
- Can a rollout flag be scheduled for removal?
- Can an external dependency now be removed?
- Can a recurring manual step become deterministic automation?

Never delete merely to produce a positive diff ratio. Preserve compatibility and migration safety.

## Output

Return three sections: `Delete now`, `Delete after migration/rollout`, and `Keep intentionally`. For deferred deletions, identify the concrete exit condition so temporary structure does not become permanent by accident.
