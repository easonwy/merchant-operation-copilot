# Implementation Plan

## Outcome

Build a production-style demonstration of a multi-agent merchant operations copilot while explicitly showing the spec-driven development workflow.

## Development approach

We will use a repeating loop:

1. Write or refine a spec for one slice.
2. Implement the smallest end-to-end increment that satisfies it.
3. Add tests and fixtures tied to the spec.
4. Demo the slice and capture follow-up requirements.

## Phases

### Phase 0: Project bootstrap

Deliverables:

- Architecture document
- Implementation plan
- SDD spec directory and templates

Exit criteria:

- The team can point to a single source of truth for scope and sequencing

### Phase 1: Foundation and first thin slice

Deliverables:

- App shell
- Typed orchestrator
- Static agent registry
- Simple classifier
- Order Agent and Refund Agent
- Stubbed tool adapters
- End-to-end query flow

Exit criteria:

- A user can submit a question about an order and refund
- The system shows which agents ran and why
- The final answer includes evidence and citations

### Phase 2: Multi-agent collaboration

Deliverables:

- Dispute Agent
- Policy Agent
- Fan-out and synthesis in orchestrator
- Execution timeline UI

Exit criteria:

- One request can invoke multiple agents
- Final response clearly merges their outputs

### Phase 3: Operational hardening

Deliverables:

- Persistent conversation and execution storage
- Structured traces and logs
- Failure handling and retries
- Replay fixtures and integration tests

Exit criteria:

- We can inspect execution state after completion
- The happy path and failure path are testable

### Phase 4: Human-in-the-loop controls

Deliverables:

- Review checkpoints for risky actions
- Operator approval UI
- Case note generation

Exit criteria:

- Recommended actions can be reviewed before submission

## Recommended repo structure

```text
docs/
  architecture.md
  implementation-plan.md
  sdd/
    000-overview.md
    001-foundation-and-first-slice.md
src/
  app/
  components/
  server/
tests/
  fixtures/
```

## Suggested first implementation task

After the docs, the next concrete step should be:

- Scaffold the TypeScript app
- Add the orchestrator contract
- Add a static registry
- Implement one scenario: "Explain why order `#10483` was refunded"
