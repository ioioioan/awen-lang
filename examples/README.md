# Examples

All examples use generic project names. The complete-project directory contains its declared source documents, but no generated application. The other examples are illustrative and may require you to create referenced files.

1. [Complete New Project handoff](complete-project/README.md) — full source pack, numbered build tasks, acceptance checks and a named refinement sheet.
2. [Hello World](hello-world.awen) — minimal software handoff.
3. [New Project](new-project.awen) — simple website with source authority.
4. [New Project refinement](new-project-refinement.awen) — change to an existing website.
5. [Book](book.awen) — manuscript editing.
6. [Video](video.awen) — short film.
7. [Data](data.awen) — dataset transformation.

## Using an example

1. Copy the chosen root example to `project.awen` in your project root.
2. Create or replace every referenced source file.
3. Remove placeholders and unused sections.
4. Ask the agent to read `project.awen` first.
5. Verify the output against `DONE WHEN`.

For the complete example, follow its own README rather than copying a single file. For an existing project, retain its root `project.awen` and list the refinement sheet as an `AUTHORITATIVE` source. A refinement cannot silently override the root contract. Missing files and conflicting authoritative decisions must be reported.

Awen does not automatically transfer context between agents. Each agent must read the same current repository revision.
