---
name: integration-testing
description: Integration testing guidelines for JS/TS services that talk to real databases, queues, or external systems. Use this skill whenever writing or reviewing tests that spin up a database/container, testing a repository or data-access layer, deciding whether something should be a unit or integration test, or managing test database state. Triggers on requests like "write an integration test", "test this repository against a real database", "set up testcontainers", or "how should I structure this test".
license: MIT
metadata:
  author: Tuan Duc Tran
  version: "1.0.0"
---

# Integration Testing

Guidelines for testing the seams between your code and real infrastructure — databases, queues, external services — without making the suite slow or flaky. Contains 6 rules across 4 categories.

## When to Apply

Reference these guidelines when:

- Deciding whether a test belongs at the unit or integration level
- Writing a test that needs a real database, cache, or message queue
- Managing database state and cleanup between tests
- Building reusable fixtures/factories for integration-level test data

## Rule Categories by Priority

| Priority | Category                        | Impact | Prefix      |
| -------- | ------------------------------- | ------ | ----------- |
| 1        | Test Boundary & Scope           | HIGH   | `scope-`    |
| 2        | Environment & Real Dependencies | HIGH   | `env-`      |
| 3        | Database State                  | HIGH   | `db-`       |
| 4        | Fixtures & Test Data            | MEDIUM | `fixtures-` |

## Quick Reference

### 1. Test Boundary & Scope (HIGH)

- `scope-integration-vs-unit-boundary` - Reserve integration tests for system boundaries

### 2. Environment & Real Dependencies (HIGH)

- `env-testcontainers-real-deps` - Use Testcontainers instead of in-memory fakes
- `env-avoid-shared-state` - Isolated environment per suite

### 3. Database State (HIGH)

- `db-transactional-rollback` - Wrap each test in a transaction + rollback
- `db-seed-minimal-fixtures` - Seed only what each test needs

### 4. Fixtures & Test Data (MEDIUM)

- `fixtures-factory-functions` - Build test data with factory functions

## How to Use This Skill

1. Read `rules/_sections.md` for full category descriptions.
2. Before writing a new test, check `scope-integration-vs-unit-boundary` to confirm it actually needs a real dependency.
3. Default to Testcontainers (`env-testcontainers-real-deps`) plus transactional rollback (`db-transactional-rollback`) for anything touching a database.

See `rules/_template.md` for the format used by every rule file.
