# Full Workflow Demo Script

End-to-end run-through of the specs-driven development workflow: Jira ticket →
GitHub branch → spec → implementation → PR → review → close-out. Copy the
commands and paste-ins below, swapping in the real ticket key and spec number
each time you run the demo.

Placeholders used below:
- `<SPM-ID>` — the Jira ticket key, e.g. `SPM-102`
- `<NNN>` — next spec number, zero-padded, e.g. `002`
- `<slug>` — short kebab-case description, e.g. `date-in-greeting`

---

## 1. Jira — create the task

Fields to fill in:
- **Project**: SPM
- **Issue type**: Task
- **Summary**: short description of the feature (e.g. `Add current date to greeting output`)
- **Description**: what the feature does and the top-line acceptance check, e.g.
```
Extend the app.py demo program so it also prints today's date after the
greeting.

Acceptance: `python app.py` prints `Hello, World!` then `Today is YYYY-MM-DD.`
```

Note the ticket key (`<SPM-ID>`) — it's referenced in the spec, the commit, and the PR.

---

## 2. GitHub — branch from dev

```bash
git fetch origin dev
git checkout -b feature/<SPM-ID> origin/dev
git push -u origin feature/<SPM-ID>
```

(`dev` only needs to be created once, from `main`: `git checkout -b dev origin/main && git push -u origin dev`.)

---

## 3. Specs-driven workflow

**Create the spec folder + file** at `specs/<NNN>-<slug>/spec.md` before touching
code — this is the source of truth for what "done" means:

```bash
mkdir -p specs/<NNN>-<slug>
```

Spec template to paste into `specs/<NNN>-<slug>/spec.md`:

```markdown
# Spec <NNN>: <Feature Title>

Jira: <SPM-ID>

## Summary
One or two sentences on what the feature does.

## Motivation
Why this is being built now / how it fits the running demo.

## Requirements
- Concrete, testable statements of behavior (e.g. exact CLI output).
- No command-line arguments, external dependencies, or configuration are
  required unless stated.

## Acceptance Criteria
- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

## Out of Scope
- Explicitly excluded behavior, to prevent scope creep during review.
```

**Implement against the spec** — make the minimal code change that satisfies
the requirements exactly, nothing more.

**Verify against acceptance criteria** — run the program, confirm the output
matches the spec's stated format, then edit the spec file and check off each
box (`- [ ]` → `- [x]`).

---

## 4. Commit and push

```bash
git add specs/<NNN>-<slug>/spec.md <changed files>
git commit -m "<Short description> (spec <NNN>)

Jira: <SPM-ID>"
git push origin feature/<SPM-ID>
```

---

## 5. Open the PR

- **Base**: `dev`  **Head**: `feature/<SPM-ID>`
- **Title**: `<Short description> (spec <NNN>)`
- **Body** (fills the repo's PR template — `.github/pull_request_template.md`):
```markdown
## Description

<What the PR does and why, referencing the spec file.>

Jira: <SPM-ID>

## Checklist

- [x] Linked to spec document(s) (`specs/<NNN>-<slug>/spec.md`)
- [x] Acceptance criteria met (all checked in the spec)
- [ ] Tests added/updated (note if out of scope per spec)
- [ ] Docs updated (if applicable)
```

---

## 6. Review the PR

Open "Files changed", confirm the diff matches the spec's requirements and
acceptance criteria exactly — reviewers check the diff against the agreed
spec rather than re-litigating requirements. Leave a review comment, e.g.:
```
Reviewed against specs/<NNN>-<slug>/spec.md — diff is a minimal, direct
implementation of the requirement. All acceptance criteria checked and
verified locally. Looks good.
```
Note: GitHub won't let you *Approve* your own PR — use "Comment" if you're
both author and reviewer, or have someone else approve.

---

## 7. Close the PR

On the PR page, click **Close pull request** (not merge, if the demo is meant
to show the full lifecycle without landing the change).

---

## 8. Delete the branch

GitHub shows a "Delete branch" button on the closed PR page — click it.
(Or via CLI: `git push origin --delete feature/<SPM-ID>`, then
`git branch -d feature/<SPM-ID>` locally.)

---

## 9. Close the Jira task

Move `<SPM-ID>` to **Done**, referencing the PR URL as the record of work.

---

Each new feature gets its own numbered spec folder (`specs/<NNN>-<slug>/`) and
its own `feature/<SPM-ID>` branch — specs accumulate as a running log of what
the app does and why, and branch names stay traceable back to a Jira ticket.
