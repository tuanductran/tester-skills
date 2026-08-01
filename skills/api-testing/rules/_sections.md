# Sections

## 1. Contract & Schema Validation (contract)

**Impact:** HIGH **Description:** Verifying response shape, not just status codes, is what actually catches breaking API changes.

## 2. Request Construction (requests)

**Impact:** HIGH **Description:** How requests are built and run against the server determines test speed and realism.

## 3. Authentication & Authorization (auth)

**Impact:** MEDIUM **Description:** Auth bugs are high-severity; tests need to cover both authenticated and unauthorized paths deliberately.

## 4. Error & Edge Cases (errors)

**Impact:** MEDIUM **Description:** Most production API incidents come from unhandled error paths, not the happy path.

## 5. Test Data Management (data)

**Impact:** MEDIUM **Description:** Where test data comes from determines whether tests are reproducible and parallel-safe.
