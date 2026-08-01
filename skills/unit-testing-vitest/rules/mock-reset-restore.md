---
title: Reset or Restore Mocks Between Tests
impact: HIGH
impactDescription: eliminates cross-test state leakage
tags: mock, isolation, cleanup
---

# Reset or Restore Mocks Between Tests

> **Impact: HIGH (eliminates cross-test state leakage)**

Mock call history and implementations persist across tests unless cleared. Configure `restoreMocks: true` (or call `vi.restoreAllMocks()` in `afterEach`) so one test's mock state can't leak into the next and cause order-dependent failures.

## Incorrect

```ts
// vitest.config.ts
export default defineConfig({
  test: {}, // mocks silently accumulate call history across tests
});
```

## Correct

```ts
// vitest.config.ts
export default defineConfig({
  test: {
    restoreMocks: true, // restores original implementations
    clearMocks: true, // clears mock.calls / mock.results
  },
});
```

## Reference

- [Vitest Config Reference](https://vitest.dev/config/)
