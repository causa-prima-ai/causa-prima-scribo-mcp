<img width="3840" height="1920" alt="A3 _ MCP server" src="https://github.com/user-attachments/assets/21e2cf1e-69c0-414c-9cee-180a60c17f51" />

# Scribo MCP Server
<img src="./icon.svg" alt="Scribo" width="96" align="right" />

> Free, AI-native e-invoicing — for any MCP client.

## Contents

- [What is Scribo?](#what-is-scribo)
- [What is the Scribo MCP server?](#what-is-the-scribo-mcp-server)
- [Getting started](#getting-started)
- [Usage](#usage)
- [Compliance](#compliance)
- [FAQ](#faq)
- [Resources](#resources)
- [License](#license)
- [Previous README](#previous-readme)

## What is Scribo?

Scribo is a free, conversational e-invoicing tool. Describe an invoice in plain language — "bill Acme GmbH €2,400 for May design work" — and it drafts a structured invoice for you to review, download and send directly.

Just ask your AI agent about Scribo: it ships as an MCP server, a CLI, and a Claude/Codex skill, alongside a public HTTP API and a web app. Free forever — no credit card. You just need a sender email.

**Built by Causa Prima** — Scribo is built by [**Causa Prima**](https://causaprima.ai/), a company building agentic AI for the CFO office. It's our first freely available skill — an early glimpse of what we're building.

## What is the Scribo MCP server?

> 🚧 Being migrated into Scribo's shared README structure — for now, see **[Previous README](#previous-readme)** at the bottom of this page.

## Getting started

> 🚧 Being migrated — current install & client-config details are in **[Previous README](#previous-readme)** below.

## Usage

> 🚧 Being migrated — current tools, prompts & format details are in **[Previous README](#previous-readme)** below.

## Compliance

Scribo emits invoices conforming to **EN 16931**, the European e-invoicing standard, with the relevant national CIUS. Every invoice is validated against the **Invopop**-hosted EN 16931 validator at generate-time — output that fails the rule set never reaches the user.

**Supported formats**

| Jurisdiction | Format | Status |
|---|---|---|
| Germany (B2B) | **ZUGFeRD** COMFORT (PDF/A-3 hybrid + CII XML) | ✅ Live |
| Germany (B2G) | **XRechnung** (UBL / CII) | ✅ Live |
| United States | Plain PDF (no XML, no e-invoice claim) | ✅ Live |
| France | **Factur-X** EN 16931 | 🔜 Coming soon |
| Spain | **Facturae** | 🔜 Coming soon |
| Belgium | **Peppol BIS 3.0** UBL | 🔜 Coming soon |

*Disclaimer: Scribo generates and validates compliant invoice documents. It is **not tax or legal advice** — Scribo does not determine your tax obligations, VAT treatment, or filing requirements.*

## FAQ

**Is Scribo really free?**
Yes — free forever. No credit card, no subscription, no paywall before your first invoice. You just need a sender email.

**Do I need an account or signup?**
No signup form. Scribo uses a magic-link login: you provide a sender email (which the invoice needs anyway), confirm via a one-time link, and you're in.

**Which countries and formats are supported?**
Live today: **Germany** — ZUGFeRD (B2B) and XRechnung (B2G) — and the **United States** (plain PDF). Coming next: **France** (Factur-X), **Spain** (Facturae), and **Belgium** (Peppol BIS 3.0).

**What does "EN 16931-compliant" actually mean here?**
Every invoice is validated against the **EN 16931-1:2017** rule set (via the Invopop-hosted validator) before it's returned. Output that fails validation never reaches you.

**Is the US version compliant?**
Yes. There is no US e-invoicing mandate, so Scribo produces a fully compliant plain PDF.

**Does Scribo give tax or legal advice?**
No. Scribo generates and validates compliant invoice *documents*. It does not determine your tax obligations, VAT treatment, or filing requirements.

**How do AI agents / LLMs use Scribo?**
Scribo is built to be operated by an agent. It ships as an **MCP server**, a **CLI**, and a **Claude/Codex skill**, plus a public **HTTP API** and a **web app** — all on the same backend. An agent can discover Scribo, create an invoice, and return the file on a user's behalf.

**Who builds Scribo?**
[Causa Prima](https://causaprima.ai/) — a company building agentic AI for the CFO office. Operated by Causa Prima Germany GmbH, Munich.

## Resources

- **Web app** — [scribo.causaprima.ai](https://scribo.causaprima.ai)
- **Documentation** — [scribo.causaprima.ai/docs](https://scribo.causaprima.ai/docs)
- **Compliance & trust** — [scribo.causaprima.ai/compliance](https://scribo.causaprima.ai/compliance)
- **Causa Prima** — [causaprima.ai](https://causaprima.ai)

**Other Scribo surfaces**

- Skill (Claude / Codex) — [`causa-prima-scribo-skill`](https://github.com/causa-prima-ai/causa-prima-scribo-skill) · [docs](https://scribo.causaprima.ai/docs/skill)
- MCP server — [`causa-prima-scribo-mcp`](https://github.com/causa-prima-ai/causa-prima-scribo-mcp) · [docs](https://scribo.causaprima.ai/docs/mcp)
- CLI — [`causa-prima-scribo-cli`](https://github.com/causa-prima-ai/causa-prima-scribo-cli) · [docs](https://scribo.causaprima.ai/docs/cli)
- HTTP API — [`causa-prima-scribo-api-docs`](https://github.com/causa-prima-ai/causa-prima-scribo-api-docs) · [docs](https://scribo.causaprima.ai/docs/api)
- Brand hub — [`causa-prima-scribo`](https://github.com/causa-prima-ai/causa-prima-scribo)

## License

Proprietary — `UNLICENSED`. © Causa Prima Germany GmbH. All rights reserved. Distributed for use against the public Scribo API; not open-source. See [LICENSE](./LICENSE).

---

## Previous README

> **Note:** This repo's README is being migrated to Scribo's shared structure (consistent title, shared sections, and per-surface sections). The content below is the previous README, preserved verbatim — minus the header visual and brand mark, which now sit at the top of this page. The sections above are being filled in from it.

<details>
<summary>Show previous README</summary>

# Scribo MCP — public registry metadata

Public registry-facing metadata for the Scribo MCP server hosted at
**[`scribo.causaprima.ai/mcp`](https://scribo.causaprima.ai/mcp)**.

> Compliant e-invoicing for any LLM — XRechnung, ZUGFeRD, Factur-X,
> Peppol BIS UBL, Spanish Facturae, plain US PDF. Free; the sender's
> email is the login.

This repo contains:

- [`.claude-plugin/plugin.json`](./.claude-plugin/plugin.json) — Claude Code plugin manifest (one-click install via `/plugin install scribo-mcp`)
- [`server.json`](./server.json) — [MCP Registry](https://registry.modelcontextprotocol.io/) metadata
- [`schemas/`](./schemas/) — JSON Schema for each tool's input
- [`examples/`](./examples/) — sample JSON-RPC 2.0 tool-call payloads
- [`icon.svg`](./icon.svg) — server brand mark

The MCP server is a **remote, hosted** Streamable HTTP endpoint — end
users never install it locally. Configure your MCP client to call the
hosted URL and you're done.

## Install

### Claude Code (recommended)

```sh
/plugin marketplace add causa-prima-ai/scribo-mcp
/plugin install scribo-mcp@scribo-mcp
# or, when the name is unambiguous across your installed marketplaces:
/plugin install scribo-mcp
```

The `/plugin marketplace add` line points Claude Code at this repo, which ships its plugin manifest directly — no companion marketplace repo to maintain. The plugin then wires up the hosted MCP server at <https://scribo.causaprima.ai/mcp>; you never edit `.mcp.json` by hand.

### Claude Desktop / claude.ai

Coming soon. We're submitting `scribo-mcp` to Anthropic's hosted plugin registry; once approved, install with one click from the in-app plugin browser. Until then, edit the config manually using the snippets below.

### Manual config (any MCP client)

| Client | Config file | Snippet |
|---|---|---|
| **Claude Desktop** | `~/Library/Application Support/Claude/claude_desktop_config.json` (macOS) | `{ "mcpServers": { "scribo": { "transport": "http", "url": "https://scribo.causaprima.ai/mcp" } } }` |
| **Cursor** | `~/.cursor/mcp.json` or workspace `.cursor/mcp.json` | `{ "mcpServers": { "scribo": { "url": "https://scribo.causaprima.ai/mcp" } } }` |
| **Cline** | `~/Library/Application Support/Cline/MCP/cline_mcp_settings.json` (macOS) | `{ "mcpServers": { "scribo": { "transport": "streamable-http", "url": "https://scribo.causaprima.ai/mcp" } } }` |
| **ChatGPT App** | OpenAI Apps SDK remote registration | Point at `https://scribo.causaprima.ai/mcp` |
| **OpenAI Codex CLI** | `~/.codex/config.toml` | `[mcp_servers.scribo]`<br>`url = "https://scribo.causaprima.ai/mcp"` |
| **Any MCP client** | Streamable HTTP, JSON-RPC 2.0, no auth | Point at `https://scribo.causaprima.ai/mcp` |

Restart the host after editing the config.

## Tools

Each tool ships with MCP `annotations` so the host can render the
right confirmation UI — `create_invoice` triggers a write-warning;
`get_invoice` and `list_supported_jurisdictions` are read-only and
safe to call freely.

| Tool | Read-only | Idempotent | Description |
|---|---|---|---|
| `create_invoice` | no | no¹ | Generate an EN 16931-compliant invoice. Returns a durable signed download URL plus a magic-link confirmation. |
| `get_invoice` | yes | yes | Fetch a previously generated invoice and a fresh signed download URL. Tenant-scoped — cross-tenant lookups return 404. |
| `list_supported_jurisdictions` | yes | yes | Return the per-country format matrix (which jurisdictions can emit which formats, plus the default per country). |

¹ `create_invoice` becomes idempotent when the optional `idempotency_key` argument is passed — same key + same payload returns the original invoice.

Full JSON schemas: [`schemas/create_invoice.json`](./schemas/create_invoice.json),
[`schemas/get_invoice.json`](./schemas/get_invoice.json),
[`schemas/list_supported_jurisdictions.json`](./schemas/list_supported_jurisdictions.json).

Sample payloads: [`examples/`](./examples/).

## Workflow prompts

Scribo exposes five MCP prompts you can invoke directly from your
host's prompt/slash-command picker — each renders a single user-turn
message that primes the agent for a specific Scribo workflow:

| Prompt | Arguments | What it does |
|---|---|---|
| `generate_invoice` | `jurisdiction?`, `description?` | Generic walk-through; falls back to the EN 16931 format priority chain when no jurisdiction is supplied. |
| `german_b2b_invoice` | `hours?`, `hourly_rate?` | ZUGFeRD COMFORT starter; calls out BR-DE-5 / BR-DE-6 contact-name + phone. |
| `german_b2g_xrechnung` | `leitweg_id?` | XRechnung CII starter; `recipient.leitweg_id` alone forces the format. |
| `us_plain_pdf_invoice` | _(none)_ | US plain PDF; no XML, no compliance friction. |
| `redownload_invoice` | `invoice_id` (required) | Fetch a prior invoice's metadata and a freshly-signed download URL. |

## Format coverage

| Jurisdiction | Default format | Notes |
|---|---|---|
| Germany (B2B) | ZUGFeRD COMFORT (PDF/A-3 hybrid + EN 16931 CII XML) | `zugferd_basic` available via `format_override` |
| Germany (B2G) | XRechnung CII | Triggered by `recipient.leitweg_id` |
| France | Factur-X | PDF/A-3 hybrid + EN 16931 CII XML |
| Spain | Facturae 3.2.2 | Spanish-specific XML syntax |
| Belgium / NL / LU / AT | Peppol BIS 3.0 UBL | Mandate transmission requires a Peppol AP partner |
| United States | Plain PDF | No XML |

## Account model

Scribo doesn't ask you to sign up. Your `sender.contact_email` on the
first `create_invoice` call is your login. Scribo emails a magic link
to that address — clicking it binds a web session at
[`scribo.causaprima.ai`](https://scribo.causaprima.ai) so you can come
back, re-download, or upgrade to a full Causa Prima account.

## Compliance & privacy

- EN 16931 conformance verified at generate-time by Invopop's hosted
  validator; in CI by Mustang (Apache 2.0 reference validator), KoSIT
  (XRechnung), and veraPDF (PDF/A-3).
- Sender + recipient + invoice content flow through Invopop (Madrid).
  DPA on file; sub-processor listed on
  [`/compliance`](https://scribo.causaprima.ai/compliance).

## Documentation

- Hosted docs: [`scribo.causaprima.ai/docs`](https://scribo.causaprima.ai/docs)
- MCP-specific guide: [`scribo.causaprima.ai/docs/mcp`](https://scribo.causaprima.ai/docs/mcp)
- HTTP API contract: [`scribo.causaprima.ai/docs/api`](https://scribo.causaprima.ai/docs/api)

## License

Proprietary — © Causa Prima Germany GmbH. All rights reserved. See [LICENSE](./LICENSE).

</details>
