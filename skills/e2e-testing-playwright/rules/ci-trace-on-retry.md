---
title: Capture Traces on Retry, Not on Every Run
impact: MEDIUM
impactDescription: gives debuggable artifacts without slowing every green run
tags: ci, trace, debugging
---

# Capture Traces on Retry, Not on Every Run

> **Impact: MEDIUM (gives debuggable artifacts without slowing every green run)**

Set `trace: 'on-first-retry'` so passing runs stay fast, but a flaky or failing test leaves a full trace (DOM snapshots, network, console) for triage — instead of an unreproducible red X.

## Incorrect

```ts
// playwright.config.ts
use: {
  trace: "off";
} // failures leave nothing to debug from
```

## Correct

```ts
// playwright.config.ts
use: {
  trace: "on-first-retry";
}
retries: process.env.CI ? 2 : 0;
```

## Reference

- [Playwright Trace Viewer](https://playwright.dev/docs/trace-viewer)
