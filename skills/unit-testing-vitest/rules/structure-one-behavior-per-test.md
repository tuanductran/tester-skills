---
title: One Behavior Per Test
impact: MEDIUM
impactDescription: isolates failures to a single cause
tags: structure, isolation
---

# One Behavior Per Test

> **Impact: MEDIUM (isolates failures to a single cause)**

Each `it` block should assert one behavior. Tests that check many unrelated things fail for ambiguous reasons and get skipped or deleted when they become annoying.

## Incorrect

```ts
it("cart behaves correctly", () => {
  const cart = new Cart();
  expect(cart.total).toBe(0);
  cart.add({ price: 10 });
  expect(cart.total).toBe(10);
  cart.remove(0);
  expect(cart.total).toBe(0);
  expect(cart.isEmpty()).toBe(true);
});
```

## Correct

```ts
describe("Cart", () => {
  it("starts empty", () => {
    expect(new Cart().total).toBe(0);
  });

  it("adds an item to the total", () => {
    const cart = new Cart();
    cart.add({ price: 10 });
    expect(cart.total).toBe(10);
  });

  it("is empty after the only item is removed", () => {
    const cart = new Cart();
    cart.add({ price: 10 });
    cart.remove(0);
    expect(cart.isEmpty()).toBe(true);
  });
});
```

## Reference

- [Vitest Guide](https://vitest.dev/guide/)
