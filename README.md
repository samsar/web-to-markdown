# web2md

Convert an article URL to a Markdown file. Uses Mozilla Readability for direct extraction and falls back to [r.jina.ai](https://r.jina.ai) for paywalled or login-walled pages (LinkedIn, Medium, etc.).

## Requirements

Node.js 18+ (uses native `fetch`).

## Install

```bash
npm install
npm link        # makes `web2md` available globally
```

Or run without installing:

```bash
node web2md.js <url>
```

## Usage

```
web2md <url> [options]
```

| Option | Description |
|---|---|
| `-o, --out <path>` | Output path (default: `<slug>.md` in current directory) |
| `--stdout` | Write to stdout instead of a file |
| `--no-fallback` | Skip the r.jina.ai fallback on failure |
| `-h, --help` | Show help |

## Examples

Save to a file (auto-named from the article title):

```bash
web2md https://example.com/some-article
```

Specify the output path:

```bash
web2md https://example.com/some-article -o article.md
```

Pipe to stdout:

```bash
web2md https://example.com/some-article --stdout | pbcopy
```

Skip the Jina fallback:

```bash
web2md https://example.com/some-article --no-fallback
```

## Output format

Each file starts with YAML frontmatter:

```yaml
---
title: "Article Title"
author: "Author Name"
source: "https://..."
site: "Site Name"
published: "2024-01-01T00:00:00Z"
fetched_at: "2024-01-01T12:00:00Z"
via: "readability"
---
```

`via` is either `readability` (direct fetch) or `jina` (fallback).
