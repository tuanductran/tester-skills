---
title: Gate CI on Coverage Thresholds, Not Just Pass/Fail
impact: MEDIUM
impactDescription: prevents silent coverage regressions
tags: coverage, ci, v8
---

# Gate CI on Coverage Thresholds, Not Just Pass/Fail

> **Impact: MEDIUM (prevents silent coverage regressions)**

Configure the v8 (or istanbul) provider with explicit thresholds per metric so a PR that adds untested code fails CI, instead of relying on someone noticing a coverage report.

## Incorrect

```ts
// vitest.config.ts
export default defineConfig({
  test: { coverage: { provider: "v8" } }, // reports but never fails the build
});
```

## Correct

```ts
// vitest.config.ts
export default defineConfig({
  test: {
    coverage: {
      provider: "v8",
      reporter: ["text", "html", "json-summary"],
      thresholds: { lines: 80, functions: 80, branches: 70, statements: 80 },
    },
  },
});
```

## Reference

- [Vitest Coverage Guide](https://vitest.dev/guide/coverage.html)
