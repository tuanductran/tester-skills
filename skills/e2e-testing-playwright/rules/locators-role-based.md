---
title: Prefer Role-Based and User-Facing Locators
impact: CRITICAL
impactDescription: resists markup and CSS refactors
tags: locators, getByRole, accessibility
---

# Prefer Role-Based and User-Facing Locators

> **Impact: CRITICAL (resists markup and CSS refactors)**

Locate elements the way a user or assistive technology would: `getByRole`, `getByLabel`, `getByText`. These survive class-name and DOM-structure changes and double as an accessibility check.

## Incorrect

```ts
await page.click(".btn.btn-primary.submit-form > span");
```

## Correct

```ts
await page.getByRole("button", { name: "Submit" }).click();
```

## Reference

- [Playwright Best Practices](https://playwright.dev/docs/best-practices)
