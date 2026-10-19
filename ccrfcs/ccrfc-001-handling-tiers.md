# Cognitive Commons Framework - CCRFC 001 - Handling Tiers

CCRFC-Checksum: 91d1fae0aa54ca53fb69384e75df052ae8ab0a773c37ae0753352c0f47bdd5a9
Status: Final. Version: 1. Date: 2026-10-18.

## Abstract

This document defines the five handling tiers of the Cognitive Commons Framework — Use Freely (UF), Service Only (SO), Conversation-Scoped (CO), No Keep (NK), and No Transmission (NT) — their normative semantics, their license-style label shorthand, how the same tier binds different obligors on the cloud and local tracks, and the gradient principle that absence is the only tier with zero downstream risk.

## 1. Introduction

The framework governs data flow per content class, per conversation. The handling tier is the unit of that governance: for each class of content, the user selects one of five tiers, and every party that touches the content is bound by the tier's semantics. The same vocabulary applies on both tracks defined in the framework whitepaper (cloud inference and local inference); the obligor differs. On the cloud track the tiers bind the provider (restraint). On the local track the tiers bind the user's own egress policy (mediation).

## 2. Conventions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

## 3. The five tiers

### 3.1 UF — Use Freely

Content at this tier MAY be used for service improvement (including training and tuning), MAY inform advertising, and MAY be used for operational purposes. UF is the open end of the gradient: no framework-imposed restriction beyond applicable law and the provider's own stated rules.

### 3.2 SO — Service Only

Content at this tier MAY be used to improve the service, including training and tuning. Content at this tier MUST NOT be used for advertising or ad targeting. SO is the tier for users willing to be the product's training data but not its ad inventory.

### 3.3 CO — Conversation-Scoped ("this conversation only")

Content at this tier MAY be used to fulfill the current conversation. Content at this tier MUST be discarded at the conversation's edge and MUST NOT be retained beyond it. Content at this tier MUST NOT inform advertising and MUST NOT be used for training. CO is the key containment primitive: the data grant expires at the conversation's edge — help me right now, then forget it.

### 3.4 NK — No Keep

Content at this tier is subject to transient processing only. The system MUST process the content to route and respond to it; the guarantee covers retention and egress, not the moment of processing. Content at this tier MUST NOT be retained after processing completes, and the discard path MUST be auditable. An implementation MUST NOT claim that the content was never observed: "we never saw it" is the lie; "we didn't keep it" is the checkable promise. The honest statement is "seen to route; not retained."

### 3.5 NT — No Transmission

Content at this tier MUST NOT leave the user's device. Inference on NT content MUST be local. The content never enters the transmission stream, so there is nothing to risk, nothing to audit, and no temporal paradox. On the cloud track, NT-flagged content MUST be handled per the flag wire protocol (CCRFC-003): the flag is checked before the payload, and content the provider cannot honor locally is refused or held, never read.

## 4. Label shorthand

For standardization across providers, each tier has a compact label:

- **UF** — Use Freely
- **SO** — Service Only
- **CO** — Conversation-Scoped
- **NK** — No Keep
- **NT** — No Transmission

Labels are case-sensitive and MUST be written in uppercase. A user's standing profile MAY be expressed in the shorthand, e.g. `Identifiers: SO, Medical: CO, Financials: NK, Medical L3: NT`. The labels are the standard; the user interface is each provider's implementation.

## 5. Per-track binding

The same tier words bind different obligors by track. On the cloud track, the tiers bind the provider: they are restraints on what the provider may do with content it necessarily sees in the moment. On the local track, the tiers bind the user's own egress policy: they are the firewall rules at the user's own boundary, mediating what the user's machine sends outward. Implementations MUST apply tier semantics according to the track on which the content is being handled.

## 6. The gradient principle

The five tiers form a gradient from open to absent. UF, SO, CO, and NK manage exposure; each reduces but does not eliminate downstream risk. NT is the terminal tier: absence is the only tier with zero downstream risk, because data that doesn't exist can't be information-shaped. Systems SHOULD present the tiers in gradient order and SHOULD make the direction of increasing privacy legible.


## Canonical serialization

All machine-readable artifacts in this framework - tier labels, flags, profiles, report bodies, egress records, condensed initializations - use one canonical form: JSON with sort_keys, separators (",",  ":"), UTF-8 encoding, no trailing whitespace, LF line endings. This is the same canonicalization the checksums (ccrfc_checksum, report_checksum, hash-chain links) are computed over: what hashes is what travels. Implementations MUST serialize in this form and MUST accept it; human-readable renderings MAY differ but MUST round-trip through the canonical form without loss.
## 7. Conflict resolution

Tiers apply at every scope level: conversation, domain, project, task, and standing profile. Where tier assignments conflict, the conflict MUST resolve to the most private position. A specific restriction overrides a general permission, and any genuine tie MUST resolve to maximum restriction. Over-privating costs a tap; over-sharing costs the 2 AM disclosure in a training set. The bias is toward the recoverable failure mode: default-deny, like a firewall.

## 8. Open questions

- **OPEN QUESTION:** RESOLVED Oct 18 - canonical serialization (new section, this document) governs: canonical JSON, sort_keys, separators (",", ":"), UTF-8.
- **OPEN QUESTION:** The exact definition of "the conversation's edge" for CO is not specified. Implementations need a shared definition of when a conversation ends for discard purposes. This is a user-provided variable: the user's profile defines when a conversation ends (session close, explicit reset, or provider signal); until set, most-private holds and CO content is retained only for the active interaction.
- **OPEN QUESTION:** Whether SO permits internal analytics beyond model training (e.g., aggregate usage metrics) is not specified. The boundary between "improve the service" and adjacent internal uses  needs definition. This is a user-provided variable: the user's profile states whether aggregate metrics count as service improvement; until set, most-private holds (training and tuning only, no analytics).

## 9. License

This document is released under the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0/).
