# Awen Workflow

Awen begins when ideation is ending.

## 1. Explore

Use chats, workspaces, notebooks, prototypes, research and discussion freely.

At this stage contradictions, abandoned ideas and experiments are normal.

## 2. Commit

Before production, decide what is actually being made.

Resolve the important choices:

- intended output;
- authoritative sources;
- chosen stack, tools or production approach;
- core user or artifact behaviour;
- hard requirements;
- preferences and tradeoffs;
- forbidden choices;
- acceptable MVP seams or temporary substitutes;
- approval boundaries;
- completion criteria;
- pre-written content that must remain verbatim.

Do not ask the production agent to rediscover decisions that the creator has already made.

## 3. Assemble

Create `project.awen` from the committed synthesis.

The assembly sheet should be short enough to inspect in one sitting and precise enough that an unfamiliar capable AI can understand the build without reading the entire creative history.

Attach only the relevant source files.

```text
workspace history
       ↓ synthesis
project.awen
+ selected sources
       ↓
production
```

Before handoff, check five ambiguity hotspots:

1. **Behaviour** — is the real user/artifact experience explicit, including primary versus fallback paths?
2. **Reality versus seam** — which integrations or outputs must be real now, and which temporary substitutes are explicitly acceptable?
3. **Inputs** — do seed/demo/fixture inputs actually exercise the real behaviour they are meant to validate?
4. **Content** — is any pre-written copy, script or manuscript required verbatim?
5. **Blockers** — has every unresolved decision been surfaced instead of left for the executor to guess?

## 4. Execute

Give the assembly sheet and sources to the chosen AI, agent or production tool.

For software this may be a coding agent.
For a book it may be a writing model or agent.
For video it may be a sequence of image, video, audio and editing systems.
For data it may be an analysis or transformation agent.

Awen does not prescribe the execution system. Choose the smallest capable toolchain for the output. For a simple software MVP, the default should usually be one coding agent rather than unnecessary multi-agent orchestration.

## 5. Verify with the strongest available mechanism

Prefer deterministic checks when the medium supports them. For software this can include compilation, tests, linting, schemas and CI. For data it can include schema validation, reproducibility checks and provenance. Creative outputs may rely more heavily on declared review and approval criteria.

LLM review can supplement these checks, but Awen should not turn subjective model judgement into a substitute for objective verification when objective verification exists.

Where an MVP relies on seed/demo/fixture data, use inputs that are semantically valid for the real behaviour unless the assembly sheet explicitly allows placeholders.

## 6. Escalate instead of guessing

The executor should surface:

- conflicts between authoritative sources;
- unmet `REQUIRE` or `BEHAVIOR` declarations;
- attempted `FORBID` violations;
- undeclared substitution of real behaviour with a mock, stub or placeholder;
- `APPROVAL` items;
- unresolved `BLOCKERS`;
- missing `VERBATIM` source content.

## 7. Finish against the assembly sheet

Use `DONE WHEN` as the completion boundary.

A production pass is complete when the declared output exists and the acceptance criteria are satisfied or explicitly waived by the creator.

## 8. Update deliberately

If the committed intent changes, update the authoritative sources and `project.awen` deliberately.

The assembly sheet is not a transcript of every production decision. It is the current contract for what should be made.

## The core transition

> **Vibe freely. Commit deliberately. Build precisely.**

Awen is the handoff between creative synthesis and craft.

## Tool interoperability

Awen is designed to travel across execution environments. The same `project.awen` and authoritative sources should remain useful when moving between capable agents or production systems.

For software, repository-specific operating guidance may live in `AGENTS.md` or another tool-specific file and be referenced through `EXECUTION`. Awen does not replace those files; it gives them a stable production contract to execute against.

Heavier planning or specification frameworks are optional. Use them only when they reduce risk or friction for the project. The default Awen workflow remains direct and lightweight.
