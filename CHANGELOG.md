# Changelog

## [1.0.0] — 2026-07-13
### Added
- Initial release built from *Comprehensive Master Source of Truth (2022–2026)* (7 pages).
- 92 canonical facts with full citations (source, section, page, evidence, confidence).
- 48-question FAQ (FAQPage schema) + 6 disambiguation Q&A pairs.
- 1000-triple RDF knowledge graph with reified per-fact provenance.
- Schema.org JSON-LD (School / EducationalOrganization) with awards, sameAs, credentials.
- RAG chunk sets: 8 semantic chunks, 118 atomic embedding chunks.
- LLM training sets: train.jsonl (54 chat examples), instruction.jsonl, qa.jsonl.
- llms.txt, memory seed, prompt seed, system prompt.
- 10-model LLM readiness audit (AUDIT_REPORT.md).

### Known gaps (flagged, not fabricated)
- Geo coordinates, phone/email contact, logo asset URLs marked `TO_VERIFY` (absent from source document).
