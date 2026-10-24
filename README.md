# afd-reports

Self-contained, publishing-ready reports on the AfD email leak (hexane corpus).

**Live site:** https://askill.github.io/afd-reports/

## Reports

| Date | Report | Topic |
|---|---|---|
| 2026-10-23 | [How the AfD's mail really moves](reports/afd-mail-flows.html) | Forwarding chains: 213,202 hops across 421,178 emails |

## What "self-contained" means

Each report is one HTML file. Data, chart code and styling are embedded; there
are no external scripts, fonts or stylesheets. A report renders offline and can
be mirrored as a single file.

## Adding a report

Read `AGENTS.md` first. Every publication needs explicit user approval recorded
in `APPROVALS.md`.

1. Produce a self-contained HTML file and place it in `reports/`.
2. Add `reports/<slug>.pii.md` with the PII inventory and exposure assessment.
3. If the report is generated, add `reports/<slug>/code/` and `inputs.csv`.
4. If it is based on an investigation, add the full investigation directory.
5. Link it from `index.html` and add a row to the table above.
6. Get approval, record it in `APPROVALS.md`, then commit and push.

## Data and methodology

Source: hexane AfD leak, 421,178 emails across 10 mailboxes. Chains are
reconstructed from forwarded-inline headers; a hop is one forwarded-header
block. Each report carries its own methodology and provenance note.

Addresses are reproduced as they appear in the leaked material. No
pseudonymisation is applied in these published reports.

## Local preview

```powershell
python -m http.server 8000
# http://localhost:8000/
```
