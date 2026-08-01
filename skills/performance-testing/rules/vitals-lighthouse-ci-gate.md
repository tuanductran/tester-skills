---
title: Run Lighthouse CI on Every Pull Request, Not Just Manually
impact: MEDIUM
impactDescription: catches regressions before merge instead of in production monitoring
tags: vitals, lighthouse, ci
---

# Run Lighthouse CI on Every Pull Request, Not Just Manually

> **Impact: MEDIUM (catches regressions before merge instead of in production monitoring)**

Manually running Lighthouse locally before a big release misses the day-to-day regressions that accumulate one PR at a time. Run Lighthouse CI as a required check against the budgets defined for the project.

## Incorrect

```yaml
# performance checked only occasionally, by hand, before major releases
```

## Correct

```yaml
# .github/workflows/lighthouse.yml
- name: Run Lighthouse CI
  run: |
    npm install -g @lhci/cli
    lhci autorun --config=lighthouserc.js
```

## Reference

- [Lighthouse CI](https://github.com/GoogleChrome/lighthouse-ci)
