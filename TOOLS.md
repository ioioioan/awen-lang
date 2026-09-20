# Tools and Awen

Awen does not require a particular AI, model, editor, repository host, framework or production tool.

Awen describes the committed production handoff. The creator chooses the tools appropriate to the output.

## Recommended tool roles

For most projects, keep the toolchain simple:

1. **Creative workspace** — explore, research, compare and refine the idea before committing to production.
2. **Source editor** — maintain the authoritative Markdown, data, scripts, references and other source material.
3. **Version control** — keep `project.awen` and its sources together under version history. Git is a sensible default but is not required by Awen.
4. **Execution agent or production system** — use one capable agent or toolchain to execute the assembly sheet. For software this may be a coding agent; for a book a writing agent; for video a set of generation and editing tools; for data an analysis or transformation environment.
5. **Deterministic verification** — prefer compilers, tests, linters, schemas, validators, checksums, CI and other objective checks wherever the output permits them.
6. **Human approval** — keep consequential decisions behind the `APPROVAL` boundaries declared by the creator.

Awen should not encourage users to collect tools for their own sake. Choose the smallest production toolchain that can satisfy the assembly sheet.

## AI and model independence

An Awen document should remain useful if the creator changes model, agent or vendor.

Prefer capability requirements over vendor names when the exact tool is not important:

```awen
TOOLS
  AGENT capable coding agent
  REASONING high
  MULTIMODAL required
```

If a named tool or model is itself a deliberate production decision, it may be locked explicitly:

```awen
TOOLS
  AGENT <chosen agent>
  IMAGE MODEL <chosen model>
```

The presence of a named model does not make Awen dependent on that vendor; it records the creator's chosen production component for that project.

## `AGENTS.md`

Software repositories may already contain `AGENTS.md` or another agent-specific instruction file. Awen can reference it without replacing it:

```awen
EXECUTION
  INSTRUCTIONS ./AGENTS.md
```

Use the distinction deliberately:

- `project.awen` describes **what is being assembled**, the governing sources, constraints, preferences, approvals and completion boundary.
- `AGENTS.md` or equivalent describes **how an agent should operate inside that repository**.

A project does not need `AGENTS.md` to use Awen.

## Heavier workflows

Awen does not require a specification framework, planning framework or multi-agent orchestrator.

If a project benefits from one, it may be used downstream of the assembly sheet. For example, a team could hand an Awen synthesis to an existing specification or planning workflow before implementation.

Do not add a heavier workflow merely because Awen can reference one. The default is direct handoff:

```text
project.awen
+ authoritative sources
        ↓
one chosen execution agent/toolchain
        ↓
artifact
```

## Production tools by output

Awen is cross-domain because it does not own the production stack.

- **Software:** coding agent + selected languages/frameworks + tests/CI.
- **Books:** writing/revision agent + manuscript/editorial tools.
- **Video:** image/video/audio generation + editing/compositing tools.
- **Data:** analysis/transformation environment + schema/validation tools.
- **Other outputs:** whatever tools are appropriate to the declared artifact.

The assembly sheet remains the portable handoff between the settled creative intent and those tools.
