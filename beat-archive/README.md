# Beat archive

This folder is for Module 4. You'll add journalism documents here and connect Claude to them using MCP (Model Context Protocol), turning this folder into a searchable knowledge base.

## What to put here

Add documents relevant to your beat. Organize them by type:

```
beat-archive/
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

Once you configure MCP (see `mcp-configs/`), Claude can search these documents, pull specific information, and cite the source file in its answers. The more documents you add, the more useful the queries become.

## Tips

- Use descriptive filenames — they show up in citations
- Keep documents focused (one meeting's minutes per file, not a year's worth in one file)
- Add new documents as you get them — the archive grows with your beat
