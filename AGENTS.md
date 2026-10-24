# AGENTS.md — afd-reports

Instructions for agents working in this repository. **This repo is public.**
Every file added here is a publication. Read this before creating, editing, or
pushing anything.

## Purpose

Publish self-contained, publishing-ready reports derived from the hexane AfD
leak corpus. Each report is a single HTML file with data, code and styling
embedded. The repo also carries the code, input manifests and investigation
material needed to reproduce and audit each report.

## Hard rules

### 1. No full texts

Never publish complete source documents, emails, threads, chat logs, database
rows, or document bodies. Publish citations instead:

- sender, recipient, date, subject, and the corpus-relative path
- a short excerpt only when the exact wording is the claim
- never a complete email, document, or thread

All source references use paths relative to the corpus root, `E:/`:

```
01_EMAIL/01_EMAIL_json/<mailbox>/emails.jsonl
03_DOCUMENTS/03_DOCUMENTS/<file>.pdf
04_TABULAR_DATA/...
```

Never use absolute Windows paths, UNC paths, usernames, or machine names.

### 2. Reproducibility

If a report contains generated content, publish:

- the code that generated it, under `reports/<slug>/code/`
- the input manifest, `reports/<slug>/inputs.csv`, one row per input:
  `path` (relative to `E:/`), `sha256` (optional), `role`, `origin`
- the exact command line, including the corpus root parameter

Scripts must accept the corpus root as a parameter and default to `E:/`:

```python
parser.add_argument("--corpus-root", default="E:/")
```

All paths inside scripts resolve relative to that root. No hard-coded absolute
paths. A reader with the corpus mounted at `E:/` must be able to re-run the
pipeline and reproduce the published numbers.

Raw corpus files are never copied into this repo. The manifest is the input.

### 3. Investigations

If a report is based on an investigation, publish the entire investigation
directory from `docs/projects/investigations/<case>/` under
`reports/<slug>/investigation/`, preserving its structure (`index.md`,
`sources/`, `extracts/`, `claims/`, `synthesis/`, `leads/`).

Before publishing, sweep the directory for full texts and replace them with
citations per rule 1. Do not silently drop files. If a file cannot be published,
record it in `reports/<slug>/investigation/WITHHELD.md` with the reason and the
citation that replaces it.

Relative links inside the published copy must resolve within the public repo.

### 4. Approval gate

Every publication requires explicit user approval before `git push`. This
includes new reports, edits to published reports, new investigation material,
and new code or manifests.

The approval request must contain:

- the exact files and paths to be published
- a PII inventory with file and line references (see rule 5)
- an exposure assessment: who is identifiable, public figure vs private
  individual, sensitivity, and risk (low / medium / high)
- the proposed redaction, or the justification for publishing as-is
- the source and provenance for each factual claim
- the reproducibility check: script, input manifest, command line

Record the approval in `APPROVALS.md`:

```
| date | report | commit | approver | scope | exposure | decision |
```

No approval, no push. Approval is per publication, not blanket.

Publication request template:

```
Report: <slug>
Files: <exact paths>
PII: <sidecar path> (<n> unique items; categories)
Exposure: <low|medium|high> — <who is identifiable>
Redaction: <none | list of redactions>
Provenance: <sources and citations>
Reproducibility: <script> --corpus-root E:/ ...
Approval: <pending>
```

### 5. PII

All PII must be highlighted before publication. PII includes names, email
addresses, phone numbers, postal addresses, dates of birth, IBANs, usernames,
IP addresses, and any combination that identifies a person.

Every report carries a sidecar `reports/<slug>.pii.md` with:

- every unique PII item, its category, and where it appears
- whether it is published, redacted, or aggregated
- the exposure assessment and the approval reference

The sidecar is part of the publication. If PII is published as-is, the sidecar
must say so and explain why.

### 6. Self-containment

Published reports must make zero external requests: no CDN scripts, no external
fonts, no trackers, no analytics. Inline all dependencies. Verify with a browser
that the only host contacted is the Pages host.

## Publication checklist

- [ ] Report is self-contained; zero external requests
- [ ] No full texts; citations and `E:/`-relative paths only
- [ ] Code, input manifest, and command line included (if generated)
- [ ] Investigation directory included in full, or `WITHHELD.md` explains gaps
- [ ] `reports/<slug>.pii.md` complete; exposure assessed
- [ ] User approval recorded in `APPROVALS.md`
- [ ] `index.html` and `README.md` updated
- [ ] Browser verification passed (desktop + mobile, no console errors)
- [ ] Commit and push

## Repo layout

```
/
  index.html
  README.md
  AGENTS.md
  APPROVALS.md
  .nojekyll
  reports/
    <slug>.html                 # published report
    <slug>.pii.md               # PII inventory + exposure assessment
    <slug>/
      code/                     # generation code
      inputs.csv                # input manifest, paths relative to E:/
      investigation/            # full investigation dir, if applicable
```

## Never publish

- raw corpus files, full email bodies, full documents
- credentials, private keys, tokens, `.env` files
- unredacted private individuals' contact data without explicit approval
- absolute local paths, machine names, usernames
- internal notes that are not part of the investigation record

## Editorial standard

Match the existing reports: white paper, Georgia serif, red accent `#E3120B`,
slate `#6E7A8A`, direct labeling, source and methodology notes on the page.
No trackers. No external fonts.

## Current approvals

See `APPROVALS.md`. The first report (`afd-mail-flows`) was approved on
2026-10-23 with addresses published as-is. Exposure is assessed as low for
public figures, party offices and government offices; moderate for private
mailboxes.
