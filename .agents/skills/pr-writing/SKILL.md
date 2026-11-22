---
name: pr-writing
description: Verify a finished branch against its spec and issue, then push it and open a draft pull request; also update an existing pull request after review. Use when the user asks to make, open or update a pull request.
---

# pr-writing

A pull request is opened when the work on an issue is finished. The agent verifies the branch first; only if everything is consistent does it push and open a **draft** pull request. The maintainer reviews it, marks it ready and squash-merges it.

## Template

The only source of the pull request structure is [`.github/pull_request_template.md`](../../../.github/pull_request_template.md). Fill it in; do not copy it into this skill.

## 1. Verify before opening the pull request

Read the current state of the work:

- the issue (number from the branch name `<prefix>/<issue number>-<description>`): body **and** all comments starting with `**Change:**` – the latest change comment is the binding state,
- the parent spec, if any (**Parent spec** in the issue), with its comments,
- the changes on the branch: `git log main..HEAD` and `git diff main...HEAD`.

Check:

1. **Consistency from the spec down.** The changes fulfil the issue's acceptance criteria (every issue type has them), stay within its scope and match **Approach**; the issue still fits the spec's requirements. Nothing has drifted apart.
2. **Wiki.** If the change affects knowledge about the device or the project, the wiki is updated and current. *Not applicable until the wiki process is defined.*
3. **Tests.** The change is covered by tests, or tests are not applicable (e.g. documentation-only changes).
4. **Form.** Branch name follows the convention; commit messages follow the `commit-writing` skill; no git-ignored material (e.g. `Wiki/Raw/`) is committed.
5. **Up to date with `main`.** Run `git fetch` and check that the branch contains the latest `origin/main` (`git merge-base --is-ancestor origin/main HEAD`). If it does not, merge it into the branch with `git merge origin/main` – no rebase, no force push – and repeat the verification. On a merge conflict, stop and ask the user.

**If anything does not match**, report the list of discrepancies and **stop** – no push, no pull request. Proposed corrections to an issue or spec are added as change comments – see "Changes after creation" in the `issue-writing` skill – only with the user's approval.

### Last sub-issue of a spec

The spec is closed only when **every item of the spec's Sub-issues list has a created sub-issue** and this pull request closes the last open one (check the list in the spec body against `gh issue view <spec number> --json subIssues` or the sub-issues panel). If any item of the list has no sub-issue yet, the spec stays open.

In that case:

- add `Closes #<spec number>` to the body, so the spec is closed automatically on merge,
- if the spec implements a ROADMAP stage, tick that stage in `ROADMAP.md` in this pull request.

## 2. Tick checkboxes, push and open a draft pull request

Only when the verification passes:

1. **Tick checkboxes** – checkboxes are meant to be ticked; this is an allowed edit of the body:
   - the acceptance criteria in the issue that the verification confirmed,
   - the issue's entry in the parent spec's **Sub-issues** list, if the issue belongs to a spec.

   Edit with `gh issue edit <number> --body-file -`, changing only the checkboxes.
2. **Push and open the pull request:**

```sh
git push -u origin <branch>
gh pr create --draft --base main --title "<type>(<scope>): <subject>" --label <issue label> --body-file - <<'EOF'
<filled-in template>
EOF
```

- **Title** – the same format as a commit subject (see `commit-writing`); with squash merge it becomes the commit on `main`. It must read as a changelog line.
- **Label** – copy the type label of the issue (`enhancement`, `bug`, `fix`, `documentation`, `chore`).
- **Body** – `Closes #<issue>`, summary, changes, parent spec, what was tested, checklist ticked according to the verification.

## 3. Update after review

When the user asks to update the pull request after review changes:

1. Repeat the full verification from step 1.
2. Push the new commits.
3. Update the pull request body so that it always describes the final state (`gh pr edit <number> --body-file -`).
4. Add a pull request comment describing what changed in this round.

Do not change the draft / ready status – the maintainer does that.

## Rules

- The maintainer merges; never merge, mark ready or close anything yourself.
- Everything is written in **English**.
