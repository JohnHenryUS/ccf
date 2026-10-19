# Cognitive Commons Framework - CCRFC 004 - Portable Profile

CCRFC-Checksum: ca1745ada752d0722ada9319cc7d0a50bda58e4f8ecf09508ca7adc0ecfbe7b0
Status: Final. Version: 1. Date: 2026-10-18.

## Abstract

This document defines the portable personal AI interaction profile: the user-held record of handling choices that is set up once and carried across providers. It specifies the profile's contents, its custody requirements, the lightweight verification pattern for new providers, and the rule that ambiguity always resolves to most-private.

## 1. Introduction

If every provider redefines the user's privacy choices, each new service is a new vocabulary to learn — a dark pattern in itself. The portable profile solves this: the user completes one serious pass through the full setup, no skipping, and carries the resulting profile across providers. Each new platform does not redefine the profile; it receives it and confirms.

## 2. Conventions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

## 3. Profile contents

A conformant profile MUST be capable of carrying all of the following:

- Per-class handling choices: the tier assigned to each content class (CCRFC-001, CCRFC-002).
- Domain flags, learned over time: private / telemetry / open-season designations per domain (CCRFC-006).
- The label vocabulary (UF/SO/CO/NK/NT) as the machine-readable layer.
- Default cloud profile: disclosure levels for cloud contexts generally.
- Local endpoint map: which models exist at which privacy level — the map the status codes check against.
- Export preferences: the user's chosen export formats (markdown, sqlite, csv).


## Canonical serialization

All machine-readable artifacts in this framework - tier labels, flags, profiles, report bodies, egress records, condensed initializations - use one canonical form: JSON with sort_keys, separators (",",  ":"), UTF-8 encoding, no trailing whitespace, LF line endings. This is the same canonicalization the checksums (ccrfc_checksum, report_checksum, hash-chain links) are computed over: what hashes is what travels. Implementations MUST serialize in this form and MUST accept it; human-readable renderings MAY differ but MUST round-trip through the canonical form without loss.
## 4. Custody

The authoritative profile MUST be user-held, in boring standard formats, on the user's hardware or device. A provider MAY hold a convenience cache with user permission, but the cache MUST be verbatim, MUST use standard formats with no proprietary extensions, MUST NOT be modified unilaterally, MUST be deletable on demand, and MUST NOT be treated as authoritative or exclusive. The full profile is exchanged once, on first contact; what travels per interaction after that is a condensed initialization carrying identity, protocol version, flags, and profile version plus hash (CCRFC-003). On match the provider enforces from cache; on mismatch it MUST delete the cached copy and refetch. On-demand delete MUST be honored immediately with acknowledgment. A cached copy MUST be treated as mismatched — deleted and refetched — once it is older than 30 days, even if version and hash match. The user MAY set a shorter lifetime, down to forget-after-each-session; the provider MUST honor the shorter setting. Forget-after-each-session MUST be opt-in, never default.

Proposals to add or change flags MUST be presented to the user for accept or reject. Acceptance is a profile change: the authoritative copy version MUST bump, and the new version propagates on next contact via the condensed init. Any proposal that would loosen handling — wider sharing, lower tier, open-season marking — MUST NOT be made unilaterally; the provider MUST propose it to the user with full transparency and MUST get user auth with active opt-in required for each handling case.

## 5. Verification on new providers

When the user presents their profile to a new provider, the provider MUST NOT require full re-onboarding. The provider presents the received profile and confirms with the user — "still this one?" — a lightweight verify, not a second setup. The provider MUST disclose any handling it cannot honor before the user commits content to it.

## 6. Ambiguity resolves to most-private

Any ambiguity in profile interpretation — missing fields, unrecognized classes, conflicting scopes — MUST resolve to the most private available handling. This rule is what makes post-setup laziness safe by construction: the user can set the profile once and stop thinking about it, because every uncertain case defaults to maximum restriction.

## 7. Open questions

- **OPEN QUESTION:** The structure of the local endpoint map is not specified: how endpoints are identified, what privacy-level attestations they carry, and how the map is kept current are undefined. This is a user-provided variable: the user's own device inventory defines endpoints and their privacy attestations; until populated, no local endpoint is assumed and cloud-hold applies.
- **OPEN QUESTION:** RESOLVED Oct 18 - canonical serialization (new section, this document) governs: canonical JSON; boring standard formats for storage, canonical form for exchange and hashing.
- **OPEN QUESTION:** RESOLVED Oct 18 — the condensed initialization is defined once in CCRFC-003 §4 (identity, protocol_version, flags, profile_version plus profile_hash, canonical JSON). This CCRFC references that definition; no second definition is needed or permitted.

### Client memo per provider

The client holds per-provider memo: last report seen, hash, timestamp, local overrides. Clear per-provider or all at once, anytime. The server declares; the client decides what to remember.

### Arbiter rule

On forget-me the provider deletes the cache and acknowledges. Next contact is first contact. New-person requires new version, and new identity for unlinkability. Same ID plus fresh profile only signals changed settings.

## 8. License

This document is released under the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0/).
