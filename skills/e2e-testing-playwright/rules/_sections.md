# Sections

## 1. Locator Strategy (locators)

**Impact:** CRITICAL **Description:** The locator strategy determines whether a suite survives UI refactors or breaks on every markup change.

## 2. Waiting & Assertions (waiting)

**Impact:** CRITICAL **Description:** Fixed waits are the single largest source of flakiness and wasted CI time in E2E suites.

## 3. Test Isolation & Data (isolation)

**Impact:** HIGH **Description:** Tests that depend on order or shared state fail unpredictably and block unrelated PRs.

## 4. Page Object Model & Structure (pom)

**Impact:** MEDIUM **Description:** Structure determines how much a suite costs to maintain as the UI grows.

## 5. CI & Reliability (ci)

**Impact:** MEDIUM **Description:** How the suite runs in CI determines whether failures are trustworthy and fast to triage.
