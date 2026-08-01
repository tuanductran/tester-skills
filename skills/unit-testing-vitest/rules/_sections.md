# Sections

This file defines all sections, their ordering, impact levels, and descriptions. The section ID (in parentheses) is the filename prefix used to group rules.

---

## 1. Test Structure & Naming (structure)

**Impact:** HIGH **Description:** How tests are organized and named determines whether a failure tells you what broke. Poor structure is the #1 cause of unmaintainable suites.

## 2. Assertions (assert)

**Impact:** HIGH **Description:** Precise, behavior-focused assertions catch real regressions and give actionable failure messages; vague assertions hide bugs.

## 3. Mocking & Test Doubles (mock)

**Impact:** HIGH **Description:** Vitest's `vi` object makes mocking easy to misuse. Correct mocking keeps tests fast and isolated without hiding real integration bugs.

## 4. Async & Timers (async)

**Impact:** HIGH **Description:** Most flaky or silently-passing unit tests trace back to un-awaited promises or unmocked timers.

## 5. Coverage & CI (coverage)

**Impact:** MEDIUM **Description:** Coverage numbers are only useful when they gate real risk and don't create a false sense of safety.

## 6. Performance & Isolation (perf)

**Impact:** MEDIUM **Description:** Test suites that stay fast and isolated get run more often, which is the real driver of bug-catching value.
