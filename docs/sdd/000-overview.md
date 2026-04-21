# SDD Overview

## Purpose

This directory holds the specifications that drive implementation. Each spec should be concrete enough to produce:

- Code changes
- Tests
- Demo scenarios
- Reviewable acceptance criteria

## Spec format

Each implementation spec should contain:

1. Problem
2. User stories
3. Functional requirements
4. Non-functional requirements
5. API or contract changes
6. Data model changes
7. Test plan
8. Acceptance criteria
9. Out-of-scope notes

## Working agreement

- Specs are updated before significant implementation changes
- Code should reference the spec it satisfies
- Tests should cover acceptance criteria, not just internal functions
- Each phase should leave the system demoable

## Definition of done

A slice is done when:

- The spec is approved or accepted for the current scope
- The implementation matches the spec
- Relevant tests pass
- The user-visible demo scenario works
- Known gaps are documented
