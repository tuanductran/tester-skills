---
name: e2e-testing-playwright
description: End-to-end (E2E) browser testing guidelines for Playwright. Use this skill whenever writing, reviewing, or debugging Playwright tests, choosing locators, diagnosing flaky tests, structuring Page Objects, or configuring CI for an E2E suite. Triggers on tasks involving *.spec.ts Playwright files, page.locator/getByRole usage, requests to "write an e2e test", "automate this flow", "fix this flaky test", or "set up Playwright CI".
license: MIT
metadata:
  author: Tuan Duc Tran
  version: "1.0.0"
---

# E2E Testing (Playwright)

Guidelines for writing stable, fast end-to-end tests with Playwright. Contains 9 rules across 5 categories, prioritized by impact on flakiness and maintainability.

## When to Apply

Reference these guidelines when:

- Writing a new Playwright test for a user flow
- Choosing locators for elements on a page
- Diagnosing a flaky or intermittently failing E2E test
- Structuring a growing suite with Page Objects
- Setting up or tuning Playwright in CI (sharding, retries, tracing)

## Rule Categories by Priority

| Priority | Category                      | Impact   | Prefix       |
| -------- | ----------------------------- | -------- | ------------ |
| 1        | Locator Strategy              | CRITICAL | `locators-`  |
| 2        | Waiting & Assertions          | CRITICAL | `waiting-`   |
| 3        | Test Isolation & Data         | HIGH     | `isolation-` |
| 4        | Page Object Model & Structure | MEDIUM   | `pom-`       |
| 5        | CI & Reliability              | MEDIUM   | `ci-`        |

## Quick Reference

### 1. Locator Strategy (CRITICAL)

- `locators-role-based` - Prefer getByRole/getByLabel/getByText
- `locators-avoid-css-xpath` - Avoid structural CSS/XPath selectors

### 2. Waiting & Assertions (CRITICAL)

- `waiting-no-fixed-timeouts` - Never use waitForTimeout in committed tests
- `waiting-web-first-assertions` - Use expect(locator).toHave*() over manual reads

### 3. Test Isolation & Data (HIGH)

- `isolation-independent-tests` - Every test independently runnable
- `isolation-seed-via-api` - Seed data via API, not UI

### 4. Page Object Model & Structure (MEDIUM)

- `pom-page-object-model` - Encapsulate locators/actions per page

### 5. CI & Reliability (MEDIUM)

- `ci-parallel-sharding` - Shard suites across CI machines
- `ci-trace-on-retry` - Capture traces only on retry

## How to Use This Skill

1. Read `rules/_sections.md` for full category descriptions.
2. When writing a new test, start from `locators-role-based` and `waiting-web-first-assertions` — most flakiness starts here.
3. When triaging a flaky test, check `waiting-no-fixed-timeouts` and `isolation-independent-tests` first.
4. As a suite grows past a handful of tests, apply `pom-page-object-model` to keep locator changes centralized.

See `rules/_template.md` for the format used by every rule file.
