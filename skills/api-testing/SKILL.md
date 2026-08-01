---
name: api-testing
description: API testing guidelines for REST/JSON HTTP services in Node.js/TypeScript, covering Supertest-style request testing, schema validation, auth coverage, and negative test cases. Use this skill whenever writing or reviewing tests for API endpoints, testing an Express/Fastify/Next.js route handler, validating response contracts, or checking auth/error paths. Triggers on requests like "test this endpoint", "write an API test", "validate this response schema", or "check auth on this route".
license: MIT
metadata:
  author: Tuan Duc Tran
  version: "1.0.0"
---

# API Testing

Guidelines for testing HTTP APIs so they catch contract breaks, access-control bugs, and unhandled edge cases before production. Contains 8 rules across 5 categories.

## When to Apply

Reference these guidelines when:

- Writing tests for a new or existing API endpoint
- Validating response shape/schema, not just status codes
- Testing authentication and authorization boundaries
- Adding negative/edge-case tests for input validation
- Setting up test data that must be safe under parallel test runs

## Rule Categories by Priority

| Priority | Category                       | Impact | Prefix      |
| -------- | ------------------------------ | ------ | ----------- |
| 1        | Contract & Schema Validation   | HIGH   | `contract-` |
| 2        | Request Construction           | HIGH   | `requests-` |
| 3        | Authentication & Authorization | MEDIUM | `auth-`     |
| 4        | Error & Edge Cases             | MEDIUM | `errors-`   |
| 5        | Test Data Management           | MEDIUM | `data-`     |

## Quick Reference

### 1. Contract & Schema Validation (HIGH)

- `contract-status-and-shape` - Assert status code AND response shape
- `contract-schema-validation` - Validate against a schema, not ad-hoc fields

### 2. Request Construction (HIGH)

- `requests-isolated-app-instance` - Test the app instance, not a live port
- `requests-idempotency` - Verify idempotency on PUT/DELETE

### 3. Authentication & Authorization (MEDIUM)

- `auth-cover-unauthorized-paths` - Test 401/403 explicitly, not just 200

### 4. Error & Edge Cases (MEDIUM)

- `errors-negative-cases` - Write negative tests for every endpoint
- `errors-consistent-error-shape` - Assert on a consistent error format

### 5. Test Data Management (MEDIUM)

- `data-independent-fixtures` - Generate data per-test, never hardcode IDs

## How to Use This Skill

1. Read `rules/_sections.md` for full category descriptions.
2. For a new endpoint, cover the happy path (`contract-status-and-shape`), then auth boundaries (`auth-cover-unauthorized-paths`), then negative cases (`errors-negative-cases`).
3. Prefer schema-based validation (`contract-schema-validation`) over field-by-field checks for anything with more than 3-4 fields.

See `rules/_template.md` for the format used by every rule file.
