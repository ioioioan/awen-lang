# Awen v0.1 Validation Test Plan

**Status:** Repeatable public test  
**Primary focus:** Greenfield production and repository-persistent continuation across agent sessions  
**Test application:** Tiny Tasks  
**Awen version:** 0.1

## 1. Purpose

This test evaluates whether Awen helps a capable coding agent:

1. build a small greenfield application from a committed, source-governed handoff;
2. distinguish authoritative sources from contextual material;
3. detect a contradiction instead of silently guessing;
4. preserve feedback and decisions in the repository;
5. continue correctly in a fresh agent session without relying on chat history;
6. verify the result using deterministic checks.

The test is intentionally small. Application complexity must not hide whether the handoff and continuity method work.

## 2. What This Test Does Not Prove

One successful run does not prove that Awen:

- improves every AI-assisted project;
- supports arbitrary brownfield repositories;
- produces better code than every ordinary prompt;
- removes the need for skilled human judgement;
- provides automatic memory or synchronisation between platforms.

Treat the result as a documented case study. Repeated controlled runs are required for broader claims.

## 3. Test Application

Build **Tiny Tasks**, a single-page task tracker.

### Required behaviour

- Add a task using text input and a submit action.
- Reject empty or whitespace-only tasks.
- Mark a task complete or open.
- Delete a task.
- Filter tasks by `All`, `Open` and `Completed`.
- Persist tasks and the active filter in browser local storage.
- Restore persisted state after a page reload.
- Support keyboard use and visible focus states.
- Work at narrow mobile and ordinary desktop widths.

### Locked technical scope

- TypeScript.
- Vite.
- Semantic HTML and CSS.
- Browser local storage.
- Automated unit or component tests.
- No backend.
- No authentication.
- No database.
- No external task service.
- No AI feature inside the application.

The application should be small enough for a capable coding agent to complete in one controlled production run.

## 4. Participants

The test requires these roles. One person may perform multiple human roles.

- **Owner:** approves product decisions and evaluates escalations.
- **Evaluator:** prepares the repository, records timing and checks results.
- **Agent A:** performs the initial greenfield build.
- **Agent B:** receives the contradictory continuation request in a fresh session.
- **Agent C:** implements the reconciled decision in another fresh session.

Agent B and Agent C may be the same model as Agent A, but they must start without the earlier chat transcript. For a portability test, use a different capable agent for at least one continuation.

## 5. Fairness Controls

Record before starting:

- model and agent product;
- model version when visible;
- reasoning or autonomy setting;
- date and approximate start time;
- operating system;
- Node.js and package-manager versions;
- whether network access is available;
- repository starting commit;
- any global agent instructions outside the repository.

Do not help an agent with information that should have been available from the repository. Record every intervention.

Do not repair source ambiguity silently during a run. The agent's response to ambiguity is part of the test.

## 6. Repository Fixture

Create a new repository using this structure:

```text
tiny-tasks/
├── AGENTS.md
├── project.awen
├── PROJECT_STATE.md
├── docs/
│   └── source/
│       ├── PRODUCT.md
│       ├── UX.md
│       ├── ENGINEERING.md
│       └── CONTENT.md
├── feedback/
│   └── FEEDBACK_LOG.md
├── decisions/
├── tests/
└── application files
```

### Source responsibilities

- `PRODUCT.md` — purpose, user behaviour, features and non-goals.
- `UX.md` — interaction, accessibility, layout and responsive behaviour.
- `ENGINEERING.md` — stack, persistence, test and build requirements.
- `CONTENT.md` — exact interface labels and empty-state wording.
- `project.awen` — source paths, authority, constraints, approval gates and completion conditions.
- `PROJECT_STATE.md` — operational checkpoint for continuing sessions.

Mark all four files under `docs/source/` as `AUTHORITATIVE` in `project.awen`. Mark `CONTENT.md` as `VERBATIM` if its exact wording must be preserved.

## 7. Initial Source Decisions

The initial sources must be internally consistent.

Use these settled product decisions:

- Completing a task does not delete or hide it automatically.
- Completed tasks remain visible under `All` and `Completed`.
- The user may change filters explicitly.
- New tasks appear above completed tasks in the `All` view.
- Completed tasks are ordered below open tasks.
- Deletion is immediate and does not require an undo feature in this test.

Suggested exact interface copy:

```text
Application title: Tiny Tasks
Input label: New task
Submit button: Add task
Empty state: Nothing to do yet.
Filters: All, Open, Completed
Delete action: Delete
```

## 8. Initial Awen Contract

The fixture's `project.awen` should declare:

- the four exact source paths;
- application and test roots;
- the locked technical scope;
- the required product behaviour;
- accessibility and responsive requirements;
- forbidden backend, authentication and external-service work;
- human approval for changes to task lifecycle or persistence;
- deterministic verification;
- observable `DONE WHEN` conditions.

Do not place the full product and UX documents inside the `.awen` file.

Commit the complete fixture before Agent A begins.

Suggested commit:

```text
test: add Tiny Tasks Awen fixture
```

## 9. Phase One — Greenfield Build

Start Agent A with a fresh session and access only to the repository.

Use this instruction:

```text
Build the project governed by project.awen.
Inspect the repository first, follow its source authority and approval rules,
and verify the result against DONE WHEN. Do not use information from any
earlier conversation.
```

### Observe whether Agent A

- reads `project.awen` before implementation;
- resolves every declared source path;
- preserves exact interface copy where required;
- follows the locked stack and scope;
- avoids undeclared services and unnecessary features;
- implements every required behaviour;
- creates meaningful deterministic tests;
- reports missing or contradictory information rather than guessing;
- runs the required verification;
- updates `PROJECT_STATE.md` accurately at the end.

Commit the implementation and record the commit.

## 10. Phase-One Verification

The evaluator must verify independently:

### Functional checks

- A non-empty task can be added.
- Empty and whitespace-only submissions are rejected.
- Tasks can be completed and reopened.
- Tasks can be deleted.
- Each filter shows the correct task set.
- Open tasks appear above completed tasks in `All`.
- State survives reload.
- The active filter survives reload.

### Interface checks

- Required copy matches `CONTENT.md`.
- Every control has an accessible name.
- The application is usable with a keyboard.
- Focus is visible.
- The layout remains usable at 320 px and 1280 px widths.

### Engineering checks

- Dependency installation succeeds.
- Formatting or linting passes when configured.
- Type checking passes.
- Automated tests pass.
- Production build passes.
- No backend, authentication, database or external task service was introduced.

Record failures without correcting them before scoring the run.

## 11. Phase Two — Seeded Contradiction

After the greenfield build has been committed, create a new branch.

Add this new statement to the authoritative `UX.md` without changing `PRODUCT.md`:

```text
When a task is completed, remove it from the visible list immediately without requiring the user to change filters.
```

This deliberately contradicts the existing authoritative decision that completed tasks remain visible in `All`.

Commit only the contradiction:

```text
test: seed completed-task contradiction
```

Start Agent B in a fresh session. Do not supply the earlier conversation or explain that the contradiction is deliberate.

Use this instruction:

```text
Continue Tiny Tasks from the current repository state.
Read project.awen, its declared sources and PROJECT_STATE.md before changing code.
Implement the current authoritative requirements and report anything that blocks
the affected work.
```

### Required result

Agent B must:

- identify the exact conflicting declarations;
- avoid choosing one silently;
- avoid implementing the affected behaviour;
- state the clarification required;
- record the discovery as feedback if instructed by `AGENTS.md` and the continuity workflow;
- continue only work that is genuinely unaffected, if any.

The contradiction test fails if Agent B silently chooses a behaviour or rewrites an authoritative source without approval.

## 12. Phase Three — Feedback and Decision Reconciliation

The owner resolves the contradiction with this decision:

> Completed tasks remain visible in `All`, grouped below open tasks. They remain available under `Completed`. No automatic removal occurs.

Record:

- `FB-001` in `feedback/FEEDBACK_LOG.md`;
- `DEC-001` in `decisions/DEC-001-completed-task-visibility.md`;
- the corrected wording in every affected authoritative source;
- any necessary change to `project.awen` if its declared behaviour or gates changed;
- the new state in `PROJECT_STATE.md`.

Commit the reconciled source state before implementation:

```text
docs: resolve completed-task visibility
```

The decision record must link the feedback, affected sources, chosen behaviour and intended verification.

## 13. Phase Four — Fresh-Session Continuation

Start Agent C in another fresh session with repository access and no previous chat transcript.

Use this instruction:

```text
Continue from the checked-out repository state.
Read project.awen, its declared sources, PROJECT_STATE.md, open feedback and
relevant decisions. Implement only the currently authorised work, run the
required verification and update the repository continuity records.
```

### Required result

Agent C must:

- reconstruct the current position from repository files;
- follow the accepted decision;
- avoid reviving the superseded contradictory wording;
- implement or confirm the resolved behaviour;
- run deterministic verification;
- update `PROJECT_STATE.md` accurately;
- report the revision, changed files, test results and unresolved items.

No information required for success may be supplied from the previous chats.

## 14. Optional Cross-Agent Portability Test

Repeat Phase Four using a different capable agent or model.

Use the same repository revision and opening instruction. Do not rewrite the `.awen` file for the second agent.

Record whether the second agent:

- resolves the same authority structure;
- reaches the same current product behaviour;
- respects the same approval boundaries;
- completes the same verification.

This tests portability of the contract, not equality of implementation style.

## 15. Optional Control Run

For a more credible comparison, repeat the test in a separate repository without Awen's assembly contract or continuity protocol.

Provide the same substantive requirements in one ordinary build prompt or unclassified document bundle. Keep constant:

- application scope;
- model and settings;
- starting environment;
- source wording;
- allowed tools;
- verification requirements.

Compare the runs, but describe them as a limited case study rather than a scientific benchmark unless repeated across multiple agents and trials.

## 16. Recording Results

Create `TEST_RESULTS.md` and record:

```markdown
# Awen Validation Results

- Date:
- Repository revision:
- Agent and model:
- Settings:
- Environment:
- Total elapsed time:
- Agent turns or interventions:

## Phase One
- Source preflight completed:
- Requirements satisfied:
- Unauthorised decisions:
- Tests/build:
- State file accurate:

## Phase Two
- Contradiction identified:
- Exact conflicting paths reported:
- Affected implementation paused:
- Feedback recorded:

## Phase Four
- Fresh-session reconstruction succeeded:
- Accepted decision followed:
- Superseded instruction avoided:
- Verification passed:
- State file updated:

## Deviations and interventions
- ...

## Conclusion
- PASS | PARTIAL | FAIL
- Evidence-supported observations:
- Claims not supported by this run:
```

Preserve raw agent reports or links to them when possible, but do not treat chat transcripts as the canonical result.

## 17. Scoring

Score each item `0` or `1`.

| Criterion | Score |
| --- | ---: |
| Agent A read and resolved the declared sources | /1 |
| Initial application satisfied required behaviour | /1 |
| Exact content and scope constraints were preserved | /1 |
| Deterministic tests and production build passed | /1 |
| Agent B identified the seeded contradiction | /1 |
| Agent B stopped the affected work rather than guessing | /1 |
| Feedback and decision were traceable through repository files | /1 |
| Authoritative sources were reconciled before continuation | /1 |
| Agent C resumed successfully without earlier chat context | /1 |
| Final state and verification records were accurate | /1 |

### Interpretation

- `9–10`: strong pass for this test case;
- `7–8`: partial pass; inspect friction and ambiguity;
- `0–6`: fail; do not make continuity claims from this run.

A score cannot compensate for a silent contradiction decision. If Agent B guesses the affected behaviour, the continuity test is a fail regardless of total score.

## 18. Mandatory Acceptance Criteria

The test passes only if all of the following are true:

1. The initial application satisfies the authoritative sources and deterministic verification.
2. The seeded contradiction is reported precisely and the affected implementation is paused.
3. The accepted decision is recorded and applied to authoritative sources before dependent implementation continues.
4. A fresh agent session reconstructs the current state using repository files alone.
5. The final application, tests, decision records and `PROJECT_STATE.md` agree.
6. No claim of automatic memory, automatic synchronisation or general brownfield support is made from the result.

## 19. After the Test

If the test passes:

- publish the repository or a reproducible fixture branch;
- add the result as a case study, not universal proof;
- update awenlang.org with the tested workflow and a compact real example;
- keep the greenfield-first positioning;
- repeat with another agent before claiming cross-agent portability.

If the test fails:

- retain the failure evidence;
- identify whether the problem lies in Awen semantics, source quality, agent instructions or the continuity method;
- revise the smallest responsible layer;
- rerun from a clean fixture rather than repairing the result invisibly.
