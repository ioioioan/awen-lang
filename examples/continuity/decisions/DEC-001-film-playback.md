# DEC-001 — Film playback uses approved external embeds

- Status: `ACCEPTED`
- Date: `2026-10-14`
- Decision owner: project owner
- Related feedback: `FB-001`
- Governing revision: `example-pre-resolution`

## Context

Authoritative product and UX sources left the primary viewing path contradictory.

## Decision

ZeroReel does not host or copy video. The film page embeds the external player when the provider permits it. The original external URL remains visible as provenance and fallback, but it is not the primary viewing path when an approved embed works.

## Rationale

This preserves the intended film-page experience while respecting external hosting, attribution and provider restrictions.

## Consequences

- Film pages require provider-aware embed handling.
- Unsupported or blocked embeds fall back to the original source link.
- ZeroReel does not acquire or imply ownership of the underlying video.
- The wider discovery and attribution model remains unchanged.

## Authoritative sources updated

- `docs/product.md`
- `docs/ux.md`
- `docs/architecture.md`

## Assembly-sheet impact

`UPDATED`

The primary and fallback behaviours are now explicit under `BEHAVIOR`.

## Verification

Test at least one permitted embed, one blocked or unsupported source and the visible provenance link.

## Supersedes

None.
