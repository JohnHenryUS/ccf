# CCF founding-set checksums

Canonical `ccrfc_checksum` values (lowercase hex sha256) for CCRFC-000 through CCRFC-006, computed 2026-10-18 per CCRFC-000 §3.0: UTF-8, LF line endings, no trailing whitespace on any line, exactly one trailing newline at EOF, `CCRFC-Checksum:` line blanked for computation then filled. All seven verified round-trip (blank → normalize → hash → compare, stable across two runs) before this manifest was written.

**Any edit to a document — including whitespace — invalidates its checksum.** That is the point: change the claim, new document, new checksum.

| Nickname | Title | ccrfc_checksum |
|---|---|---|
| CCRFC-000 | CCRFC Format and Conventions | `313170ba0e84a0ee2598891cf2e5b7eaa56615d27ebfc0aae7badaa77f990359` |
| CCRFC-001 | Handling Tiers | `91d1fae0aa54ca53fb69384e75df052ae8ab0a773c37ae0753352c0f47bdd5a9` |
| CCRFC-002 | Content Classes | `1ecb237480f185c133f5d80efdaacf0aaae423558e330925700ef2199193d9fc` |
| CCRFC-003 | Flag Wire Protocol | `70da42c67a2c30e02c32b70cdb819394e44f6bb7846f7da055c45e29a600ab31` |
| CCRFC-004 | Portable Profile | `ca1745ada752d0722ada9319cc7d0a50bda58e4f8ecf09508ca7adc0ecfbe7b0` |
| CCRFC-005 | Egress Audit Record | `a1eba2f2ae19fdc8035432054c2f0e0a769830b60798ab8d3b236121dd3bbcc7` |
| CCRFC-006 | Domain Flags | `9e2f10eb0b2416c60fe3b99c82b6cda7536c149aa5429c9bc51d3160809a877e` |

Display shorts (first 16 hex, extend on collision): `313170ba0e84a0ee`, `91d1fae0aa54ca53`, `1ecb237480f185c1`, `70da42c67a2c30e0`, `ca1745ada752d072`, `a1eba2f2ae19fdc8`, `9e2f10eb0b2416c6`.

Verify anywhere: take the file, blank the FIRST `CCRFC-Checksum:` value only (key kept; the §3 example in CCRFC-000 keeps its illustration line — verify against the header line), normalize to canonical form (UTF-8, LF, no trailing whitespace, one trailing newline), `sha256sum`, compare to the value in the file and to this manifest.

*This manifest is a companion record, not a CCRFC. It carries no normative weight; the documents name themselves.*
