---
title: Don't Mock Code You Own and Can Test Directly
impact: MEDIUM
impactDescription: keeps tests meaningful
tags: mock, over-mocking
---

# Don't Mock Code You Own and Can Test Directly

> **Impact: MEDIUM (keeps tests meaningful)**

Mocking your own pure functions or simple modules just to isolate a test usually means the unit under test is too large, or the test isn't actually testing anything. Reserve mocks for true boundaries: network calls, the filesystem, timers, and third-party services.

## Incorrect

```ts
vi.mock("./calculateTax", () => ({ calculateTax: () => 5 }));
it("adds tax to the total", () => {
  expect(getTotal(100)).toBe(105);
});
```

## Correct

```ts
// calculateTax is pure and cheap — just let it run for real
it("adds tax to the total", () => {
  expect(getTotal(100)).toBe(105);
});
```

## Reference

- [Vitest Mocking Guide](https://vitest.dev/guide/mocking.html)
