# AGENTS.md

Instructions for AI coding agents (Claude Code, Gemini CLI, Codex, Copilot and others) working in this repository.

## Purpose

This file is the **single source of truth** for how agents work in this project.
Tool-specific files (e.g. `CLAUDE.md`) only point here and must not contain rules of their own.
Reusable procedures live as skills (see [Skills](#skills)).

Project overview: [README.md](README.md). Stages and progress: [ROADMAP.md](ROADMAP.md).

## Workspace boundary

- Work **only inside the repository root** (the directory containing this file).
- Do not read, list, search or write anything outside it: no home directory (`~`), no absolute paths outside the repository, no parent directories (`..`), no system-wide locations.
- `Wiki/Raw/` is local, git-ignored reference material (datasheets, a clone of the Seeed wiki). It is inside the repository and may be read, but must never be committed.
- GitHub of this repository may be used through `gh` as part of the workflow. Any other web access only when the user explicitly asks for it.

## No agent-private memory

- Do not store anything in agent- or session-private memory (e.g. Claude Code auto memory, Gemini memory files).
- All persistent project knowledge lives in files in this repository.

## Language

- Talk to the user in the language the user writes in.
- Everything written to the repository is in **English**: documentation, code, comments, commit messages, command names and skill names.

## Skills

- Skills follow the [Agent Skills](https://agentskills.io) standard: `.agents/skills/<skill-name>/SKILL.md` with YAML frontmatter (`name`, `description`).
- `.agents/skills/` is read natively by Gemini CLI and other tools; `.claude/skills` is a symlink to it for Claude Code.
- Agents without skill support should read the relevant `SKILL.md` as plain instructions.

Available skills:

- `spec-writing` – write or revise a spec issue (label `spec`).
- `issue-writing` – write, create or revise any other issue (enhancement, bug, fix, documentation, chore), including sub-issues of a spec.
- `commit-writing` – write a commit message (Conventional Commits with scope) and commit only on explicit approval.
- `pr-writing` – verify a finished branch against its spec and issue, push it and open a draft pull request; update it after review.

## Workflow

Every change goes through: **issue → branch → commits → pull request → squash merge**.
Each step starts only on an explicit command from the user; the commands are given in quotes.

1. **Issue** – a large topic gets a spec (`spec-writing`), everything else an issue (`issue-writing`). Each ROADMAP stage is implemented as a spec.
2. **Brainstorm** – discuss the issue with the user: reasons, risks, alternatives, open questions. No files are changed.
3. **"write plan"** – write the plan into the **Approach** section of the issue (`issue-writing`).
4. **"code"** – sync the local repository, create the branch and implement the accepted plan:

   1. **Update `main`:**

      ```sh
      git switch main
      git pull --ff-only
      git fetch --prune
      ```

      Uncommitted changes are carried over by `git switch`. If git refuses to switch or `git pull --ff-only` fails, stop and ask the user – never stash, reset or discard anything.
   2. **Delete merged local branches** – for every local branch other than `main`, run `git branch -D <branch>` only if `gh pr view <branch> --json state --jq .state` returns `MERGED`. Other branches are kept.
   3. **Create the branch from `main`:**

      ```sh
      gh issue develop <issue number> --name <prefix>/<issue number>-<slug> --checkout
      ```

      `<slug>` is the issue title without the prefix, spaces replaced by hyphens, e.g. `chore/7-agent-instructions`. Never base a branch on another unmerged branch; if the work depends on an unmerged pull request, wait for its merge or combine the work into one pull request.
5. **Commit** – `commit-writing`; never commit on `main`; commit only when the user explicitly asks.
6. **"make PR"** – `pr-writing`: verify the branch, push it and open a draft pull request.
7. **Merge** – the maintainer marks the pull request ready and squash-merges it. The issue is closed automatically; a spec is closed automatically by the pull request of its last sub-issue.

Never commit or push unless the user explicitly asks for it ("make PR" includes the push).
