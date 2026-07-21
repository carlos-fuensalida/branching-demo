# Spec 001: Hello World

## Summary
A minimal Python program that prints `Hello, World!` to standard output when executed.

## Motivation
First iteration of the specs-driven development demo: establish the folder structure
(`specs/<id>-<slug>/spec.md`) and branch naming convention (`claude/<slug>-<id>`) used
by subsequent iterations.

## Requirements
- A file named `app.py` at the repository root.
- Running `python app.py` prints `Hello, World!` followed by a newline.
- No command-line arguments, external dependencies, or configuration are required.

## Acceptance Criteria
- [ ] `python app.py` exits with status code 0.
- [ ] `python app.py` writes exactly `Hello, World!` to stdout.

## Out of Scope
- Tests, packaging, or CLI argument handling (may be addressed in a future spec).
