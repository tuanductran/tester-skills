---
title: Use Web-First Assertions Instead of Manual Reads
impact: CRITICAL
impactDescription: eliminates race conditions between render and assert
tags: waiting, assertions, expect
---

# Use Web-First Assertions Instead of Manual Reads

> **Impact: CRITICAL (eliminates race conditions between render and assert)**

`expect(locator).toHaveText()` retries until the condition is true or the timeout elapses. Reading `.textContent()` once and comparing it manually races against the page still rendering.

## Incorrect

```ts
const text = await page.locator(".status").textContent();
expect(text).toBe("Saved");
```

## Correct

```ts
await expect(page.locator(".status")).toHaveText("Saved");
```

## Reference

- [Playwright Auto-waiting](https://playwright.dev/docs/actionability)
