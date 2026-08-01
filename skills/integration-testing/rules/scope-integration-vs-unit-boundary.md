---
title: Reserve Integration Tests for Boundaries Between Systems
impact: HIGH
impactDescription: keeps the test pyramid fast at the base
tags: scope, test-pyramid, boundaries
---

# Reserve Integration Tests for Boundaries Between Systems

> **Impact: HIGH (keeps the test pyramid fast at the base)**

Integration tests should verify that your code correctly talks to a real database, queue, or external API — not re-verify business logic that a unit test already covers with a mock. Pure logic belongs in unit tests; wiring belongs in integration tests.

## Incorrect

```ts
// Integration test that re-checks pure discount math already covered by a unit test
it("calculates a 10% discount correctly", async () => {
  const db = await startTestDb();
  expect(calculateDiscount(100, 0.1)).toBe(90);
});
```

## Correct

```ts
// Integration test verifies the repository actually persists and reads back correctly
it("persists an order and reads it back with the correct total", async () => {
  const db = await startTestDb();
  const repo = new OrderRepository(db);
  const saved = await repo.save({ total: 90 });
  expect((await repo.findById(saved.id)).total).toBe(90);
});
```

## Reference

- [Martin Fowler - Test Pyramid](https://martinfowler.com/bliki/TestPyramid.html)
