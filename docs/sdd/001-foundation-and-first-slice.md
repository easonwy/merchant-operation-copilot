# Spec 001: Foundation and First Slice

## Problem

We need a first end-to-end slice that demonstrates the multi-agent architecture from the article without waiting for every production concern to be fully built. The slice must still look and behave like a real system, not a toy script.

## Demo scenario

An operations user asks:

`Why was order #10483 refunded, and what should we do next?`

The application should:

1. Classify the request.
2. Select the relevant agents.
3. Gather evidence from stubbed tools.
4. Produce a structured final answer with citations and next-step guidance.
5. Show the execution trace in the UI.

## User stories

- As an operations user, I can ask a merchant case question in natural language.
- As an operations user, I can see which agents participated in the answer.
- As an operations user, I can inspect the supporting evidence used in the recommendation.
- As a developer, I can add a new agent without rewriting the orchestrator.

## Functional requirements

### Request handling

- The system shall expose an endpoint to submit a copilot query.
- The request shall create an execution record with a unique id.
- The orchestrator shall invoke the classifier before selecting agents.

### Classification

- The classifier shall return a normalized intent.
- The classifier shall return a confidence score.
- The classifier shall suggest one or more candidate capabilities.

### Registry

- The registry shall map capabilities to agents.
- The registry shall be statically configured in this phase.

### Agent execution

- The orchestrator shall invoke the Order Agent and Refund Agent for the demo scenario.
- Each agent shall return structured output using a shared TypeScript schema.
- The orchestrator shall synthesize agent outputs into a final response object.

### UI

- The app shall provide a query input view.
- The app shall render the final answer.
- The app shall show the agents invoked and their status.
- The app shall show evidence entries and citations.

## Non-functional requirements

- Shared contracts shall be strongly typed.
- Stubbed tool calls shall be deterministic for local demos and tests.
- The execution path shall support structured logging.
- Failures in one tool call shall produce a safe user-visible fallback.

## API contract

### `POST /api/copilot/query`

Request:

```json
{
  "message": "Why was order #10483 refunded, and what should we do next?",
  "sessionId": "demo-session-1"
}
```

Response:

```json
{
  "executionId": "exec_123",
  "intent": "order_refund_analysis",
  "agents": [
    {
      "id": "order-agent",
      "status": "completed"
    },
    {
      "id": "refund-agent",
      "status": "completed"
    }
  ],
  "answer": {
    "summary": "The refund was issued after the shipment missed the promised delivery date by 6 days and the compensation policy threshold was met.",
    "recommendedAction": "Close the refund investigation and add a merchant coaching note.",
    "citations": [
      {
        "source": "shipment-status",
        "label": "Shipment status timeline"
      },
      {
        "source": "refund-history",
        "label": "Refund event log"
      }
    ]
  }
}
```

## Data model

### Execution record

- `id`
- `sessionId`
- `message`
- `intent`
- `status`
- `startedAt`
- `completedAt`
- `agentRuns`

### Agent result

- `agentId`
- `summary`
- `evidence`
- `recommendedAction`
- `confidence`
- `citations`

## Test plan

- Unit tests for classifier routing
- Unit tests for registry resolution
- Unit tests for orchestrator synthesis
- Integration test for the end-to-end demo scenario
- UI test for rendering answer and execution timeline

## Acceptance criteria

- A developer can run the app locally and submit the demo question.
- The response consistently uses the Order Agent and Refund Agent.
- The answer contains a summary, recommended action, and at least two citations.
- The UI displays the execution id and per-agent status.
- Tests cover the classifier, registry, orchestrator, and one end-to-end path.

## Out of scope

- Real model provider integration
- Real MCP server deployment
- Human approval workflow
- Persistent database storage beyond in-memory or fixture-backed storage
