# Merchant Operations Copilot

This repository demonstrates a production-style multi-agent application inspired by Microsoft's article ["Designing Multi-Agent Intelligence"](https://developer.microsoft.com/blog/designing-multi-agent-intelligence).

We are building it using a spec-driven development (SDD) workflow:

1. Define the product and architecture first.
2. Break the system into implementation phases with acceptance criteria.
3. Implement one thin vertical slice at a time.
4. Keep specs, code, and tests aligned as the system evolves.

## Demo Goal

The application is a merchant operations copilot for an e-commerce platform. It helps operations staff handle requests such as:

- "Why was order `#10483` refunded?"
- "Should this dispute be escalated?"
- "Show the merchant impact if we approve this compensation."
- "Draft the next action for this delayed shipment case."

The system uses a multi-agent architecture with:

- An orchestrator
- A classifier
- An agent registry
- Specialized domain agents
- Shared conversation and execution state
- Tool integrations behind a consistent interface

## Project Docs

- [Architecture](./docs/architecture.md)
- [Implementation Plan](./docs/implementation-plan.md)
- [SDD Overview](./docs/sdd/000-overview.md)
- [Phase 1 Spec](./docs/sdd/001-foundation-and-first-slice.md)

## Proposed Stack

- Frontend: Next.js + TypeScript
- Backend: Next.js route handlers or a lightweight Node service
- Workflow runtime: typed orchestrator layer in TypeScript
- Storage: PostgreSQL + Redis
- Observability: OpenTelemetry-compatible tracing and structured logs
- AI integration: pluggable model provider interface

## Initial Scope

The first production-style slice will support a single end-to-end scenario:

- User submits a merchant operations question
- Classifier identifies the task
- Orchestrator selects one or more agents
- Agents call tools and produce structured results
- Orchestrator returns a final answer with citations, reasoning summary, and audit trail metadata
