---
title: Choose vi.fn(), vi.spyOn(), or vi.mock() Deliberately
impact: HIGH
impactDescription: prevents over-mocking and hidden bugs
tags: mock, vi, spy
---

## Choose vi.fn(), vi.spyOn(), or vi.mock() Deliberately

> **Impact: HIGH (prevents over-mocking and hidden bugs)**

Use `vi.fn()` for a throwaway callback you fully control, `vi.spyOn()` to observe or override one method on a real object while keeping the rest real, and `vi.mock()` to replace an entire module (e.g. a network client) at the module-resolution level.

## Incorrect

```ts
// Replacing a whole module just to stub one small helper
vi.mock("./math", () => ({
  add: vi.fn(() => 2),
  subtract: (a, b) => a - b, // still has to be reimplemented by hand
}));
```

## Correct

```ts
// Spy on just the one function that needs to be observed/stubbed
import * as math from "./math";
const addSpy = vi.spyOn(math, "add").mockReturnValue(2);
// math.subtract keeps its real implementation automatically
```

## Reference

- [Vitest Mocking Guide](https://vitest.dev/guide/mocking.html)
