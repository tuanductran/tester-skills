---
title: Profile With Flame Graphs Before Optimizing
impact: MEDIUM
impactDescription: directs optimization effort at the actual bottleneck
tags: profiling, flame-graph, cpu
---

# Profile With Flame Graphs Before Optimizing

> **Impact: MEDIUM (directs optimization effort at the actual bottleneck)**

Don't guess which function is slow. Capture a CPU profile under representative load and read the flame graph to find where time is actually spent before changing any code.

## Incorrect

```ts
// optimizing a function because it "seems" like it could be slow, with no profile data
```

## Correct

```ts
node --prof server.js
// generate load, then:
node --prof-process isolate-*.log > profile.txt
// or use 0x for a flame graph: npx 0x server.js
```

## Reference

- [Node.js Profiling Guide](https://nodejs.org/en/docs/guides/simple-profiling)
