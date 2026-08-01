---
title: Assert Errors Return a Consistent, Documented Shape
impact: LOW
impactDescription: lets clients handle errors programmatically instead of parsing messages
tags: errors, error-format, consistency
---

# Assert Errors Return a Consistent, Documented Shape

> **Impact: LOW (lets clients handle errors programmatically instead of parsing messages)**

Error responses should follow one consistent structure (e.g. `{ error: { code, message } }`) across all endpoints. Test that failures return this shape, not just a 4xx/5xx status, so client error handling can rely on it.

## Incorrect

```ts
it("rejects invalid input", async () => {
  const res = await request(app).post("/orders").send({});
  expect(res.status).toBe(400); // shape of res.body never checked
});
```

## Correct

```ts
it("rejects invalid input with a structured error", async () => {
  const res = await request(app).post("/orders").send({});
  expect(res.status).toBe(400);
  expect(res.body).toMatchObject({
    error: { code: "VALIDATION_ERROR", message: expect.any(String) },
  });
});
```

## Reference

- [JSON:API Error Objects](https://jsonapi.org/format/#errors)
