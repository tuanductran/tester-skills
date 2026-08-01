---
title: Follow Arrange-Act-Assert Structure
impact: HIGH
impactDescription: improves readability and debugging speed
tags: structure, aaa, readability
---

# Follow Arrange-Act-Assert Structure

> **Impact: HIGH (improves readability and debugging speed)**

Split every test into three clear blocks: set up state (Arrange), perform the action under test (Act), and check the outcome (Assert). Mixing these together makes it hard to tell what a test is actually checking when it fails.

## Incorrect

```ts
it("applies a discount", () => {
  const cart = new Cart();
  cart.add({ price: 100 });
  expect(cart.applyDiscount(0.1).total).toBe(90);
  cart.add({ price: 50 });
});
```

## Correct

```ts
it("applies a discount to the cart total", () => {
  // Arrange
  const cart = new Cart();
  cart.add({ price: 100 });

  // Act
  const result = cart.applyDiscount(0.1);

  // Assert
  expect(result.total).toBe(90);
});
```

## Reference

- [Vitest Guide](https://vitest.dev/guide/)
