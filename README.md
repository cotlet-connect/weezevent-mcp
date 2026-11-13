# Weezevent MCP server for ChatGPT and Claude

Connect Weezevent to ChatGPT, Claude and other AI agents through Cotlet. Work with events, orders, attendees, discount codes, invitations and refund requests in your own signed-in account. Cotlet provides an independent connection for your Weezevent back office and is not affiliated with Weezevent.

## What you can ask

> List the orders for the event I select and show unpaid reservations.

> List attendees by ticket source and promo code.

> Draft a discount code, invitation or refund request and stop for my approval.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Claude

Add `https://cotlet.dev/mcp/v1` as a custom connector in Claude and sign in with Cotlet.dev.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {"Authorization": "Bearer ${COTLET_API_KEY}"}
    }
  }
}
```

## Run it locally (stdio)

This repo is a small MCP server that forwards tool calls to the hosted Cotlet.dev server. It uses only Python's standard library.

```json
{"mcpServers": {"weezevent": {"command": "python3", "args": ["/absolute/path/to/weezevent-mcp/weezevent_agent.py", "serve"], "env": {"COTLET_API_KEY": "your-key"}}}}
```

Or with Docker:

```bash
docker build -t weezevent-mcp .
docker run -i --rm -e COTLET_API_KEY weezevent-mcp
```

Tools: `weezevent_guide`, `weezevent_status`, `weezevent_open`, `weezevent_read`, `weezevent_click`, `weezevent_type`, `weezevent_close`. Without `COTLET_API_KEY` a tool call explains where to get a key.

## Command line

Python 3.10+, nothing else to install:

```bash
export COTLET_API_KEY="your-key"
python3 weezevent_agent.py connect
python3 weezevent_agent.py status
python3 weezevent_agent.py guide
python3 weezevent_agent.py read
python3 weezevent_agent.py serve
```

## Questions from Weezevent users

**How do I connect Weezevent to ChatGPT or Claude?**

Sign up at cotlet.dev, log in to Weezevent once in its Cloud Browser and add Cotlet to ChatGPT or Claude. No Weezevent API key is required for the Cloud Browser connection.

**What can an AI agent do in Weezevent?**

It can list events, orders and attendees, inspect discount codes and participation, and prepare changes such as invitations, discount codes or refund requests. Actions that affect other people wait for your approval.

**Does Weezevent have an API or MCP server?**

Weezevent has a REST API for events, tickets and participants, documented for registered partners, and no native MCP server was found on 31 October 2026. Cotlet provides 13 hosted tools over MCP and REST for scripts.

**Is Cotlet affiliated with Weezevent?**

No. Cotlet is independent and connects to the Weezevent account you choose in its Cloud Browser.

## Find it on

- [Weezevent on Cotlet](https://cotlet.dev/integrations/weezevent-api-mcp-server)
- [All Cotlet packages](https://github.com/cotlet-connect)

More: https://cotlet.dev/integrations/weezevent-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=weezevent

Request access: https://cotlet.dev/signup?app=weezevent&utm_source=github&utm_medium=readme&utm_campaign=weezevent
