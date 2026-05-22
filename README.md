# API Knowledge (knowledge)

> "If you know where the APIs are, you end up with more control in your workplace. If you know the people who own these APIs, you end up with more control in your workplace. It isn't something that just happens overnight. You have to do the work." — *[With API Knowledge Comes Great Power](https://apievangelist.com/2026/04/24/with-api-knowledge-comes-great-power/)*, Kin Lane, 2026-04-24.

API knowledge is the layer of indexes, descriptions, contexts, and signals that lets humans and agents reason about which APIs exist, what they do, who operates them, what they cost, how to call them, and how trustworthy they are. This topic repo catalogs the formats and platforms that publish API knowledge today — and provides the JSON Schema, JSON-LD context, vocabulary, and examples for a portable, multi-source **API knowledge record**.

**URL:** [https://github.com/api-evangelist/knowledge](https://github.com/api-evangelist/knowledge)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=topic-knowledge&utm_content=repo)

## Tags

API Knowledge, Knowledge Graphs, API Discovery, API Search, Catalogs, Indexes, Registries, RAG, Semantic Web, JSON-LD, LLMs, AI Agents, Topic

## Timestamps

- **Created:** 2026-05-22
- **Modified:** 2026-05-22

## The Landscape

API knowledge has been built up in layers over fifteen years:

1. **The contract layer** — OpenAPI describes a single API surface. The current version, OpenAPI 3.2.0, was released on 19 September 2025 and is the dominant contract format.
2. **The catalog layer** — APIs.json (sitemap for an API project), APIs.guru (community OpenAPI directory), RapidAPI Hub, and the Postman Public API Network aggregate many providers' contracts into searchable indexes.
3. **The agent layer** — Jentic (Arazzo workflows over OpenAPI), Composio (1,000+ apps as agent-ready tools, including an MCP surface), and the MCP server registries turn the contract layer into something an LLM can use directly.
4. **The site-level hint layer** — llms.txt and schema.org/WebAPI let any provider publish lightweight, LLM-friendly knowledge directly from their own website.
5. **The signals layer** — Naftiko Signals (884 companies, 50 industries, 44 signal groups) joins the contract and catalog layers to hiring, investment, and organizational signals, so analysts can reason about which APIs are well-supported and which are likely to fade.

This repo catalogs all five layers and defines a portable **API knowledge record** that pulls them together with explicit source citation.

## API Knowledge Platforms

### Open Indexes

| Platform | Role | Notes |
|----------|------|-------|
| [APIs.json](https://apisjson.org) | Sitemap-for-APIs index format | Current revision 0.20, 0.21 draft. |
| [APIs.guru](https://apis.guru) | Community OpenAPI directory | 2,529 APIs, 677 providers, 3,992 specs, 108,837 endpoints (per `api.apis.guru/v2/metrics.json`, retrieved 2026-05-22). |

### Commercial Marketplaces

| Platform | Role | Notes |
|----------|------|-------|
| [RapidAPI Hub](https://rapidapi.com/hub) | API marketplace with metering & billing | Single key, single bill, "Try it" across the catalog. |
| [Postman Public API Network](https://www.postman.com/explore) | Collection-format network | Discovery by category (App Security, AI, Payments, ...). |

### Standards

| Platform | Role | Notes |
|----------|------|-------|
| [OpenAPI Initiative](https://www.openapis.org) | Stewards OpenAPI | OAS 3.2.0 (2025-09-19); learn.openapis.org is the spec knowledge surface. |
| [schema.org/WebAPI](https://schema.org/WebAPI) | Structured-data vocabulary | Subclass of `schema:Service`; properties include `documentation`, `provider`, `termsOfService`. |
| [llms.txt](https://llmstxt.org) | Site-level LLM hint | Markdown file at `/llms.txt`. |

### Agent-Facing Layers

| Platform | Role | Notes |
|----------|------|-------|
| [Jentic](https://jentic.com) | Governed execution layer for agents | "Backed by the Arazzo open standard, Jentic workflows are portable, testable, and built for production." |
| [Composio](https://composio.dev) | Tool registry for agents | 1,000+ apps; exposes both OpenAPI-native and MCP formats. |
| [Naftiko](https://github.com/api-evangelist/naftiko) | Spec-driven integration platform | YAML capability spec compiled to MCP / SKILL / REST. |
| [Naftiko Signals](https://signals.naftiko.io) | Company-level signal feed | 884 companies, 50 industries, 44 signal groups. |

## The API Knowledge Record

An **API knowledge record** is a single, agent-readable description of one API that aggregates evidence from one or more sources. It is the smallest portable unit of the knowledge layer.

A record carries:

- A stable **id** and **name**.
- A **provider** (an `Organization`).
- A **capability** — what the API can do, in agent-readable form, with named operations and an `agentReady` profile.
- A **sources** array — every place the API is described, each carrying a `type`, `url`, and optional `evidence` (a verbatim quote with a claim).
- A `sourceOfTruth` — the canonical source for tie-breaking.
- An **artifacts** object — links to OpenAPI, AsyncAPI, JSON Schema, JSON-LD, Postman, Arazzo, MCP server, and `llms.txt`.
- A **signals** array — timestamped, third-party signals (GitHub stars, status page presence, Naftiko signal groups, changelog cadence).
- A **confidence** — `High | Medium | Low`, derived from source diversity and recency.

This is the format described by [`json-schema/knowledge-record-schema.json`](json-schema/knowledge-record-schema.json) and serialized as JSON-LD via [`json-ld/knowledge-context.jsonld`](json-ld/knowledge-context.jsonld).

## Common Properties

- [Portal](https://github.com/api-evangelist/knowledge)
- [GitHubRepository](https://github.com/api-evangelist/knowledge)
- [Vocabulary](vocabulary/knowledge-vocabulary.yml)
- [JSONLD](json-ld/knowledge-context.jsonld)
- [JSONSchema](json-schema/knowledge-record-schema.json)

## Features

| Name | Description |
|------|-------------|
| Multi-Source Aggregation | A record cites multiple sources (APIs.json, APIs.guru, RapidAPI, Postman, provider portal, Naftiko Signals) for the same API. |
| Capability Modeling | Records describe what the API can *do*, not just that it exists. |
| Evidence and Provenance | Every claim carries a verbatim quote, URL, and timestamp. |
| Source-of-Truth Hierarchy | Each record marks a primary source for conflict resolution. |
| Semantic Alignment | Records align to schema.org/WebAPI, APIs.json, and PROV-O via JSON-LD. |
| Agent-Readable Index | Designed for RAG, MCP tool selection, and agent-framework consumption. |

## Use Cases

| Name | Description |
|------|-------------|
| API Discovery | Search APIs.guru, RapidAPI, Postman simultaneously and merge by canonical URL. |
| RAG Over API Documentation | Index a provider's OpenAPI, `llms.txt`, and portal; answer with source-cited responses. |
| Tool Selection for Agents | MCP hosts and agent frameworks pick the right tool given an intent and a policy. |
| API Provider Intelligence | Join APIs.guru entries with Naftiko Signals to spot well-supported providers. |
| Knowledge-Driven Governance | Only on-board APIs that have public OpenAPI, status page, and rate-limit docs. |

## Integrations

| Name | Description |
|------|-------------|
| APIs.json + OpenAPI | APIs.json indexes point to one or more OpenAPI specs per API entry. |
| APIs.guru + OpenAPI | APIs.guru stores raw OpenAPI 2.0/3.x and serves them via REST. |
| Postman + Collections | The Postman Network distributes executable Collection artifacts. |
| schema.org + JSON-LD | Knowledge records embed schema.org/WebAPI via JSON-LD. |
| Jentic + Arazzo | Jentic describes API workflows in Arazzo over OpenAPI. |
| Composio + MCP | Composio exposes its tool registry as MCP servers in addition to native tools. |
| Naftiko Signals + JSON-LD | Naftiko Signals publishes company records as JSON-LD. |

## Solutions

| Name | Description |
|------|-------------|
| Open Indexes | APIs.json and APIs.guru. |
| Commercial Marketplaces | RapidAPI Hub, Postman Public API Network. |
| Agent-Facing Knowledge Layers | Jentic and Composio. |
| Site-Level LLM Hints | llms.txt and schema.org/WebAPI. |
| Signals-Based Intelligence | Naftiko Signals. |

## Artifacts

Machine-readable descriptions of the knowledge layer.

### JSON Schema

- [API Knowledge Record](json-schema/knowledge-record-schema.json) — the top-level, agent-readable description of one API.
- [API Knowledge Source](json-schema/knowledge-source-schema.json) — one place where an API is described or indexed.
- [API Knowledge Evidence](json-schema/knowledge-evidence-schema.json) — a single verbatim quote with a URL backing a claim.
- [API Capability](json-schema/knowledge-capability-schema.json) — the agent-facing capability description.
- [API Knowledge Signal](json-schema/knowledge-signal-schema.json) — a single observed third-party signal.
- [API Knowledge Observation](json-schema/knowledge-observation-schema.json) — a timestamped retrieval event with field-level snapshot.

### JSON-LD

- [Knowledge Context](json-ld/knowledge-context.jsonld) — aligns record types to schema.org/WebAPI, schema.org/Organization, PROV-O, and the APIs.json namespace.

### Examples

- [Stripe Payments Knowledge Record](examples/stripe-payments-knowledge-record-example.json) — aggregates docs.stripe.com, APIs.guru, github.com/stripe, and Postman.
- [Twilio Messaging Knowledge Record](examples/twilio-messaging-knowledge-record-example.json) — aggregates twilio.com/docs, github.com/twilio/twilio-oai, APIs.guru, and Postman.
- [OpenAI Platform Knowledge Record](examples/openai-platform-knowledge-record-example.json) — aggregates platform.openai.com, github.com/openai/openai-openapi, and the MCP surface.
- [APIs.guru Source](examples/apisguru-source-example.json) — a standalone source entry.
- [Naftiko Signals Source](examples/naftiko-signals-source-example.json) — a standalone source entry.
- [Evidence](examples/evidence-example.json) — a single cited quote.
- [Capability](examples/capability-example.json) — an agent-facing capability profile.
- [Signal](examples/signal-example.json) — a Naftiko-style signal observation.
- [Observation](examples/observation-example.json) — a versioned snapshot with a delta.

## Vocabulary

- [API Knowledge Vocabulary](vocabulary/knowledge-vocabulary.yml) — operational dimension (concepts, source types, trust levels) and capability dimension (intents, agent readiness, personas, workflows, signals, confidence levels).

## Notable Absences

- **No public OpenAPI for the knowledge layer itself.** This repo describes the knowledge layer with JSON Schema and JSON-LD; the layer is data, not an HTTP API.
- **No commercial pricing or rate limits at the topic level.** Where individual platforms (RapidAPI Hub, Postman, Composio) have their own commercial surface, that is captured in their per-provider repos, not here.
- **No single canonical "API of APIs."** The knowledge layer is intentionally federated — APIs.guru, RapidAPI, Postman, Naftiko Signals, and provider portals each hold a partial view, and a knowledge record's job is to stitch them together with provenance.

## Related Reading

- *[With API Knowledge Comes Great Power](https://apievangelist.com/2026/04/24/with-api-knowledge-comes-great-power/)* — Kin Lane, 2026-04-24.

## Maintainers

**FN:** Kin Lane

**Email:** kinlane@gmail.com
