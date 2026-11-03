# Complete New Project example

This is a complete **handoff source pack**, not a prebuilt application. It includes the Awen sheet and every declared source document; an agent must still write and test the application.

1. Copy this directory to a new workspace, retaining the directory structure.
2. Ask a coding agent: "Read project.awen and its declared sources, then implement and verify the build."
3. Review the resulting src/ and tests/ against DONE WHEN.
4. For a subsequent change, add the line `REFINEMENT ./refinements/add-filter.awen AUTHORITATIVE` to the root sheet's SOURCES, then instruct the agent to start with project.awen again.
5. Remove that line when the change is incorporated into the root requirements and no longer needs a separate change sheet.

The named refinement file demonstrates why a descriptive filename can coexist with a standard root entrypoint. The root sheet stays the discovery point; the named sheet defines a scoped change. The refinement is **not active by default**.

The local-storage seam is intentional. There is no claim that this example has been independently executed or benchmarked against ordinary Markdown instructions.
