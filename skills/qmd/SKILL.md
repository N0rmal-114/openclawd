---
name: qmd
description: Search personal markdown knowledge bases, notes, meeting transcripts, and documentation using QMD - a local hybrid search engine. Combines BM25 keyword search, vector semantic search, and LLM re-ranking. Use when users ask to search notes, find documents, look up information in their knowledge base, retrieve meeting notes, or search documentation. Triggers on "search markdown files", "search my notes", "find in docs", "look up", "what did I write about", "meeting notes about".
license: MIT
compatibility: Windows/Bun. Uses local wrapper D:\MyProjects\Moltbot\MoltbotWorkspace\qmd.ps1
metadata:
  author: tobi
  version: "1.1.1"
allowed-tools: exec
---

# QMD - Quick Markdown Search (Local Wrapper)

QMD is a local, on-device search engine for markdown content. It indexes your notes, meeting transcripts, documentation, and knowledge bases for fast retrieval.

## QMD Status

`D:\MyProjects\Moltbot\MoltbotWorkspace\qmd.ps1 status`

## When to Use This Skill

- User asks to search their notes, documents, or knowledge base
- User needs to find information in their markdown files
- User wants to retrieve specific documents or search across collections
- User asks "what did I write about X" or "find my notes on Y"
- User needs semantic search (conceptual similarity) not just keyword matching
- User mentions meeting notes, transcripts, or documentation lookup

## Search Commands

All commands use the local wrapper script: `D:\MyProjects\Moltbot\MoltbotWorkspace\qmd.ps1`

| Command | Use When | Speed |
|---------|----------|-------|
| `...qmd.ps1 search` | Exact keyword matches needed | Fast |
| `...qmd.ps1 vsearch` | Keywords aren't working, need conceptual matches | Medium |
| `...qmd.ps1 query` | Best results needed, speed not critical | Slower |

```powershell
# Fast keyword search (BM25)
D:\MyProjects\Moltbot\MoltbotWorkspace\qmd.ps1 search "your query"

# Semantic vector search (finds conceptually similar content)
D:\MyProjects\Moltbot\MoltbotWorkspace\qmd.ps1 vsearch "your query"

# Hybrid search with re-ranking (best quality)
D:\MyProjects\Moltbot\MoltbotWorkspace\qmd.ps1 query "your query"
```

## Common Options

```powershell
-n <num>                 # Number of results (default: 5)
-c, --collection <name>  # Restrict to specific collection
--all                    # Return all matches
--min-score <num>        # Minimum score threshold (0.0-1.0)
--full                   # Show full document content
--json                   # JSON output for processing
--files                  # List files with scores
--line-numbers           # Add line numbers to output
```

## Document Retrieval

```powershell
# Get document by path
D:\MyProjects\Moltbot\MoltbotWorkspace\qmd.ps1 get "collection/path/to/doc.md"

# Get document by docid (shown in search results as #abc123)
D:\MyProjects\Moltbot\MoltbotWorkspace\qmd.ps1 get "#abc123"

# Get with line numbers for code review
D:\MyProjects\Moltbot\MoltbotWorkspace\qmd.ps1 get "docs/api.md" --line-numbers
```

## Index Management

```powershell
# Check index status and available collections
D:\MyProjects\Moltbot\MoltbotWorkspace\qmd.ps1 status

# List all collections
D:\MyProjects\Moltbot\MoltbotWorkspace\qmd.ps1 collection list

# Add current workspace to index (Run this first!)
D:\MyProjects\Moltbot\MoltbotWorkspace\qmd.ps1 collection add D:\MyProjects\Moltbot\MoltbotWorkspace --name workspace --mask "**/*.md"

# Generate embeddings (Run after adding files)
D:\MyProjects\Moltbot\MoltbotWorkspace\qmd.ps1 embed
```

## Score Interpretation

| Score | Meaning | Action |
|-------|---------|--------|
| 0.8 - 1.0 | Highly relevant | Show to user |
| 0.5 - 0.8 | Moderately relevant | Include if few results |
| 0.2 - 0.5 | Somewhat relevant | Only if user wants more |
| 0.0 - 0.2 | Low relevance | Usually skip |
