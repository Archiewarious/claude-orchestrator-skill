# Orchestrator skill for Claude Code

This skill turns one Claude Code session into an HQ. You talk to it in plain words. It turns what
you say into agreed tasks, picks a model and effort level for each one, and hands them to separate
sub-sessions, each working in its own git worktree. When a sub-session finishes, HQ checks the
commit, the diff and the check output. The sub-session's own summary counts only as a claim.

## Why

Long conversations cost the most, because every turn resends the whole history. HQ keeps its
state in a file, and each sub-session gets one short task.

Most failures start with a badly specified task. HQ asks you only what you want, never how to build
it. Before it launches anything, it retells the plan with concrete examples ("if X, you'll see Y")
and waits for your go.

Splitting sequential work across agents usually makes the result worse. The skill keeps dependent
work in one session and runs in parallel only work on separate files, plus read-only research.

## Install

```
git clone https://github.com/Archiewarious/claude-orchestrator-skill
cp -r claude-orchestrator-skill/skills/orchestrator ~/.claude/skills/
cp claude-orchestrator-skill/project-config.example.md <your project>/.claude/orchestrator-config.md   # optional, then edit
```

Then say "orchestrator", "HQ" or "split this into sessions" in a Claude Code session.

## How it differs from plain subagents

| Plain subagents | This skill |
|---|---|
| Run inside your conversation and return a summary | Writing work goes to separate sessions in their own worktrees, each with its own commit |
| You decide how to split the work | HQ decides the split, model and effort, and tells you the cost before starting |
| The summary is the result | The result is the commit, the diff and the check output |
| Nothing is remembered between runs | An HQ file keeps the goals, your decisions word for word, task states and a calibration log |

## What it can't do

The skill is a set of instructions. Nothing enforces them, and a model can still skip a step.

Real sub-sessions need a tool that starts sessions. The Claude Code desktop app has one. Without
it, HQ can only write briefs, and you paste them into new sessions yourself.

The model and effort table is an example based on vendor benchmarks for specific model versions.
Calibrate it with the log the skill keeps.

It was built and used on one project, with one owner and one machine. The defaults (nesting depth,
at most 3 coding sessions at once, context thresholds) come from that setup. The Defaults section
in `SKILL.md` explains each one and how to change it.

It doesn't push or merge into your main branch without your word, and it doesn't publish anything.

## License

MIT. See [LICENSE](LICENSE).
