# Cognitive Commons Framework — User Guide

## The one thing to know

Flags on your end mean nothing unless the other end reads them. A green flag in your app is a claim, not a shield. DO NOT send what you can't afford to lose until you have confirmed that BOTH your own equipment and the provider you are sending to honor the Cognitive Commons Framework. The outlet doesn't care that you meant well.

## What this is

When you use an AI, your words leave your machine and land on somebody else's computer. That computer can keep them, train on them, hand them over, get breached. The Cognitive Commons Framework is a set of flags you attach to your words before they leave: this is private, this never trains, this never transmits. Providers that honor the framework read the flag first and refuse what they cannot handle — without reading the content they refuse.

## The flags, plainly

Five tiers, strictest last. These are the same tiers the providers implement (CCRFC-001) — the plain words here must never promise more than the spec:

- UF (Use Freely): use it for anything — improving the service, advertising, the works. The open end. No framework restriction beyond the law and the provider's own stated rules.
- SO (Service Only): use it to make the service better, including training and tuning — but never for advertising or ad targeting.
- CO (Conversation-Scoped): use it to help me right now, in this conversation — then forget it. Not retained past the conversation's edge, never trained on, never used for ads.
- NK (No Keep): transient processing only. The system has to see it to route it and answer — "seen to route" — but must not retain it afterward, and the discard path is auditable.
- NT (No Transmission): this never leaves my machine; local inference only. If it somehow arrives at a provider, the provider must refuse it unread, without peeking at the content.

Your app sets these per topic — medical, financial, bedroom, bathroom, mortality, mental health, and anything personal. Unknown flags mean most-private. That is the safe default, not a bug.

## How to check your provider

Ask your provider for their self-report: the JSON at `/.well-known/ccrfc-report`. It lists which CCRFCs they honor, what handling they actually do per topic, how long they cache, and what constraints (law, their own rules) override your flags. If they publish nothing, they honor nothing — treat every word you send as public. If their report honors less than it used to, your client should warn you. Listen to it.

## The 202 moment

Sometimes you are about to send something intimate and you have no private endpoint configured. Your client will stop you and ask: hold this, or send it somewhere less private? It will tell you plainly that "most private available" is NOT private-only-to-you. That warning is the framework working. Do not click through it on autopilot.

## Your egress record

Your system keeps a record of what left, when, and to whom — exportable as markdown, sqlite, or csv, your choice. Read it. It proves accounting, not non-use: no log can prove "we didn't use your data," and anyone who tells you otherwise is lying. The export itself is sensitive — it lives on your machine, encrypted, key in your hands.

## What DeepGravity does first

DeepGravity stops NT content before it leaves the box. The flag is enforced on your own hardware, so the provider never has to refuse what it never receives. The framework does not require anyone else to do this. Providers can refuse-at-receipt and still be compliant. We do it first to set the example — and because it is the only direction with zero downstream risk.

## License

This document is released under the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0).
