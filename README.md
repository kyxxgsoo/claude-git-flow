# claude-git-flow

A Claude Code plugin that ships one subagent, **`git-flow-manager`**. It carries out branch → commit → pull request → CI → merge → tag → release work, and it reads each repository's own rules first.

## What it does

- Reads `CLAUDE.md`, `AGENTS.md`, `CONTRIBUTING.md` and the PR template before acting, and follows them over its own defaults.
- Detects the branching model: Git Flow (`develop` exists) or trunk-based.
- Runs the repository's declared gates before merging (named scripts, or `lint`/`typecheck`/`test` when present) and judges them by exit code.
- Waits for CI in the foreground and merges only when every check is green.
- Never force-pushes, never stages files it was not given, and never touches uncommitted work it was not asked to commit.

## Install

```
/plugin marketplace add kyxxgsoo/claude-git-flow
/plugin install git-flow@kyxxgsoo-git-flow
```

Or from a shell:

```
claude plugin marketplace add kyxxgsoo/claude-git-flow
claude plugin install git-flow@kyxxgsoo-git-flow
```

Start a new session after installing. The agent is available as `git-flow:git-flow-manager`.

## Use

Ask Claude to hand git work to it, for example:

> Use the git-flow-manager agent: branch `feature/login` from main, commit only `src/auth.ts` and `test/auth.test.ts`, open a PR, wait for CI, merge when green.

A repository that defines its own `.claude/agents/git-flow-manager.md` keeps using that one. Project agents take precedence over plugin agents.

## Layout

```
.claude-plugin/marketplace.json        marketplace "kyxxgsoo-git-flow"
plugins/git-flow/.claude-plugin/plugin.json
plugins/git-flow/agents/git-flow-manager.md
```

## License

MIT
