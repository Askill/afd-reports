# Publication approvals

Every publication requires explicit user approval before push. One row per
publication. Public branch history was rebuilt on 2026-10-24 to expunge a
revoked publication at the user's request; per-row commit hashes were dropped
in that rebuild.

| Date | Report | Approver | Scope | Exposure | Decision |
|---|---|---|---|---|---|
| 2026-10-23 | `afd-mail-flows` | Askill | Publish report as-is; 158 unique email addresses, no pseudonymisation | Low for public figures, party offices and government offices; moderate for 9 private mailboxes | Approved |
| 2026-10-24 | `identification` | Askill | (contents expunged from history at user request) | — | Revoked 2026-10-24: judged not ready before readiness review; page, sidecar, code and manifest expunged |

## 2026-10-23 — afd-mail-flows

- **Files:** `reports/afd-mail-flows.html`
- **PII inventory:** `reports/afd-mail-flows.pii.md` (158 unique addresses, 2,694 occurrences)
- **Exposure:** low for public figures, party offices and government offices; moderate for private mailboxes
- **Reproducibility:** source `viz/afd_mail_flows.html`; build `scripts/publish/build_report.py` in the analysis workspace; data from the forwarding-chain pipeline (see the report's methodology note)
- **Decision:** approved, publish as-is
