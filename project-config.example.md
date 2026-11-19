# Orchestrator — project config (example)

Copy to `<your project>/.claude/orchestrator-config.md` and fill in. Every field is optional:
anything left out falls back to the defaults in `SKILL.md`. Delete the lines you don't need.

## Worktrees

- Worktree root: `../myproject-wt/<name>`
- Create: `git worktree add -b wt/<name> ../myproject-wt/<name> origin/main`
  (or your own script, if new worktrees need extra setup: dependencies, local env files)
- Remove: `git worktree remove ../myproject-wt/<name> && git branch -d wt/<name>`
- Base branch: `main`

## Checks (ladder step 0) — each runs separately, with its own exit code

- `npm run typecheck`
- `npm run lint`
- `npm test`
- <data consistency check, if you have one>

## Before and after push

- Pre-push review (run once, by the collector): `<command or skill name>`
- Post-deploy check: `<command, skill name or URL to check>`
- Live / staging URL for end-to-end checks: `<url>`

## Off-limits paths (never writable in a brief)

- `<path owned by another team or person>`

## HQ file

- Location: `.claude/hq/<date>-<topic>.md`

## Your own skills and agents (leave empty if you don't have them)

- Brief-writing skill: `<name>`
- Read-only explore subagent: `Explore`
- Pre-change research subagent: `<name>`
- Plan subagent: `Plan`
- Skeptic / red-team reviewer subagent: `<name>`
- Deep research skill: `<name>`
- Council (multi-model) skill: `<name>`

## Overrides of defaults

- Max sessions writing code at once: 3
- Merge verified branches without asking: yes
- HQ handoff threshold: ~250k tokens; sub-session: ~400k
- Most expensive model tier: recommend only / allowed
- Nesting depth below HQ: 2

## Model table overrides

Replace the example tiers in §3 with your models and the effort levels you calibrated, e.g.:

| Task | Model | Effort |
|---|---|---|
| Small change with precise spec | <model> | medium |
