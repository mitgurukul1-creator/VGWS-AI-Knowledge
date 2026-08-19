# VGWS Press Release Archive — RAG / AEO / GEO / PEO File Package

**Vishwashanti Gurukul World School (VGWS)** | 3 press releases | 38 tracked distribution/citation links
Prepared: August 2026

This package covers a different content type than the earlier FAQ Bank package: **press releases and their third-party media pickup data**, extracted from your three distribution reports (MIT_VISHWASHANTI.pdf, Report_basic_NW_2611.pdf, Report_NWpplus_1710.pdf) and the PR_Links.xlsx tracking sheet.

## Important: upload this into its own folder, not the repo root

Your `VGWS-AI-Knowledge` GitHub repo already has three prior batches sharing generic filenames (`README.md`, `llms.txt`, `faq.json`, `schema.jsonld`, etc.), where each new upload silently overwrote the last one's version. **Do not repeat that here.** Upload this package into a dedicated subfolder — e.g. `press-releases/` — so these filenames never collide with the FAQ bank or identity/knowledge-graph batches already in the repo. The `llms.txt` file in this package is deliberately named `llms-press-releases.txt` rather than `llms.txt` for the same reason; if you want it discoverable at the root `llms.txt`, add a link to it from your one root-level `llms.txt` instead of overwriting that file.

## Files in this package

| File | Format | Purpose |
|---|---|---|
| `VGWS_PressRelease_Master.docx` | Word | Human review, source-of-record formatting |
| `VGWS_PressRelease_Master.xlsx` | Excel (4 sheets: Press Releases, Distribution Links, Accuracy Flags, Dataset Info) | Editing, filtering, handoff to your team |
| `VGWS_PressRelease_Chunks.csv` | CSV | Spreadsheet tools, bulk import |
| `VGWS_PressRelease_Master.json` | JSON (nested) | Full dataset: releases + all 38 distribution links, preserves structure |
| `VGWS_PressRelease_Chunks.json` | JSON (flat, RAG-ready) | **Primary file for vector databases** — 28 chunks (3 full releases + 25 grouped citation records), each with metadata |
| `VGWS_PressRelease_Chunks.md` | Markdown | Readable archive page, best format for AI crawler parsing |
| `VGWS_PressRelease_Chunks.txt` | Plain text | Simplest ingestion for embedding pipelines |
| `VGWS_PressRelease_schema.jsonld` | Schema.org JSON-LD | `NewsArticle` structured data for the three releases — embed in the live press-release pages' `<head>` |
| `llms-press-releases.txt` | Plain text (llms.txt-style) | Namespaced summary file — link to it from your root `llms.txt`, don't replace that file with this one |

## Two accuracy issues found in your own source material

Before this goes into a public repo or gets cited by an AI system, these are worth resolving — they're documented in full in the "Accuracy Flags" sheet of the xlsx and inline in the JSON/MD records:

1. **Sports programme count conflicts.** This ranking press release states VGWS offers **"18+ sports."** The FAQ Bank processed in the earlier session states **"21+ sports."** Two official VGWS sources disagree — an AI system citing either number could be wrong. Confirm the current figure.
2. **Arpit Sharma's title conflicts.** The Annual Day 2024 release calls him **"Vice Principal."** The IBCP authorization release calls him **"the Principal."** Confirm his correct, current title before either release circulates further as an AI-citable source.

Neither of these was invented — both come directly from the two source PDFs you uploaded, compared against each other and against the FAQ Bank from your last session.

## Ingesting into vector databases

`VGWS_PressRelease_Chunks.json` drops directly into Pinecone, ChromaDB, FAISS, Azure AI Search, OpenSearch, Elasticsearch, LangChain, or LlamaIndex the same way the FAQ chunks did — embed the `text` field, use `metadata` for filtering. Note the `type` field distinguishes `press_release` chunks (full article text) from `press_citation` chunks (which outlet published which headline) — you may want to filter or weight these differently depending on your retrieval use case.

## Platform notes

Same guidance as the FAQ Bank package applies: live-browsing platforms (ChatGPT, Gemini, Claude, Perplexity, Grok, Copilot) are reached through what's actually published on mitgurukul.com plus indexed third-party coverage — the 38 distribution links in this package are themselves useful evidence of that third-party coverage, since a well-cited press release across 38 independent outlets is a stronger AEO/GEO signal than the same content sitting only in your own repo. Open-weight models (DeepSeek, Qwen, Llama, Kimi) benefit primarily from this same third-party coverage entering their training data over time, not from the GitHub repo directly.
