# Cognitive Commons Framework - CCRFC 002 - Content Classes

CCRFC-Checksum: 1ecb237480f185c133f5d80efdaacf0aaae423558e330925700ef2199193d9fc
Status: Final. Version: 1. Date: 2026-10-18.

## Abstract

This document defines the content class taxonomy of the Cognitive Commons Framework: the categories of user content to which handling tiers (CCRFC-001) are assigned per class. Users think in kinds of content, not in binary toggles; the taxonomy gives those kinds standard names so expectations port across providers.

## 1. Introduction

A single global privacy switch is too coarse to match how people actually reason about disclosure. The framework therefore defines content classes, and the user assigns a handling tier to each class independently. The classes below are the standard set. The taxonomy is extensible: providers and communities MAY define additional classes, but the classes defined here MUST be recognized by any conformant implementation.

## 2. Conventions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

## 3. The classes

### 3.1 Identifiers

Content that points directly at the user: full name, license numbers, account numbers, Social Security number, and equivalent directly-identifying data. Identifiers are the front door: compromise here amplifies the compromise of every other class.

### 3.2 Medical — Level 1

Basic medical queries requiring no serious disclosure. Example: "What's a normal resting heart rate?" Level 1 covers questions answerable without the user revealing anything about their own body or health.

### 3.3 Medical — Level 2

Ongoing and detailed health information: chronic conditions, detailed general health, weight goals, limb difference. Gym-intake-form level: the kind of thing routinely disclosed to non-intimate service providers, but still personal.

### 3.4 Medical — Level 3

The things we all deal with but mostly consider private or intimate: things related to the bedroom, the bathroom, mortality, and mental health. Level 3 is the inner vault: content the user is most likely to want under the strictest tier available to them.

### 3.5 Financials

Financial content, tiered the same way as medical: balances and account numbers are Identifiers; "how should I budget?" is Level 1; the full unvarnished financial picture is Level 3. The three-level structure of Section 3.2–3.4 applies by analogy.

### 3.6 Personal conversation

The talking itself: how private the conversation should be, and how far the assistant should go with what it is told. This class governs the conversational layer rather than any topical domain, and pairs with the conversation quantifier (just answer / offer practical help / full concierge) defined in the framework whitepaper.

## 4. Per-class tiering

Each class MUST be assignable an independent handling tier from CCRFC-001. The user sets handling per class; a single global setting MUST NOT substitute for per-class assignment during initial setup, though implementations MAY offer bulk presets that expand into per-class values. Class-level examples SHOULD be illustrated with two or three concrete scenarios each in the user interface, not merely described.

## 5. Extensibility

The taxonomy defined here is the minimum standard set. Additional classes MAY be defined by anyone without permission, using self-describing IDs (reverse-DNS style) — not small integers from a central assigner — provided they do not redefine the classes in Section 3. Extended classes SHOULD follow the same naming pattern and MUST be documented with the same per-class tiering behavior. No registry or authority confers standard status; canon is whatever interoperates. Receivers MUST NOT reject a profile for containing unknown classes; they MUST enforce most-private on unknown content automatically.

## 6. Open questions

- **OPEN QUESTION:** The exact Level 1 / Level 2 / Level 3 criteria for Financials are defined only by analogy to Medical. Precise criteria for the financial levels are needed. This is a user-provided variable: the user assigns their own financial content to levels by analogy to Medical; until set, all financial content defaults to the most-private tier assigned to any financial level.
- **OPEN QUESTION:** RESOLVED Oct 12, confirmed Oct 18 — no registry authority by design (§5). Anyone may define extended classes with self-describing IDs; canon is whatever interoperates; unknown means most-private. Registries may exist as plural competing conveniences, none authoritative.
- **OPEN QUESTION:** RESOLVED Oct 18 — precedence is stated in CCRFC-006 §6: where a domain flag and a class tier conflict, the conflict MUST resolve to the most private position per CCRFC-001 §7. No further guidance needed; the rule governs.

## 7. License

This document is released under the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0/).
