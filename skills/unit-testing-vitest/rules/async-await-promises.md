---
title: Always Await Async Assertions
impact: HIGH
impactDescription: prevents tests that pass even when the code throws
tags: async, promises, await
---

# Always Await Async Assertions

> **Impact: HIGH (prevents tests that pass even when the code throws)**

A missing `await` on an async call or a `rejects`/`resolves` assertion lets the test function return before the assertion runs, so a broken implementation can still report green. Vitest's `expect(fn).rejects.toThrow()` must itself be awaited.

## Incorrect

```ts
it("throws on invalid input", () => {
  expect(parseConfig("{bad json")).rejects.toThrow();
  // test function returns before the rejection is checked
});
```

## Correct

```ts
it("throws on invalid input", async () => {
  await expect(parseConfig("{bad json")).rejects.toThrow();
});
```

## Reference

- [Vitest Expect API](https://vitest.dev/api/expect.html)
