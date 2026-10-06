---
name: architecture-change-gate
description: Review proposed structural changes before Promise adds a service, queue, database, repository, runtime, package, abstraction, framework, scheduled job, cache, or external dependency.
---

# Architecture Change Gate

Use before accepting a structural addition.

## Required questions

1. What concrete problem exists today?
2. Why can the existing architecture not solve it cleanly?
3. What permanent thing is being added: state, runtime, dependency, deployable, queue, repo, abstraction, flag, job, or operational procedure?
4. Who or what will operate it when the founder is unavailable?
5. What new failure modes and observability requirements appear?
6. What does this replace, simplify, or allow us to delete?
7. Can the decision be reversed cheaply?
8. Does it increase cross-repo or cross-runtime coordination?
9. Is the proposed boundary independently deployable or merely conceptually distinct?
10. What is the 10x-user behavior and cost?

## Default posture

Prefer extending an existing well-bounded component over adding a new architectural primitive. Do not add structure merely to reduce file size, agent context, or aesthetic discomfort.

## Output

Return: problem, options considered, permanent cost, failure/operational impact, deletion opportunity, reversibility, recommendation, and explicit conditions that would justify revisiting the decision.
