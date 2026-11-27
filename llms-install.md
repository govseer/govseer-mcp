# Installing the Govseer MCP server (for Cline and other AI agents)

Govseer is a hosted, remote MCP server. There is nothing to install, build or run, and
no API key, account or environment variable is needed.

- Server name: `govseer`
- URL: `https://govseer-api-823928849037.europe-west1.run.app/mcp`
- Transport: Streamable HTTP (in Cline: `"type": "streamableHttp"`)
- Authentication: none

## Cline

Open MCP Servers → Configure → Configure MCP Servers, and add this entry to
`cline_mcp_settings.json` (keep any servers already there):

```json
{
  "mcpServers": {
    "govseer": {
      "type": "streamableHttp",
      "url": "https://govseer-api-823928849037.europe-west1.run.app/mcp",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

Set `"type": "streamableHttp"` explicitly: without it Cline falls back to the legacy SSE
transport, which this server does not offer.

## Check it works

The server should list eight tools. Ask, for example:

- "Use govseer to check this EU label: Danger, GHS05, H318, P280, P305+P351+P338, P310."
  → `check_clp_label` lists what is missing (supplier details, nominal quantity, "Contains"
  line), each with its CLP article.
- "What is the CPSC eFiling flag for HTS 9503.00.0073?" → `cpsc_hts_flag` returns CP2, Toys.

All tools are read-only. Limit: 120 tool calls an hour per IP address; over it, a call
returns an error saying so. Documentation: https://govseer.com/docs/mcp
