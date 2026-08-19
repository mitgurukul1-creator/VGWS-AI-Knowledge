# VGWS AI Knowledge Base — RAG / AEO / GEO / PEO File Package

**Vishwashanti Gurukul World School (VGWS), Pune, India — MAEER MIT Group**
Prepared: August 2026 | 173 Q&A pairs | 11 topic sections

This package converts the VGWS Master FAQ Bank into machine-readable formats for two distinct goals that are worth telling apart before you upload anything:

1. **AI visibility (AEO/GEO)** — being cited or paraphrased correctly by answer engines and chatbots (ChatGPT, Gemini, Claude, Perplexity, Grok, Copilot, DeepSeek, Qwen, Llama, Kimi) when a parent asks them about VGWS.
2. **RAG infrastructure** — feeding this same content into a vector database so VGWS's *own* chatbot/search tools can answer accurately.

The same underlying 173 Q&A pairs power both goals — only the packaging differs. A note on scope: rather than producing ten duplicate copies of identical content re-labelled per model, this package gives you one accurate master dataset in every format a model or vector store actually needs, plus the platform-specific notes below on how each one actually gets to your content.

## File-by-file guide

| File | Format | Best for |
|---|---|---|
| `VGWS_Master_FAQ_Bank.docx` | Word | Human review, internal sign-off, source-of-record before publishing |
| `VGWS_Master_FAQ_Bank.xlsx` | Excel (3 sheets: All FAQ Q&A, Section Index, Dataset Info) | Editing, filtering, handoff to content/marketing team |
| `VGWS_RAG_Chunks.csv` | CSV | Spreadsheet tools, SQL-style/bulk import into most CMS or CRM systems |
| `VGWS_RAG_Master.json` | JSON (nested) | Preserves the full section → subsection → Q&A hierarchy; good for custom pipelines that need document structure |
| `VGWS_RAG_Chunks.json` | JSON (flat, RAG-ready) | **Primary file for vector databases** — one chunk per Q&A with metadata (section, subsection, source, URL, tags) already attached |
| `VGWS_RAG_Chunks.md` | Markdown | Website FAQ page source, GitHub README-style publishing, and the format LLM crawlers parse most reliably |
| `VGWS_RAG_Chunks.txt` | Plain text | Simplest possible ingestion for any embedding pipeline that just wants delimited text blocks |
| `VGWS_FAQPage_schema.jsonld` | Schema.org JSON-LD | Embed in the `<head>` of the live FAQ webpage — this is what tells Google/Bing/AI crawlers "this is structured FAQ data" |
| `llms.txt` | Plain text (llms.txt standard) | Place at `mitgurukul.com/llms.txt` — an emerging convention AI crawlers check for a curated summary + links to canonical content |

## Ingesting into vector databases

`VGWS_RAG_Chunks.json` is pre-chunked one-Q&A-per-record with metadata, so it drops in directly:

- **Pinecone / ChromaDB / FAISS / Weaviate:** embed the `text` field of each chunk; store the `metadata` object as-is for filtering (by section, subsection, etc.).
- **Azure AI Search / OpenSearch / Elasticsearch:** index `text` as the searchable field, `metadata.*` as filterable/facetable fields.
- **LangChain / LlamaIndex:** load via their JSON loaders — each record already matches the `Document(page_content, metadata)` shape both frameworks expect.
- **NotebookLM:** upload `VGWS_RAG_Chunks.md` or the `.docx` directly — NotebookLM handles chunking internally.

## Platform notes — how each AI system actually reaches this content

Not every model in your list works the same way, and this matters for where you spend effort:

- **Live-web-browsing models (ChatGPT with browsing, Gemini, Claude, Perplexity, Grok, Copilot):** These retrieve content at answer-time via search/crawling. Priority actions: publish `VGWS_RAG_Chunks.md` content as an actual FAQ page on mitgurukul.com, embed the JSON-LD schema in that page's `<head>`, and add `llms.txt` at the site root. Perplexity and Copilot (Bing-backed) weight structured data and schema markup especially heavily.
- **Open-weight models (DeepSeek, Qwen, Llama, Kimi):** These are not live-browsing by default — their base knowledge comes from what was in their pretraining corpus, and any "visibility" in a deployed product depends on that product's own retrieval layer (if any) rather than the base model. The highest-leverage move here is making sure this content exists in high-authority, frequently-crawled locations (a public GitHub repo, Wikipedia-adjacent citations, well-linked press coverage) that are likely to be swept into future training corpora — not expecting instant pickup.
- **Google Gemini specifically:** benefits doubly from being both a live-browsing assistant and from Google's own index (AI Overviews) — so standard technical SEO (site speed, mobile, structured data) still compounds here more than for other platforms.
- **GitHub as a distribution channel:** publishing this repo publicly (as you're planning) helps the open-weight/training-corpus category directly, and helps live-browsing models indirectly since GitHub pages are heavily crawled and often surfaced in search results for exact-match queries.

## Before publishing

The source FAQ bank itself flags this, and it's worth repeating: validate figures that change over time (fees, current-year staffing, current-year award listings, named individuals in role) against live mitgurukul.com pages before this goes into any public repo, llms.txt, or chatbot training set. Everything else in this package is a direct, unmodified restructuring of the FAQ bank content you provided — nothing has been invented or altered beyond formatting.

## Official channels (for attribution / schema)

mitgurukul.com | admissions@mitgurukul.com | +91 7897894804 | Instagram @mitgurukulofficial | Facebook MITGurukulOfficial | LinkedIn MIT Vishwashanti Gurukul | YouTube @Mitgurukulpune
