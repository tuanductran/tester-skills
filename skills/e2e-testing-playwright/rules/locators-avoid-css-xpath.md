---
title: Avoid CSS and XPath Selectors Tied to DOM Structure
impact: HIGH
impactDescription: reduces selector breakage on refactors
tags: locators, css, xpath
---

# Avoid CSS and XPath Selectors Tied to DOM Structure

> **Impact: HIGH (reduces selector breakage on refactors)**

Structural selectors like `div > div:nth-child(3) > span` break the moment a wrapper div is added. When no role-based option exists, use a dedicated `data-testid` instead of styling classes or DOM position.

## Incorrect

```ts
await page.locator("div.card:nth-child(2) .price").textContent();
```

## Correct

```ts
await page.getByTestId("product-price").textContent();
```

## Reference

- [Playwright Locators Guide](https://playwright.dev/docs/locators)
