# Awen Lang — instructions for AI agents

Awen Lang is a small declarative assembly-sheet language for AI production.

Its purpose is to turn a settled creative synthesis into a precise handoff for an AI agent, coding agent, model, or production toolchain.

## Start here

1. Read `README.md` for the project overview.
2. Read `SPEC.md` for Awen Lang v0.1 semantics.
3. Read `WORKFLOW.md` for the intended handoff workflow.
4. Read `TOOLS.md` for the AI-agnostic tool philosophy.
5. Use `TEMPLATE.awen` when creating a new assembly sheet.
6. Read the closest example in `examples/` when useful.

## Core rule

Awen is an assembly sheet, not an implementation language, prompt framework, agent runtime, or replacement for domain tools.

An `.awen` file captures the creator's committed production intent: output, authoritative sources, core behaviour, stack/tool choices, requirements, preferences, allowed seams, exclusions, approval gates, and completion criteria.

## When creating or editing an `.awen` file

- Preserve the creator's settled intent.
- Do not revive discarded brainstorming or infer decisions that were not made.
- Do not invent unresolved choices. Mark them explicitly when they block production.
- Use exact relative paths for sources when available.
- Label source roles clearly.
- Distinguish `AUTHORITATIVE` sources from `CONTEXT` sources.
- Mark pre-written content `VERBATIM` when exact wording must survive production unchanged.
- Make core user or artifact behaviour explicit when technical wording could permit multiple plausible experiences.
- Declare acceptable mocks, stubs, placeholders and temporary substitutes in `SEAMS`; do not create undeclared seams silently.
- Keep the assembly sheet concise. Put detailed narrative in source files rather than duplicating it in `.awen`.
- Preserve explicit `REQUIRE`, `PREFER`, `AVOID`, and `FORBID` distinctions.
- Preserve human approval gates.
- Make `DONE WHEN` criteria concrete enough to evaluate.
- Remain vendor-neutral unless the creator deliberately selects a named model, agent, tool, language, framework, or service.

## Execution

When an `.awen` file is provided for production:

1. Read the assembly sheet first.
2. Resolve and read its declared sources according to their roles, authority and handling qualifiers.
3. Treat the assembly sheet and `AUTHORITATIVE` sources as the committed handoff.
4. Preserve `VERBATIM` content exactly unless human approval changes it.
5. Use `CONTEXT` sources as supporting material, not as authority over committed decisions.
6. Implement `BEHAVIOR` as the real user/artifact semantics, not merely a technically plausible approximation.
7. Use a mock, stub, placeholder or local substitute only when `SEAMS` explicitly permits it.
8. Follow declared constraints and approval gates.
9. Use ordinary domain tooling to produce the requested artifact.
10. Prefer deterministic verification where available: tests, compilers, schemas, validators, linters, render checks, or equivalent objective checks.
11. Do not change the committed build contract silently.

Awen is AI-agnostic. These instructions should remain usable with Codex, Claude, Gemini, Cursor, GitHub Copilot, local models, specialist production agents, and future AI systems.
