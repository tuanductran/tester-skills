---
title: Make Every Test Independently Runnable
impact: HIGH
impactDescription: lets tests run in any order or in isolation
tags: isolation, independence
---

# Make Every Test Independently Runnable

> **Impact: HIGH (lets tests run in any order or in isolation)**

A test should never rely on a previous test having run (e.g. a login test creating a session that a cart test reuses). Each test should set up its own preconditions, typically via fixtures or `beforeEach`.

## Incorrect

```ts
test("logs in", async ({ page }) => {
  /* logs in, leaves session for next test */
});
test("adds item to cart", async ({ page }) => {
  /* assumes still logged in */
});
```

## Correct

```ts
test.beforeEach(async ({ page }) => {
  await loginAs(page, "test-user");
});
test("adds item to cart", async ({ page }) => {
  /* independently logged in */
});
```

## Reference

- [Playwright Best Practices](https://playwright.dev/docs/best-practices)
