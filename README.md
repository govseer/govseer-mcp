# Govseer MCP server

Govseer's product compliance checks as tools for AI assistants that speak the Model Context Protocol (MCP). Each result cites the legal text it comes from. Free, no account or key.

This repository holds no code: the server is a hosted service. It is here for MCP directories and for setup instructions.

## Address

```
https://govseer-api-823928849037.europe-west1.run.app/mcp
```

Streamable HTTP. Listed on the official MCP Registry as `com.govseer/compliance`, and on Glama:

[![Govseer MCP connector](https://glama.ai/mcp/connectors/com.govseer/compliance/badges/score.svg)](https://glama.ai/mcp/connectors/com.govseer/compliance)

**Claude Code**

```
claude mcp add --transport http govseer https://govseer-api-823928849037.europe-west1.run.app/mcp
```

**VS Code** (`.vscode/mcp.json`)

```json
{
  "servers": {
    "govseer": { "type": "http", "url": "https://govseer-api-823928849037.europe-west1.run.app/mcp" }
  }
}
```

**Cursor** (`~/.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "govseer": { "url": "https://govseer-api-823928849037.europe-west1.run.app/mcp" }
  }
}
```

In apps with a connector or custom server setting, paste the address there.

## Tools

| Tool | What it does |
| --- | --- |
| `check_clp_label` | Checks a label's signal word, pictograms, H, EUH and P codes, product identifier and "Contains" line against the EU CLP Regulation, with the article behind each finding. |
| `clp_statement_wording` | The official wording of H, EUH and P statements in any of the 24 EU languages, from the consolidated CLP text on EUR-Lex. |
| `scan_green_claims` | Finds environmental claims the EU bans since 27 September 2026 in product or advert text, and, for hazardous products, wording CLP keeps off labels and online offers. |
| `scan_amazon_listing` | Finds pesticide-type claims ("kills germs", "repels insects"…) in an Amazon US title or description, and any EPA registration numbers. |
| `us_limited_quantity` | Whether US ground shipping may use the limited quantity exception for a hazard class and packing group (49 CFR part 173), with the inner packaging limit. |
| `cpsc_lab_lookup` | Whether a lab is on CPSC's list of accepted labs, and the rules it is accepted for. |
| `cpsc_hts_flag` | CPSC's eFiling flag (CP1 or CP2) for 10-digit HTS codes. |
| `upcoming_rules` | Dated rule changes ahead for EU CLP, OSHA HCS, WHMIS, Quebec French labels, CPSC eFiling and Amazon, with their official sources. |

All tools are read-only. They read no documents; to read a safety data sheet or a lab test report, use the [Govseer API](https://govseer.com/docs/api) with a key.

## Limits and data

- Free, up to 120 tool calls an hour from one address.
- What you send is checked in memory and not stored. Govseer logs which tool was called and the name your client gives, not what you sent.
- Protocol revisions: 2026-07-28, and 2025-11-25 back to 2024-11-05 over Streamable HTTP.

## More

- Documentation: https://govseer.com/docs/mcp
- Support: https://govseer.com/support · hello@govseer.com
- Privacy: https://govseer.com/privacy · Terms: https://govseer.com/terms

The results are a tool, not legal advice.
