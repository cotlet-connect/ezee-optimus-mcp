# eZee Optimus MCP server

eZee Optimus connects to ChatGPT, Claude, Codex and Claude Code through the hosted Cotlet.dev MCP server. Work with restaurant orders, kitchen tickets and bills in your own signed-in Cloud Browser.

This repository provides an optional Python stdio adapter and connection configuration. You can connect directly to the hosted server without installing it. The live integration page describes 8 restaurant operations; the local adapter exposes 7 general browser tools, which are a separate interface.

[Read the eZee Optimus integration guide](https://cotlet.dev/integrations/ezee-optimus-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=ezee-optimus).

## Connect your account

1. [Sign up for Cotlet.dev](https://cotlet.dev/signup?app=ezee-optimus) and turn on eZee Optimus in the console.
2. Open app.ipos247.com in your Cloud Browser. Enter your user name, password and restaurant code yourself, then choose your terminal and outlet.
3. Add `https://cotlet.dev/mcp/v1/connect` as the connector URL in ChatGPT or Claude and sign in to Cotlet.dev.

For Codex and Claude Code, use `https://cotlet.dev/mcp/v1` with an API key from the Cotlet.dev console in the `Authorization: Bearer` header. The same connector serves the other apps you enable.

## Restaurant operations

The live page lists these operations, checked against the page on 17 November 2026:

| Operation | What it does |
| --- | --- |
| `filter_restaurant_orders` | List orders by type, table or date. |
| `record_table_guest_info` | Add or correct guest details on a table. |
| `send_orders_to_kitchen` | Send a table order to the kitchen. |
| `create_takeaway_orders` | Enter a pickup order. |
| `update_order_items` | Change items or extra charges on an open order. |
| `apply_order_discounts` | Apply an order-level discount. |
| `print_receipts_and_kots` | Print receipts or kitchen order tickets. |
| `settle_or_split_bills` | Split a bill or settle it in a separate call. |

Six of the seven write operations ask for confirmation by default. Recording table guest details and reading orders run without approval. Confirmations can be switched off per tool. The agent works in the outlet selected at sign-in, with your existing user rights.

Example requests:

> List today's open takeaway orders.

> Prepare a pickup order for Lee and show me the items before saving it.

> Show me how to split the table bill before settling it.

## Optional local adapter

Python 3.10 or later is required; the adapter uses only the standard library. Set `COTLET_API_KEY` in your environment with a key from the Cotlet.dev console, then run:

```sh
python ezee_optimus_agent.py serve
```

The stdio adapter exposes `ezee_optimus_guide`, `ezee_optimus_status`, `ezee_optimus_open`, `ezee_optimus_read`, `ezee_optimus_click`, `ezee_optimus_type` and `ezee_optimus_close`. These forward to the hosted Cotlet.dev browser tools. Call the guide first, read the current screen before acting and ask for confirmation before changes that affect kitchen work, printers or a guest's bill.

The adapter needs a Cotlet.dev account and its hosted service. It does not run a standalone restaurant server. The included `mcp.json` describes a direct hosted connection for clients that support environment substitution.

## Does eZee Optimus have an official API?

The live page's vendor check from 15 November 2026 documents an official Connectivity API for F&B purchases, F&B sales and financial accounts. It found no order, kitchen ticket or bill endpoint, and verified no official MCP server or ChatGPT or Claude connector. Use the official API for the finance reads it covers. Cotlet.dev works through your signed-in web POS.

## Access and security

You sign in yourself. Cotlet.dev stores an encrypted browser profile and does not store your password. If eZee Optimus signs you out, sign in again in the Cloud Browser. You can disable the app for agents or reset the browser in your console. See the live guide for current pricing and access details.

Unofficial and not affiliated with eZee Optimus or Yanolja Cloud Solution.

## License

Elastic License 2.0. See [LICENSE](LICENSE).
