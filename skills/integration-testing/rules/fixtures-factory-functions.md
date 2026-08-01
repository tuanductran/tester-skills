---
title: Build Test Data With Factory Functions, Not Copy-Pasted Objects
impact: MEDIUM
impactDescription: makes fixtures easy to extend and evolve with the schema
tags: fixtures, factories, maintainability
---

# Build Test Data With Factory Functions, Not Copy-Pasted Objects

> **Impact: MEDIUM (makes fixtures easy to extend and evolve with the schema)**

A factory function with sensible defaults and override support means adding a new required field only requires updating the factory once, instead of every test file that hardcodes a full object literal.

## Incorrect

```ts
const user1 = {
  id: 1,
  email: "a@test.com",
  name: "A",
  role: "user",
  createdAt: new Date(),
};
const user2 = {
  id: 2,
  email: "b@test.com",
  name: "B",
  role: "admin",
  createdAt: new Date(),
};
// repeated with slight variations across dozens of test files
```

## Correct

```ts
function buildUser(overrides: Partial<User> = {}): User {
  return {
    id: randomUUID(),
    email: "test@example.com",
    name: "Test User",
    role: "user",
    createdAt: new Date(),
    ...overrides,
  };
}
const admin = buildUser({ role: "admin" });
```

## Reference

- [Object Mother Pattern](https://martinfowler.com/bliki/ObjectMother.html)
