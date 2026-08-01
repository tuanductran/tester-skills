---
title: Set Explicit Budgets for Core Web Vitals
impact: HIGH
impactDescription: ties performance testing to user-perceived experience
tags: vitals, lcp, cls, inp
---

# Set Explicit Budgets for Core Web Vitals

> **Impact: HIGH (ties performance testing to user-perceived experience)**

Track Largest Contentful Paint, Cumulative Layout Shift, and Interaction to Next Paint against explicit numeric budgets (e.g. LCP < 2.5s) rather than a general 'feels slow' judgment. Budgets make regressions objectively testable.

## Incorrect

```js
// no defined budget — a PR that adds 200ms to LCP merges without any signal
```

## Correct

```js
// lighthouserc.js
module.exports = {
  ci: {
    assert: {
      assertions: {
        "largest-contentful-paint": ["error", { maxNumericValue: 2500 }],
        "cumulative-layout-shift": ["error", { maxNumericValue: 0.1 }],
      },
    },
  },
};
```

## Reference

- [web.dev - Core Web Vitals](https://web.dev/articles/vitals)
