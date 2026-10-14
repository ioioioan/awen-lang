# Integrating This Update

Copy the `docs/`, `templates/` and `examples/continuity/` directories into the Awen repository.

This update is documentation and workflow guidance. It does not change Awen v0.1 syntax. Do not modify `SPEC.md` or `TEMPLATE.awen` merely to install it.

## README additions

Add these entries under the repository-contents section:

```markdown
- [`docs/AWEN_SHARED_REPOSITORY_WORKFLOW.md`](docs/AWEN_SHARED_REPOSITORY_WORKFLOW.md) — the canonical shared-repository method for planning and agent implementation.
- [`docs/CONTINUITY.md`](docs/CONTINUITY.md) — optional context preservation across longer agent runs.
- [`templates/`](templates/) — optional project-state, feedback and decision templates.
- [`examples/continuity/`](examples/continuity/) — a worked ZeroReel reconciliation example.
```

Add this positioning near the main explanation of Awen:

```markdown
Awen is strongest for greenfield projects, major new production phases and controlled rebuilds. Once the project is established, its shared-repository workflow can preserve decisions and production context across later agent sessions. Brownfield adoption remains an emerging workflow.
```

## `AGENTS.md` additions

Add to the reading order:

```markdown
- Read `docs/AWEN_SHARED_REPOSITORY_WORKFLOW.md` when setting up or synchronising a project repository.
- For continuing work, read `docs/CONTINUITY.md` and the project's `PROJECT_STATE.md` when present.
```

Add to the execution rules:

```markdown
- Record material implementation discoveries as feedback when the project uses the continuity protocol.
- Do not treat feedback, chat history or existing implementation as authority until the relevant decision and governing sources are reconciled.
- At the end of a continuing run, update `PROJECT_STATE.md` with verification, unresolved feedback and the next permitted action.
```

## Validation

Before committing:

1. confirm all relative links resolve;
2. confirm the example uses only Awen v0.1 constructs;
3. confirm `SPEC.md` and `TEMPLATE.awen` are unchanged;
4. confirm the README does not claim automatic agent memory or automatic workspace synchronisation;
5. review the ZeroReel example as public documentation rather than a private project source.

## Commit

Suggested commit message:

```text
docs: add shared repository and continuity workflow
```

Suggested pull-request summary:

```text
Adds a Git-native, agent-agnostic method for sharing authoritative sources and preserving context across longer production runs. Includes optional state, feedback and decision templates plus a worked ZeroReel example. Clarifies that Awen is strongest for greenfield work, does not provide automatic agent memory, and does not change v0.1 language semantics.
```

## Website

Do not update awenlang.org until this repository change has been merged and exercised on one real ZeroReel continuation.

After that test, add a small link to the shared-repository workflow. Do not claim general brownfield support or automatic synchronisation.
