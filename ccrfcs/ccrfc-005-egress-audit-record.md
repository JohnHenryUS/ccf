# Cognitive Commons Framework - CCRFC 005 - Egress Audit Record

CCRFC-Checksum: a1eba2f2ae19fdc8035432054c2f0e0a769830b60798ab8d3b236121dd3bbcc7
Status: Final. Version: 1. Date: 2026-10-18.

## Abstract

This document defines the egress audit record of the Cognitive Commons Framework: the user-readable export of what left the user's boundary, when, and to whom. It specifies export formats, the record's honest scope (accounting, not proof of non-use), tamper-evidence requirements, the caution that the export is itself a sensitive artifact, and the placement of self-auditing inside the trust boundary.

## 1. Introduction

Controls without audit are theater. The framework therefore requires a complete, legible egress record: not a compliance-theater download in an arcane format six weeks later, but an export in formats the user chooses from the boring commons, human-readable and immediately useful. The power inversion is deliberate: the user's system defines the export standard, and data consumers adapt.

## 2. Conventions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

## 3. Export formats

The egress record MUST be exportable in markdown, sqlite, and csv — formats readable without the provider's tooling. The user chooses which; implementations MUST support all three. Exports SHOULD be generatable on demand, not gated behind request queues or waiting periods.


## Canonical serialization

All machine-readable artifacts in this framework - tier labels, flags, profiles, report bodies, egress records, condensed initializations - use one canonical form: JSON with sort_keys, separators (",",  ":"), UTF-8 encoding, no trailing whitespace, LF line endings. This is the same canonicalization the checksums (ccrfc_checksum, report_checksum, hash-chain links) are computed over: what hashes is what travels. Implementations MUST serialize in this form and MUST accept it; human-readable renderings MAY differ but MUST round-trip through the canonical form without loss.
## 4. Record contents

Each egress record MUST capture, at minimum: what left the user's boundary, when it left, and to whom it went. Records MUST be tamper-evident and user-inspectable. The canonical tamper-evidence method is hash-chaining: each record carries the sha256 of the canonical JSON of the previous record, forming an append-only chain any gap in which is detectable. The status-code vocabulary (CCRFC-003) SHOULD be used in records so that entries are both machine-parseable and human-readable (e.g., "202 raised, user chose hold").

## 5. Honest scope

No export proves the negative. No log can prove "we didn't use your data" — unprovable in principle. The egress record provides proof of accounting, not proof of non-use: a complete, legible account of what left, when, and to whom. Implementations MUST NOT represent the record as proof that data was never used. You can't audit what you can't read, which is exactly why arcane exports are a failure mode.

## 6. The export is itself an artifact

Legibility is symmetric: the same file that lets the user audit their egress makes a breach, subpoena, or seizure maximally productive. Information-shaped data is fungible. The export MUST therefore live user-side, encrypted at rest, with the key in the user's hands — the user's opsec, the user's responsibility, like any file they own. The tier gradient holds for the export itself: SO and CO manage exposure, but NK — and above it, NT — is the only direction with zero downstream risk.

## 7. Self-auditing inside the trust boundary

The system audits its own flows: what left, what was used, whether handling matched the flag. But the gatekeeper paradox applies: an auditor that decides what flows must see everything it gates. Run the auditor in the cloud and you have built surveillance that happens to do compliance — it sees the flagged content, and knowledge in a third party's hands creates duty. The auditor MUST therefore run inside the user's trust boundary (on the user's hardware on the local track; within the user's own account boundary on the cloud track), reporting to the user, who was always going to know their own disclosures. The seeing was never the problem; the address of the seeing was. This is a user-provided variable: the user designates which account is theirs (provider account ID, org, or device); the auditor runs inside that boundary wherever the user points it.

## 8. Open questions

- **OPEN QUESTION:** RESOLVED Oct 18 — hash-chaining is the canonical tamper-evidence method (§4). Each record carries the sha256 of the previous record's canonical JSON; any gap is detectable.
- **OPEN QUESTION:** The exact record schema — field names, types, and required versus optional fields beyond the "what, when, to whom" minimum — is not specified. This is a user-provided variable in part: the what/when/to-whom minimum plus hash-chain link are normative (section 4); additional fields are user-chosen export preferences carried in the profile.
- **OPEN QUESTION:** On the cloud track, the precise definition of "the user's own account boundary" for auditor placement (Section 7) needs elaboration, particularly for providers whose infrastructure the user cannot inspect. This is a user-provided variable: the user designates which account is theirs (provider account ID, org, or device); the auditor runs inside that boundary wherever the user points it.

### Deletion acknowledgment

Forget-me acknowledgment is a record event: what was deleted, when, scope. Guarantee is deletion-plus-receipt, not the negative of cold backups, old logs, trained weights.

## 9. License

This document is released under the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0/).
