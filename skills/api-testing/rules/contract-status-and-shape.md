---
title: Assert Status Code AND Response Shape
impact: HIGH
impactDescription: catches both broken endpoints and silently changed payloads
tags: contract, status-code, shape
---

# Assert Status Code AND Response Shape

> **Impact: HIGH (catches both broken endpoints and silently changed payloads)**

A 200 status code doesn't guarantee the response body is correct. Always assert on the fields, types, and structure the caller depends on, not just the HTTP status.

## Incorrect

```ts
const res = await request(app).get("/users/1");
expect(res.status).toBe(200);
```

## Correct

```ts
const res = await request(app).get("/users/1");
expect(res.status).toBe(200);
expect(res.body).toMatchObject({
  id: 1,
  email: expect.stringMatching(/@/),
  createdAt: expect.any(String),
});
```

## Reference

- [Supertest](https://github.com/ladjs/supertest)
