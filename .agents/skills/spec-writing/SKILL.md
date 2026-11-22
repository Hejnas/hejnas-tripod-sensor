---
name: spec-writing
description: Write or revise a spec – a GitHub issue labelled `spec` that describes a large topic (a device feature or a repository/workflow topic) as requirements only, with no code, split into sub-issues. Use when the user asks for a spec or a large topic needs to be planned.
---

# spec-writing

A spec is a GitHub issue with the label `spec`. It describes **what** is needed and **why**, never **how**. It contains no code. The work is done in its sub-issues.

The structure is based on the GitHub Spec Kit `spec-template.md`, without user stories (this project designs a device), with optional non-functional requirements and a list of sub-issues.

## Template

The only source of the template is [`.github/ISSUE_TEMPLATE/spec.md`](../../../.github/ISSUE_TEMPLATE/spec.md). Use its body (without the front matter) and follow the HTML comments in it. Do not copy the template into this skill.

## Steps

1. **Gather input.** Ask the user for the topic and its purpose. Ask about anything unclear instead of guessing.
2. **Draft the spec** by filling in the template.
3. **Show the draft** to the user and revise it until the user accepts it.
4. **Create the issue – only when the user explicitly asks for it:**

   ```sh
   gh issue create --title "spec/<short description>" --label spec --body-file - <<'EOF'
   <spec body>
   EOF
   ```

5. **Create sub-issues** one at a time, when the work on them starts, using the `issue-writing` skill. The **Sub-issues** list in the spec stays as the original plan; progress is shown in the native sub-issues panel.

## After creation

- The spec body stays unchanged; changes are added as comments – see "Changes after creation" in the `issue-writing` skill.
- The spec is closed automatically by the pull request of its last sub-issue (see the `pr-writing` skill).

## Rules

- **What and why, not how.** No implementation details, no code, no file or library names unless they are an external requirement (e.g. a BLE profile required for watch compatibility).
- **Subject** of requirements: "The device", "The firmware" or "The repository".
- **Requirements** are testable, one capability each, written with **MUST**, numbered `FR-001`, `FR-002`, …
- **Non-functional requirements** (`NFR-001`, …) only when relevant – typically for the device: battery life, size, weight, water resistance, temperature, cost.
- **Success criteria** are measurable, numbered `SC-001`, …
- **Unknowns** are marked `[NEEDS CLARIFICATION: question]` – never guessed.
- **Out of scope** items go to **Assumptions**.
- Remove the template comments and unused optional sections.
- Everything is written in **English**.

## Sub-issue prefixes and labels

See the "Issue types" table in the `issue-writing` skill.
