---
name: unit-testing-vitest
description: Unit testing guidelines for Vitest (and Jest-compatible) JavaScript/TypeScript projects. Use this skill whenever writing, reviewing, or refactoring unit tests, adding vi mocks, configuring coverage, or debugging flaky/async test failures. Triggers on tasks involving *.test.ts, *.spec.ts files, vi.fn/vi.mock/vi.spyOn usage, Vitest config, or any request to "write tests", "add unit tests", "mock this", or "improve test coverage".
license: MIT
metadata:
  author: Tuan Duc Tran
  version: "1.0.0"
---

# Unit Testing (Vitest)

Guidelines for writing reliable, fast, and maintainable unit tests with Vitest in JS/TS projects. Contains 13 rules across 6 categories, prioritized by impact.

## When to Apply

Reference these guidelines when:

- Writing new unit tests for functions, classes, or components
- Adding or reviewing `vi.fn()` / `vi.mock()` / `vi.spyOn()` usage
- Configuring Vitest coverage thresholds or CI gates
- Debugging a test that's flaky, hangs, or silently passes
- Refactoring code and needing tests that won't break on implementation changes

## Rule Categories by Priority

| Priority | Category                | Impact | Prefix       |
| -------- | ----------------------- | ------ | ------------ |
| 1        | Test Structure & Naming | HIGH   | `structure-` |
| 2        | Assertions              | HIGH   | `assert-`    |
| 3        | Mocking & Test Doubles  | HIGH   | `mock-`      |
| 4        | Async & Timers          | HIGH   | `async-`     |
| 5        | Coverage & CI           | MEDIUM | `coverage-`  |
| 6        | Performance & Isolation | MEDIUM | `perf-`      |

## Quick Reference

### 1. Test Structure & Naming (HIGH)

- `structure-aaa-pattern` - Arrange-Act-Assert in every test
- `structure-descriptive-names` - Name tests after behavior, not method
- `structure-one-behavior-per-test` - One assertion focus per test

### 2. Assertions (HIGH)

- `assert-specific-matchers` - Use the most specific matcher available
- `assert-behavior-not-implementation` - Assert output, not internals

### 3. Mocking & Test Doubles (HIGH)

- `mock-vi-fn-spyon` - Choose vi.fn/vi.spyOn/vi.mock deliberately
- `mock-reset-restore` - Reset/restore mocks between tests
- `mock-avoid-mocking-what-you-own` - Don't mock code you can test directly

### 4. Async & Timers (HIGH)

- `async-await-promises` - Always await async assertions
- `async-fake-timers` - Use vi.useFakeTimers() instead of real delays

### 5. Coverage & CI (MEDIUM)

- `coverage-ci-thresholds` - Gate CI on explicit coverage thresholds
- `coverage-dont-chase-100` - Don't chase 100% on low-risk code

### 6. Performance & Isolation (MEDIUM)

- `perf-test-isolation` - Keep tests isolated for safe parallel runs

## How to Use This Skill

1. Read `rules/_sections.md` for full category descriptions.
2. For a specific task, open the relevant rule file(s) under `rules/` — each has an incorrect/correct code example.
3. When reviewing existing tests, check them against the HIGH-impact rules first (structure, assertions, mocking, async), then MEDIUM.
4. When writing new tests, default to the AAA pattern, prefer `vi.spyOn` over full `vi.mock` when only one function needs stubbing, and always `await` async assertions.

See `rules/_template.md` for the format used by every rule file.
