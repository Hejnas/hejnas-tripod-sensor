---
name: issue-writing
description: Write, create or revise a non-spec GitHub issue – enhancement, bug, fix, documentation or chore – including sub-issues of a spec. Use when the user reports a problem, asks for a feature or task, or a sub-issue of a spec needs to be created.
---

# issue-writing

Every change starts from an issue. This skill covers all issue types except `spec` (see the `spec-writing` skill).

## Issue types

This table is the single source of issue types, title prefixes and labels.

| Type | Template | Title prefix | Label | Used for |
|---|---|---|---|---|
| Enhancement | [`enhancement.md`](../../../.github/ISSUE_TEMPLATE/enhancement.md) | `feat/` | `enhancement` | New product feature |
| Bug | [`bug.md`](../../../.github/ISSUE_TEMPLATE/bug.md) | `bug/` | `bug` | Something does not work |
| Fix | [`fix.md`](../../../.github/ISSUE_TEMPLATE/fix.md) | `fix/` | `fix` | Small correction, no analysis needed |
| Documentation | [`documentation.md`](../../../.github/ISSUE_TEMPLATE/documentation.md) | `docs/` | `documentation` | Documentation and wiki |
| Chore | [`chore.md`](../../../.github/ISSUE_TEMPLATE/chore.md) | `chore/` | `chore` | Repository, process and tooling |

The templates in `.github/ISSUE_TEMPLATE/` are the only source of the issue structure. Use the template body (without the front matter) and follow the HTML comments in it. Do not copy templates into this skill.

## Steps

1. **Gather input.** Ask the user what is needed and why. Ask about anything unclear instead of guessing.
2. **Choose the type** from the table above. A large enhancement should belong to a spec – suggest a spec if there is none.
3. **Draft the issue** by filling in the template. Leave **Approach** as `[TBD – filled in at the plan stage]`.
4. **Show the draft** to the user and revise it until the user accepts it.
5. **Create the issue – only when the user explicitly asks for it:**

   ```sh
   gh issue create --title "<prefix>/<short description>" --label <label> --body-file - <<'EOF'
   <issue body>
   EOF
   ```

   For a sub-issue of a spec add `--parent <spec number>` and set **Parent spec** in the body. Do not edit the spec's **Sub-issues** list now; its entry is ticked when the sub-issue's work is verified (see the `pr-writing` skill).

## Approach – the plan lives in the issue

- **Approach** is filled in only after the brainstorm, when the user asks for the plan.
- The first fill replaces `[TBD …]` in the body with `gh issue edit <number> --body-file -`, keeping the rest of the body unchanged.
- Code is written only after the plan in **Approach** is accepted.

## Changes after creation – comments, not edits

This section is the single source of the change-comment rule for all issues, including specs.

The body of an issue or spec is the original agreement and stays unchanged. There are two exceptions: the first fill of **Approach**, and ticking checkboxes (acceptance criteria, the spec's **Sub-issues** list) when the work is verified – see the `pr-writing` skill. Every later change of scope, requirements, acceptance criteria or approach is added as a comment, only with the user's approval:

```
**Change:** <what changes>
**Reason:** <why>
```

The latest change comment is the binding state.

## Rules

- **Title**: `<prefix>/<short description>` – lowercase, a few words, no trailing period. The description becomes part of the branch name, e.g. `chore/7-agent-instructions`.
- **Changing the type**: if an issue turns out to be of another type (e.g. a fix that needs analysis), do not open a new issue. Change the label and the title prefix of the same issue; if a branch already exists, rename it to the new prefix.
- Everything is written in **English**.
