---
title: Encapsulate Page Structure in Page Objects
impact: MEDIUM
impactDescription: isolates locator changes to one place
tags: pom, structure, maintainability
---

# Encapsulate Page Structure in Page Objects

> **Impact: MEDIUM (isolates locator changes to one place)**

Wrap a page's locators and common actions in a Page Object class. When the UI changes, only the page object updates — tests that use it stay unchanged.

## Incorrect

```ts
test("adds item to cart", async ({ page }) => {
  await page.goto("/products/1");
  await page.getByRole("button", { name: "Add to cart" }).click();
  await expect(page.getByRole("status")).toHaveText("Added to cart");
});
// repeated verbatim in every test that touches this page
```

## Correct

```ts
class ProductPage {
  constructor(private page: Page) {}
  async goto(id: string) {
    await this.page.goto(`/products/${id}`);
  }
  async addToCart() {
    await this.page.getByRole("button", { name: "Add to cart" }).click();
  }
  get statusMessage() {
    return this.page.getByRole("status");
  }
}

test("adds item to cart", async ({ page }) => {
  const productPage = new ProductPage(page);
  await productPage.goto("1");
  await productPage.addToCart();
  await expect(productPage.statusMessage).toHaveText("Added to cart");
});
```

## Reference

- [Playwright Page Object Models](https://playwright.dev/docs/pom)
