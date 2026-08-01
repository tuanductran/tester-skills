# Tester Skills

A collection of testing skills for AI coding agents, covering the full-stack JS/TS testing lifecycle: unit, integration, API, end-to-end, and performance testing.

Skills follow the open Agent Skills (`SKILL.md`) specification, making them compatible with Claude, Claude Code, and other agent runtimes that support the format.

## Available Skills

### unit-testing-vitest

Unit testing guidelines for Vitest (Jest-compatible) projects. Covers test structure, assertions, mocking with `vi`, async/timer handling, and coverage gating.

**Use when:**

- Writing or reviewing unit tests
- Adding `vi.fn()` / `vi.mock()` / `vi.spyOn()` mocks
- Configuring Vitest coverage thresholds
- Debugging a flaky or silently-passing async test

**Categories covered:** Test Structure & Naming (HIGH) · Assertions (HIGH) · Mocking & Test Doubles (HIGH) · Async & Timers (HIGH) · Coverage & CI (MEDIUM) · Performance & Isolation (MEDIUM)

### e2e-testing-playwright

End-to-end browser testing guidelines for Playwright. Covers locator strategy, auto-waiting, test isolation, the Page Object Model, and CI reliability.

**Use when:**

- Writing or automating a user-flow test
- Choosing locators for UI elements
- Diagnosing a flaky E2E test
- Setting up Playwright sharding, retries, or tracing in CI

**Categories covered:** Locator Strategy (CRITICAL) · Waiting & Assertions (CRITICAL) · Test Isolation & Data (HIGH) · Page Object Model & Structure (MEDIUM) · CI & Reliability (MEDIUM)

### api-testing

API/HTTP testing guidelines for REST/JSON services. Covers contract validation, request construction, auth coverage, negative test cases, and test data.

**Use when:**

- Testing a new or existing endpoint
- Validating response schemas
- Checking authentication/authorization boundaries
- Adding negative or edge-case tests

**Categories covered:** Contract & Schema Validation (HIGH) · Request Construction (HIGH) · Authentication & Authorization (MEDIUM) · Error & Edge Cases (MEDIUM) · Test Data Management (MEDIUM)

### integration-testing

Integration testing guidelines for services that talk to real databases, queues, or external systems. Covers test scope, Testcontainers, transactional isolation, and fixtures.

**Use when:**

- Deciding whether a test belongs at unit or integration level
- Testing against a real database/queue via Testcontainers
- Managing database state and cleanup between tests

**Categories covered:** Test Boundary & Scope (HIGH) · Environment & Real Dependencies (HIGH) · Database State (HIGH) · Fixtures & Test Data (MEDIUM)

### performance-testing

Performance testing guidelines covering backend load testing (k6) and frontend Core Web Vitals (Lighthouse CI).

**Use when:**

- Writing a load test
- Setting performance budgets that gate CI
- Investigating a performance regression
- Profiling a slow endpoint or page

**Categories covered:** Load Testing (HIGH) · Web Vitals & Frontend Budgets (HIGH) · Profiling & Diagnosis (MEDIUM)

## Repository Structure

```text
tester-skills/
├── README.md
├── LICENSE
└── skills/
    ├── unit-testing-vitest/
    │   ├── SKILL.md          # frontmatter (name, description) + quick reference
    │   ├── README.md
    │   ├── metadata.json
    │   └── rules/
    │       ├── _sections.md  # category definitions, ordering, impact
    │       ├── _template.md  # format every rule file follows
    │       └── <prefix>-<rule-name>.md
    ├── e2e-testing-playwright/
    ├── api-testing/
    ├── integration-testing/
    └── performance-testing/
```

Each rule file follows the same format: frontmatter (`title`, `impact`, `impactDescription`, `tags`) followed by a short explanation, an **Incorrect** example, a **Correct** example, and a reference link.

## Using These Skills

Drop the `skills/` directory (or an individual skill folder) into your agent's skills directory. Each `SKILL.md`'s frontmatter `description` is written to trigger on natural testing-related requests (e.g. "write a unit test", "fix this flaky e2e test", "test this endpoint"). The agent reads the relevant rule files under `rules/` on demand rather than loading the whole corpus up front.

## Why These Five Skills

They map to the layers of the test pyramid plus the two testing concerns that cut across all of them:

- **unit** → fast, isolated logic checks
- **integration** → the seams between your code and real infrastructure
- **api** → the contract your service exposes over HTTP
- **e2e** → what a real user actually experiences
- **performance** → whether it's fast enough under load, at each of the above layers

## License

MIT
