# Awen Lang v0.1 Specification

## 1. Purpose

Awen Lang is a small declarative domain-specific language for describing the assembly of AI-assisted outputs.

Its role is **post-ideation, pre-production**. It captures the creator's committed synthesis and points the production system at the exact supporting sources.

Awen is not a general-purpose programming language, prompt language, workflow engine or agent framework.

## 2. Design goals

A valid Awen document should be:

- understandable without specialist tooling;
- concise enough to include in agent context;
- explicit enough to reduce avoidable guessing;
- independent of any single model, vendor or agent;
- useful even when no Awen-specific parser exists;
- suitable for software, writing, video, data and other AI-assisted production;
- portable across capable models, agents and vendors;
- explicit about named tools only when tool choice is itself part of the committed synthesis.

## 3. File convention

Recommended filename:

```text
project.awen
```

Recommended encoding: UTF-8.

Paths are relative to `ROOT` unless explicitly documented otherwise.

## 4. Syntax philosophy

Awen uses section headings and indented declarations.

- Section names are uppercase keywords.
- Braces and semicolons are intentionally avoided.
- Free text is permitted where controlled vocabulary would add no value.
- Exact paths should be used when referring to files or directories.
- Awen should not imitate an implementation language.

Awen v0.1 is defined semantically rather than by a formal parser grammar. Future grammar work must preserve readability and backwards compatibility where practical.

## 5. Core sections

### `AWEN`

Declares the language version.

```awen
AWEN 0.1
```

### `REVISION`

Optional. Binds the handoff to a known project/source state such as a Git commit, tag or source-pack version.

```awen
REVISION <identifier>
```

Use this when stale or changing sources could make the handoff ambiguous.

### `PROJECT`

Human-readable project or artifact name.

```awen
PROJECT ZeroReel
```

### `OUTPUT`

Declares the primary artifact to be produced.

```awen
OUTPUT software MVP
```

Examples:

```awen
OUTPUT novel manuscript
OUTPUT short film
OUTPUT cleaned analysis dataset
OUTPUT slide presentation
```

### `ROOT`

Declares the project root for relative paths.

```awen
ROOT .
```

### `SOURCES`

Lists relevant source files or directories.

Recommended form:

```awen
SOURCES
  PRODUCT       ./docs/product.md       AUTHORITATIVE
  UX            ./docs/ux.md            AUTHORITATIVE
  RESEARCH      ./docs/research.md      CONTEXT
```

Each source has:

1. a **role** chosen by the creator;
2. an exact relative **path**;
3. an **authority** level.

Awen v0.1 defines two authority levels:

- `AUTHORITATIVE` — current settled source; production should follow it unless a conflict is explicitly escalated.
- `CONTEXT` — useful supporting material that must not override authoritative sources.

Source role names are intentionally open. Examples include `PRODUCT`, `UX`, `ARCHITECTURE`, `ENGINEERING`, `STYLE`, `STORY`, `SCRIPT`, `DATA`, `SCHEMA`, `CONTENT`, `RESEARCH`, `REFERENCE` and `AGENT`.

Source resolution rules:

- resolve relative paths against `ROOT`;
- do not invent or search for a replacement when an exact declared path is missing; surface the missing source;
- read `AUTHORITATIVE` sources as governing inputs and `CONTEXT` sources as supporting inputs;
- source ordering does not override authority;
- prefer precise files over broad directories when practical, to avoid unnecessary context ingestion.


### `IMPLEMENTATION`

Optional. Declares locations where produced or maintained implementation artifacts belong.

```awen
IMPLEMENTATION
  ROOT  ./src/
  TESTS ./tests/
  INFRA ./infra/
```

Use only when location matters. Do not prescribe arbitrary internal structure.

### `STACK`

Optional. Declares chosen technologies or production components.

```awen
STACK
  TypeScript
  PostgreSQL
  Azure
```

For non-software projects this may list production tools or required components.

### `TOOLS`

Optional. Declares required production capabilities or deliberately chosen tools, models, agents or production systems.

Prefer roles or capabilities when the specific vendor is not important:

```awen
TOOLS
  AGENT capable coding agent
  MULTIMODAL required
  EDITOR non-linear editor
```

Lock a named tool or model only when that choice is part of the creator's committed synthesis:

```awen
TOOLS
  AGENT <chosen agent>
  IMAGE MODEL <chosen model>
```

Awen is AI-agnostic by default. A named tool records a project decision; it does not make the Awen language dependent on that vendor.

Awen does not define model routing, API invocation or tool-specific command syntax in v0.1.

### `REQUIRE`

Non-negotiable production requirements.

```awen
REQUIRE
  semantic HTML
  accessibility
```

If a requirement cannot be satisfied, the executor should stop or escalate rather than silently weaken it.

### `PREFER`

Strong preferences that guide implementation when compatible with requirements.

```awen
PREFER
  CSS OVER JavaScript
  progressive enhancement
```

A preference may be overridden when necessary, but the executor should be able to explain why.

### `AVOID`

Choices that should normally not be introduced.

```awen
AVOID
  unnecessary dependencies
  unnecessary client state
```

### `FORBID`

Explicitly prohibited choices.

```awen
FORBID
  client-side authorization
```

The executor should not violate a `FORBID` declaration without human intervention.

### `APPROVAL`

Declares changes or decisions requiring human approval.

```awen
APPROVAL
  HUMAN authentication changes
  HUMAN database migrations
  HUMAN new external services
```

Approval declarations describe authority, not implementation mechanics. The consuming tool or workflow determines how approval is requested.

### `DONE WHEN`

Acceptance criteria for the output.

```awen
DONE WHEN
  submission works
  curation works
  tests pass
  deployment succeeds
```

Criteria should be concrete enough that a human or production system can assess completion.

### `NON-GOALS`

Optional. Explicitly excludes tempting scope.

```awen
NON-GOALS
  native mobile application
  recommendation engine in MVP
```

### `BLOCKERS`

Optional. Lists unresolved decisions that must not be guessed.

```awen
BLOCKERS
  payment provider not selected
```

A project intended for committed execution should ideally have no blockers.

### `EXECUTION`

Optional. References downstream operating instructions or an intentionally chosen production process without making Awen dependent on them.

```awen
EXECUTION
  INSTRUCTIONS ./AGENTS.md
```

For software, `AGENTS.md` or an equivalent file may describe how a coding agent should operate inside the repository. `project.awen` remains the assembly sheet describing what is being built, its governing sources and its production boundaries.

Specification frameworks, planning systems and multi-agent orchestrators are optional downstream tools. Awen v0.1 does not define or require any particular workflow engine. Direct handoff to one capable execution agent/toolchain is the default.

## 6. Conflict rules

Awen should not silently resolve genuine contradictions in the committed synthesis. If two authoritative declarations cannot both be true, the executor should surface the conflict and stop or escalate.

Where guidance overlaps without being directly contradictory, use this strength ordering:

1. `FORBID`
2. `REQUIRE`
3. `APPROVAL` boundaries
4. `AVOID`
5. `PREFER`
6. contextual source material

Authoritative sources should not contradict one another. If they do, the executor should surface the conflict rather than choose silently.

## 7. Model, tool and verification independence

Awen defines the production contract, not the execution vendor. An Awen document should remain meaningful if the production environment changes from one capable model, agent or toolchain to another.

Prefer capability statements over vendor names unless a vendor choice is itself part of the committed synthesis.

Preferred when the vendor is not important:

```awen
TOOLS
  AGENT capable coding agent
  REASONING high
```

Also valid when intentionally locked:

```awen
TOOLS
  AGENT <chosen named agent>
```

Additional rules:

- Tool choice should be omitted when irrelevant, expressed as a capability when possible, and named only when deliberately fixed.
- Git or another version-control system is recommended for keeping the assembly sheet and its sources together, but version control is not part of the language semantics.
- Deterministic verification should be preferred whenever the artifact permits it: compilers, tests, linters, schemas, validators, checksums, CI and equivalent objective checks.
- LLM review may supplement deterministic checks but should not replace them without reason.
- Human approval remains authoritative wherever `APPROVAL` declares it.

See `TOOLS.md` for non-normative tool guidance.

## 8. Progressive enhancement

Awen is designed for progressive enhancement:

1. Markdown and ordinary project files remain the baseline.
2. An `.awen` file adds a concise assembly contract.
3. LLMs can consume the contract directly.
4. Future tools may parse, validate, transform or verify it.
5. No project should become unusable merely because Awen-specific tooling is absent.

## 9. What belongs in sources

Sources may contain whatever the creator needs. Awen does not impose a universal documentation schema.

However, sources used for production should represent **current settled decisions**, not raw brainstorming history.

Typical authoritative source roles:

- product or artifact definition;
- structure and requirements;
- UX or presentation direction;
- architecture or production approach;
- data or schema definitions;
- style, tone or continuity rules;
- content or script;
- safety, compliance or quality constraints.

Research and inspiration are usually better marked `CONTEXT` unless deliberately promoted into the committed specification.

## 10. v0.1 non-goals

Awen v0.1 does not define:

- a parser;
- a compiler;
- an execution runtime;
- model routing;
- a package manager;
- a workflow engine;
- a plugin ecosystem;
- vendor-specific agent commands;
- a universal ontology for creative work.

These should only be introduced after real projects show that they remove friction or improve precision.
