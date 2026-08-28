# 00 — Architecture

Three layers. The point of the split is that a writing practice contains
two very different kinds of work, and most tools confuse them.

**Layer 1 — Directive.** Markdown SOPs (this folder). Goal, inputs, the
step to run, expected output, known failure modes. Written the way you
would brief a capable colleague. Everything requiring judgment lives here,
in prose, where you can read it and argue with it.

**Layer 2 — Orchestration.** The model. It reads the directive, works
through it in order, asks when the directive is ambiguous, and updates the
directive when it learns something. It does not invent process.

**Layer 3 — Execution.** Deterministic operations: fetching sources,
deduplicating, rendering, writing to the log. Anything with one correct
answer.

## Why a writing system is mostly Layer 1

This repository is deliberately light on code. That is the finding, not an
omission.

Deciding whether a topic is worth 1,200 words, whether a paragraph sounds
like you, whether a claim is safe to make — none of that has a correct
answer a function could return. Pushing it into code produces confident
wrong answers. Leaving it in prose keeps it inspectable and arguable.

What belongs in Layer 3 for a writing practice is narrow: pulling feeds,
deduping against what you have already covered, appending to the log. If
you find yourself writing a script that decides something, it belongs in a
directive instead.

## The self-annealing loop

When a run goes wrong:

1. Fix the immediate problem
2. **Write what you learned back into the directive** — the constraint you
   hit, the failure mode, the thing you assumed wrongly
3. The next run does not repeat it

A correction that lives only in a chat transcript is lost. A correction
written into the directive is permanent. This is the only mechanism in the
system that makes it better over time.
