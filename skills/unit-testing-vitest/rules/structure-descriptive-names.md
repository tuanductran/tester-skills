---
title: Write Behavior-Describing Test Names
impact: MEDIUM
impactDescription: faster triage of failures in CI
tags: structure, naming
---

# Write Behavior-Describing Test Names

> **Impact: MEDIUM (faster triage of failures in CI)**

Name tests after the observable behavior, not the method name. A reader (or a CI notification) should understand what broke without opening the file.

## Incorrect

```ts
it("works", () => {
  /* ... */
});
it("test discount", () => {
  /* ... */
});
```

## Correct

```ts
it("returns the original total when no discount code is applied", () => {
  /* ... */
});
it("rejects a discount code that has already been redeemed", () => {
  /* ... */
});
```

## Reference

- [Vitest Guide](https://vitest.dev/guide/)
