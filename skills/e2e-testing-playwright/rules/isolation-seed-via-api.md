---
title: Seed Test Data Through the API, Not the UI
impact: HIGH
impactDescription: cuts test time and removes UI as a dependency for setup
tags: isolation, fixtures, api
---

# Seed Test Data Through the API, Not the UI

> **Impact: HIGH (cuts test time and removes UI as a dependency for setup)**

Driving setup steps (creating an account, adding items) through the UI multiplies test time and makes every test fail if an unrelated UI flow breaks. Use a direct API/database call for setup, and reserve UI interaction for what's actually under test.

## Incorrect

```ts
test("checkout applies a discount code", async ({ page }) => {
  await page.goto("/signup");
  await fillSignupForm(page); // slow, unrelated to what's tested
  await addItemToCartViaUI(page);
  await applyDiscountCode(page, "SAVE10");
  await expect(page.getByText("Total: $90")).toBeVisible();
});
```

## Correct

```ts
test("checkout applies a discount code", async ({ page, request }) => {
  const user = await createUserViaApi(request);
  await addItemToCartViaApi(request, user, { price: 100 });
  await loginAs(page, user);
  await applyDiscountCode(page, "SAVE10");
  await expect(page.getByText("Total: $90")).toBeVisible();
});
```

## Reference

- [Playwright Best Practices](https://playwright.dev/docs/best-practices)
