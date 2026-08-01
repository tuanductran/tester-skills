---
title: Ramp Virtual Users Gradually, Don't Spike From Zero
impact: HIGH
impactDescription: reveals the actual breaking point instead of just confirming a crash
tags: load, k6, ramping
---

# Ramp Virtual Users Gradually, Don't Spike From Zero

> **Impact: HIGH (reveals the actual breaking point instead of just confirming a crash)**

Jumping straight to peak concurrency tests connection-establishment behavior, not sustained capacity. Use staged ramp-up/steady-state/ramp-down so you can see where latency starts degrading, not just whether the system survives a spike.

## Incorrect

```ts
export const options = { vus: 500, duration: "1m" }; // instantly hits 500 users
```

## Correct

```ts
export const options = {
  stages: [
    { duration: "2m", target: 50 }, // ramp up
    { duration: "5m", target: 50 }, // sustained load
    { duration: "2m", target: 500 }, // ramp to peak
    { duration: "3m", target: 500 }, // sustained peak
    { duration: "2m", target: 0 }, // ramp down
  ],
};
```

## Reference

- [k6 Ramping VUs Executor](https://k6.io/docs/using-k6/scenarios/executors/ramping-vus/)
