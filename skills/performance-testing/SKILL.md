---
name: performance-testing
description: Performance testing guidelines covering backend load testing (k6) and frontend Core Web Vitals (Lighthouse CI). Use this skill whenever writing or reviewing a load test, setting performance budgets or thresholds, investigating a performance regression, or profiling a slow endpoint or page. Triggers on requests like "write a load test", "set up k6", "check Core Web Vitals", "why is this slow", or "add a performance budget to CI".
license: MIT
metadata:
  author: Tuan Duc Tran
  version: "1.0.0"
---

# Performance Testing

Guidelines for making performance testing objective and CI-gatable instead of a manual, occasional check. Contains 5 rules across 3 categories.

## When to Apply

Reference these guidelines when:

- Writing a k6 (or similar) load test for an API or service
- Setting performance budgets/thresholds that should fail CI when breached
- Investigating a reported performance regression
- Setting up Lighthouse CI for frontend Core Web Vitals

## Rule Categories by Priority

| Priority | Category                      | Impact | Prefix       |
| -------- | ----------------------------- | ------ | ------------ |
| 1        | Load Testing                  | HIGH   | `load-`      |
| 2        | Web Vitals & Frontend Budgets | HIGH   | `vitals-`    |
| 3        | Profiling & Diagnosis         | MEDIUM | `profiling-` |

## Quick Reference

### 1. Load Testing (HIGH)

- `load-k6-thresholds` - Define pass/fail thresholds in the script itself
- `load-ramping-vus` - Ramp virtual users gradually, don't spike

### 2. Web Vitals & Frontend Budgets (HIGH)

- `vitals-core-web-vitals-budget` - Explicit LCP/CLS/INP budgets
- `vitals-lighthouse-ci-gate` - Run Lighthouse CI on every PR

### 3. Profiling & Diagnosis (MEDIUM)

- `profiling-flame-graphs` - Profile before optimizing

## How to Use This Skill

1. Read `rules/_sections.md` for full category descriptions.
2. For a new load test, start from `load-k6-thresholds` so the test is CI-gatable from day one.
3. For frontend regressions, check budgets first (`vitals-core-web-vitals-budget`), then profile (`profiling-flame-graphs`) rather than guessing at a fix.

See `rules/_template.md` for the format used by every rule file.
