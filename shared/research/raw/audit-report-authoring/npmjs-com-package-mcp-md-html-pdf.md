<!--
URL: https://www.npmjs.com/package/mcp-md-html-pdf
Fetch date: 2026-08-18
Source type: vendor blog
Research cluster: audit-report-authoring
Archived by: forge stage 2 sweep round 3 (deeper research pass, mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., targeting previously-flagged thin coverage.
-->

# mcp-md-html-pdf

URL: https://www.npmjs.com/package/mcp-md-html-pdf

Markdown -> branded HTML/PDF documents. CLI, MCP server, and web app.

- Version: 0.2.0
- License: MIT
- Author: Vojtech Klima
- Weekly downloads: 4
- Created: 2026-03-13

## Keywords

markdown, document, pdf, html, brand, mcp, mcp-server, claude, proposal, invoice, report, contract, branded-documents, markdown-to-html, markdown-to-pdf

## What it does

Takes markdown content plus a brand definition (logo, colors, fonts) and produces a self-contained HTML document (about 10 KB) that:

- Opens on any device: phone, tablet, desktop
- Sends via WhatsApp, email, Slack: recipient clicks and sees it
- Prints to A4: clean layout with proper margins and page breaks
- Looks like it was designed by a professional

No accounts, no subscriptions, no export workflows.

## Setup: brand.json

Create a folder for the brand (for example `~/my-brand/`) and put a `brand.json` in it:

```json
{
  "name": "Your Company",
  "tagline": "We build great things.",
  "web": "yourcompany.com",
  "email": "hello@yourcompany.com",
  "logo": "./logo.svg",
  "icon": "./icon.svg",
  "colors": {
    "primary": "#1E3A5F",
    "accent": "#C9A84C",
    "muted": "#7F8C8D",
    "surface": "#F4F6F7"
  },
  "fonts": {
    "heading": "Georgia, serif",
    "body": "-apple-system, 'Segoe UI', 'Helvetica Neue', Arial, sans-serif"
  },
  "style": "modern",
  "footer": {
    "showContact": true,
    "note": ""
  }
}
```

The logo file (SVG or PNG) is placed in the same folder; it is automatically converted to base64 and embedded into the HTML, so the output is always a single self-contained file.

All fields are optional. A brand can start with just `name` and `colors` and add the rest later.

### Brand fields

| Field | What it does |
|---|---|
| `name` | Company name, shown in header and footer |
| `tagline` | Short tagline below the logo |
| `web`, `email` | Shown in footer (if `footer.showContact` is true) |
| `logo` | Path to logo file (SVG, PNG), shown in document header |
| `icon` | Path to small icon, shown in document footer |
| `colors.primary` | Headings, borders, strong elements |
| `colors.accent` | Links, highlights, accent lines |
| `colors.muted` | Captions, labels, secondary text |
| `colors.surface` | Background of boxes, table headers |
| `fonts.heading` | Font stack for headings (h1 to h4) |
| `fonts.body` | Font stack for body text |
| `style` | Document style preset |
| `footer.showContact` | Show web/email in footer |
| `footer.note` | Small note at the bottom (example: "Confidential") |

### Available fonts

Headings (serif): Georgia, Palatino, Cambria, Times New Roman. Headings (sans-serif): System Sans, Calibri, Trebuchet, Verdana. Body (sans-serif): System Sans, Calibri, Verdana. Body (serif): Georgia, Palatino, Cambria.

## MCP tools

| Tool | Description | Key inputs |
|---|---|---|
| `build_document` | Markdown -> branded HTML | `content`, `outputPath`, `brandOverrides` |
| `export_pdf` | HTML -> A4 PDF | `htmlPath`, `format` (A4/Letter) |
| `full_pipeline` | Markdown -> HTML + PDF in one step | `content`, `filename`, `formats` |
| `list_components` | List all 21 HTML components with examples | (none) |
| `list_styles` | List all 8 style presets | (none) |

### build_document inputs

| Input | Type | Description |
|---|---|---|
| `content` | string | Markdown or HTML content |
| `title` | string? | Document title |
| `brand` | string? | Path to brand.json (overrides env-var default brand) |
| `brandOverrides` | object? | Inline overrides: `name`, `colors`, `fonts`, `style`, etc. |
| `outputPath` | string? | Where to save the HTML file |
| `isHtml` | boolean? | Set to true if content is already HTML |

## How the brand layers work

Brand settings can be overridden at multiple levels, each layer overriding the one below:

```
brandOverrides     <- highest priority (inline in tool call)
brand path         <- tool call parameter (path to a different brand.json)
MODDOC_BRAND        <- env var (default brand)
built-in default   <- fallback (generic neutral style)
```

This means a default brand can be set via an env var while specific fields (a different style or accent color for a particular client) are still overridden per document.

## Style presets

Styles define layout personality (typography, spacing, density) and never override brand colors or fonts.

| Style | Personality | Best for |
|---|---|---|
| `modern` | Airy, large light headings | Proposals, presentations |
| `formal` | Compact, conservative | Contracts, legal documents |
| `minimal` | Clean, bold headings, max whitespace | Reports, tech docs |
| `executive` | Authoritative, accent lines | Board reports, C-level |
| `creative` | Bold, high contrast | Agency proposals, portfolios |
| `technical` | Data-dense, monospace accents | Analyses, audits, API docs |
| `invoice` | From/to blocks, line items, totals | Invoices |
| `compact` | Maximum content per page | SOWs, contracts, specs |

[Fetch truncated here; the remainder of the style-preset table, the "21 HTML components" reference list, and CLI usage examples beyond the setup snippets above were not captured.]
