---
title: Keep Tests Isolated for Safe Parallel Runs
impact: MEDIUM
impactDescription: enables full-speed parallel execution
tags: perf, isolation, parallel
---

# Keep Tests Isolated for Safe Parallel Runs

> **Impact: MEDIUM (enables full-speed parallel execution)**

Vitest runs test files in parallel workers by default. Tests that share mutable module-level state, a global DB connection, or a fixed port will pass alone and fail under parallel execution. Give each test file its own state.

## Incorrect

```ts
let counter = 0; // module-level state shared across tests in the file
it("increments once", () => {
  counter++;
  expect(counter).toBe(1);
});
it("increments twice", () => {
  counter++;
  expect(counter).toBe(2);
}); // order-dependent
```

## Correct

```ts
it("increments once", () => {
  let counter = 0;
  counter++;
  expect(counter).toBe(1);
});
it("increments twice from its own state", () => {
  let counter = 0;
  counter += 2;
  expect(counter).toBe(2);
});
```

## Reference

- [Vitest Guide - Test Isolation](https://vitest.dev/guide/)
