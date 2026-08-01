---
title: Test Unauthenticated and Unauthorized Access Explicitly
impact: MEDIUM
impactDescription: catches broken access control, a top-severity bug class
tags: auth, security, 401, 403
---

# Test Unauthenticated and Unauthorized Access Explicitly

> **Impact: MEDIUM (catches broken access control, a top-severity bug class)**

For every protected endpoint, assert both that a missing token returns 401 and that a valid token without sufficient permissions returns 403 — not just that a valid admin token returns 200.

## Incorrect

```ts
it("returns the admin dashboard", async () => {
  const res = await request(app).get("/admin").set("Authorization", adminToken);
  expect(res.status).toBe(200);
});
// no test for what happens without a token, or with a non-admin token
```

## Correct

```ts
it("returns 401 without a token", async () => {
  expect((await request(app).get("/admin")).status).toBe(401);
});
it("returns 403 for a non-admin user", async () => {
  const res = await request(app).get("/admin").set("Authorization", userToken);
  expect(res.status).toBe(403);
});
```

## Reference

- [OWASP API Security Top 10](https://owasp.org/www-project-api-security/)
