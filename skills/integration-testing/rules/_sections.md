# Sections

## 1. Test Boundary & Scope (scope)

**Impact:** HIGH **Description:** Knowing what an integration test should and shouldn't cover prevents both slow, brittle suites and false confidence.

## 2. Environment & Real Dependencies (env)

**Impact:** HIGH **Description:** Using real dependencies (via containers) instead of hand-written fakes is what makes integration tests catch real bugs.

## 3. Database State (db)

**Impact:** HIGH **Description:** How database state is managed between tests determines both correctness and speed of the suite.

## 4. Fixtures & Test Data (fixtures)

**Impact:** MEDIUM **Description:** Reusable, composable fixtures keep integration tests readable as the domain model grows.
