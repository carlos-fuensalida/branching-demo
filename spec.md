# Spec 002: Date in Greeting

Jira: SPM-102

## Summary
The greeting output includes the current date, so `python app.py` tells the reader
what day it is in addition to saying hello.

## Motivation
Second iteration of the specs-driven development demo: extend the existing
`Hello, World!` program (spec 001) with a small, well-scoped behavior change,
tracked end-to-end from a Jira ticket through branch, spec, implementation, and PR.

## Requirements
- Running `python app.py` prints:

Hello, World!
Today is YYYY-MM-DD

- The date is computed at run time via `datetime.date.today()` (system local date).
- No command-line arguments, external dependencies, or configuration are required.

## Acceptance Criteria
- [ ] `python app.py` exits with status code 0.
- [ ] `python app.py` writes `Hello, World!` on the first line.
- [ ] `python app.py` writes `Today is YYYY-MM-DD.` on the second line, matching
    `datetime.date.today()` formatted as ISO-8601 (`%Y-%m-%d`).

## Out of Scope
- Timezone handling (uses system local date only).
- Custom or configurable date formats.
- Internationalization/localization of the date string.
