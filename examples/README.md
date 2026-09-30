# Awen examples

These are illustrative handoffs, not runnable source packs. Their referenced product documents, content and repositories must be supplied by the project using them; replace repository and revision placeholders before execution.

For a new project, copy one of these root-sheet examples to `project.awen` at that project's root:

- [`zeroreel.awen`](zeroreel.awen) — responsive web MVP.
- [`book.awen`](book.awen) — edited manuscript.
- [`video.awen`](video.awen) — short film.
- [`data.awen`](data.awen) — cleaned dataset.

The descriptive filenames distinguish examples in this collection. In each actual project, `project.awen` is the canonical root assembly sheet. Agents start there and read `SOURCES` from top to bottom, respecting each source's authority.

## Root with a refinement sheet

For an existing ZeroReel project, retain its `project.awen` and copy [`zeroreel-refinement.awen`](zeroreel-refinement.awen) to `changes/playback-refinement.awen`:

```text
AGENTS.md
project.awen
docs/
  product.md
  ux.md
  architecture.md
  engineering.md
  references.md
changes/
  playback-refinement.awen
```

Add the refinement to the root sheet's existing `SOURCES` list:

```awen
SOURCES
  PRODUCT       ./docs/product.md                    AUTHORITATIVE
  UX            ./docs/ux.md                         AUTHORITATIVE
  ARCHITECTURE  ./docs/architecture.md               AUTHORITATIVE
  ENGINEERING   ./docs/engineering.md                AUTHORITATIVE
  REFERENCE     ./docs/references.md                 CONTEXT
  REFINEMENT    ./changes/playback-refinement.awen   AUTHORITATIVE
```

Read these entries in order, including the refinement's sources when reached. `ROOT .` in both sheets refers to the project root, so the refinement still resolves `./docs/` there. The refinement applies within its declared scope; it does not replace the root or silently override its constraints, approvals or completion criteria. Surface contradictions instead of choosing whichever sheet was read last. Use `CONTEXT` for a sheet supplied only as background.

The project's `AGENTS.md` should contain:

```markdown
# Agent instructions

Start with `project.awen`.

Follow its source reading order, authority rules, constraints, approvals and completion criteria before making changes.
```

```text
AGENTS.md -> project.awen -> referenced sources -> build
```
