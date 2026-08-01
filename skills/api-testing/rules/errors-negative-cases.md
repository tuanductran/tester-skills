---
title: Write Negative Test Cases for Every Endpoint
impact: MEDIUM
impactDescription: covers the paths most incidents actually come from
tags: errors, negative-testing, edge-cases
---

## Write Negative Test Cases for Every Endpoint

> **Impact: MEDIUM (covers the paths most incidents actually come from)**

For each endpoint, deliberately test malformed input, missing required fields, wrong types, and boundary values — not only the happy path with valid data.

## Incorrect

```ts
it("creates an order", async () => {
  const res = await request(app).post("/orders").send({ qty: 2, price: 10 });
  expect(res.status).toBe(201);
});
```

## Correct

```ts
it("creates an order", async () => {
  const res = await request(app).post("/orders").send({ qty: 2, price: 10 });
  expect(res.status).toBe(201);
});
it("rejects a negative quantity", async () => {
  const res = await request(app).post("/orders").send({ qty: -1, price: 10 });
  expect(res.status).toBe(400);
});
it("rejects a missing price field", async () => {
  const res = await request(app).post("/orders").send({ qty: 2 });
  expect(res.status).toBe(400);
});
```

## Reference

- [OWASP API Security Top 10](https://owasp.org/www-project-api-security/)
