# Cognitive Commons Framework - CCRFC - Unknown Handling and Discovery

CCRFC-Checksum: cbf7dbe55c9d7a79bd91e982995e760ef77a2cf66d1cf221d3e63f5479e14048
Status: Draft. Version: 0.1. Date: 2026-10-19.
Updates: CCRFC-002, CCRFC-003, CCRFC-006

## Abstract

This document closes two gaps in the founding set: graceful handling of unrecognized identifiers and discoverability of newly minted identifiers without a central authority. It specifies fail-closed enforcement with loud hold-and-ask, the two-question solicitation flow, collision handling by checksum, discovery without authority, and status-code class fallback. It Updates CCRFC-002, CCRFC-003, and CCRFC-006 without contradicting them.

## 1. Introduction

Anyone MAY mint a new class, domain, or code with a self-describing ID and no permission, and any receiver MUST enforce most-private on what it does not know, but enforcement without negotiation turns openness on paper into silent rejection on the wire, which is the opposite of what this framework claims, so this document defines the loud loop that makes extensibility real: halt the payload, hold the interaction, tell the user, ask twice, bump the profile, retry.

## 2. Conventions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

## 3. Three unknowns

Unknown class or domain IDs, unknown status codes, and unknown protocol versions are distinct cases and MUST NOT be conflated into a single token type, because each travels in a different place and fails in a different direction, and CCRFC-003 already splits versions into major-breaking versus letter-additive while leaving status codes beyond 202 as deferred classes by design.

## 4. Enforcement stays fail-closed

On encountering an identifier the receiver cannot resolve against embedded core definitions, local cache, or the user profile, the receiver MUST halt before reading the payload, MUST NOT buffer the remainder, MUST NOT log partial content, and MUST NOT peek at the payload to classify it, per CCRFC-003 Section 3, and the payload MUST be returned to the sender with zero content processed.

## 5. Failures must be loud

Receivers MUST NOT silently drop, silently reject, or silently clamp an unknown identifier, because a silent failure leaves a hole in the user's policy the user cannot see and leaves the minter with no path to interoperability, so every halt MUST produce a user-visible hold notice in plain language naming the string encountered and the claimant where determinable, and MUST produce an audit event with zero payload bytes per CCRFC-005.

## 6. Two-question solicitation

Evaluation of the tag and evaluation of its application are two different questions and MUST NOT be inferred from one another, so the hold notice MUST solicit both separately: first what tier the user assigns to this identifier going forward, and second whether the user accepts this specific application of it right now, and a valid tag misapplied is still a violation while an unknown tag correctly applied still halts until the user decides.

## 7. Collisions

Where the same reverse-DNS identifier arrives with a different document checksum than one already carried, both exist per CCRFC-000 Section 3, and the receiver MUST hold, MUST show the user both claimants with store-plus-checksum and first-seen dates as precedence evidence without authority, MUST NOT auto-overwrite, and MUST record the user's winner as a profile change with a version bump.

## 8. Discovery without authority

A minter that wishes to be found SHOULD publish a human-readable definition at a predictable URI derived from its reverse-DNS name, but no receiver MAY require that URI to enforce, enforcement runs on local knowledge only, any fetch is display-label only and out-of-band and MUST NOT delay enforcement, offline nodes MUST NOT fetch, fetch timeouts are local policy and carry no normative value, and any discovered definition MUST carry its document checksum so collisions are detectable.

## 9. Status-code fallback

Receivers MUST parse the class digit and never require the exact code, so a known 2xx the receiver recognizes proceeds with notice per CCRFC-003, an unknown 2xx MUST NOT proceed and MUST be treated as hold, an unknown 4xx or 5xx MUST be treated as hold plus audit in CCRFC-003 vocabulary, and an unknown leading digit MUST be treated as provider limitation with fail-closed hold, all loud to the user and never silent.

## 10. Inline hints are transport not trust

A profile or condensed initialization MAY carry an inline hint describing a non-core identifier for zero-round-trip display, but receivers MUST NOT enforce off the hint, enforcement remains most-private until the user confirms, and a hint that carries the definition checksum is preferred because it makes collision detection immediate.

## 11. Audit

Every unknown-encounter halt MUST emit a hash-chained egress-audit event per CCRFC-005 naming what was encountered, when, to whom the hold was returned, and which action was taken, with zero payload bytes, and implementations MUST NOT represent the entry as proof of non-reading because no export proves the negative and the record provides proof of accounting only.

## Canonical serialization

All machine-readable artifacts in this framework - tier labels, flags, profiles, report bodies, egress records, condensed initializations - use one canonical form: JSON with sort_keys, separators (",", ":"), UTF-8 encoding, no trailing whitespace, LF line endings. This is the same canonicalization the checksums (ccrfc_checksum, report_checksum, hash-chain links) are computed over: what hashes is what travels. Implementations MUST serialize in this form and MUST accept it; human-readable renderings MAY differ but MUST round-trip through the canonical form without loss.
## 12. Open questions

- **OPEN QUESTION:** Whether specific code assignments such as 428 for bootstrap or 209 for delta challenge should be adopted is not decided here; Section 9 defines class behavior only and any specific assignments require a separate proposal.
- **OPEN QUESTION:** The exact predictable URI shape for voluntary definitions under Section 8 is not specified; reverse-DNS to well-known path is a candidate and needs agreement.
- **OPEN QUESTION:** The exact user-interface wording for the hold notice and the two-question prompt is not specified; plain language naming the string and claimant is normative and phrasing is implementation choice.
- **OPEN QUESTION:** Precedence weighting of first-seen dates versus tally counts versus user explicit choice in collision display order is not specified beyond use-decides per CCRFC-000.

## 13. License

This document is released under the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0/).
