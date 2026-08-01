---
title: Use Fake Timers Instead of Real Delays
impact: HIGH
impactDescription: makes timer-dependent tests fast and deterministic
tags: async, timers, vi.useFakeTimers
---

# Use Fake Timers Instead of Real Delays

> **Impact: HIGH (makes timer-dependent tests fast and deterministic)**

Never let a test actually wait out a `setTimeout` or `setInterval`. Use `vi.useFakeTimers()` and advance time explicitly with `vi.advanceTimersByTime()` so the test is both instant and deterministic.

## Incorrect

```ts
it("shows a toast after 3 seconds", async () => {
  showToast("Saved");
  await new Promise((r) => setTimeout(r, 3000)); // real 3s wait
  expect(document.querySelector(".toast")).toBeTruthy();
});
```

## Correct

```ts
it("shows a toast after 3 seconds", () => {
  vi.useFakeTimers();
  showToast("Saved");
  vi.advanceTimersByTime(3000);
  expect(document.querySelector(".toast")).toBeTruthy();
  vi.useRealTimers();
});
```

## Reference

- [Vitest Mocking Guide - Timers](https://vitest.dev/guide/mocking.html#timers)
