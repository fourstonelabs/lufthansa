# LH467 Cancellation Claim — Booking 7MNCBE

Claim package for the cancellation of **Lufthansa flight LH467** (San Diego → Munich), **23 June 2026**, affecting four passengers on a single booking. Prepared for submission to Lufthansa under **EU261** and for reimbursement of documented expenses.

**Contact:** Gordon Kelly · gordon.kelly@gmail.com · +1 858 449-2066

---

## What we are asking Lufthansa

| # | Ask | Amount |
|---|-----|--------|
| 1 | **EU261 compensation** (Art. 7) — 4 passengers | **€2,400** reference (4 × €600) |
| 2 | **Reimbursement of documented out-of-pocket expenses** (meals, transport, baggage) | **$1,337.91** |
| 3 | **UA replacement-itinerary baggage** (outbound) — *highlighted separately; already included in #2* | **$210.00** |
| 4 | **Hertz prepaid rental loss** (Kraków; pro-rata for delayed pickup) — separate from #2 | **$121.39** |

**Documented expense breakdown ($1,337.91):**

- Transportation **$257.39** — Ubers (Attachments M, O, Y)
- Meals **$330.52** — Melt, lunch 24 Jun, Karl Strauss dinner (N, U, V, W)
- Baggage **$750.00** — LH excess $540 (T) + UA outbound $210 (J)

**Basis (summary):** Lufthansa cancelled after boarding; written reason “lack of the planned crew,” consistent with duty-time limits after Lufthansa’s own delays. No Art. 9 care (hotel/meals/vouchers) was provided.

---

## Repository layout

```
lufthansa/
├── README.md                 ← this file
├── executive_summary.md      ← Document 1: cover letter, EU261, expenses, requests
├── evidentiary_record.md     ← Document 2: chronology, witness, attachment index A–Z
├── evidence.pdf              ← Master evidence bundle (91 pp, attachments A–Z)
├── submission/               ← Ready-to-upload files (≤3.7 MB each)
│   ├── 1_executive_summary.pdf
│   ├── 2_evidentiary_record.pdf
│   ├── 3_01_evidence_ABCDEF.pdf
│   ├── 3_02_evidence_F-O.pdf
│   ├── 3_03_evidence_O-Z.pdf
│   ├── 4_form_submission_failure.png
│   └── EMAIL_DRAFT.txt
├── sources/
│   └── form_submission_failure.png
└── receipts/
    ├── meals/
    ├── transportation/
    ├── accommodation/        ← empty (returned home; see README.txt)
    ├── communication/        ← empty (see README.txt)
    └── others/
```

| File | Role |
|------|------|
| `executive_summary.md` | Short claim letter — read **first** by reviewer |
| `evidentiary_record.md` | Full narrative, witness, index — read **second** |
| `evidence.pdf` | All supporting documents (tickets, emails, receipts, photos) |
| `submission/*.pdf` | Same content, split for Lufthansa’s upload size limit |
| `submission/EMAIL_DRAFT.txt` | Email body + addresses for fallback submission |
| `receipts/*/*.jpg` | Individual expense receipts by category (meals, transportation, others) |

**Attachment index (A–Z):** See section 10 of `evidentiary_record.md`. Inline `(Attachment X)` references in the markdown match divider pages in `evidence.pdf`.

---

## How to submit

### 1. Online form (attempted — failed 26 Jun 2026)

**URL:** [Lufthansa Fast Compensation (EU261)](https://www.lufthansa.com/us/en/fast-compensation.html)

The form returned an **unexpected error** after receipt upload (see `submission/4_form_submission_failure.png`, Attachment Z). If retrying:

- Upload files from `submission/` **in numeric order** (1 → 3_03)
- Upload individual receipts from `receipts/` — if the form shows **0.000 MB**, re-select the file or use a smaller JPG
- Do **not** refresh the page after an error (Lufthansa's own message)

### 2. Email submission (recommended fallback)

Use **`submission/EMAIL_DRAFT.txt`** — copy the body, attach:

1. `1_executive_summary.pdf`
2. `2_evidentiary_record.pdf`
3. `3_01_evidence_ABCDEF.pdf`
4. `3_02_evidence_F-O.pdf`
5. `3_03_evidence_O-Z.pdf`
6. `4_form_submission_failure.png`

**Send to:** `customer.relations@lufthansa.com`  
**Alternative:** [Lufthansa USA Customer Relations form](https://www.lufthansa.com/us/en/local-page/customer-relations-usa) (paste same body + attachments)

**Mail (certified):** Lufthansa Customer Relations · 1400 RXR Plaza, West Tower · Uniondale, NY 11556  
**Phone:** +1 (516) 738-4422

### 3. Upload rules (online form)

| Rule | Detail |
|------|--------|
| **Max size** | **3.7 MB per file** (decimal: 3,700,000 bytes) |
| **Formats** | PDF, JPEG, JPG, PNG |
| **Filenames** | Avoid `# $ % ^ * ( ) [ ]` in names |
| **Multiple files** | Allowed — use all five files above |

Do **not** upload `evidence.pdf` as a single file (~33 MB) — it exceeds the limit.

### 4. What to paste in free-text fields

Use the executive summary opening: cancellation date, four passengers, ~2-day delay to Kraków (rebooked arrival **26 Jun 2026, 09:30**), EU261 reference amount **€2,400**, documented expenses **$1,337.91**, and point to attached PDFs for detail.

---

## Rebuilding the submission pack

After editing the markdown or `evidence.pdf`, regenerate the upload files.

### Letter PDFs (requires [Pandoc](https://pandoc.org/) + [Tectonic](https://tectonic-typesetting.github.io/))

`build_submission.py` uses Pandoc + Tectonic for letter PDFs (proper table layout). To rebuild letters only:

```bash
pandoc executive_summary.md -o submission/1_executive_summary.pdf \
  --pdf-engine=tectonic -V geometry:margin=1in -V fontsize=10pt

pandoc evidentiary_record.md -o submission/2_evidentiary_record.pdf \
  --pdf-engine=tectonic -V geometry:margin=1in -V fontsize=10pt
```

Tectonic may download LaTeX packages on first run (needs network).

### Evidence chunks (requires Python + PyMuPDF)

Evidence pages are **rasterized at 150 dpi** and bin-packed into three PDFs under the decimal 3.7 MB limit. Rebuild with `python3 build_submission.py` after editing markdown or `evidence.pdf`.

Individual receipt JPGs for the expense form: `python3 extract_receipts.py` → `receipts/{meals,transportation,others}/`.

**Master copy:** Always keep `evidence.pdf` as the full-resolution source; `submission/3_*.pdf` are upload-optimized copies.

---

## Status / next steps

- [x] Claim narrative, expenses, and attachment index aligned (A–Y)
- [x] Sentence-level verification: markdown → Tectonic PDFs complete
- [x] Submission pack: 5 PDFs + form failure screenshot, all under 3.7 MB
- [x] Online form attempted — error documented (Attachment Z)
- [ ] **Submit by email** — see `submission/EMAIL_DRAFT.txt`
- [ ] Optional: retry online form if portal recovers
- [ ] Optional: clarify request #3 wording so UA $210 is noted as *included in* #2 total (avoid double-count impression)
- [x] `build_submission.py` + `submission/MANIFEST.txt` for one-command rebuilds
- [ ] Optional: add `.gitignore` for `.venv/`, local audit/temp folders
- [ ] Retain Lufthansa confirmation / reference number after submission

---

## Quick reference

| Field | Value |
|-------|--------|
| Booking | **7MNCBE** |
| Flight | **LH467** SAN → MUC |
| Cancelled | 23 Jun 2026 |
| Passengers | Gordon, Barbara, Oliver, Alexander Kelly |
| Rebooked | UA1069 (SAN→ORD) + LO2098 (ORD→KRK) |
| Arrival KRK | 26 Jun 2026, ~09:30 |
