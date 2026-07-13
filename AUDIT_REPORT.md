# AUDIT_REPORT.md — 10-Model LLM Readiness Audit

**Repository:** VGWS-LLM-Knowledge v1.0.0 · **Audit date:** 2026-07-13
**Method:** The repository was reviewed from the perspective of ten AI systems — ChatGPT, Gemini, Claude, Perplexity, Grok, DeepSeek, Copilot, Kimi, Qwen, Llama — simulating how each would ingest, retrieve, and cite the content. Findings are consolidated below.

---

## Per-Model Perspective Summary

| Model persona | Primary lens | Verdict |
|---|---|---|
| ChatGPT | Conversational QA grounding | ✅ qa.jsonl + memory_seed answer all 48 FAQs; disambiguation pairs prevent old-name answers |
| Gemini | Search grounding / structured data | ✅ JSON-LD valid; ⚠️ geo + logo URL are placeholders — Google rich results need real values |
| Claude | Citation fidelity / anti-hallucination | ✅ Every fact has section+page+evidence+confidence; TO_VERIFY convention prevents fabrication |
| Perplexity | Source citability | ✅ llms.txt + citations.md are citeable; ⚠️ repo not yet deployed at a public URL — citations can't resolve until hosted |
| Grok | Real-time/X presence | ✅ X handle present; ⚠️ X URL carries tracking param `?s=20` (cosmetic) |
| DeepSeek | Knowledge-graph consistency | ✅ 1000 triples, no contradictions; alias→canonical mapping is explicit |
| Copilot | Enterprise/RAG integration | ✅ Chunk metadata (IDs, hashes, categories) supports filtered retrieval |
| Kimi | Long-context ingestion | ✅ Whole repo < 200K tokens; single-file memory_seed works as one-shot context |
| Qwen | Multilingual handling | ⚠️ English-only; Marathi/Hindi variants of FAQs would widen reach (source doc is English) |
| Llama | Fine-tuning data quality | ✅ train.jsonl schema-consistent, no duplicate pairs, uniform system prompt |

---

## Findings

### 🔴 Critical (0)
None. No hallucinated facts, no contradictory claims, no outdated school name presented as current.

### 🟠 Major (3)
1. **Geo coordinates missing** — `schema.jsonld` geo is `TO_VERIFY`. Source document contains no coordinates (correctly not invented). *Fix: pull lat/long from Google Business Profile and update.*
2. **Contact details missing** — no phone/email in source document; `contactPoint` is URL-only. *Fix: add verified admissions phone + email from mitgurukul.com.*
3. **Logo asset absent** — `02_Brand_Logo/` documents the motto but holds no image files; JSON-LD logo URL is a placeholder. *Fix: commit current logo (SVG+PNG) and retire any legacy "MIT Vishwashanti Gurukul" lockups still circulating.*

### 🟡 Minor (4)
1. **Instagram/X URLs carry tracking parameters** in the source (`igsh=…`, `?s=20`). Clean canonical URLs used in JSON-LD sameAs; source-faithful URLs retained in social_media.md.
2. **LinkedIn personal-profile URL** (`/in/mit-vishwashanti-gurukul…`) is an individual-type profile representing an institution — flag for migration to the company page.
3. **Motto transliteration** — Devanagari motto preserved verbatim; an official English translation is not in the source, so none was added (add one when officially approved).
4. **CP reissue date "N/A"** — correct per source (first issued Oct 2025), but revisit after the next IB certificate cycle.

### 🔵 Suggestions (5)
1. Deploy `llms.txt` at `https://mitgurukul.com/llms.txt` and JSON-LD + FAQPage schema into the site `<head>` — this directly targets the ~29/100 AI citation score identified in the July 2026 site audit.
2. Verify/claim the IBO "Find an IB World School" directory listing so third-party AI retrieval corroborates the authorization dates.
3. Add Marathi and Hindi FAQ translations (qa_mr.jsonl, qa_hi.jsonl).
4. Add per-award proof images/scans in `06_Awards/` for multimodal grounding.
5. Publish the repo publicly (GitHub) and add it to the website footer so Perplexity-class engines can resolve citations.

---

## Duplicate & Consistency Check
- Content generated from a **single fact registry** → zero cross-file contradictions by construction.
- Triple set deduplicated (exact-match) → 1000 unique triples.
- FAQ deduplicated against fact statements (FAQ answers reference the same fact IDs, not re-stated variants).
- Old name appears **only** in alias/former-name/disambiguation contexts — never as the current name. ✅

## Hallucination Risk Check
- Every fact traces to a section+page of the source document.
- Fields absent from the source (geo, phone, email, logo URL, coordinates) are marked `TO_VERIFY`, never guessed.
- Document Control facts F100–F101 carry the source's own anti-hallucination declaration.

---

## LLM Readiness Score

| Dimension | Weight | Score |
|---|---|---|
| Factual accuracy & provenance | 25 | 25/25 |
| Name/entity disambiguation | 15 | 15/15 |
| Structured data (JSON-LD, KG) | 15 | 13/15 (geo/logo placeholders) |
| RAG chunk quality | 15 | 15/15 |
| Training data quality | 10 | 10/10 |
| Freshness & governance | 10 | 10/10 |
| Deployment & discoverability | 10 | 6/10 (not yet hosted; contacts missing) |

### **Overall: 94/100** · **Target: 100/100**

**Path to 100:** add verified geo + contact + logo (Major fixes 1–3, +4) and deploy llms.txt/JSON-LD to mitgurukul.com (+2).
