---
title: Give Each Test Suite Its Own Isolated Environment
impact: HIGH
impactDescription: prevents cross-suite interference and flaky CI runs
tags: env, isolation, ci
---

## Give Each Test Suite Its Own Isolated Environment

> **Impact: HIGH (prevents cross-suite interference and flaky CI runs)**

Sharing one long-lived test database or queue across the whole CI run means one suite's leftover data can break another's assertions. Spin up a fresh container (or fresh schema) per test file or per CI job.

## Incorrect

```ts
// one shared Postgres instance for the entire CI run, all suites write into it
const db = connect(process.env.SHARED_TEST_DB_URL);
```

## Correct

```ts
// each test file gets its own container, torn down after
beforeAll(async () => {
  container = await new PostgreSqlContainer().start();
});
afterAll(async () => {
  await container.stop();
});
```

## Reference

- [Testcontainers for Node.js](https://node.testcontainers.org/)
