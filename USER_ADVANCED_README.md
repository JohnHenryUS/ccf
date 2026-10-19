# Cognitive Commons Framework — Advanced User Guide

## How it works

Flag-before-payload. Your flags travel ahead of your content. The receiver checks the flag before reading the payload — the sealed envelope: the marking is on the outside, the content stays sealed. On a flag the receiver cannot honor, parsing halts immediately: no buffering, no partial logging, no peeking to classify. The payload is returned. The audit log records the refusal without the content. "I don't know what it was" becomes a true statement instead of a lie.

## The handshake

Two-sided, fails closed, modeled on TLS cipher negotiation. Your side declares terms; the provider decides whether to accept under them. Neither side dictates. Each interaction is a fast transparent query — "X at SO?" — resolving to allowed, held, or refused. Status codes give it vocabulary: 2xx proceeds with notice, 4xx you crossed your own line, 5xx the provider cannot honor the handling here.

## Why unknown means most-private

Self-describing IDs, no central registry (CCRFC-002 §6, CCRFC-006 §7). Anyone may define extended classes. Canon is whatever interoperates. An unknown flag is therefore a stranger at the door — and the safe default is to treat strangers as most-private, not least. This is fail-closed at the namespace level.

## The hash dance

After first contact, the handshake carries `report_checksum` only — 64 hex characters instead of the full provider report. Same bytes as an ETag. Match proceeds, mismatch refetches, honors-less-than-cached warns. The checksum is transient: computed on the fly, forgotten whenever. It is deliberately distinct from `ccrfc_checksum`, which permanently names a CCRFC document. Same algorithm, different jobs — cache validation versus identity.

## Why content addressing

CCRFC documents name themselves: `ccrfc_checksum` is the sha256 of the canonical bytes. No counter, no registrar, no coordination. Same bytes anywhere — our repo, a Tokyo mirror, an email attachment — same name. Two different documents cannot share a name. Canon-as-observed replaces canon-as-decided: profiles carry a checksum, providers honor it, tallies count it, use decides.

## Why neglect instead of authority

Anyone may file. No permission, no quality bar, no veto — including against someone else's document via Updates/Supersedes. Filing makes nothing true; honoring does. Unused documents sit numbered and ignored. This is not laziness. It is the only design where no editor can become a gatekeeper, and where a thousand junk filings harm nobody because nobody drinks from the filing bucket.

## Why your egress record can't prove non-use

Unprovable in principle. No log demonstrates that data was never copied, never trained on, never seen. The record proves accounting — what left, when, to whom — which is the strongest true claim available. Demand accounting from providers. Distrust anyone selling proof of a negative.

## License

This document is released under the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0).
