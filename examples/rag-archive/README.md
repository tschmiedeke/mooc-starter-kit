# Optional — local RAG archive

This folder is for students who want to try the optional Module 4 exercise: load a corpus of beat-specific documents into a searchable archive that Claude can query.

This is no longer the main Module 4 exercise. The current Module 4 focuses on context management, sub-agents, and cross-model review — see `docs/context-management.md` and `docs/cross-model-review.md`. But if you want to wire up local RAG over your own documents, here's the folder to do it in.

## What to put here

Add documents relevant to your beat. Organize them by type:

```
examples/rag-archive/
|-- council-minutes/
|   +-- council-minutes-2024-03.md
|-- press-releases/
|   +-- park-closure-announcement.md
|-- budget-docs/
|   +-- fy2025-budget-memo.md
+-- interviews/
    +-- martinez-interview-notes.md
```

Markdown (`.md`) and plain text (`.txt`) work best. Claude can also read `.html` and `.pdf` files.

## How it works

One way to make this folder queryable is to point an MCP filesystem server at it — see `mcp-configs/` for an example. With that wired up, Claude can search these documents, pull specific information, and cite the source file in its answers. The more documents you add, the more useful the queries become.

Note: MCP is now framed as optional advanced material in this kit, not a required Module 4 component. You can also just paste documents into the conversation, or read them with the file tools, depending on how often you need them.

## Tips

- Use descriptive filenames — they show up in citations
- Keep documents focused (one meeting's minutes per file, not a year's worth in one file)
- Add new documents as you get them — the archive grows with your beat
