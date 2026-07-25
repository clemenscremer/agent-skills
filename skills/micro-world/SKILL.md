---
name: micro-world
description: Build a small, self-contained interactive page that lets a human understand code or results by playing with them — a parameter playground, an execution timeline scrubber, or a side-by-side behavior comparison — always on real project data. Use when behavior is easier to inhabit than to read about — calibration or threshold trade-offs, state machines, parsers/interpreters, dynamic or emergent behavior — or when the user says "I can't picture this", "show me how this actually behaves", "let me play with it", "build me a playground / visual debugger". Single-use teaching UIs are cheap now; understanding is not.
license: MIT
---

# Micro-world

After Seymour Papert: you learn French best in France, and a system best
inside a small world that runs it. Agents can now afford to write throwaway
code whose only job is to teach a human how *other* code behaves. The best
micro-worlds let the human **rediscover the finding themselves** rather than
being told it.

**Provenance:** Geoffrey Litt's micro-world / ephemeral-teaching-UI practice
("understanding is the new bottleneck"), hardened on a research project; the
`debrief` skill embeds a compact version of these rules for arc-close use.

## Pick the world's shape

Match the shape to the question being asked:

- **Parameter playground** — the question is "how does the result depend on
  X?" One control (slider, scrubber) tied to the single quantity under
  discussion; everything visible recomputes in response.
- **Execution scrubber** — the question is "what does this code actually do
  as it runs?" Instrument the *real* code to record an execution trace, dump
  it as JSON, inline it; then a timeline slider steps through the trace
  showing the state that matters at each step (stack, bindings, queue,
  canvas). Let the human attach inline annotations to steps (localStorage or
  an export button) so they can log their thinking while exploring — those
  notes are debugging gold.
- **Comparison world** — the question is "how do old and new behavior
  differ?" Run the same inputs through both versions, display side by side,
  one input selector.

If the question doesn't fit any shape, reconsider whether a micro-world is
the right artifact — a well-written explainer section may serve better.

## Hard requirements

- **Real project data**, inlined or precomputed. A toy with fake data teaches
  the wrong lesson with confidence. Downsample real data rather than invent
  it; if live computation is too heavy for the browser, precompute a curve or
  trace over the control's range and interpolate.
- **One control, one lesson.** A micro-world answers one question. If a
  second control is tempting, that's a second micro-world (or a preset
  button). Never build a dashboard.
- **Annotate the discovery path**: a "what to notice" box with 2–3 numbered
  observations, plus preset buttons for the states that matter — but place
  them so the human can explore *first* and confirm second. Write labels and
  annotations for a reader with zero shared vocabulary: expand abbreviations
  at first use, introduce symbols before using them.
- **Verify headlessly before delivering** (e.g. playwright): page renders,
  controls work, zero console errors — and check the world's own claims
  against what it displays. It may teach *you* that your annotation was
  wrong; fix the annotation and say so.
- **Self-contained single HTML file**, no external dependencies, so it
  survives offline and can be shared as one attachment.

## Placement

Ephemeral by default: `YYYY-MM-DD-microworld-<slug>.html` outside version
control. Promote into the project's docs (e.g. `docs/explainers/`, indexed
from the front door) only when it captures something of lasting value — a
negative result, a calibration decision the team will revisit.
