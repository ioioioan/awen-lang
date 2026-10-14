# Continuity Across Agent Sessions

**Status:** Recommended Awen workflow  
**Scope:** Long-running work that must survive changes of session, workspace, model or build agent.

## Accurate capability

Awen can preserve project context across agents when every participant reads and updates the same version-controlled repository.

It does not provide automatic memory, automatic repository access or automatic synchronisation between platforms.

## Core rule

> Feedback records what was discovered. Decisions determine what changes. Sources preserve current truth. Awen authorises the next production run.

## Optional continuity files

```text
project.awen
PROJECT_STATE.md
feedback/
  FEEDBACK_LOG.md
decisions/
  DEC-001-short-title.md
```

Projects expected to finish in one controlled run do not need these files.

`project.awen` may reference continuity files as `CONTEXT` sources when an executor needs them. That reference does not make them product authority.

## Lifecycle

```text
BUILD → OBSERVE → RECORD → EVALUATE → DECIDE → REVISE → VERIFY → CONTINUE
```

### Build

Execute from a known repository revision and its governing `.awen` contract.

### Observe

Notice contradictions, omissions, invalid assumptions, verification failures or material opportunities revealed by production.

### Record

Create a feedback item with a stable identifier. Preserve the observation separately from any proposed answer.

### Evaluate

Compare the observation with the assembly sheet, authoritative sources, implementation evidence and current scope.

### Decide

Use one outcome:

- `ACCEPTED` — governing truth or the production contract must change;
- `REJECTED` — no change, with rationale;
- `DEFERRED` — potentially valid but outside the current production target;
- `NEEDS_CLARIFICATION` — authorised human judgement is required;
- `RESOLVED` — accepted changes have been applied and verified.

### Revise

For accepted feedback:

1. create a decision record when the resolution is consequential or non-obvious;
2. update every affected authoritative source;
3. update `project.awen` only if paths, authority, behaviour, constraints, gates, blockers or completion conditions changed;
4. update the implementation and tests;
5. link the feedback item to the decision and resulting revision.

### Verify

Use deterministic checks where available. Record enough evidence to distinguish a verified resolution from an administrative status change.

### Continue

Refresh `PROJECT_STATE.md`, commit the reconciled state and begin the next session from that revision.

## Stable identifiers

Use simple repository-local identifiers such as `FB-001` and `DEC-001`. Never reuse them. Rejected, deferred or superseded records remain in Git history.

## Session-start protocol

For continuing work, an agent should:

1. inspect the repository and current revision;
2. check for uncommitted changes;
3. read `project.awen`;
4. resolve and read its authoritative sources;
5. read `PROJECT_STATE.md` when present;
6. inspect open or clarification-required feedback and relevant decisions;
7. confirm the permitted task;
8. stop on unresolved contradictions rather than guessing.

Suggested instruction:

```text
Continue from the checked-out repository state.
Read project.awen first and resolve its declared sources.
Then read PROJECT_STATE.md and any OPEN or NEEDS_CLARIFICATION feedback.
Do not silently alter authoritative sources or the Awen contract.
Record material implementation discoveries in feedback/FEEDBACK_LOG.md.
```

## Session-end protocol

Before declaring a continuing run complete, the agent should:

1. run the relevant verification;
2. record material discoveries that must survive the session;
3. identify decisions requiring approval;
4. update `PROJECT_STATE.md` with facts rather than a transcript;
5. report changed files, verification, unresolved feedback and the next permitted action.

## Conflict handling

- When implementation conflicts with an authoritative source, the source remains authoritative until deliberately revised.
- When authoritative sources conflict, stop or escalate. Do not select a winner from chat history or existing code.
- When feedback proposes work outside the current output, mark it `DEFERRED` rather than expanding scope.
- When `PROJECT_STATE.md` conflicts with authoritative sources or `project.awen`, treat the state file as stale and correct it.

## Scope boundary

This workflow adds no database, hosted service, parser, agent memory system or mandatory automation. Git provides persistence. Markdown provides inspectable records. Awen remains the concise production contract.
