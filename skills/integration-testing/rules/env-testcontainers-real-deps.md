---
title: Use Testcontainers for Real Dependencies Instead of In-Memory Fakes
impact: HIGH
impactDescription: catches bugs that only exist against the real engine
tags: env, testcontainers, docker
---

# Use Testcontainers for Real Dependencies Instead of In-Memory Fakes

> **Impact: HIGH (catches bugs that only exist against the real engine)**

An in-memory SQLite or a hand-rolled fake Redis behaves differently from production Postgres or Redis in subtle ways (constraint enforcement, transaction isolation, data types). Spin up the real dependency in a disposable Docker container per test run via Testcontainers.

## Incorrect

```ts
// sqlite:memory: doesn't enforce the same constraints as production Postgres
const db = new Database(":memory:");
```

## Correct

```ts
import { PostgreSqlContainer } from "@testcontainers/postgresql";

const container = await new PostgreSqlContainer("postgres:16").start();
const db = createConnection(container.getConnectionUri());
```

## Reference

- [Testcontainers for Node.js](https://node.testcontainers.org/)
