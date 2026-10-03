---
anchor: knowledge
title: Knowledge bases
menu: Knowledge
order: 40
---
Nota's depth comes from two SQLite-vec databases queried with Voyage AI embeddings, which let
every skill ground its output in concrete sources rather than the model's general knowledge.

| Database | Scope | Storage |
|---|---|---|
| **`knowledge.db`** | [MusaDSL](https://musadsl.yeste.studio) documentation, API reference, 23 demo projects, 23 built-in composition best practices. | Downloaded to `~/.config/nota/`, refreshed when a new index is published. |
| **`private.db`** | Your indexed compositions (added with `/nota:index`), their musical analyses (created with `/nota:analyze`), and your custom best practices (`/nota:best-practices`). Search across them as easily as the public docs. | Local, in `~/.config/nota/`. Never leaves your machine. |
{: .libraries-table}

Both databases use [sqlite-vec](https://github.com/asg017/sqlite-vec){:target="_blank" rel="noopener"}
for vector storage and [Voyage AI](https://www.voyageai.com/){:target="_blank" rel="noopener"}
for high-quality multilingual code-aware embeddings. The plugin's MCP server exposes a
`search` tool that every skill consults transparently.
{: .section__note}
