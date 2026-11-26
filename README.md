# Event Escapes MCP Server

AI-accessible commerce for event-driven travel: sports and entertainment events, hotels near the venue, curated packages and experiences, with checkout on Event Escapes.

[![MCP](https://img.shields.io/badge/Protocol-MCP-blue)](https://modelcontextprotocol.io)
[![Status](https://img.shields.io/badge/Status-Live-brightgreen)](https://eventescapes.com/ai)
[![Events](https://img.shields.io/badge/Events-4000%2B-orange)](https://eventescapes.com/ai)

Event Escapes is an Australian travel technology company focused on event-driven travel. This server lets AI agents search events, hotels near a venue, packages and experiences, and create a payment link that the customer pays on the Event Escapes checkout.

Works with Claude, ChatGPT, Claude Code, Cursor, Gemini and any MCP client.

- Connection guide: https://eventescapes.com/ai
- Technology overview: https://eventescapes.com/technology
- Partnerships: https://eventescapes.com/technology/partners

---

## Endpoint

```
https://mcp.eventescapes.com/sse
```

Transport: streamable HTTP. No key is needed for search.
Manifest: https://eventescapes.com/.well-known/mcp.json

The same tools are available as a REST API (OpenAPI 3.1): https://eventescapes.com/openapi.json

| Method | Path | Tool |
|---|---|---|
| GET | `/api/v1/events` | `search_events` |
| GET | `/api/v1/events/{idOrSlug}` | `get_event_details` |
| GET | `/api/v1/events/{idOrSlug}/hotels` | `search_hotels_near_event` |
| GET | `/api/v1/packages` | `search_packages` |
| GET | `/api/v1/experiences` | `search_experiences` |
| POST | `/api/v1/payment-links` | `create_payment_link` |

---

## Tools

| Tool | What it does |
|---|---|
| `search_events` | Find sports and concert events by sport, competition, city, country and dates |
| `get_event_details` | Full event information, venue and prices |
| `search_hotels_near_event` | Hotels around an event venue for the event dates, with distance |
| `search_packages` | Curated packages around major events |
| `search_experiences` | Tours and activities in the event city |
| `build_event_link` | Link to an event booking page on Event Escapes |
| `build_package_link` | Link to a package page on Event Escapes |
| `create_payment_link` | Lock live prices for hotel rooms and event tickets and return one secure payment link for the customer |

Search and link tools are read only. Coverage (November 2026): 4,000+ sports and concert events in 60+ countries. Trade fairs and business events are on the website only.

---

## Two ways to book

1. **A link to the booking page**: `build_event_link` (the event page, with hotels near the venue already loaded and an optional pinned hotel), `build_package_link` (a curated package page) or an experience page. The customer books on eventescapes.com.
2. **A direct payment link**: `create_payment_link` locks live prices for hotel rooms and event tickets (up to 4 items) and returns one secure payment link.

## Booking through an agent

`create_payment_link` starts a booking; the customer completes it.

- The agent sends the customer's email and name, `customer_consent` (the customer's own words asking for the booking), the items and `agent_terms_accepted: true`, its acceptance of the AI Agent Terms: https://eventescapes.com/terms/ai-agents
- Event Escapes locks live prices and returns one payment URL for the whole trip. It expires after about 30 minutes, and a new link replaces the customer's previous unpaid one.
- Creating the link charges nothing. The customer pays on the Event Escapes checkout, and the card is only charged for the bookings that are confirmed, and anything that cannot be booked is released. Event Escapes is the merchant of record.
- Experiences come back as a link to the experience page, where the customer books them.
- Orders above about AUD 5,000 also need `total_confirmation` in the customer's words; above about AUD 20,000 the customer books with our team.
- If more is needed (a ticket category, approval of a price change, attendee details), the tool returns `action_required`; call again with the same items plus those fields.
- Every payment link is recorded with the agent, the customer's consent, the items and the total.

---

## Quick start

**Claude.ai**: Settings, Connectors, Add custom connector, paste the endpoint.

**ChatGPT**: Settings, Apps, Advanced, turn on Developer mode, Create, paste the endpoint, no auth.

**Claude Code**

```bash
claude mcp add --transport http event-escapes https://mcp.eventescapes.com/sse
```

**Claude Desktop** (`claude_desktop_config.json`)

```json
{
  "mcpServers": {
    "event-escapes": {
      "command": "npx",
      "args": ["mcp-remote", "https://mcp.eventescapes.com/sse"]
    }
  }
}
```

---

## Example: one `search_events` result

Illustrative values; live prices and availability change.

```json
{
  "event_id": "58b8e350-aea2-41c7-bcc3-bfd0d3335f01",
  "title": "Arsenal vs Manchester City",
  "category": "sports",
  "venue": "Emirates Stadium",
  "city": "London",
  "country_code": "GB",
  "event_date": "2026-11-29",
  "price_from": 498.33,
  "currency": "USD",
  "availability": "available",
  "url": "https://eventescapes.com/events/arsenal-vs-manchester-city-london-2026-393006"
}
```

---

## Links

- Website: https://eventescapes.com
- Ask Jenny, our AI travel concierge: https://eventescapes.com/jenny
- LLM index: https://eventescapes.com/llms.txt
- AI Agent Terms: https://eventescapes.com/terms/ai-agents
- Partnerships: partnerships@eventescapes.com

## About

Event Escapes is a trading name of Zeroopay Technologies Pty Ltd (ABN 78 688 499 489), Melbourne, Australia.

Use of this server is subject to the Event Escapes terms (https://eventescapes.com/terms) and the AI Agent Terms (https://eventescapes.com/terms/ai-agents).
