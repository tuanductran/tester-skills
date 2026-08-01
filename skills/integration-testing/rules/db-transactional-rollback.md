---
title: Wrap Each Test in a Transaction and Roll Back
impact: HIGH
impactDescription: keeps the suite fast without a full DB reset per test
tags: db, transactions, rollback
---

# Wrap Each Test in a Transaction and Roll Back

> **Impact: HIGH (keeps the suite fast without a full DB reset per test)**

Instead of truncating and reseeding tables between every test (slow), open a transaction before each test and roll it back after. This gives every test a clean, isolated state at near-zero cost.

## Incorrect

```ts
afterEach(async () => {
  await db.query("TRUNCATE users, orders CASCADE"); // reseeds from scratch every test
});
```

## Correct

```ts
beforeEach(async () => {
  await db.query("BEGIN");
});
afterEach(async () => {
  await db.query("ROLLBACK");
}); // instantly undoes all writes
```

## Reference

- [Database Testing Patterns](https://www.postgresql.org/docs/current/tutorial-transactions.html)
