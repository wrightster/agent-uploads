# agent-uploads

Ephemeral staging ground for getting local-only images/documents into the JWRG
office (office.jwrgnc.com) via its MCP `attach-*-from-url` tools.

## Why this exists
The office fetches attachments server-side over SSRF-safe HTTP. That works for most
public URLs, but some sources can't be fetched directly:
- files that only exist locally (clipboard pastes, generated images) — no URL at all
- hosts that block the office's **datacenter IP** or bot requests (e.g. Wix
  `static.wixstatic.com` 403s the droplet even though a browser gets 200)

For those, drop the file here, push, and hand the office the `raw.githubusercontent.com`
URL — public, instant (no deploy), and not IP/bot-blocked.

## Workflow (for an agent)
1. `gh repo clone wrightster/agent-uploads /tmp/agent-uploads`
2. copy the file in, then `git add` / `commit` / `push`
3. attach via `https://raw.githubusercontent.com/wrightster/agent-uploads/main/<file>`
4. `git rm <file>` + commit/push to clean up — the office keeps its own copy

PUBLIC by necessity (the office fetcher is unauthenticated). Only ever holds
transient public marketing assets; anything here is safe to delete.
