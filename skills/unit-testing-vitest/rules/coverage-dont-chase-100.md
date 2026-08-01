---
title: Don't Chase 100% Coverage on Low-Risk Code
impact: LOW
impactDescription: keeps test effort proportional to risk
tags: coverage, prioritization
---

# Don't Chase 100% Coverage on Low-Risk Code

> **Impact: LOW (keeps test effort proportional to risk)**

100% coverage on trivial getters or generated code wastes effort and often produces tests that just re-assert the implementation. Prioritize coverage on business logic, edge cases, and error paths over boilerplate.

## Incorrect

```ts
// Testing a plain data class getter just to move the coverage number
it("getter returns the field", () => {
  expect(new Point(1, 2).x).toBe(1);
});
```

## Correct

```ts
// Spend the equivalent effort on an actual edge case instead
it("rejects negative radius when constructing a circle", () => {
  expect(() => new Circle(-1)).toThrow("radius must be positive");
});
```

## Reference

- [Vitest Coverage Guide](https://vitest.dev/guide/coverage.html)
