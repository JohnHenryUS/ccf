# Cognitive Commons Framework — Provider Manual

## Thirty seconds to runtime

1. Serve this JSON at `/.well-known/ccrfc-report` (static file, any web server).
2. Serve the byte-identical JSON in your handshake declaration.
3. Done. Forget it until your handling changes.

```json
{
  "protocol_version": "v1",
  "ccrfcs_honored": ["ccrfc-001", "ccrfc-003"],
  "per_class_handling": {"medical_l3": "NT"},
  "cache_lifetime": 30,
  "precedence_constraints": ["law"],
  "report_checksum": "<sha256 of the above, canonical JSON>"
}
```

`report_checksum` is the lowercase hex sha256 of the canonical JSON (sort_keys, separators (",",":")) of the report without `report_checksum` itself. Recompute it whenever the report changes. Clients use it the way browsers use ETags: match proceeds, mismatch refetches.

## What you are promising

Each `ccrfcs_honored` entry is a claim your users will verify. `per_class_handling` maps class IDs to the handling tier you actually enforce — SO, CO, NK, NT per CCRFC-001. Unknown class IDs MUST be treated as most-private. If the law requires retention or your auditor must see content, say so in `precedence_constraints` in plain language. No false comfort: a 5xx MUST state which limitation applies (CCRFC-003 §5.3).

## Both doors

If you publish, you MUST publish through both doors: the well-known endpoint and the in-handshake declaration. Both doors MUST serve byte-identical payloads. Either door is canonical. Divergence between doors is mismatch — clients MUST flag it. If you do not wish to be discoverable, publish nothing at all.

## The hash dance

After first contact, handshakes carry `report_checksum` only — 64 hex characters instead of the full report. Match: proceed. Mismatch: refetch the full report. If the new report honors less than the cached one, the client warns, holds, or refuses. That behavior is client-side and fails closed; you do not need to implement it, only to serve accurate bytes so it triggers correctly.

## Downgrades are visible

Lowering what you honor is allowed. Hiding it is not. The checksum makes silent downgrades impossible: any change to the report changes the checksum, the client's next handshake mismatches, and the user gets told. Design your change process around that.

## Cache lifetime

`cache_lifetime` is integer days. 30 is the default mismatch horizon. You MUST honor shorter user settings, including forget-after-each-session. On-demand delete is honored immediately, not queued.

## What you do NOT need

No login system. No key registry. No approval process. No account with anyone. Serve the file, keep it accurate, and you are a provider in the commons. Canon is whatever profiles carry and providers honor — observable, not decidable.

## Reference implementation

`ccrfc-self-report-server.py` in this kit is a working stdlib-only server: both doors, 304-on-match, 404 clean. Read it, steal from it, replace it.

## Verification

Live-tested Oct 18 against the reference server with the canonical sample `report.json`: GET well-known 200 with ETag, If-None-Match 304, wrong-path 404 (GET and POST), handshake first-contact full report, handshake checksum-match 304, handshake mismatch refetch, and refusal to start on checksum mismatch. 10/10 passing. The test driver ships alongside the server; re-run it against your own implementation before you claim conformance.

## License

This document is released under the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0).
