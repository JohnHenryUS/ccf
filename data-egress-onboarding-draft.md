# Data Onboarding: "How private should this be?"

A first-draft onboarding flow for per-user, per-class data-flow control. Companion to *A Standardized Approach to AI User Privacy* v0.2 — aligned to its two tracks, five tiers, and portable profile.

Principle: the default is stated honestly, the controls are real, most people won't touch them — and that's fine. The fire exit you never use but always check.

---

## Screen 0 — Our boundaries (the provider speaks first)

**Before you tell us anything: this isn't the place for your most intimate thoughts.**

We're a frontier cloud provider — a public-facing service. That means there's always a non-zero possibility of data leaks, including yours. We'd rather tell you that now than have you discover it later.

Your choices here sit inside two harder constraints: **the law** (warrants, mandatory reporting, retention duties) and **our rules** (terms of service, abuse systems). Where those apply, they win. Your settings govern everything else — which is almost everything, day to day — but not those. We're telling you because pretending otherwise would be a lie.

We appreciate the trust you're placing in us, and we want to respect it the honest way: by making sure you don't tell us things we shouldn't know. If something is too sensitive for a cloud service to hold, we'd rather you kept it to yourself — and we'll help you figure out where that line is. That's what the next few minutes are for.

This is a different decision for everyone. Some people genuinely don't care about sharing intimate information. Others are horrified by the mere suggestion that they *have* intimate information — the "Queen of Spain has no legs," and they'd like to keep it that way. We want both of you comfortable here.

So: a little touch of discomfort now, up front, in a safe structured moment — so you don't have to go through a whole bunch of it later, mid-conversation, when it's real. Think of it as inoculation.

---

## Screen 1 — The honest default

**What we do with your conversations.**

By default, we use your conversations for three things (other than generally processing them enough to participate in them):

1. **Improving the service** — training, tuning, making answers better.
2. **Advertising** — understanding what you're into so the ads fit.
3. **Keeping it smooth** — making sure you get answers without nonsense or extra steps.

That's the deal, stated plainly. If you're fine with it, you're done — most people are, and that's fine.

If you're not fine with all of it, keep going. You get to draw the lines.

---

## Screen 2 — Content classes

**Tell us how to treat each kind of content.**

For every class below, pick one:

- **Use Freely** — improve the service, inform advertising, the works. *(UF)*
- **Service Only** — use it to make things better, keep it out of advertising. *(SO)*
- **Conversation-Scoped** — use this information only for the duration of the conversation containing it, then forget it. *(CO)*
- **No Keep** — transient processing only. We have to see it to route it; we don't retain it, and the discard path is auditable. *(NK)*
- **No Transmission** — never leaves your device. Local inference only. *(NT)*

### The classes

- **Identifiers** — your full name, license numbers, account numbers, Social Security number. The stuff that points directly at you.
- **Medical — Level 1** — basic queries. "What's a normal resting heart rate?" Simple questions that don't involve telling us you're sick.
- **Medical — Level 2** — the ongoing stuff. Chronic conditions, detailed general health, "I want to lose weight," the missing limb. The kind of thing you'd put on a gym intake form.
- **Medical — Level 3** — the things we all deal with but mostly consider private or intimate: things related to the bedroom, the bathroom, mortality, and mental health.
- **Financials** — same tiering, your call. Balances and account numbers are identifiers; "how should I budget?" is Level 1; the full unvarnished picture is Level 3.
- **Personal conversation** — how private should the talking be? See next screen.

### The NT check

"No transmission" is the strongest tier and the only one we can't honor alone — it needs a model on *your* hardware. If you pick NT for a class and no local endpoint is configured, we tell you straight, right here:

> You flagged this as never-leave-the-device, but there's no local model configured to receive it. Do you want to hold these messages until you set one up, or downgrade to "No Keep" with eyes open — which means it *will* cross the wire and exist outside your direct control.

No false comfort at the exact moment comfort would be easiest to sell. The codes are the posted lines; you learn the boundary by reading it, not by colliding with it.

---

## Screen 3 — The conversation quantifier

**What should we *do* with what you tell us?**

This isn't about what we keep — it's about how far we go with it.

- **Just answer.** You ask, we answer, nothing more.
- **Offer practical help.** We'll suggest next steps when they seem useful.
- **Full concierge.** We'll go find things — services, professionals, options.

Example: you ask us about grocery stores near you.  We can give you a list of stores, we can ask you to select a store or ask some questions to find the best shopping deals for your needs, and we can ask you if you want us to start a pickup order for you at your selected store.  You tell us — that's what this setting is for.

---

## Screen 4 — The promise

**You do this properly once.** No skipping. What you set here becomes your portable profile — it travels with you. New service, same you: they just ask "still this one?" instead of making you start over. Anything ambiguous defaults to your most private choice, so it's safe to get lazy after the serious setup.

**You can change any of this anytime** — per conversation, or across the board.

And the honest ceiling, stated once: no system can stop you from being the final egress point. Paste it into a web UI yourself and no architecture saves you. Our obligation stops at making the flow visible and warning at the boundary. After that, it's yours — including your autonomy to be wrong.

Most people will set it once and never look at it again. That's fine. It's here because you should have it.

---

## The trust receipt

End state: a generated contract. "Here's what you told us. Here's what we'll do. Signed, us." Plus your profile in the standard shorthand, e.g. `Identifiers: SO, Medical L1/L2: CO, Financials: NK, Medical L3: NT` — portable across providers, readable without our tooling. Screenshotable, shareable, printable. Free marketing and a commitment device in one — and the thing people will post to prove the company actually did it.

---

## Gamification: stop fearing the length

Conventional wisdom says short onboarding or nobody finishes. Conventional wisdom assumes onboarding is a chore. If the onboarding *is* the product demo — and for a product whose thesis is user agency, it is — then length is content. Nobody complains that character creation in an RPG takes 45 minutes.

**Frame: build your vault.** You're not filling out a privacy form. You're designing your data vault — which rooms exist, who gets keys, what happens inside each room. Identifiers are the front door. Medical L3 is the inner vault. Financials are the safe. NT content never leaves the building. You're the warden handing out keys.

**Mechanics:**

1. **Scenarios, not checkboxes.** Each class arrives as a vivid 2–3 line scenario with a choice, not an abstract category. The rash. The divorce lawyer. The bank balance. The 2 AM confession. You choose what happens next; the system records the preference *and* teaches you the control model at the same time.
2. **Live data-flow visualization.** A diagram of your pipes that rewires as you choose. Pick "service only" — watch the ad pipe cap off. Pick "this conversation only" — watch the retention pipe dissolve at the conversation's edge. Pick "no transmission" — watch the domain go dark entirely. Rewiring pipes is inherently satisfying, like a skill tree lighting up.
3. **Levels, not forms.** Privacy Cadet → Data Citizen → Sovereign. Basics first; advanced controls (per-conversation overrides, full export, local endpoint mapping, the gnarly stuff) unlock as you go. Curiosity gets rewarded instead of punished.
4. **The trust receipt.** End state: a generated contract, plus your profile in portable shorthand. (See above.)

The meta-point: rushing this signals you don't believe your own thesis. A company that actually respects agency *lingers* here. The onboarding is where you prove it.

---

*Aligned to whitepaper v0.2 (October 5, 2026): five tiers (UF/SO/CO/NK/NT), two tracks (cloud/local), portable profile, precedence stack, NT local- endpoint check. Draft notes: five tiers is the working set — the gradient runs from open to absent, and absence is the only tier with zero downstream risk. "This conversation only" remains the key containment primitive for the cloud track; "no transmission" is its terminal form on the local track. Level definitions should be illustrated with two or three concrete examples each in the final UI, not just described. Details there can probably be left to the provider's discretion*
