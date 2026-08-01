---
title: Validate Responses Against a Schema, Not Ad-Hoc Field Checks
impact: HIGH
impactDescription: catches structural drift across the whole endpoint, not just fields you thought to check
tags: contract, schema, zod, openapi
---

# Validate Responses Against a Schema, Not Ad-Hoc Field Checks

> **Impact: HIGH (catches structural drift across the whole endpoint, not just fields you thought to check)**

Ad-hoc field-by-field assertions miss extra/missing fields you didn't think to check. Validate the full response against a JSON Schema, Zod schema, or the OpenAPI spec so any structural drift fails the test.

## Incorrect

```ts
expect(res.body.id).toBeDefined();
expect(res.body.name).toBeDefined();
// an unexpected extra `internalNotes` field would pass silently
```

## Correct

```ts
const UserSchema = z
  .object({
    id: z.number(),
    name: z.string(),
    email: z.string().email(),
  })
  .strict(); // .strict() rejects unexpected extra fields

expect(() => UserSchema.parse(res.body)).not.toThrow();
```

## Reference

- [Zod](https://zod.dev)
