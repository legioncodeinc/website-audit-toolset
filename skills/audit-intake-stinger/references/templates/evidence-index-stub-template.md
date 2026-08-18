# Evidence index

Stub written by `audit-intake-worker-bee` at scaffold time. Every subsequent Bee appends one row per artifact it produces (build plan section 3: "every artifact, what produced it, when"). This Bee does not populate any rows beyond its own intake artifacts; it only establishes the table shape so downstream Bees have a consistent append target.

| Artifact path | Produced by | Produced at | Notes |
|---|---|---|---|
| `00-intake/answers.md` | audit-intake-worker-bee | {intake_timestamp_iso8601} | The four recorded intake answers |
| `README.md` | audit-intake-worker-bee | {intake_timestamp_iso8601} | Run manifest |
| `_shared/run-ledger.json` | audit-intake-worker-bee | {intake_timestamp_iso8601} | Per-Bee status ledger, append-only from here |
| `_shared/target-profile.json` | audit-intake-worker-bee | {intake_timestamp_iso8601} | Stub only; populated by stack-fingerprint-worker-bee |

## Append rule

Add one row per artifact, in the order produced, never remove or rewrite an existing row. This is the same evidence-at-the-moment-of-finding discipline as conduct rule 2 in `rules/website-audit-conduct.md`, applied to the artifact index itself rather than to individual findings.
