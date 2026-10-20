# Cognitive Commons Framework - CCRFC - Format Open Questions Discipline

CCRFC-Checksum: 6de126818cc0be37d57c77369e2f24035b23ae21db4d6ca926baa299f4280db4
Status: Draft. Version: 0.1. Date: 2026-10-20.
Updates: CCRFC-000

## Abstract

This document clarifies CCRFC-000 Section 8 with one distinction: open means genuinely undecided, delegated means decided-by-delegation to the user, resolved means decided, and a section stating none open is compliant. It Updates CCRFC-000 without contradicting it and changes no existing checksum.

## 1. Introduction

CCRFC-000 Section 8 requires every CCRFC to carry an Open questions section and to mark ambiguity rather than bury it, and that requirement is correct, but it never states what counts as open, so resolved history and delegated closes accumulate under the heading and read as undone work, which punishes finishing and manufactures false todos, so this document defines the three states and permits the empty honest section.

## 2. Conventions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

## 3. Three states

Every item that could appear in an Open questions section is in exactly one of three states: open means genuinely undecided and awaiting a future decision, delegated means decided by assigning the decision to the user as a user-provided variable with most-private as the default until set, and resolved means decided with the decision recorded in the document body. Delegated is closed. Resolved is closed. Only open is open.

## 4. The honest empty section

A CCRFC with no open items MUST still carry the Open questions section per CCRFC-000 Section 8, and the section stating no open questions is compliant. The section MUST NOT be filled with resolved history or delegated closes to satisfy a perceived requirement that it be non-empty. Resolved history belongs in the body. Delegated closes belong in the body as user-provided variables. The Open questions section lists open items only.

## 5. No other change

This document changes nothing else in CCRFC-000. The section requirement stands. The mark-ambiguity rule stands. Citation, checksum, succession, and filing rules are untouched.

## Canonical serialization

All machine-readable artifacts in this framework - tier labels, flags, profiles, report bodies, egress records, condensed initializations - use one canonical form: JSON with sort_keys, separators (",", ":"), UTF-8 encoding, no trailing whitespace, LF line endings. This is the same canonicalization the checksums (ccrfc_checksum, report_checksum, hash-chain links) are computed over: what hashes is what travels. Implementations MUST serialize in this form and MUST accept it; human-readable renderings MAY differ but MUST round-trip through the canonical form without loss.
## 6. Open questions

None open.

## 7. License

This document is released under the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0/).
