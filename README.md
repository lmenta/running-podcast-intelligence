# Running Podcast Intelligence

Semantic search engine for running podcasts. Ask anything — get answers with timestamps and sources.

## Architecture

```
RSS Feeds → Crawler → Supabase (episodes)
                   → Modal (Whisper transcription)
                   → Embedding pipeline → pgvector
                   → FastAPI + Claude RAG → Next.js
```

## Setup

1. Copy `.env.example` to `.env` and fill in your keys
2. Create a Supabase project and run `supabase/migrations/001_initial_schema.sql`
3. Install dependencies: `pip install -e .`

## Phase 1 — Data Foundation

```bash
# Check all RSS feeds are reachable
python scripts/check_feeds.py

# Seed podcasts into Supabase
python scripts/seed_podcasts.py

# Crawl all feeds for new episodes
python scripts/crawl.py
```

## Project Structure

```
src/
  registry/     — Curated podcast list
  ingestion/    — RSS crawler
  transcription/— Whisper pipeline (Modal)
  embeddings/   — Chunking + embedding
  api/          — FastAPI backend
scripts/        — CLI tools
supabase/       — DB migrations
```
