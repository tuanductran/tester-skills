---
title: Assert on Behavior, Not Internals
impact: HIGH
impactDescription: prevents brittle tests that break on refactors
tags: assert, behavior, refactor-safety
---

# Assert on Behavior, Not Internals

> **Impact: HIGH (prevents brittle tests that break on refactors)**

Test the public output of a function or component, not its private fields or call counts of helper functions it happens to use today. Internal-detail assertions force a test rewrite on every safe refactor.

## Incorrect

```ts
it("formats a price", () => {
  const formatter = new PriceFormatter();
  const spy = vi.spyOn(formatter, "_roundToCents");
  formatter.format(19.999);
  expect(spy).toHaveBeenCalled();
});
```

## Correct

```ts
it("formats a price to two decimal places", () => {
  const formatter = new PriceFormatter();
  expect(formatter.format(19.999)).toBe("$20.00");
});
```

## Reference

- [Vitest Component Testing Guide](https://vitest.dev/guide/browser/component-testing)
