---
name: explain-change
description: Produce a rich, self-contained explainer for a single substantive change — a diff, branch, commit range, or PR, but also any other reviewable revision (a config, a document, a model setup) — with layered background, intuition-first narrative, a literate walkthrough in execution order, and an interactive check-your-understanding quiz. Use when the user asks to have a change explained ("explain this PR/diff/refactor", "walk me through what you just did", "what changed here?"), or proactively before asking the human to approve or merge a substantive agent-written change. For a whole arc of work spanning many changes or sessions, use the debrief skill instead; for behavior easier to play with than to read about, use the micro-world skill.
license: MIT
---

# Explain Change

A raw diff is ordered for machines: alphabetical files, interleaved hunks, no
why. This skill replaces it with a document a human can actually learn from —
so they can *participate* in the next decision about this work, not just
thumbs-up the current one.

**Provenance:** adapted from Geoffrey Litt's `explain-diff` practice
("understanding is the new bottleneck"), sharing craft rules with the sibling
`debrief` skill.

## Scope first

Pin down exactly which change is being explained: working-tree diff, a branch
against its base, a commit range, a PR — or a non-code revision such as an
edited document, configuration, or model setup; the same structure applies.
Then **explore the surrounding material liberally** — the change never
contains its own context, and the explainer's job is mostly to supply what
the diff leaves out.

## The explainer

One document, fixed structure, in this order:

1. **Background, two layers.** First a deep background for a reader new to
   this part of the system — label it as skippable for those already
   familiar. Then the narrow background: the specific pre-existing behavior
   this change touches, and why it was the way it was. Never assume the
   reader watched the change happen.
2. **Intuition before details.** The core trick or essence of the change in
   plain language, with a concrete toy example (small, real-shaped data)
   before any real code. Use figures liberally: pick one or two **diagram
   families** and reuse them throughout — e.g. a simplified sketch of the UI
   the user sees, or a system/dataflow diagram *with example data flowing
   through it*. Build diagrams in HTML/SVG, never ASCII art.
3. **Literate walkthrough.** Present the change in execution or conceptual
   order — never file-tree or alphabetical order. Group related hunks into
   one step. Before each code block, one or two paragraphs of prose
   explaining *why* this piece exists and how it fits the flow; the code then
   confirms what the prose promised.
4. **Honest edges.** What the change deliberately does not handle, known
   weaknesses, follow-ups it creates. An explainer that sells the change
   teaches the reader to distrust the next one.
5. **Quiz, interactive.** Exactly five multiple-choice questions of medium
   difficulty — hard enough that you must have understood the substance of
   the change to answer, but no gotchas or trivia. Clicking an option reveals
   correct/incorrect plus a one-line explanation and a pointer to the section
   that covers it. State the house rule in the document: **the quiz is a
   speed regulator** — the change isn't approved or merged until the reader
   passes.

Budget: ~10 minutes reading time for a typical PR. A change too large for
that should be explained in acts, not in a longer wall of text.

## Format

- **One self-contained HTML file**: inline CSS and JS, no external
  dependencies, table of contents, one long scrollable page (no top-level
  tabs), basic responsive styling so it reads on a phone.
- **Ephemeral by default.** Name it `YYYY-MM-DD-explanation-<slug>.html` and
  put it *outside* version control (a scratch or temp directory) — per-change
  explainers are high-volume and would rot in the repo. Only promote one to
  the project's docs if the team decides it should be kept; then it follows
  the project's docs conventions and CI.
- Write with the clarity and flow of Martin Kleppmann — engaging, classic
  style, smooth transitions between sections. Use callouts for key concepts,
  definitions, and important edge cases.
- Code blocks use `<pre>` tags; any custom-styled block must set
  `white-space: pre` or `pre-wrap`. Before delivering, scan every code block
  in the source and confirm this, and if a headless browser is available,
  open the file once: page renders, quiz interactions work, zero console
  errors.
- Every claim and number must trace to the diff or the repo. An explainer is
  a *view* of the change, never a second source of truth — and never spin.
