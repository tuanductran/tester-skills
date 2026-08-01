---
title: Use the Most Specific Matcher Available
impact: HIGH
impactDescription: catches subtle regressions and gives clearer diffs
tags: assert, matchers
---

# Use the Most Specific Matcher Available

> **Impact: HIGH (catches subtle regressions and gives clearer diffs)**

Prefer `toEqual`, `toHaveLength`, `toMatchObject`, or `toBeCloseTo` over a generic truthy check. A specific matcher fails with a readable diff; `toBeTruthy()` on an object just says 'truthy' when a field is wrong.

## Incorrect

```ts
expect(user).toBeTruthy();
expect(items.length > 0).toBe(true);
```

## Correct

```ts
expect(user).toEqual({ id: 1, name: "Ada", active: true });
expect(items).toHaveLength(3);
```

## Reference

- [Vitest Expect API](https://vitest.dev/api/expect.html)
