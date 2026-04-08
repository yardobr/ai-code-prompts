---
name: change-impact-analysis
description: Use when reviewing a diff, pull request, patch, or staged changes to identify semantic behavior changes, downstream consumer impact, stale integrations, or regression risk.
---

# Change Impact Analysis

## Overview

Analyze semantic changes, not files or diff chunks. Your job is to identify what behavior or contract changed, trace who depends on it, and distinguish broad impact from developer attention required.

This skill is read-only. Do not modify files or suggest patches unless explicitly asked.

## When to Use

Use when asked to:
- analyze a PR, diff, patch, or code change for system impact
- identify downstream effects or possible regressions
- check whether changed code has stale callers or unhandled consumers
- review API, DB, interface, config, dependency, or behavior changes for hidden fallout

Do not use for:
- general code quality review without impact analysis
- security-focused review
- root-cause debugging of an existing bug

## Core Rules

1. Use **semantic changes** as the unit of analysis.
2. **Consumer tracing is mandatory.** Do not stop at the changed file.
3. Separate **impact** from **importance**:
   - `impact` = blast radius and system criticality
   - `importance` = whether the change needs developer attention because it looks under-handled, risky, inconsistent, or regression-prone
4. Call out both direct breakage and second-order effects.
5. Stay evidence-based. Mark uncertainty instead of guessing.
6. Use one row per semantic change. If a producer change and a stale consumer are two sides of the same contract break, keep them in one row unless separate attention is required.

## Workflow

1. Parse the input change set: PR, diff, patch, staged changes, or changed files.
2. Extract semantic changes rather than listing files.
3. Classify each semantic change. Common categories:
   - API or request/response contract
   - type or interface contract
   - database schema or persistence behavior
   - business logic or runtime behavior
   - config, flags, or startup flow
   - events, jobs, caching, or side effects
   - dependency or package change
4. Trace affected consumers:
   - direct callers
   - implementations and interfaces
   - serializers, adapters, and generated clients
   - routes, handlers, jobs, cron tasks, plugins, registries, and other runtime wiring
   - tests that document expected behavior
5. For each semantic change, decide:
   - what changed
   - what parts of the system are affected
   - whether the impact appears handled, partially handled, or unhandled
   - whether a regression risk or non-obvious mismatch exists
6. Score:
   - `impact` on a `1-10` scale
   - `importance` as `low`, `medium`, `high`, or `critical`
7. Produce the required output in this order:
   - top 5 changes overview
   - full change table
   - supporting evidence

## Consumer Tracing Checklist

For every semantic change, check the nearest relevant consumers and boundaries:

- callers and importers
- implementations of changed interfaces or types
- request builders, API clients, SDKs, and handlers
- persisted data readers and writers
- config readers and startup paths
- override sources for defaults, such as env vars, remote config, or persisted settings
- caches, queues, jobs, webhooks, and event subscribers
- tests that may now be stale or incomplete

Known blind spots:
- string-based lookups
- dependency injection or registries
- generated code
- optional fields that became required in practice
- nullability changes
- ordering, retries, caching, or timing assumptions

## Row Granularity Rules

Use one row per semantic change, not per file.

Merge edits into one row when they represent one contract or behavior shift across producer and consumer boundaries.

Split into separate rows when any of these are true:
- different developer attention is required
- different consumers are affected
- different rollout or migration risk exists
- one change is handled but another is not
- one change is only a supporting implementation detail while another is the observable behavior change

For config changes:
- use one row per changed default or flag behavior, not one row for the whole config file
- explicitly note whether the effective behavior is controlled by code defaults, shipped config, env vars, remote config, or persisted settings
- note whether the blast radius applies to all deployments, only new installs, or only environments that rely on defaults

## Scoring Rubric

### Impact

Score impact by blast radius and criticality:

| Score | Meaning |
|------|---------|
| `1-2` | Cosmetic or semantics-preserving change with negligible system effect |
| `3-4` | Low-scope change with limited downstream surface area |
| `5-6` | Moderate subsystem change affecting multiple callers or flows |
| `7-8` | High-impact contract or workflow change affecting important behavior or integrations |
| `9-10` | System-critical change in startup, auth, persistence, core runtime, or equivalent high-blast-radius path |

In the table, write impact as `score/10 - scope note`.

Example: `8/10 - API contract and generated clients`

### Importance

Score importance by how much developer attention is needed:

| Level | Meaning |
|------|---------|
| `low` | Impact exists but appears safely handled |
| `medium` | Some uncertainty, indirect consumers, or partial handling |
| `high` | Likely missing updates, stale consumers, contract mismatch, or credible regression risk |
| `critical` | Clear breakage, unsafe migration, or severe mismatch across system boundaries |

Rank the top 5 by `importance` first, then `impact`.

## Second-Order Effects

Always look for:

- schema drift
- stale callers
- optional parameter mismatches
- unhandled nullability
- changed defaults
- changed error behavior
- cache invalidation assumptions
- retries, ordering, or idempotency changes
- client/server contract divergence
- migration or rollout ordering risks

## Output Format

### 1. Top 5 Changes Overview

Start with the 5 most meaningful changes.

For each change:
- 3-4 sentences
- explain what changed
- explain what it impacts
- explain why it may or may not need attention

If fewer than 5 meaningful changes exist, include only the real ones.

### 2. Full Change Table

Include **all** identified semantic changes in a markdown table with these columns only:

| change | description | impact | importance |
|--------|-------------|--------|------------|

Rules:
- one row per semantic change
- `description` must be 1-2 sentences
- `impact` must use `score/10 - scope note`
- `importance` must be one of `low`, `medium`, `high`, `critical`

### 3. Supporting Evidence

After the table, group evidence by semantic change.

For each change include:
- why this change was identified
- affected producers and consumers
- repo-relative file paths
- relevant code snippets or symbols
- why the change appears handled, partially handled, or unhandled
- explicit regression risks or remaining uncertainty

## Quick Reference

| If the diff changes... | Always trace... |
|------------------------|-----------------|
| API shape | clients, handlers, SDKs, serializers, tests |
| DB schema or persistence | readers, writers, migrations, background jobs |
| shared type or interface | implementers, callers, generated types, tests |
| config or startup | boot path, env readers, deployment assumptions |
| behavior in shared logic | callers, error handling, retries, caches, user flows |
| dependency | where it is used, privilege level, replaced behavior |

## Common Mistakes

- Listing changed files instead of semantic changes
- Stopping at direct callers
- Treating “refactor” as automatically no-impact
- Confusing `impact` with `importance`
- Reporting only obvious breakage and missing second-order effects
- Presenting speculation as fact
- Omitting repo-relative paths in evidence

## Minimal Example

```markdown
## Top 5 Changes Overview

### 1. Response payload now omits `status`
The API response for session creation removed the `status` field and now derives readiness implicitly. This affects API consumers, generated clients, and any UI logic branching on `status`. The server-side change is impactful because it alters a shared contract, but it becomes important only if downstream consumers were not updated. In this case, one web client still reads `status`, so the change needs attention.

## Full Change Table

| change | description | impact | importance |
|--------|-------------|--------|------------|
| Session response contract changed | `status` was removed from the session payload, changing how readiness is communicated to consumers. One client still branches on the old field. | 7/10 - API clients and UI state | high |

## Supporting Evidence

### Session response contract changed
- Producer: `packages/opencode/src/server/session.ts`
- Consumer: `packages/app/src/lib/session.ts`
- Risk: client still reads `status`, creating a stale contract dependency
```
