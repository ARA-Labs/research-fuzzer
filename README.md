# research-fuzzer

Treat an open-ended investigation the way a greybox fuzzer treats a program:
after every action, answer the two questions a fuzzer always knows and an agent
never does — **did anything new happen**, and **where have I not been yet** —
and let the answers steer the next action.

The skill is a protocol, not a framework: one append-only notebook
(`fuzz-notebook.jsonl`), five hard rules, and a panel that reports coverage,
the queue of untried leads, unexplained crashes, and a going-in-circles alarm —
all computed from the agent's own footprints, no god's-eye view required.
Everything works in any domain (experiments, debugging, data analysis,
literature or market research) and with zero tooling; the bundled
`scripts/tally.py` (stdlib-only Python) is an optional convenience.

Read [`SKILL.md`](SKILL.md) — that file *is* the skill.

## Install

**Claude Code** — copy this directory into your skills folder:

```bash
# for one project
cp -r research-fuzzer /path/to/project/.claude/skills/
# or for all projects
cp -r research-fuzzer ~/.claude/skills/
```

Then invoke with `/research-fuzzer`, or let the agent load it automatically
when an investigation starts.

**Codex / Cursor / Gemini CLI / anything else** — add one line to your agent's
context file (`AGENTS.md`, `.cursorrules`, `GEMINI.md`, ...):

```
For any open-ended investigation, read research-fuzzer/SKILL.md and follow its
protocol: frame first, bet before every action, settle after, panel each batch,
gate before any conclusion.
```

**No tooling at all** — the protocol is executable by hand: keep the notebook
as a plain text file and compute the panel by counting. Every reading is a
count.

## The loop, in one breath

```
frame  → write the question, your candidate sub-questions, current beliefs
bet    → before each action: what you'll do, what you PREDICT, how confident
settle → after: confirmed (learned little) / surprised (write what belief
         changed) / anomaly (goes on the crash ledger)
         + always: what new leads did this open?
panel  → python scripts/tally.py   # coverage · queue · novelty · crashes · spread · gate
claim  → only through the gate: crashes resolved or carried as limitations,
         one kill-shot attempted, scope stated
```

## Files

```
SKILL.md                     the protocol (this is the skill)
scripts/tally.py             panel + protocol validation, stdlib only
examples/example-notebook.jsonl  a tiny worked notebook
```

## Provenance

Companion to *Agentic Auto-Research is Fuzz Testing*
([arXiv:2608.09855](https://arxiv.org/abs/2608.09855)), the essay
[*The Goal of Science Is Not to Win*](https://www.agenticresearch.sh/blog/the-goal-of-science-is-not-to-win),
and the [fuzz-testing-for-science](https://github.com/ARA-Labs/fuzz-testing-for-science)
demo. Built at [ARA Lab](https://www.agenticresearch.sh).

MIT.
