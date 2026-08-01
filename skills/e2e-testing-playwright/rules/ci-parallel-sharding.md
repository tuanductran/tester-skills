---
title: Run Tests in Parallel With Sharding in CI
impact: MEDIUM
impactDescription: cuts CI wall-clock time proportionally to shard count
tags: ci, parallel, sharding
---

# Run Tests in Parallel With Sharding in CI

> **Impact: MEDIUM (cuts CI wall-clock time proportionally to shard count)**

Playwright workers already parallelize within a machine; use `--shard` to split the suite across multiple CI machines for large suites, keeping each shard's worker isolation intact.

## Incorrect

```ts
// single job runs the entire suite serially in CI
npx playwright test
```

## Correct

```ts
// .github/workflows split into 4 parallel jobs
npx playwright test --shard=${{ matrix.shard }}/4
```

## Reference

- [Playwright CI Guide](https://playwright.dev/docs/test-sharding)
