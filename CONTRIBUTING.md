# Contributing to Awen Lang

Awen is intentionally small. Contributions should reduce ambiguity, preserve intent or remove production friction without turning Awen into a general-purpose language, prompt framework or workflow engine.

## Before proposing a core keyword

Ask:

1. Does a real production handoff need this?
2. Can the same precision be achieved with an existing Awen section or a Markdown source?
3. Does the addition remain understandable to a human without tooling?
4. Is it model- and vendor-agnostic?
5. Does it preserve progressive enhancement?
6. Does it remain useful across capable models, agents and vendors?
7. Is this really language semantics, or should it remain non-normative guidance in `TOOLS.md`?
8. Is the proposal backed by a real production ambiguity or failure mode rather than speculation?

Prefer examples and evidence from real projects over speculative language growth.

## Changes

- Keep `SPEC.md` authoritative for language semantics.
- Update `TEMPLATE.awen` when a core section changes.
- Update an existing-project example when repository semantics change.
- Add or update examples when a change affects real usage.
- Avoid breaking v0.1 syntax without a clear precision or usability benefit.
- Prefer small hardening changes proven by real assembly sheets.

## Scope

The MVP intentionally has no parser, compiler, runtime, package manager or agent framework. Tooling should be proposed only when real usage shows that it removes friction or enables useful deterministic checks.
