---
title: Generate Test Data Per-Test, Never Hardcode Shared IDs
impact: MEDIUM
impactDescription: makes tests parallel-safe and order-independent
tags: data, fixtures, factories
---

# Generate Test Data Per-Test, Never Hardcode Shared IDs

> **Impact: MEDIUM (makes tests parallel-safe and order-independent)**

Hardcoded IDs like `user-1` collide when tests run in parallel or in a different order. Use a factory function that generates unique data per test (e.g. via a random suffix or UUID).

## Incorrect

```ts
it("fetches the user", async () => {
  const res = await request(app).get("/users/user-1"); // collides with other tests
});
```

## Correct

```ts
async function createUser(overrides = {}) {
  return request(app)
    .post("/users")
    .send({ email: `${randomUUID()}@test.com`, ...overrides });
}
it("fetches the user", async () => {
  const created = await createUser();
  const res = await request(app).get(`/users/${created.body.id}`);
});
```

## Reference

- [Test Data Management Patterns](https://martinfowler.com/bliki/ObjectMother.html)
