# Copilot instructions for WireBox docs

## Project snapshot
- This repo is the WireBox manual (v7.x) written as GitBook-style Markdown; the root entry is README.md and the navigation lives in SUMMARY.md.
- Content is organized by topic folders (getting-started, configuration, usage, advanced-topics, extending-wirebox, aspect-oriented-programming), each with README.md as a section landing page.

## Documentation structure and patterns
- Pages commonly start with YAML front matter (e.g., description fields). See getting-started/overview.md for a typical header.
- Section landing pages are named README.md inside the folder; keep this convention when adding new sections.
- Use GitBook hints blocks for callouts: `{% hint style="info" %}...{% endhint %}` as shown in configuration/configuring-wirebox/README.md.
- Images and diagrams are stored in .gitbook/assets and referenced with relative paths like `![](<../.gitbook/assets/overview_WireBoxIcon (1).png>)` in getting-started/overview.md. Preserve the existing relative-path style and angle-bracket wrapping for assets with spaces.
- Internal links are relative Markdown links and should match SUMMARY.md paths (e.g., configuration/configuring-wirebox/README.md).

## Authoring conventions
- Keep headings and tone consistent with existing pages: concise H1, then short sections with bullets or short paragraphs.
- Code samples often use fenced blocks labeled `javascript` even for CFML snippets; mirror the local page style (see configuration/configuring-wirebox/README.md).
- When adding a new page, add it to SUMMARY.md in the correct section and keep ordering consistent.

## What is NOT in this repo
- There are no build/test scripts documented here; avoid inventing commands. If a workflow is needed, ask or check upstream ColdBox platform docs.

## Examples to follow
- Overview page structure and front matter: getting-started/overview.md
- GitBook hint blocks and code fences: configuration/configuring-wirebox/README.md
- Navigation structure: SUMMARY.md

## MCP For GitBook Formatting

https://gitbook.com/docs/~gitbook/mcp