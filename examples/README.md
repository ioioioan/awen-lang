# Examples

These examples are generic, illustrative handoffs. They are not runnable source packs unless you also create the referenced files.

1. [Hello World](hello-world.awen) — minimal software handoff.
2. [New Project](new-project.awen) — simple website with source authority.
3. [New Project refinement](new-project-refinement.awen) — change to an existing website.
4. [Book](book.awen) — manuscript editing.
5. [Video](video.awen) — short film.
6. [Data](data.awen) — dataset transformation.

## Using an example

1. Copy the chosen root example to `project.awen` in your project root.
2. Create or replace every referenced source file.
3. Remove placeholders and unused sections.
4. Ask the agent to read `project.awen` first.
5. Verify the output against `DONE WHEN`.

For an existing project, retain its root `project.awen` and list the refinement sheet as an `AUTHORITATIVE` source. A refinement cannot silently override the root contract. Missing files and conflicting authoritative decisions must be reported.

Awen does not automatically transfer context between agents. Each agent must read the same current repository revision.
