---
name: commit-writing
description: Write a commit message in the project's Conventional Commits format and create the commit only on explicit approval. Use when changes are ready to be committed or the user asks for a commit.
---

# commit-writing

Commit messages follow [Conventional Commits](https://www.conventionalcommits.org/) with a mandatory scope.

## Format

```
<type>(<scope>): <subject>

<body – optional>

Co-Authored-By: <agent attribution line>
```

### Type – derived from the branch prefix

| Branch prefix | Commit type |
|---|---|
| `feat/` | `feat` |
| `bug/` | `fix` |
| `fix/` | `fix` |
| `docs/` | `docs` |
| `chore/` | `chore` |

### Scope – mandatory

- The area of the repository the change affects, e.g. `imu`, `ble`, `algo`, `power`, `logger` (firmware) or `agents`, `skills`, `templates`, `wiki`, `ci`, `docs` (repository and process).
- There is no fixed list. Before choosing a scope, check the existing ones with `git log --format=%s` and reuse a matching scope; create a new one only when none fits.

### Subject

- Imperative mood (`add`, not `added`), lowercase, no trailing period, at most 72 characters including type and scope.
- No issue number – the pull request links the issue, and squash merge appends the pull request number.

### Body – optional

- What changed and why, not how. Wrap at 72 characters.

### Co-Authored-By

- Keep the `Co-Authored-By` trailer of the agent that worked on the change.

## Steps

1. **Check the branch.** Never commit on `main`. Work happens on the issue branch (`<prefix>/<issue number>-<description>`).
2. **Review the changes** with `git status` and `git diff`. Stage only files that belong to this change; never stage git-ignored material such as `Wiki/Raw/`.
3. **Draft the message** according to the format above and show it to the user together with the list of files.
4. **Commit – only when the user explicitly asks for it.**
5. **Push – only when the user explicitly asks for it**, as a separate step.

## Squash merge

Pull requests are squash-merged: the pull request title becomes the commit subject on `main`. Branch commits should follow this format too, but the pull request title is the one that must be exact (see the `pr-writing` skill).

Everything is written in **English**.
