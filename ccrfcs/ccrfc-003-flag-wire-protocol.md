# Cognitive Commons Framework - CCRFC 003 - Flag Wire Protocol

CCRFC-Checksum: 70da42c67a2c30e02c32b70cdb819394e44f6bb7846f7da055c45e29a600ab31
Status: Final. Version: 1. Date: 2026-10-18.

## Abstract

This document defines the flag wire protocol of the Cognitive Commons Framework: flag-before-payload handling, the two-sided handshake between user flags and provider acceptance, and the HTTP-style status codes that give the protocol its machine-readable vocabulary. The protocol enforces handling tiers (CCRFC-001) without requiring the enforcer to read the content it refuses.

## 1. Introduction

Declaring a handling tier is not enough; the declaration must be enforceable at the boundary where content moves. The flag protocol is that enforcement: handling flags travel ahead of content, the receiver checks the flag before reading the payload, and each interaction is a transparent query — allowed, held, or refused — that fails closed.

## 2. Conventions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

## 3. Flag-before-payload

Handling flags MUST travel ahead of content. The receiver MUST check the flag before reading the payload — the sealed envelope: the marking is on the outside, the content stays sealed. On detection of a flag the receiver cannot honor, parsing MUST halt immediately. The receiver MUST NOT buffer the remainder, MUST NOT log the partial content, and MUST NOT peek at the payload to classify it. The payload MUST be returned to the sender. The audit log MUST record the event without the content, in the form: "NT-flagged payload received, parsing halted at flag, payload returned, zero content processed." The absence of content in the log is the proof of non-reading: "I don't know what it was" becomes a true statement instead of a lie. This is the clamp done correctly: not reaching back upstream to unsee the seen, but acting at the boundary before processing begins.


## Canonical serialization

All machine-readable artifacts in this framework - tier labels, flags, profiles, report bodies, egress records, condensed initializations - use one canonical form: JSON with sort_keys, separators (",",  ":"), UTF-8 encoding, no trailing whitespace, LF line endings. This is the same canonicalization the checksums (ccrfc_checksum, report_checksum, hash-chain links) are computed over: what hashes is what travels. Implementations MUST serialize in this form and MUST accept it; human-readable renderings MAY differ but MUST round-trip through the canonical form without loss.
## 4. The handshake

The handshake is two-sided and fails closed. Per interaction, a condensed initialization carries identity, protocol version, and the flags. The condensed initialization is a single canonical-JSON object with exactly these fields: identity (string, provider-assigned session or user identifier), protocol_version (string, canonical form v<major><letter?> per the Report fields section below), flags (object mapping class-id or domain-id strings to handling-tier code strings), and profile_version plus profile_hash (string and lowercase hex sha256, identifying the user's profile revision). Then: (1) user-side flags declare whether the information is allowed to be shared, and at what tier; (2) the inference provider decides whether to accept it under those terms. Neither side dictates. The model is TLS cipher negotiation: the client offers, the server picks from the overlap, and the interaction fails closed if there is nothing in common. The NT machinery — flag-before-payload, honor-or-refuse — generalizes to every flag, so each interaction is a fast, transparent query ("X at SO?") resolving to allowed, held, or refused, all visible and all disclosed.

## 5. Status codes

Status codes are machine-readable privacy states in the HTTP mold: the number is the protocol, the human sentence is the expansion. The codes give the audit log its vocabulary — "202 raised, user chose hold" is machine-parseable and human-readable.

### 5.1 2xx — proceeding with notice

The interaction proceeds, but the user is warned at the boundary. Code 202 is defined as: "You are approaching a topic domain you've flagged as intimately private, but you don't have a model configured at that privacy level. Hold this message, or send it to the most private available endpoint? Note: 'most private available' is by definition NOT PRIVATE ONLY TO YOU and will exist outside your direct control." No false comfort at the exact moment comfort would be easiest to sell.

### 5.2 4xx — crossed own line

The user has crossed their own boundary: the domain flag tripped, and the message is held until the user decides. This is a client-side boundary under the user's own rules.

### 5.3 5xx — provider limitation

The provider cannot honor the requested handling here: no endpoint at this privacy level exists, the law requires retention, or the auditor must see it. This is not the user's choice failing; it is the environment's. A 5xx MUST state which limitation applies.

## 6. Open questions

- **OPEN QUESTION:** RESOLVED Oct 18 - canonical serialization (new section, this document) governs: flags travel as canonical-JSON objects; framing (headers vs envelopes) is transport's choice, bytes are canonical.
- **OPEN QUESTION:** NOTE Oct 18 - 202 pl] ] ] ] ] us the 4xx/5xx classes are sufficient for v1; specific code assignments beyond 202 are deferred to a later CCRFC by design, not omission. Only code 202 is individually defined; 4xx and 5xx are defined as classes. A registry of specific assigned codes beyond 202 is needed.
- **OPEN QUESTION:** RESOLVED Oct 18 — the condensed initialization is now defined in §4 above (identity, protocol_version, flags, profile_version plus profile_hash, canonical JSON). Single definition; CCRFC-004 references this section.

### Self-report on first contact

The provider publishes a small machine-readable self-report: protocol version, CCRFCs honored, per-class handling it can do, cache lifetime, precedence constraints. Same payload two doors: well-known endpoint plus in-handshake declaration. Voluntary to publish, verifiable on contact.

If a provider publishes a self-report, it MUST publish through both doors: the well-known endpoint at `/.well-known/ccrfc-report` and the in-handshake declaration. Both doors MUST serve byte-identical payloads. Clients MUST treat either door as canonical and MUST flag divergence between doors as mismatch. A provider that does not wish to be discoverable MUST publish nothing at all.

### Report hash and downgrade rule

After first contact the handshake carries report-checksum only. Match proceeds, mismatch refetches. If a new report honors less than the cached one, the client warns, holds, or refuses. Fails closed.

### Report fields

- protocol_version — string, canonical form v<major><letter?> (e.g. v1, v1a, v1b, v2). Major bump means breaking wire change: old clients MUST refetch and hold. Letter bump means additive: old clients MAY proceed. Versions only the framing (report shape plus handshake), never the bundle; bundle version is ccrfcs_honored plus each document's own version line.
- ccrfcs_honored — array of strings, canonical IDs sorted ascending (e.g. ["ccrfc-001","ccrfc-003"]). Bare numbers and unprefixed forms MUST NOT be used.
- per_class_handling — object mapping class-id string to handling-tier code string (e.g. {"medical_l3":"NT"}). Keys are self-describing; unknown keys mean most-private.
- cache_lifetime — integer, days. MUST be >=0. The 30-day TTL is the default mismatch horizon per Q-21; providers MUST honor shorter user settings including forget-after-each-session.
- precedence_constraints — array of strings, plain-language constraints (e.g. ["law","provider-rules"]).
- report_checksum — string, lowercase hex sha256 of the canonical JSON (sort_keys, separators (",",":")) of the report without report_checksum itself. Carried in-handshake after first contact; match proceeds, mismatch refetches. Transient cache validator, not identity: computed on the fly, forgotten whenever. Distinct from ccrfc_checksum, which permanently names a CCRFC document.

### Tally conventions

Tallying counts what is used and blesses nothing. Providers MAY self-publish counts. Independent crawlers MAY publish tallies. Clients SHOULD compare both when available. Divergence between self-published and crawler-observed counts is signal, not verdict, and MUST be surfaced to the user.

## 7. License

This document is released under the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0/).
