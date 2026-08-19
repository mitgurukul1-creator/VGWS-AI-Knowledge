# VGWS IB Authorizations — Production RAG Knowledge Base

Production-ready knowledge base for **Vishwashanti Gurukul World School's International Baccalaureate authorizations** (PYP, MYP, DP, CP), derived from four source IB certificates.

## Provenance and Integrity

- **Source documents:** `PYP IB Certificate .pdf`, `MYP Certificate .pdf`, `DP IB Certificate .pdf`, `CP IB Certificates.pdf` (as referenced in the master repository).
- **Deduplication:** The two uploaded repository files (`.txt` and `.docx`) contained identical content; they were merged into a single canonical set.
- **Fidelity guarantees:** Every factual statement from the source repository is preserved. No information has been invented. Fields not stated in the source are marked `"Not specified in source"` or `null`.

## File Manifest

| File | Format | Purpose |
|---|---|---|
| `knowledge_base.md` | Markdown | Human-readable canonical knowledge base (overview, program records, governance, relationships, retrieval anchors, implementation guide, validation rules, keywords) |
| `knowledge_base.json` | JSON | Complete structured representation (school profile, authorizations, governance, relationships, anchors, rules) |
| `knowledge_base.jsonl` | JSONL | 9 RAG-ready chunks, one JSON record per line, each with `id`, `type`, `title`, `text`, `metadata` — ready for embedding pipelines |
| `schema.jsonld` | JSON-LD | Schema.org graph: `School`, `Organization`, `Person`, and four `EducationalOccupationalCredential` nodes — suitable for website structured data / AI visibility |
| `llms.txt` | Text (llms.txt spec) | AI-crawler-friendly summary with key facts, timeline, and file index |
| `entities.json` | JSON | Entity extraction (institution, governing body, programs, individuals, locations) plus subject–predicate–object relationship triples |
| `metadata.json` | JSON | Field-level metadata with source attribution and KB info |
| `citations.json` | JSON | Fact-to-source-certificate citation mapping (9 citations) |
| `faq.json` | JSON | 9 Q&A pairs derived strictly from source facts, each with source attribution |
| `README.md` | Markdown | This file |

## Key Facts at a Glance

| Program | Original Issue | Reissue | Scope |
|---|---|---|---|
| DP | May 2006 | November 2025 | Not specified in source |
| PYP | April 2009 | November 2025 | Not specified in source |
| MYP | April 2018 | November 2025 | Years 1, 2, 3, 4 and 5 |
| CP | October 2025 (authorization date) | None listed | Not specified in source |

- **Governing body:** International Baccalaureate (Baccalauréat International / Bachillerato Internacional)
- **Director General:** Olli-Pekka Heinonen, Geneva (signature appears as "Olli-Pekha Hein"; standardized per validation Rule 2)
- **Authentication:** Hologram and watermark present on all certificates
- **Status:** Authorized; most recent authorization/reissue window October–November 2025

## Data Validation Rules (embedded in KB)

1. MYP recorded with explicit scope "Years 1, 2, 3, 4 and 5."
2. Director General standardized as "Olli-Pekka Heinonen" (from signature "Olli-Pekha Hein").
3. CP certificate date is October 2025; DP, MYP, PYP reissue dates are November 2025.
4. Program titles stored in full English nomenclature per source headers.
5. Hologram and watermark presence is a mandatory condition for record activation (`has_physical_security_features: true`).

## Usage

- **RAG ingestion:** Embed each line of `knowledge_base.jsonl`; use `metadata` fields for filtering (e.g., `type: program_authorization`).
- **Structured queries:** Load `knowledge_base.json` or `entities.json` for graph/lookup use cases.
- **Web/AI visibility:** Embed `schema.jsonld` in the school website's `<head>` and serve `llms.txt` at the site root.
- **Audit trails:** Use `citations.json` to trace any fact back to its source certificate.

## Validation

All files were machine-validated before delivery: JSON/JSONL/JSON-LD files parse cleanly (`json.load` / per-line `json.loads`), JSON-LD `@id` references resolve within the graph, and cross-file fact consistency (dates, scope, names) was verified against the source repository.
