# MemoMind — AI Knowledge Engine

> Turn your documents into a searchable, conversational knowledge base.  
> Ask questions. Get cited answers. Never lose institutional memory again.

---

## What It Does

MemoMind lets you upload documents and query them using natural language.  
Instead of keyword search, it understands *meaning* — and always tells you  
exactly which part of which document the answer came from.

**Core capabilities:**
- Upload PDFs and documents → instantly queryable
- Citation-backed Q&A (answers link back to source paragraphs)
- Semantic search across all documents simultaneously
- Voice interaction for hands-free querying
- Secure document isolation per user/workspace

---

## Why I Built It

Our team kept losing decisions, context, and knowledge buried in old  
project files. People would re-research things that had already been  
figured out. MemoMind was built to fix that — give teams a memory.

The first time a colleague used it to recover a technical decision from  
18 months earlier in under 10 seconds, I knew it was solving a real problem.

---

## Architecture
```
User Query
    │
    ▼
Supabase Storage → LLaMA Parser → Document Chunking
    │
    ▼
Embeddings (OpenAI) → Supabase pgvector
    │
    ▼
Edge Function → Semantic Retrieval → LLM (OpenAI / Claude)
    │
    ▼
Citation-Backed Answer + Voice Response
```

**Stack:**
| Layer | Technology |
|---|---|
| Backend | Supabase Edge Functions (serverless) |
| Storage | Supabase Storage |
| AI / LLM | OpenAI, Claude, RAG, LLaMA Parser |
| Vector Search | Supabase (PostgreSQL + pgvector) |
| Embeddings | OpenAI Embeddings API |
| Search | Semantic Search, Vector Similarity |
| Voice | Web Speech API integration |
| Hosting | Vercel, Supabase |

---

## Key Technical Decisions

**Why RAG over fine-tuning?**  
Fine-tuning bakes knowledge into the model — it can't cite sources and  
goes stale as documents change. RAG retrieves fresh, current content  
at query time and always shows its work.

**Why Supabase Edge Functions over a traditional backend?**  
No server to manage, no cold-start overhead for this use case, and  
everything lives in one platform — storage, database, vector search,  
and serverless functions. Supabase Edge Functions handle document  
processing and LLM orchestration directly, keeping the stack lean  
and deployment instant via Vercel.

**Why document isolation per workspace?**  
This is a knowledge tool. Users must trust that their documents are  
not mixed with another organisation's data. Isolation is a first-class  
feature, not an afterthought.

---

## Results

- Reduced manual document lookup time by **over 50%** in internal use
- Sub-second semantic retrieval across large document sets
- Supports concurrent users with isolated, secure document contexts

---

## Status

> Core engine is functional and in active development.  
> Source code is private. Architecture overview and design decisions  
> are documented here.  
>
> **Live demo / walkthrough available on request.**

---

## Contact

Built by [Umar Farook M](https://umarfarook.vercel.app)  
[linkedin.com/in/umarfarookm](https://linkedin.com/in/umarfarookm)
