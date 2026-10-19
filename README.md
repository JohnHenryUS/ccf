# The Cognitive Commons Framework

*Per-class, per-conversation data-flow control for conversational AI.*

**The pitch:** AI providers give you one privacy choice: accept the terms or don't use the product. The Cognitive Commons Framework is a proposed open standard that replaces that binary with five handling tiers you assign per content class, a wire protocol that enforces them without the enforcer reading your content, and a portable profile you set up once and carry across providers. Creative Commons, but for data flow.

**The five tiers:**

| Label | Tier | Meaning |
|---|---|---|
| UF | Use Freely | Improve the service, inform advertising, the works. |
| SO | Service Only | Use it to make things better; keep it out of advertising. |
| CO | Conversation-Scoped | Help me right now, then forget it. The data grant expires at the conversation's edge. |
| NK | No Keep | Transient processing only. Seen to route; not retained; the discard path is auditable. |
| NT | No Transmission | Never leaves the device. Local inference only. |

**Repo contents:**

- `standardized-ai-user-privacy-whitepaper.md` — the full whitepaper (v1)
- `ccrfcs/` — seven CCRFCs in RFC 2119 normative language: format, handling tiers, content classes, flag wire protocol, portable profile, egress audit record, domain flags
- `ccrfc-checksums.md` — founding-set checksums manifest
- `PROVIDER_README.md` — sysadmin-level provider manual (thirty seconds to runtime)
- `USER_README.md` / `USER_ADVANCED_README.md` — plain-language user guides
- `data-egress-onboarding-draft.md` — companion onboarding UX draft

**Status:** v1. Seven CCRFCs with implementation notes marked — the parameters implementers fill in, each labeled with its owner and default. Reference server live-tested 10/10 (see PROVIDER_README verification section).

**Reference implementation:** [ccf-srs](https://github.com/JohnHenryUS/ccf-srs) — stdlib-only Python self-report server. Read it, steal from it, replace it.

**License:** [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0). Use it. Build it. Cite it if you're decent.
