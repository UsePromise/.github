# Contributing to Promise

## Choose the owning repository

- Use `UsePromise/ios` for the native app, extensions, widgets, StoreKit, and
  Apple release work.
- Use `UsePromise/platform` for web, APIs, workers, data, AI, infrastructure,
  and cross-surface product contracts.
- Track cross-repository outcomes in the repository that owns the primary
  contract, then link any implementation issues in the other repository.

## Create useful issues

1. Search open and closed issues first.
2. Capture one user outcome or operational result per issue.
3. Explain impact and acceptance criteria; avoid prescribing code prematurely.
4. Apply one type, one priority, and the relevant area labels during triage.
5. Add confirmed work to the `Promise` project.

Priority means:

- **P0 Critical:** active security, privacy, data, or production failure.
- **P1 High:** blocks a core journey or the next meaningful product outcome.
- **P2 Medium:** valuable planned work without immediate urgency.
- **P3 Low:** useful when capacity permits.

An issue is ready when its outcome, scope, dependencies, and acceptance criteria
are clear. It is done only when the behavior is merged, validated in the target
environment, and documented where users or operators depend on it.

Never include credentials, signing material, access tokens, or private customer
content in issues, pull requests, logs, fixtures, or screenshots.
