# Feedback Log

## FB-001 — Primary film playback path is contradictory

- Status: `RESOLVED`
- Found during: ZeroReel MVP implementation
- Found at revision: `example-pre-resolution`
- Reported by: build agent
- Affected paths: `docs/product.md`, `docs/ux.md`, `project.awen`
- Type: `CONTRADICTION`
- Severity: `BLOCKING`

### Observation

The product source can be read as sending viewers to an external platform, while the UX source presents playback on the ZeroReel film page. Both cannot define the primary path.

### Evidence

The implementation cannot choose the film-page interaction without privileging one authoritative source over another.

### Proposed resolution

Embed the externally hosted player on the film page when permitted. Retain the original external URL as provenance and fallback.

### Evaluation

The proposal preserves ZeroReel as a discovery and viewing surface without copying or hosting video. It also preserves attribution and handles providers that prevent embedding.

### Outcome

- Decision: `RESOLVED`
- Decision record: `DEC-001`
- Resulting revision: `example-post-resolution`
- Verification: film page tested with embeddable and non-embeddable sources
