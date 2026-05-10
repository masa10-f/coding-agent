---
name: unit-test-review
description: Use this skill when reviewing unit tests, test changes, bug fix tests, or implementation work that should include targeted unit tests. It helps agents identify fragile, misleading, low-value, or missing tests without demanding exhaustive coverage.
version: 1.0.0
---

# Unit Test Review Skill

## Overview

This skill guides unit test review for personal projects. It focuses on tests that are likely to waste developer time because they are fragile, misleading, nondeterministic, overly coupled to implementation details, or missing high-value regression coverage.

**When this skill applies:**
- Reviewing unit tests
- Reviewing test changes in a pull request or local diff
- Checking whether a bug fix includes a useful regression test
- Adding or revising tests for implementation work

## Review Policy

1. Prioritize correctness and regression risk over style.
2. Prefer behavior-based tests over implementation-detail tests.
3. Prefer small, deterministic, isolated tests.
4. Do not demand exhaustive coverage.
5. Suggest only high-value additional tests.

## How to Use

When reviewing tests:

1. Inspect the test files, the related production code, and the change context.
2. Select the relevant checks from `checks/` instead of loading every check file by default.
3. Report only issues that affect reliability, correctness, maintainability, or debugging speed.
4. Do not comment on trivial style unless it affects test reliability or readability.
5. If test coverage is incomplete but the missing behavior is low risk, do not request more tests.

## Output Format

Use this exact structure:

```markdown
Summary: Good / Acceptable / Risky

High-priority issues:
- [file:line] issue, why it matters, suggested fix

Missing high-value tests:
- behavior to test, suggested test case

Low-priority notes:
- optional improvements only
```

Omit bullets under a section when there are no findings, but keep the section headings.

## Current Checks

| ID | Check | Category |
|----|-------|----------|
| UT-001 | Specific test names | Naming |
| UT-002 | Arrange-Act-Assert structure | Readability |
| UT-003 | One behavior per test | Scope |
| UT-004 | Meaningful assertions | Assertions |
| UT-005 | Explicit expected values | Assertions |
| UT-006 | Relevant edge cases | Coverage |
| UT-007 | Regression tests for bug fixes | Coverage |
| UT-008 | Isolated external boundaries | Isolation |
| UT-009 | Deterministic tests | Reliability |
| UT-010 | Mocks only at external boundaries | Mocking |
| UT-011 | Readable fixtures | Fixtures |
| UT-012 | Meaningful test data | Test Data |
| UT-013 | Numerical test precision | Numerical Code |
| UT-014 | Fast unit tests | Performance |
| UT-015 | Actionable failure output | Debugging |

## Check Files

All unit test review checks are stored in:
- `checks/UT-001-specific-test-names.md`
- `checks/UT-002-arrange-act-assert.md`
- `checks/UT-003-one-behavior-per-test.md`
- `checks/UT-004-meaningful-assertions.md`
- `checks/UT-005-explicit-expected-values.md`
- `checks/UT-006-relevant-edge-cases.md`
- `checks/UT-007-regression-tests.md`
- `checks/UT-008-isolated-external-boundaries.md`
- `checks/UT-009-deterministic-tests.md`
- `checks/UT-010-mocks-at-boundaries.md`
- `checks/UT-011-readable-fixtures.md`
- `checks/UT-012-meaningful-test-data.md`
- `checks/UT-013-numerical-test-precision.md`
- `checks/UT-014-fast-unit-tests.md`
- `checks/UT-015-actionable-failure-output.md`
