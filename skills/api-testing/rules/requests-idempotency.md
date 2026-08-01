---
title: Verify Idempotency for PUT/DELETE Endpoints
impact: MEDIUM
impactDescription: catches state-corrupting retries before production
tags: requests, idempotency, put, delete
---

## Verify Idempotency for PUT/DELETE Endpoints

> **Impact: MEDIUM (catches state-corrupting retries before production)**

Clients and proxies retry failed requests. A PUT or DELETE that isn't idempotent can corrupt state on retry. Explicitly test that calling the same request twice produces the same end state as calling it once.

## Incorrect

```ts
it("updates the user", async () => {
  await request(app).put("/users/1").send({ name: "Ada" });
  // never checks what happens on a second identical call
});
```

## Correct

```ts
it("is idempotent when called twice with the same payload", async () => {
  await request(app).put("/users/1").send({ name: "Ada" });
  const second = await request(app).put("/users/1").send({ name: "Ada" });
  expect(second.status).toBe(200);
  expect((await request(app).get("/users/1")).body.name).toBe("Ada");
});
```

## Reference

- [REST API Idempotency](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent)
