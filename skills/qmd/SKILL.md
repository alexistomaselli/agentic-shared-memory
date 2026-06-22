---
name: qmd
description: Search markdown knowledge bases, notes, and documentation using QMD. Use when users ask to search notes, find documents, or look up information.
license: MIT
compatibility: Requires qmd CLI or MCP server. Install via `npm install -g @tobilu/qmd`.
metadata:
  author: tobi
  version: "2.0.0"
allowed-tools: Bash(qmd:*), mcp__qmd__*
---

# QMD - Quick Markdown Search

Local search engine for markdown content. Essential for Agentic Shared Memory (ASM).

## Workspace Index

In this workspace, always use the dedicated index for the project (e.g. `<project-name>-asm`):

```bash
qmd --index <project-name>-asm ...
```

## Status

!`qmd --index <project-name>-asm status 2>/dev/null || echo "Not installed: npm install -g @tobilu/qmd"`

## MCP: `query`

```json
{
  "searches": [
    { "type": "lex", "query": "CAP theorem consistency" },
    { "type": "vec", "query": "tradeoff between consistency and availability" }
  ],
  "collections": ["docs"],
  "limit": 10
}
```

### Query Types

| Type | Method | Input |
|------|--------|-------|
| `lex` | BM25 | Keywords — exact terms, names, code |
| `vec` | Vector | Question — natural language |
| `hyde` | Vector | Answer — hypothetical result (50-100 words) |

### Writing Good Queries

**lex (keyword)**
- 2-5 terms, no filler words
- Exact phrase: `"connection pool"` (quoted)
- Exclude terms: `performance -sports` (minus prefix)
- Code identifiers work: `handleError async`

**vec (semantic)**
- Full natural language question
- Be specific: `"how does the rate limiter handle burst traffic"`
- Include context: `"in the payment service, how are refunds processed"`

**hyde (hypothetical document)**
- Write 50-100 words of what the *answer* looks like
- Use the vocabulary you expect in the result

**expand (auto-expand)**
- Use a single-line query (implicit) or `expand: question` on its own line
- Lets the local LLM generate lex/vec/hyde variations
- Do not mix `expand:` with other typed lines — it's either a standalone expand query or a full query document

### Intent (Disambiguation)

When a query term is ambiguous, add `intent` to steer results:

```json
{
  "searches": [
    { "type": "lex", "query": "performance" }
  ],
  "intent": "web page load times and Core Web Vitals"
}
```

Intent affects expansion, reranking, chunk selection, and snippet extraction. It does not search on its own — it's a steering signal that disambiguates queries like "performance" (web-perf vs team health vs fitness).

### Combining Types

| Goal | Approach |
|------|----------|
| Know exact terms | `lex` only |
| Don't know vocabulary | Use a single-line query (implicit `expand:`) or `vec` |
| Best recall | `lex` + `vec` |
| Complex topic | `lex` + `vec` + `hyde` |
| Ambiguous query | Add `intent` to any combination above |

First query gets 2x weight in fusion — put your best guess first.

### Lex Query Syntax

| Syntax | Meaning | Example |
|--------|---------|---------|
| `term` | Prefix match | `perf` matches "performance" |
| `"phrase"` | Exact phrase | `"rate limiter"` |
| `-term` | Exclude | `performance -sports` |

Note: `-term` only works in lex queries, not vec/hyde.

### Collection Filtering

```json
{ "collections": ["docs"] }              // Single
{ "collections": ["docs", "notes"] }     // Multiple (OR)
```

Omit to search all collections.

## Other MCP Tools

| Tool | Use |
|------|-----|
| `get` | Retrieve doc by path or `#docid` |
| `multi_get` | Retrieve multiple by glob/list |
| `status` | Collections and health |

## CLI Examples

```bash
qmd --index <project-name>-asm query "question"              # Auto-expand + rerank
qmd --index <project-name>-asm query $'lex: X\nvec: Y'       # Structured
qmd --index <project-name>-asm query $'expand: question'     # Explicit expand
qmd --index <project-name>-asm query --json --explain "q"    # Show score traces
qmd --index <project-name>-asm search "keywords"             # BM25 only (no LLM)
qmd --index <project-name>-asm get "#abc123"                 # By docid
qmd --index <project-name>-asm multi-get "qmd://docs/*" -l 40
qmd --index <project-name>-asm multi-get qmd://docs/foo.md,qmd://decisions/bar.md
```

## HTTP API

```bash
curl -X POST http://localhost:8181/query \
  -H "Content-Type: application/json" \
  -d '{"searches": [{"type": "lex", "query": "test"}]}'
```

## Setup

```bash
npm install -g @tobilu/qmd
qmd --index <project-name>-asm collection list
qmd --index <project-name>-asm embed
```