# Awen Lang

**Assembly sheets for AI production.**

Awen Lang is a small declarative language for handing a settled creative synthesis to an AI, agent or production tool with precision.

It is designed for the moment after creative exploration is finished and before production begins.

You explore, research, argue, refine and lock decisions in whatever workspace you prefer. Then you distil the committed result into one `.awen` assembly sheet plus the exact source files that matter. A capable AI, coding agent or production tool can then execute from that handoff with far less guesswork.

> **Vibe freely. Commit deliberately. Build precisely.**

## For AI agents

If you are an AI or coding/production agent reading this repository, start with [`AGENTS.md`](AGENTS.md), then read [`SPEC.md`](SPEC.md) and [`TEMPLATE.awen`](TEMPLATE.awen).

Your job is to preserve a creator's settled intent and turn it into a concise assembly sheet or execute an existing assembly sheet with its declared sources. Do not treat Awen as an implementation language or invent unresolved decisions.

## What Awen is

Awen is a lightweight, AI-agnostic handoff format for turning a settled creative synthesis into a precise production brief.

It can describe:

- what is being produced;
- which files are authoritative sources;
- where those files live;
- which pre-written content must be preserved verbatim;
- which tools, languages, models or stacks are chosen;
- core user or artifact behaviour that must not be misinterpreted;
- what is required, preferred, avoided or forbidden;
- which temporary seams or substitutes are explicitly acceptable;
- what needs human approval;
- what counts as done;
- optionally, which exact source/repository revision the handoff represents.

Awen does **not** replace programming languages, creative tools, models, agents or production workflows. It sits above them as the assembly sheet.

Awen also has **no official AI vendor or execution stack**. A project can be assembled with Codex, Claude, Gemini, Cursor, another capable agent, a specialist production pipeline, or future tools without changing Awen's core model.

## Why it exists

AI-assisted work is fast while ideas are fluid, but the transition from "we know what we want" to "build it" is often lossy. Context is scattered across chats and documents, old ideas survive beside current decisions, and agents are forced to guess.

Awen creates a commit point:

```text
creative workspace
        ↓
settled synthesis
        ↓
project.awen
+ authoritative sources
        ↓
AI / agent / toolchain
        ↓
finished artifact
```

## Core principles

1. **Assembly sheet, not implementation language.** Awen describes the build; normal tools produce it.
2. **AI-agnostic.** The file should remain useful across models and agents.
3. **Human-readable.** Awen uses a small declarative vocabulary and minimal syntax.
4. **Precision over ceremony.** Add only information that removes ambiguity or preserves intent.
5. **Progressive enhancement.** Markdown and ordinary project files remain useful without Awen-aware tooling.
6. **Exact sources.** Prefer explicit relative paths, roles and authority over dumping whole workspaces into context.
7. **Semantic behaviour first.** Describe what the user or artifact must actually experience, not just the technologies involved.
8. **Explicit seams.** If a mock, stub, placeholder or temporary substitute is acceptable, say so. Do not let an agent silently replace real behaviour with a seam.
9. **Human authority.** Approval gates make consequential decisions explicit.
10. **Portable intent.** The same committed synthesis should survive a change of model, agent or production tool.
11. **Roles before vendors.** Recommend tool roles and capabilities by default; lock a named tool or model only when the creator intentionally chooses it.
12. **Deterministic checks first.** Where possible, verify outputs with tests, compilers, schemas, validators and other objective tooling rather than asking an LLM to judge everything.

## Minimal example

```awen
AWEN 0.1

PROJECT ZeroReel
OUTPUT software MVP
ROOT .

SOURCES
  PRODUCT       ./docs/product.md       AUTHORITATIVE
  UX            ./docs/ux.md            AUTHORITATIVE
  CONTENT       ./content/homepage.md    AUTHORITATIVE VERBATIM
  RESEARCH      ./docs/research.md       CONTEXT

STACK
  TypeScript
  PostgreSQL
  Azure

BEHAVIOR
  primary film playback stays on the film detail page through approved embeds
  external source links remain visible for provenance, fallback and attribution

REQUIRE
  responsive web
  semantic HTML
  accessibility

PREFER
  CSS OVER JavaScript
  progressive enhancement
  native platform features

AVOID
  unnecessary dependencies
  unnecessary client state

FORBID
  client-side authorization

SEAMS
  only explicitly listed temporary substitutes are acceptable

APPROVAL
  HUMAN authentication changes
  HUMAN database migrations
  HUMAN new external services

DONE WHEN
  film submission works
  curation works
  discovery works
  responsive UI works
  tests pass
  deployment succeeds
```

## Recommended production workflow

Awen deliberately recommends **roles**, not a mandatory tool stack:

```text
creative workspace
      ↓
settled sources + project.awen
      ↓
version control / repository
      ↓
one chosen execution agent or production toolchain
      ↓
deterministic verification + declared human approvals
      ↓
artifact
```

For software, an optional `AGENTS.md` may provide repository-operating instructions to the coding agent. Awen may reference it, but does not depend on it. Heavier specification or planning systems may also be used downstream when a project genuinely needs them; they are not part of the default Awen workflow.

See [`TOOLS.md`](TOOLS.md) for the tool-selection philosophy.

## Repository contents

- [`AGENTS.md`](AGENTS.md) — canonical entrypoint and operating instructions for AI agents.
- [`SPEC.md`](SPEC.md) — Awen Lang v0.1 specification.
- [`WORKFLOW.md`](WORKFLOW.md) — how Awen fits between creative work and production.
- [`TOOLS.md`](TOOLS.md) — AI-agnostic tool roles, optional integrations and verification guidance.
- [`TEMPLATE.awen`](TEMPLATE.awen) — canonical starting template.
- [`examples/`](examples/) — small examples across software, book, video and data outputs.

## MVP status

Awen v0.1 intentionally requires **no Awen-specific tooling**. No parser or compiler is required to prove the idea: capable LLMs, agents and production systems can already read the assembly sheet directly.

Tooling should only be added after real use demonstrates that it removes friction or enables deterministic verification.

## Naming

**Awen** is the project. **Awen Lang** is the declarative assembly-sheet language. Files use the `.awen` extension.

## License

Apache License 2.0. See [`LICENSE`](LICENSE).
