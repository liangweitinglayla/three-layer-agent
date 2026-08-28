# An AI Writing System

A working method for running a writing practice with AI agents — built
around the parts of writing a machine should never touch.

Most AI writing tools optimise for producing text. This one is built on the
opposite premise: **text is the cheap part.** What a working writer
actually needs help with is everything around the drafting — knowing what
happened this week, deciding what is worth writing, checking that a number
is right, catching when a draft has stopped sounding like them, and knowing
whether any of it landed.

The drafting itself stays with the writer. A system that publishes its own
output produces text nobody stands behind, and that is the one thing
writing cannot afford.

---

## The three layers

**Layer 1 — Directive** (`directives/`). Markdown SOPs. Goal, inputs, the
step to run, expected output, known failure modes. Everything that requires
judgment lives here, in prose you can read and argue with.

**Layer 2 — Orchestration.** The model, reading the directives and working
through them. It asks when a directive is ambiguous and writes back what it
learns. It does not invent process.

**Layer 3 — Execution.** Deterministic operations only: fetching feeds,
deduplicating, rendering, appending to the log. Anything with exactly one
correct answer.

### Why this repository is mostly prose

That is the finding, not an omission.

Whether a topic deserves 1,200 words, whether a paragraph still sounds like
you, whether a claim is safe to make — none of those have a correct answer
a function could return. Pushed into code they become confident wrong
answers. Left in prose they stay inspectable, and you can disagree with
them.

For a writing practice, the genuinely deterministic surface is small:
pulling sources, deduping against what you have already covered, appending
to a log. If you are writing a script that *decides* something, it belongs
in a directive instead.

---

## The pipeline

| Directive | What it does |
|---|---|
| [`00_architecture`](directives/00_architecture.md) | The three layers, and the loop that makes the system improve |
| [`01_topic_monitoring`](directives/01_topic_monitoring.md) | Watchlist streams → weekly digest → candidate pieces. **Stops and asks** which to write |
| [`02_drafting`](directives/02_drafting.md) | Chosen topic + style guide + sources → draft. The draft is raw material, never the published text |
| [`03_editorial_review`](directives/03_editorial_review.md) | Three passes: facts, voice, guardrails |
| [`04_repurposing`](directives/04_repurposing.md) | One piece → 3–5 short-form items, each making one claim |
| [`05_tracking`](directives/05_tracking.md) | Outcome metrics, not vanity metrics |

Templates for the three state files the system reads and writes are in
[`templates/`](templates/): the style guide, the topic watchlist, and the
tracking log.

---

## Four decisions worth stealing

**The style guide is the load-bearing file.** Directive 02 reads it before
drafting; directive 03 checks against it. It records how the writer
actually sounds — including the constructions a copy editor would remove.
For a writer working in a second language it says so explicitly, and says
the slightly raw register is the voice and must not be polished out.
Everything else in the system degrades gracefully. This file does not.

**Fact-checking assumes the specific way numbers go wrong.** Directive 03
names currency and unit errors first, because a figure remembered in one
currency and published in another is wrong by an order of magnitude and
ends your credibility on contact. It also prefers sources with an
adversarial interest in the claim — a figure conceded by a hostile party is
worth more than one asserted by a friendly one.

**The watchlist is the steering wheel.** Streams are switched `on` or `off`
in a markdown file. Turning one off is the entire interface for changing
what the system pays attention to. No configuration, no code.

**Reduced-capacity mode is built in.** Real practices have periods —
illness, exams, a crisis — when the normal cadence is simply wrong. The
tracking log carries an explicit mode with an end date and reduced targets,
so the writer is graded against what is actually possible instead of
failing against numbers that no longer apply. A system that manufactures
urgency to look useful is worse than no system.

---

## Using it

1. Fill in `templates/style_guide.md` with how you actually write. This is
   the work; do not rush it.
2. Fill in `templates/topic_watchlist.md` with your subjects.
3. Copy `templates/kpi_log.json` and name the one outcome you want.
4. Point an agent at `directives/` and start with `01_topic_monitoring`.

There is nothing to install. The directives are the system.

---

## Adapting it

The pattern generalises past writing: separate the judgment into readable
prose, keep only the deterministic operations in code, and write every
correction back into the directive so it survives. The domain changes; the
split does not.

MIT licensed — see [`LICENSE`](LICENSE).
