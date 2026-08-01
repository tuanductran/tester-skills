---
title: Seed Only the Data Each Test Needs
impact: MEDIUM
impactDescription: keeps tests fast and their dependencies explicit
tags: db, fixtures, seeding
---

# Seed Only the Data Each Test Needs

> **Impact: MEDIUM (keeps tests fast and their dependencies explicit)**

Loading a large shared fixture file for every test hides what a specific test actually depends on and slows the suite. Create the minimal rows a test needs inline, using a factory helper.

## Incorrect

```ts
beforeEach(async () => {
  await loadFixtures("full-database-snapshot.sql");
}); // hundreds of rows, unclear what's used
```

## Correct

```ts
beforeEach(async () => {
  user = await createUser({ email: "test@example.com" }); // exactly what this test needs
});
```

## Reference

- [Object Mother Pattern](https://martinfowler.com/bliki/ObjectMother.html)
