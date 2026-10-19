# Cognitive Commons Framework - CCRFC 000 - CCRFC Format and Conventions

CCRFC-Checksum: 313170ba0e84a0ee2598891cf2e5b7eaa56615d27ebfc0aae7badaa77f990359
Status: Final. Version: 1. Date: 2026-10-18.

## Abstract

This document defines the shape of Cognitive Commons Framework CCRFCs: the required header block, normative language conventions, formatting rules, and the open-questions discipline. Every CCRFC MUST conform to this document.

## 1. Introduction

A standard is only as legible as its documents. This CCRFC exists so that every CCRFC is recognizable, comparable, and implementable — same header, same normative vocabulary, same honesty about what is undecided.

The name is deliberate homage to the original RFC ethos: notes, numbered so people can point at them, carrying zero authority. CCRFC numbers confer no rank and no approval; anyone may publish one. CCRFCs claim no standing in the IETF series and derive no validity from the association — only from the method, and from whether the mechanism works.

There is no acceptance process. A CCRFC is canon if and only if profiles carry its identifiers and providers honor them — observable, not decidable. Unused CCRFCs are not rejected; they are simply never displayed. Neglect does the work.

## 2. Conventions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

## 3. Header block

Every CCRFC MUST open with the following, in order: the title in the form "Cognitive Commons Framework - CCRFC NNN - <title>", a CCRFC-Checksum line (blank until computed, then filled), a Status line, a Version line, and a Date line. Example:

Cognitive Commons Framework - CCRFC 001 - Handling Tiers

CCRFC-Checksum:
Status: Final. Version: 1. Date: 2026-10-18.

Numbering is three-digit, sequential, and assigned in the order CCRFCs are drafted. Numbers MUST NOT be reused. CCRFC-000 through CCRFC-006 are the founding set; their numbers are frozen nicknames. No CCRFC-007 or higher SHALL be assigned. All CCRFCs after the founding set are identified by checksum only.

### 3.0 Content addressing: the ccrfc_checksum

Every CCRFC names itself. The canonical identifier is the `ccrfc_checksum`: the lowercase hex sha256 of the canonical bytes of the document.

Canonical bytes: UTF-8, LF line endings, no trailing whitespace on any line, exactly one trailing newline at end of file. The `CCRFC-Checksum:` header line itself is blanked (value removed, key kept) for the computation, then filled in. Everything else — including `Updates:` and `Supersedes:` lines — is included. Change the claim, new document, new checksum.

Compute it anywhere: `sha256sum` over the normalized file on any platform, or the equivalent one-liner. Same bytes in, same 64 hex characters out, everywhere, forever. No registrar, no counter, no coordination.

The full 64-character checksum is the normative ID. A leading prefix (16 hex recommended) MAY be used as a display short; if the short collides, extend it until it does not. Slugs and titles are hints for humans, not identifiers — two documents MAY share a slug and disambiguate by checksum.

Filenames are local only, not protocol. Recommended form: `ccrfc-<short>-<slug>.md`. Never 64-character filenames.

The founding set keeps its numbers as frozen nicknames alongside checksums. New filings pick a slug, the store checks local uniqueness of the filename only, and the checksum does the rest. Same slug in two stores for different documents: both exist; cite store-plus-checksum when pointing must be unambiguous; use decides which one lives.

The Date line is the author's claim. First-seen is the store's observation. They are different jobs; a store index SHOULD record first-seen dates as precedence evidence without touching the document.

### 3.1 Succession: Updates and Supersedes

A CCRFC MAY declare succession against an earlier CCRFC with one or both of two optional header lines: `Updates: <ccrfc_checksum>` and `Supersedes: <ccrfc_checksum>`. For the founding set (CCRFC-000 through CCRFC-006), the frozen numbers MAY be used in place of checksums.

`Updates` means compatible addition: the earlier CCRFC still stands alongside. `Supersedes` means intended replacement: the earlier CCRFC stays archived and findable, marked as superseded-by in the store index, never edited, never deleted.

Anyone MAY claim either line against anyone's CCRFC, including one they did not author. The original author has no veto. A superseding CCRFC MUST carry a short section stating what changed and why. No silent takeover.

If two CCRFCs both claim to supersede the same checksum, both exist. Canon is whatever profiles carry and providers honor — observable, not decidable. Neglect buries the loser.

CCRFCs are immutable. A published CCRFC MUST NOT be edited in place — any change, including adding a superseded-by note, produces a new document with a new checksum. Back-pointers live in the store index, never in the document.

### 3.2 Filing

Anyone MAY file a CCRFC. No permission, no gatekeeper, no quality bar. Stores set their own house rules — rate limits, format checks, merge process — in their own docs, not in this framework. What is filed becomes true only when profiles carry it and providers honor it. Neglect does the work.

## 4. Abstract

Every CCRFC MUST include an Abstract section immediately after the header, stating in a few sentences what the CCRFC defines and which other CCRFCs it relates to.

## 5. Normative language

Normative requirements MUST use RFC 2119 keywords (MUST, MUST NOT, SHOULD, MAY). Descriptive prose MUST NOT use these keywords in their normative sense; where ambiguity is possible, prefer plain verbs.

## 6. Formatting

CCRFCs are written in Markdown. Headings, lists, blockquotes, and code blocks follow standard Markdown. This rule exists because hard wraps are editing friction with zero rendering benefit.

### 6.1 No hard returns for line wraps (core canon, immutable)

We do not use hard returns to create line wraps in CCRFCs and related documentation. Paragraphs MUST be single-line: no hard line wraps inside paragraphs; the renderer handles wrapping. A sentence broken with soft line feeds to fake neat margins MUST NOT happen.

This is checksum load-bearing, not style. Every hard wrap is a byte the next editor's reflow will change — and any byte change invalidates the ccrfc_checksum. Content addressing cannot survive authors hand-wrapping paragraphs. Single-line paragraphs keep the canonical bytes stable across editors, platforms, and reflows.

## 7. The whitepaper is the authority

CCRFCs specify mechanisms described in the framework whitepaper (*A Standardized Approach to AI User Privacy: The Cognitive Commons Framework*). A CCRFC MUST NOT contradict the whitepaper. Where the whitepaper is ambiguous or silent, the CCRFC MUST NOT silently decide: it MUST mark the point as an open question per Section 8.

## 8. Open questions

Every CCRFC MUST include an Open questions section listing each point the CCRFC could not normatively resolve, in the form "OPEN QUESTION: <description>". Ambiguity MUST be marked, never buried. The open questions across all CCRFCs constitute the work list for the next revision pass.

## 8.5 Companion documents

Four non-normative guides accompany this framework: PROVIDER_README.md (sysadmin-level provider manual, including the thirty-seconds-to-runtime setup), USER_README.md (plain-language user guide with the honest-scope warning), USER_ADVANCED_README.md (how-and-why for curious users), and data-egress-onboarding-draft.md (the scenario-based onboarding flow). They carry no MUSTs. Where they disagree with a CCRFC, the CCRFC governs.

## 9. License footer

Every CCRFC MUST close with an Apache License 2.0 notice.

## 10. Open questions

- **OPEN QUESTION:** RESOLVED Oct 15 — no lifecycle by design. Draft is the only status. A CCRFC does not graduate; it is either used or it sits numbered and ignored. Lifecycle implies an authority to promote, and there is none.
- **OPEN QUESTION:** RESOLVED Oct 18 — succession (§3.1 Updates/Supersedes, anyone may claim, use decides) plus anyone-may-file (§3.2) answer this. Founding numbers are frozen nicknames; all later CCRFCs are checksum-identified; no editor or registry role is needed or defined.

## 11. License

This document is released under the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0/).
