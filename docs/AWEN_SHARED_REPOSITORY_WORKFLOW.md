# Awen Shared Repository Workflow

**Status:** Canonical workflow  
**Purpose:** Keep planning, authoritative sources and agent implementation synchronised through one Git repository.

## Where Awen fits

Awen is strongest for greenfield projects, major new production phases and controlled rebuilds where the governing sources can be settled before execution.

Once that foundation exists, the same repository can preserve context across later agent sessions. Awen supplies the build contract; ordinary source files preserve product truth; Git preserves revision history.

Awen does not provide agent memory or automatic platform synchronisation. Every participating workspace or agent must read the current repository revision.

## Core principle

A project uses one Git repository as its shared, versioned workspace.

```text
Planning workspace
      ↓ reads and refines sources
Git repository
      ↑ reads, implements and commits
Build agent
```

The repository holds the canonical files and revision history. Chat history is not treated as project authority.

## Recommended repository structure

```text
project/
├── AGENTS.md
├── project.awen
├── PROJECT_STATE.md          # optional for continuing work
├── docs/
│   └── source/
├── feedback/                 # optional for continuing work
├── decisions/                # optional for continuing work
├── testing/
├── seed/
├── deployment/
└── application code
```

Use only the directories the project needs. Awen does not require a universal repository layout.

## File responsibilities

### `AGENTS.md`

Tells coding or production agents how to operate inside the repository:

- read `project.awen` first;
- follow its source order and authority rules;
- read `PROJECT_STATE.md` when present;
- do not invent missing product decisions;
- preserve unrelated repository changes;
- report blockers before implementing affected work;
- record material discoveries when the continuity protocol is active.

### `project.awen`

Acts as the assembly and production contract.

It declares the output, roots, exact source paths, source authority, behaviour, requirements, preferences, exclusions, approval gates, blockers, verification and completion conditions.

The `.awen` file does not duplicate the source documents or become a running project diary.

### `docs/source/`

Contains current authoritative product, content, UX, architecture, data and governance decisions.

Product decisions are changed here first. Files elsewhere may provide context or evidence, but they do not silently override declared authoritative sources.

### `PROJECT_STATE.md`

Provides a compact factual checkpoint for the next session: current revision, completed work, active work, unresolved feedback, blockers, verification state and next permitted action.

It is operational orientation, not product authority.

### `feedback/`

Records contradictions, omissions, invalid assumptions and verification failures discovered during production.

Feedback is evidence awaiting evaluation. It does not change the product merely by being recorded.

### `decisions/`

Records consequential resolutions, rationale, affected sources and verification expectations.

Accepted decisions must be incorporated into the current authoritative sources. The decision record preserves why the change occurred; it does not replace the corrected source.

### Application code or produced output

Implements the approved sources. Existing implementation is evidence of the current build state, not permission to redefine the product silently.

## Initial production workflow

```text
Explore freely
→ settle product and creative decisions
→ write authoritative sources
→ assemble project.awen
→ commit the production contract
→ agent implements
→ tests and verification run
→ implementation committed
```

## Continuing production workflow

```text
Feedback or contradiction discovered
→ record the observation
→ evaluate against authoritative sources and evidence
→ accept, reject, defer or request clarification
→ update authoritative sources when accepted
→ update .awen only if its contract changed
→ commit the reconciled source state
→ agent pulls the new revision
→ implementation and verification continue
→ implementation committed
```

## Synchronisation rules

1. Pull or retrieve the intended repository revision before starting work.
2. Check for uncommitted changes before modifying files.
3. Read `project.awen` and resolve its declared sources before implementing.
4. Commit authoritative source changes before or with their dependent implementation changes, keeping the relationship traceable.
5. Do not rely on chat history for decisions absent from the repository.
6. Do not copy source prose into `.awen` unless exact wording is itself a required constraint.
7. Missing or contradictory decisions block only the affected work.
8. Agents report the exact clarification needed instead of guessing.
9. Material implementation feedback returns to the source layer before the affected work is finalised.
10. Update `PROJECT_STATE.md` at the end of a continuing run when the project uses it.
11. Git remains the shared persistent state between participating workspaces and agents.

## Recommended commit sequence

```text
Commit 1: checkpoint existing implementation
Commit 2: synchronise authoritative sources and Awen contract
Commit 3+: implement, verify and deploy from approved sources
```

Small changes may use one atomic commit when source, implementation and verification remain clearly traceable.

## Existing repositories

Awen does not yet claim a complete brownfield-adoption method. Before governing an established repository:

1. inspect the implementation and current documentation;
2. identify which behaviour is deliberate and which is accidental or obsolete;
3. establish authoritative sources without treating code as unquestionable product truth;
4. record unresolved conflicts as blockers;
5. issue the first `.awen` contract only after the baseline is reviewable.

Until this process has been tested across real existing repositories, describe brownfield support as emerging.

## Locked principle

> One repository holds the truth. Sources define the product. Awen assembles the instructions. Agents implement them. Git history preserves the feedback loop.
