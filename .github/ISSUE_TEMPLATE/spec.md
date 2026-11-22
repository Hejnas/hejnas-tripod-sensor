---
name: Spec
about: Large topic – requirements only, no code; split into sub-issues
title: "spec/"
labels: spec
---

<!--
  A spec describes WHAT and WHY, never HOW. No code, no implementation details.
  Subject of requirements: "The device", "The firmware" or "The repository".
  Mark every unknown with [NEEDS CLARIFICATION: question] instead of guessing.
  Delete these comments and any optional section you do not use.
-->

# Feature Specification: [NAME]

**Created**: [YYYY-MM-DD]

**Input**: [1–2 sentences: what this is and why it is needed]

## Requirements

<!-- Testable functional requirements, one capability each. -->

- **FR-001**: [Subject] MUST [capability]
- **FR-002**: [Subject] MUST [capability] [NEEDS CLARIFICATION: question]

## Non-functional Requirements *(optional)*

<!-- Constraints: battery life, size, weight, water resistance, temperature, cost, … -->

- **NFR-001**: [Subject] MUST [constraint with a value]

## Edge Cases

<!-- Boundary conditions and error situations that must be handled. -->

- [What happens when …?]

## Success Criteria

<!-- Measurable outcomes that prove the spec is fulfilled. -->

- **SC-001**: [Measurable outcome]

## Assumptions

<!-- Defaults chosen, scope boundaries (out of scope), dependencies. -->

- [Assumption]

## Sub-issues

<!--
  The original plan of sub-issues. Title format: <prefix>/<short description>. Prefixes: feat/, bug/, fix/, docs/, chore/.
  Entries are not changed later; each one is ticked when its sub-issue's work is verified.
-->

- [ ] [prefix]/[short description]
