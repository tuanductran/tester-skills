---
title: Never Use waitForTimeout in Committed Tests
impact: CRITICAL
impactDescription: the #1 cause of flaky and slow suites
tags: waiting, flaky, anti-pattern
---

# Never Use waitForTimeout in Committed Tests

> **Impact: CRITICAL (the #1 cause of flaky and slow suites)**

`page.waitForTimeout()` waits a fixed duration regardless of actual page state — too short and it's flaky, too long and it wastes CI time. Every locator action and web-first assertion already auto-waits for the element to be actionable.

## Incorrect

```ts
await page.waitForTimeout(5000);
await page.getByRole("button", { name: "Submit" }).click();
```

## Correct

```ts
await page.getByRole("button", { name: "Submit" }).click(); // auto-waits until actionable
```

## Reference

- [Playwright Docs - waitForTimeout](https://playwright.dev/docs/api/class-page#page-wait-for-timeout)
