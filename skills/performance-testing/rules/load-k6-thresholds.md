---
title: Define Pass/Fail Thresholds in the Load Test Itself
impact: HIGH
impactDescription: makes load tests CI-gatable instead of eyeballed
tags: load, k6, thresholds
---

# Define Pass/Fail Thresholds in the Load Test Itself

> **Impact: HIGH (makes load tests CI-gatable instead of eyeballed)**

A load test that only produces a report requires a human to interpret it. Define explicit `thresholds` (e.g. p95 latency, error rate) in the script so the test process exits non-zero and fails CI automatically when a budget is breached.

## Incorrect

```ts
// k6 script with no thresholds — output has to be read manually
export default function () {
  http.get("https://api.example.com/products");
}
```

## Correct

```ts
export const options = {
  thresholds: {
    http_req_duration: ["p(95)<300"], // 95% of requests under 300ms
    http_req_failed: ["rate<0.01"], // error rate under 1%
  },
};
export default function () {
  http.get("https://api.example.com/products");
}
```

## Reference

- [k6 Thresholds](https://k6.io/docs/using-k6/thresholds/)
