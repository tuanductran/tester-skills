---
title: Test Against an In-Process App Instance, Not a Running Server
impact: HIGH
impactDescription: removes network flakiness and speeds up the suite
tags: requests, supertest, isolation
---

# Test Against an In-Process App Instance, Not a Running Server

> **Impact: HIGH (removes network flakiness and speeds up the suite)**

Pass the Express/Fastify app instance directly to your HTTP testing library instead of starting a real server on a port and hitting it over the network. This avoids port conflicts, is faster, and removes an entire class of network-related flakiness.

## Incorrect

```ts
beforeAll(() => {
  server = app.listen(4000);
});
const res = await fetch("http://localhost:4000/users/1");
```

## Correct

```ts
import request from "supertest";
const res = await request(app).get("/users/1"); // no listening port needed
```

## Reference

- [Supertest](https://github.com/ladjs/supertest)
