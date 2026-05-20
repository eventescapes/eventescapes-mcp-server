# Event Escapes MCP Server

Compatible with Claude, ChatGPT, OpenAI Agents, and MCP-compatible AI systems.

Event Escapes currently supports AI-assisted discovery workflows where users complete checkout directly on Event Escapes.

> AI-accessible sports and entertainment travel infrastructure for AI agents, copilots, and autonomous trip planners.

[![MCP](https://img.shields.io/badge/Protocol-MCP-blue)](https://modelcontextprotocol.io)
[![Status](https://img.shields.io/badge/Status-Live-brightgreen)](https://mcp.eventescapes.com)
[![Events](https://img.shields.io/badge/Inventory-3000%2B%20Events-orange)](https://eventescapes.com/sports)

Event Escapes is a premium sports and entertainment travel OTA based in Melbourne, Australia. This MCP server gives AI agents direct access to event tickets, hotels, curated travel packages, and local experiences worldwide.

Built for Claude, ChatGPT, AI travel agents, and any MCP-compatible client.

---

# MCP Endpoint

```bash
https://mcp.eventescapes.com/sse
```

---

# Why Event Escapes?

Event Escapes combines global event inventory with AI-accessible travel commerce infrastructure.

## Features

- Sports, concerts, festivals, and entertainment inventory
- Curated ticket + hotel travel packages
- Premium and VIP experiences
- Multi-market pricing and currencies
- AI-friendly structured responses
- Payment plans available in Australia
- Global events coverage
- Real-time hotel and experience search
- MCP-native architecture for AI agents

---

# Supported Events

| Category | Competitions |
|---|---|
| Motorsport | Formula 1, MotoGP, NASCAR |
| Football | Premier League, La Liga, Serie A, Champions League, World Cup 2026, MLS |
| US Sports | NFL, NBA, NHL, MLB |
| Tennis | Wimbledon, Australian Open, US Open, French Open |
| Rugby | Six Nations, Rugby World Cup, Super Rugby |
| Cricket | ICC Events, Test Matches |
| Entertainment | Concerts, Festivals, WWE, Tomorrowland |
| Other | Golf Majors, Royal Ascot, Diamond League |

---

# Available MCP Tools

## `search_events`

Search for events by keyword, destination, category, or date range.

### Example Request

```json
{
  "query": "Formula 1",
  "country": "Australia",
  "date_from": "2026-10-01",
  "date_to": "2026-12-31"
}
```

### Example Response

```json
{
  "event": "Formula 1 Australian Grand Prix 2026",
  "city": "Melbourne",
  "country": "Australia",
  "price_from": 899,
  "availability": "Available",
  "event_url": "https://eventescapes.com/sports/f1"
}
```

Returns:
- Event name
- Venue
- Date
- City
- Country
- Ticket availability
- Price range
- Event URL

---

## `get_event_details`

Get full details for a specific sporting or entertainment event.

### Example

```json
{
  "event_id": "formula-1-australian-grand-prix-melbourne-2026"
}
```

Returns:
- Ticket categories
- Venue information
- Event schedule
- Seating information
- Package availability

---

## `search_hotels`

Search hotels near event venues.

### Example

```json
{
  "destination": "Melbourne",
  "check_in": "2026-11-26",
  "check_out": "2026-11-28",
  "guests": 2
}
```

Returns:
- Hotel options
- Pricing
- Ratings
- Distance from venue
- Room availability

---

## `search_packages`

Find curated travel packages combining tickets, hotels, and experiences.

### Example

```json
{
  "query": "F1 Melbourne",
  "tier": "premium"
}
```

Returns:
- Curated event packages
- Hotel inclusions
- Ticket types
- Experience add-ons
- Package pricing

---

## `search_experiences`

Search tours, attractions, and local experiences in event destinations.

### Example

```json
{
  "destination": "Singapore",
  "date": "2026-09-21"
}
```

---

## `get_destinations`

List all available destinations with upcoming event counts.

---

## `get_package_details`

Get full details for a specific travel package.

---

# Example AI Prompts

Use Event Escapes with Claude, ChatGPT, and MCP-compatible AI agents.

- Find Formula 1 races in November 2026
- Show me NFL games in London
- Search for Wimbledon packages
- Find hotels near the Melbourne Grand Prix circuit
- What experiences are available during Singapore F1?
- Search for World Cup 2026 packages
- Show premium packages for the Australian Open
- Find concerts happening in Melbourne next month

---

# AI Agent Workflow

```text
AI Agent
   ↓
Event Escapes MCP Server
   ↓
Tickets + Hotels + Experiences
   ↓
Event Escapes Checkout
```

Event Escapes currently supports AI-assisted discovery and booking workflows. Users complete checkout directly on Event Escapes.

---

# Quick Start

## Claude Desktop

Add to `claude_desktop_config.json`

```json
{
  "mcpServers": {
    "event-escapes": {
      "url": "https://mcp.eventescapes.com/sse"
    }
  }
}
```

---

## Claude.ai

Search for "Event Escapes" in the Claude MCP Connectors directory.

---

## Any MCP Client

Connect using:

```bash
https://mcp.eventescapes.com/sse
```

---

# Markets & Currencies

| Market | Currency | Payment Methods |
|---|---|---|
| Australia | AUD | Stripe, Afterpay |
| New Zealand | NZD | Stripe |
| Singapore | SGD | Stripe |
| Malaysia | MYR | Stripe |
| United States | USD | Stripe |
| United Kingdom | GBP | Stripe |

---

# Architecture

```text
AI Agent (Claude / ChatGPT / Custom)
        ↓
MCP Protocol (SSE)
        ↓
Event Escapes MCP Server (Cloudflare Workers)
        ↓
Supabase Edge Functions
        ├── SE365 API (tickets)
        ├── RateHawk API (hotels)
        ├── Hotelbeds API (experiences)
        └── Supabase Database (packages + cache)
```

---

# AI Travel Infrastructure

Event Escapes is building AI-accessible travel commerce infrastructure for sports and entertainment travel.

The MCP server enables:
- AI travel agents
- Autonomous trip planners
- Conversational travel commerce
- AI-powered sports travel search
- Event discovery workflows
- Structured booking experiences

---

# Links

- Website: https://eventescapes.com
- MCP Server: https://mcp.eventescapes.com
- Sports Events: https://eventescapes.com/sports
- Music Events: https://eventescapes.com/music
- Travel Packages: https://eventescapes.com/packages
- LLM Index: https://eventescapes.com/llms.txt

---

# About Event Escapes

Event Escapes (Zeroopay Technologies Pty Ltd) is a premium event travel platform based in Melbourne, Australia.

We curate sports and entertainment travel experiences by combining:
- Event tickets
- Hotels
- Flights
- Experiences
- Hospitality packages

for customers worldwide.

---

# License

This MCP server is provided as a public AI-accessible API.

Usage is subject to:
https://eventescapes.com/terms-of-service
