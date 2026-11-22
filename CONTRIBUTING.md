# Contributing

Thank you for your interest in hejnas-tripod-sensor! Contributions of any size are welcome – bug reports, ideas, documentation and code.

The project follows a spec-driven workflow. The full rules live in [`AGENTS.md`](AGENTS.md) and in the skills in [`.agents/skills/`](.agents/skills/); this guide summarises them for human contributors.

## 1. Start with an issue

Every change starts from an issue. Open one from a [template](https://github.com/Hejnas/hejnas-tripod-sensor/issues/new/choose) – blank issues are disabled.

| Template | Title prefix | Use for |
|---|---|---|
| Spec | `spec/` | Large topic – requirements only, split into sub-issues |
| Enhancement | `feat/` | New product feature |
| Bug | `bug/` | Something does not work |
| Fix | `fix/` | Small correction |
| Documentation | `docs/` | Documentation and wiki |
| Chore | `chore/` | Repository, process and tooling |

For anything larger than a small fix, wait for the discussion in the issue before writing code.

## 2. Branch

Fork the repository and create a branch from `main`:

```
<prefix>/<issue number>-<short-description>
```

For example `fix/12-cadence-zero-on-coasting`. Do not base a branch on another unmerged branch.

## 3. Commits

Commit messages follow [Conventional Commits](https://www.conventionalcommits.org/) with a mandatory scope:

```
<type>(<scope>): <subject>
```

For example `feat(ble): add RSC service`. Types: `feat`, `fix`, `docs`, `chore`. Details: [`commit-writing`](.agents/skills/commit-writing/SKILL.md).

## 4. Pull request

- Open a pull request against `main`; the [template](.github/pull_request_template.md) is filled in automatically.
- Use the commit format for the title – it becomes the commit on `main`.
- Reference the issue with `Closes #<issue number>`.
- The maintainer reviews the pull request and squash-merges it.

## Working with an AI agent

If you use an AI coding agent (Claude Code, Gemini CLI or another), it reads [`AGENTS.md`](AGENTS.md) and follows the same workflow.

## License

By contributing, you agree that your contributions are licensed under the [MIT License](LICENSE).

## Code of Conduct

This project follows the [Code of Conduct](CODE_OF_CONDUCT.md). Security issues are reported privately – see [`SECURITY.md`](SECURITY.md).
