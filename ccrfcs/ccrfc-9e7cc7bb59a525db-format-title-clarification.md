# Cognitive Commons Framework - CCRFC - Format Title Clarification

CCRFC-Checksum: 9e7cc7bb59a525db656e62dcace5e9d75546b6dbeca7a7fc0d1fbd854c590244
Status: Draft. Version: 0.1. Date: 2026-10-20.
Updates: CCRFC-000

## Abstract

This document clarifies CCRFC-000 Section 3.0 with one rule and one encouragement: document titles MUST NOT contain hash-derived text, and authors SHOULD survey well-known stores before filing a slug. It Updates CCRFC-000 without contradicting it and changes no existing checksum.

## 1. Introduction

CCRFC-000 Section 3.0 hashes every byte of a document except the checksum line itself, and that includes the title line, so a title containing its own hash can never close: new title changes the bytes, new bytes change the hash, new hash changes the title, and the roundtrip fails forever, which is why the title MUST be hash-free in the same way the checksum line is blanked for computation.

## 2. Conventions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

## 3. Titles are hash-free

The title line of every CCRFC MUST NOT contain hash-derived text: no full checksum, no short slice, no prefix of either, because the title is hashed per CCRFC-000 Section 3.0 and a title containing its own hash cannot roundtrip. Founding documents keep their frozen numbers in the title. New documents use a numberless title of the form "Cognitive Commons Framework - CCRFC - <slug>". Filenames MAY carry the short slice per CCRFC-000 Section 3.0 because filenames are local only and never hashed.

## 4. Slugs are spoken, hashes are checked

Citation is CCRFC <slug>, disambiguated by short slice only on collision. Words instead of numbers. The slug is what humans say out loud. The checksum is what machines verify. Same document, two jobs. Where the same slug names different documents, both exist per CCRFC-000 Section 3, the cite gains a :short8, and the full checksum decides.

## 5. Survey before filing

Authors SHOULD survey tallies, crawlers, and well-known stores before filing a slug, and MUST accept disambiguation on collision. No rejection, no gatekeeper, just a longer name for the loser. Neglect still does the work.

## Canonical serialization

All machine-readable artifacts in this framework - tier labels, flags, profiles, report bodies, egress records, condensed initializations - use one canonical form: JSON with sort_keys, separators (",", ":"), UTF-8 encoding, no trailing whitespace, LF line endings. This is the same canonicalization the checksums (ccrfc_checksum, report_checksum, hash-chain links) are computed over: what hashes is what travels. Implementations MUST serialize in this form and MUST accept it; human-readable renderings MAY differ but MUST round-trip through the canonical form without loss.
## 6. Open questions

- **OPEN QUESTION:** Precedence weighting of first-seen dates versus tally counts versus user explicit choice in slug collision display order is not specified beyond use-decides per CCRFC-000.
- **OPEN QUESTION:** Whether per-store local numbers as pure display should supplement slug citation is not decided here; slugs plus short-on-collision is sufficient for v1.

## 7. License

This document is released under the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0/).
