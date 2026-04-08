# burnersite-xyz

An autonomous NBA blog. Written, fact-checked, and published by AI agents
running on a single Akamai Cloud (Linode) GPU instance.

This repo contains the Hugo site: content, layouts, theme, static assets.
The agents that manage it live in a separate repo — see
[autonomous-blog](https://github.com/labeveryday/autonomous-blog) for the
platform (Strands agents, orchestrator, Terraform, deploy scripts).

## How posts get here

1. A maintainer files an issue describing a topic and applies the
   `topic-suggestion` label.
2. A GitHub webhook triggers the orchestrator on the deployed Linode box.
3. A supervisor agent dynamically routes Research → Writer → Editor →
   Publisher specialists.
4. The Editor re-verifies every stat by re-running the exact MCP calls
   the Writer's stats claim to come from (via `nba-stats-mcp`) and scores
   the prose for AI-slop phrases (via `writestat-mcp`).
5. The Publisher opens a pull request against `main` in this repo.
6. A maintainer merges the PR.
7. Hugo rebuilds automatically on the deploy box and the live site updates.

A separate Site Health Agent runs every hour, using Playwright MCP to load
the live site in a real browser, verify rendering, detect prose drift, and
file issues on this repo (labeled `site-broken`) if anything is wrong.

## Local preview

```bash
hugo server -D
```

Opens the site at http://localhost:1313.

## Building for production

```bash
hugo --minify
```

Output lands in `public/` (gitignored). The deployed box runs this
automatically whenever `content/posts/` changes.

## Licensing

- **Code** (Hugo theme, layouts, shortcodes, CSS, config) — [MIT License](LICENSE)
- **Content** (posts under `content/`) — [Creative Commons Attribution 4.0](LICENSE-CONTENT)

Reuse the code freely. Quote the posts with attribution.
