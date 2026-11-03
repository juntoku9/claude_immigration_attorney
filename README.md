[![Try EB-1A / NIW / O-1 Petition Workflow on Socialistic](https://socialistic.ai/api/embed/immigration-petition-package-eb3e7b?lang=en)](https://socialistic.ai/en/skill/immigration-petition-package-eb3e7b?utm_source=github&utm_medium=pr&utm_campaign=d3874e35&utm_content=badge)

<p align="center">
  <img src="assets/logo.png" alt="Claude Immigration Attorney" width="200">
</p>

<h1 align="center">Claude Immigration Attorney</h1>

<p align="center">Claude Code skills for immigration attorneys and self-petitioning candidates.<br>Draft O-1A, EB-1A, and EB-2 NIW petitions with AI — every claim backed by evidence.</p>

## What This Is

A set of [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skills that handle the most time-consuming parts of immigration petition work. Built for two audiences:

**For immigration attorneys:**
- Organize 100+ client documents into a structured evidence index
- Optionally run a pre-draft check on which criteria or NIW prongs look supportable from the index (skip if you prefer to go straight to drafting)
- Optionally build a normalized publication and citation table for research-heavy O-1A, EB-1A, or NIW cases
- Draft petition letters with proper legal structure, exhibit references, and evidence enrichment
- Audit drafts for factual errors, unsupported claims, and legal issues before signing
- Draft expert/recommendation letters with strategic criteria assignment

**For self-petitioning candidates (EB-1A, NIW):**
- Understand what evidence you need and how strong your case is
- Research government sources that support your national importance argument
- Generate a first draft of your self-petition letter to review with your attorney
- Identify evidence gaps before you file

## Skills

| Skill | What It Does |
|-------|-------------|
| [`document-summary-arrangement`](document-summary-arrangement/) | Ingests source documents (PDFs, images, scans), triages by importance, summarizes key documents, and produces a structured index arranged by evidentiary criterion |
| [`case-strength-assessor`](case-strength-assessor/) | **Optional.** Reads the document index and outputs a frank pre-draft assessment of which O-1A/EB-1A criteria or NIW prongs are strong, moderate, weak, or unsupported — use only if you want that extra pass |
| [`publication-citation-table`](publication-citation-table/) | **Optional.** Summary table + TSV, lead picks for C5, C3 side list — from the index and optional Scholar/ORCID; tags Criterion 5 vs press (Criterion 3) and `NEEDS VERIFICATION` for publication-heavy cases |
| [`o1-petition-narrative`](o1-petition-narrative/) | Drafts O-1A/O-1B petition support letters — criterion-by-criterion arguments with exhibit references and evidence enrichment |
| [`eb1a-petition-narrative`](eb1a-petition-narrative/) | Drafts EB-1A green card petitions — same criteria as O-1A but stricter scrutiny, adds sustained acclaim totality argument, intent to continue work, and substantial U.S. benefit |
| [`niw-national-importance-research`](niw-national-importance-research/) | Researches authoritative gov sources, national plans, and federal funding — produces a quotable research document matched to the petitioner's background |
| [`niw-petition-narrative`](niw-petition-narrative/) | Drafts EB-2 NIW self-petition support letters using the Dhanasar three-prong framework |
| [`expert-letter-drafter`](expert-letter-drafter/) | Drafts expert/reference/recommendation letters — assigns criteria to experts by credential, ensures no two letters overlap, produces ready-to-customize drafts |
| [`petition-audit`](petition-audit/) | Audits any petition letter — verifies every factual claim against source documents, flags legal errors, checks internal consistency, produces severity-rated report |
| [`rfe-response-drafter`](rfe-response-drafter/) | Analyzes a USCIS RFE, diagnoses what went wrong in the original petition, maps each deficiency to a fix, and drafts the point-by-point response with new evidence strategy |

## Knowledge Base

The `knowledge/` directory contains best practices distilled from real cases and USCIS adjudication patterns. Skills read these files before drafting.

```
knowledge/
├── overview-o1a-eb1a.md       # O-1A/EB-1A standard, Kazarian framework
├── overview-niw.md            # NIW standard, Dhanasar framework
├── criteria/                  # Best practices per O-1A/EB-1A criterion
│   ├── 01-awards.md
│   ├── 02-membership.md
│   ├── 03-published-material.md
│   ├── 04-original-contributions.md
│   ├── 05-scholarly-articles.md
│   ├── 06-critical-employment.md
│   ├── 07-high-remuneration.md
│   └── 08-judging.md
├── prongs/                    # Best practices per NIW Dhanasar prong
│   ├── 01-substantial-merit.md
│   ├── 02-well-positioned.md
│   └── 03-national-interest-balance.md
├── evidence-hierarchy.md      # How USCIS weighs evidence (Tier 1–4)
├── argument-patterns.md       # Reusable argument structures
└── uscis-policy-alerts.md     # Key citations (PA-2022-03, Kazarian, Dhanasar)
```

## Workflow

```
Source documents
       ↓
document-summary-arrangement → document index (arranged by criterion)
       ↓
knowledge/ (read best practices)
       ↓
o1-petition-narrative              → O-1A petition package   ─┐
eb1a-petition-narrative            → EB-1A petition package  ─┤
niw-national-importance-research   → research document        │
  → niw-petition-narrative         → NIW petition package   ──┤
expert-letter-drafter              → expert letter drafts     │
                                                              ↓
                                             petition-audit → audit report
                                                              ↓
                                                     Attorney reviews & signs
```

*Optional, any time after the index exists (often before or during narrative drafting):* [`case-strength-assessor`](case-strength-assessor/) — pre-draft criterion/prong strength; [`publication-citation-table`](publication-citation-table/) — master publication/citation table for research-heavy petitions. **Neither is required;** skip if you do not need them.

## Sample Output

Here's what the skills actually produce — from a real test run on the Judging criterion:

### Evidence Research
Every entity is researched with facts traced to source documents and verified web URLs:

<img src="assets/sample-research.png" alt="Sample source registry showing verified facts from client documents and web research" width="700">

### Web Source Verification
Web sources are compiled with exact quotes, retrieval dates, and attorney action checkboxes:

<img src="assets/sample-sources.png" alt="Sample web sources with URLs, quotes, and attorney verification checklist" width="700">

### Petition Draft
The final draft uses ONLY sourced facts — every number has a citation:

<img src="assets/sample-draft.png" alt="Sample petition paragraph with sourced statistics and exhibit references" width="700">

---

Each petition package is a single file containing:
- The full support letter draft
- Source registry (every fact traced to a document or URL)
- Web sources the attorney needs to print for filing
- Evidence gaps and strength assessment

## Quick Start

### For attorneys
1. Install [Claude Code](https://docs.anthropic.com/en/docs/claude-code)
2. Clone this repo
3. Install dependencies:
   ```bash
   ./document-summary-arrangement/scripts/setup.sh
   ```
4. Point Claude at your client's documents:
   ```
   /document-summary-arrangement
   ```
5. Optionally assess case strength from the index before drafting:
   ```
   /case-strength-assessor
   ```
   For research-heavy clients, optionally normalize publications and citations:
   ```
   /publication-citation-table
   ```
6. Draft the petition:
   ```
   /o1-petition-narrative     # O-1A temporary visa
   /eb1a-petition-narrative   # EB-1A green card
   /niw-petition-narrative    # EB-2 NIW
   ```
7. Draft expert letters:
   ```
   /expert-letter-drafter
   ```
8. Audit before signing:
   ```
   /petition-audit
   ```

### For self-petitioning candidates
1. Install [Claude Code](https://docs.anthropic.com/en/docs/claude-code)
2. Clone this repo
3. Gather your documents (awards, memberships, publications, employment records, funding docs)
4. Index your documents:
   ```
   /document-summary-arrangement
   ```
5. Optionally see which criteria or prongs look strong or weak before drafting:
   ```
   /case-strength-assessor
   ```
   If you have many papers, optionally build a publication/citation table from the index:
   ```
   /publication-citation-table
   ```
6. For NIW — research your national importance argument:
   ```
   /niw-national-importance-research
   ```
7. Draft your self-petition:
   ```
   /eb1a-petition-narrative   # EB-1A self-petition
   /niw-petition-narrative    # NIW self-petition
   ```
8. Audit the draft:
   ```
   /petition-audit
   ```
9. **Take the draft to an immigration attorney for review before filing.**

## Scripts

Helper scripts for document processing in `document-summary-arrangement/scripts/`:

| Script | What It Does |
|--------|-------------|
| `setup.sh` | Installs dependencies (poppler for PDF tools) |
| `scan-collection.sh` | Scans a directory — reports file types, sizes, page counts, batch plan |
| `pdf-to-text.sh` | Extracts text from PDF (auto-detects scanned vs. text) |
| `pdf-to-images.sh` | Converts PDF pages to PNG for multimodal reading |
| `docx-to-text.sh` | Extracts text from .docx (macOS/Linux) |

## Who This Is For

- **Immigration attorneys** drafting O-1A, EB-1A, and NIW petitions who want structured, evidence-backed first drafts
- **Self-petitioning candidates** (EB-1A, NIW) who want to understand their case strength, organize evidence, and prepare a draft before engaging an attorney
- **Legal teams** that want to reduce time spent on document organization, research, and initial drafting

## What This Is NOT

- **Not legal advice.** Every output is a draft. An immigration attorney must review, edit, and sign before filing.
- **Not a replacement for an attorney.** Self-petitioning candidates should use these tools to prepare — then take the output to a licensed immigration attorney.
- **Not guaranteed to result in approval.** Petition outcomes depend on the facts, the evidence, and USCIS adjudication.

## Contributing

The knowledge base improves with every case. After a case outcome:
- Add anonymized best practices to the relevant `criteria/` or `prongs/` file
- Never commit client names, company names, or identifying details
- Keep entries concise and actionable

## Contact

For professional immigration guidance (EB-1, NIW, O-1), you can contact [Neo Global](https://www.neoglob.info/).

## License

MIT
