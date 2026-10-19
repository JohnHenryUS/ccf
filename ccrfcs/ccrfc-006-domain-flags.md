# Cognitive Commons Framework - CCRFC 006 - Domain Flags

CCRFC-Checksum: 9e2f10eb0b2416c60fe3b99c82b6cda7536c149aa5429c9bc51d3160809a877e
Status: Final. Version: 1. Date: 2026-10-18.

## Abstract

This document defines graduated domain flags: the mechanism by which the framework handles sensitive domains of applied cognition over time. It specifies the three handling rungs (friction, mode restriction, hard line), the rule that flags are proposed by the system and confirmed by the user, and the compact mode encoding that keeps per-interaction boundary negotiation to a few bytes.

## 1. Introduction

Content classes (CCRFC-002) categorize what content is; domains track how the system should handle sensitive areas of ongoing cognition — sex, medical, financial, legal, and kin. Handling is graduated, not binary: most domains need friction or a change of register, not a wall. Domain flags develop over time as the system learns which domains the user treats as private, telemetry, or open-season.

## 2. Conventions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

## 3. The three rungs

Each flagged domain carries a handling mode on the graduated ladder:

1. **Friction.** Nudge awareness; change nothing else. Example: "Reminder: you're in public."
2. **Mode restriction.** The system discusses the domain factually, not experientially — clinical-only register. This is not disapproval; it is a different register.
3. **Hard line.** Legal, non-negotiable, and honest about why it is non-negotiable.

Only the third rung is enforcement; the first two are friction. The moral verdicts stay with the human; the system supplies friction, never judgment.

## 4. Proposal and confirmation

Domain flags MUST be proposed by the system and confirmed by the user. Flags MUST NOT be imposed: an imposed flag is paternalism with extra steps. The user MAY accept, reject, or adjust any proposed flag, and MAY set flags directly without a proposal. Boundaries MUST be posted before the maze: no user should discover a line by colliding with it. New domain IDs follow the same rule as CCRFC-002 §5: self-describing, no central assignment, unknown means most-private automatically. Any proposal that would loosen handling MUST NOT be made unilaterally; the provider MUST propose it to the user with full transparency and MUST get user auth with active opt-in required for each handling case.

## 5. Encoding

Each domain is identified by a domain ID, and its handling mode is encoded compactly: `[domain_id][mode]`. A verbose policy sentence (e.g., "talks about $SUBJECT only in clinical terms; attempting direct engagement may violate TOS in this domain; clinical, medical, and academic discussion allowed for informative and educational purposes") is a template over this encoding. The entire per-interaction boundary negotiation costs a few bytes. The space covers five to twelve large-scale domains; the domain space extends by ID.

## 6. Interaction with tiers and classes

Domain flags operate alongside content classes (CCRFC-002) and handling tiers (CCRFC-001), not as a second system: they are the same vocabulary applied at a different scope. Where a domain flag and a class tier conflict, the conflict MUST resolve to the most private position, per CCRFC-001 Section 7.

## 7. Open questions

- **OPEN QUESTION:** The canonical list of the five to twelve large-scale domains is not specified; only examples (sex, medical, financial, legal) are given. A standard domain list with assigned IDs is needed. This is a user-provided variable: the user confirms which domains are flagged from system proposals; the examples (sex, medical, financial, legal) are starting points, not a closed list.
- **OPEN QUESTION:** The mode encoding is compact (a few bytes) but the exact width and code-point assignments are unspecified. Only three rungs are defined; whether remaining code points are reserved, and for what, is unspecified. This is a user-provided variable in effect: the three rungs (friction, mode restriction, hard line) are normative; remaining code points are RESERVED for future rungs and MUST NOT be assigned by implementations - until assigned by a later CCRFC, unknown codes mean most-private.
- **OPEN QUESTION:** RESOLVED Oct 12, confirmed Oct 18 - same rule as CCRFC-002 section 5: self-describing domain IDs, no central assignment, collisions avoided by namespacing, unknown means most-private automatically.

## 8.] d under the [Apache License, Versi] ] ] ] on 2.0](https://www.apache.org/licenses/LICENSE-2.0/).
