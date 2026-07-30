---
name: debrief
description: Produce understanding artifacts at the close of a substantive work arc — a background-first explainer packet ending in a check-your-understanding quiz, and (when a result is easier to inhabit than to read) an interactive micro-world built on real project data. Use this whenever a multi-session or multi-PR push wraps up, before asking the human to green-light a next phase, or when they say things like 'where do we stand', 'catch me up', 'summarize what we did', 'explain what you built', 'I've lost the plot', or ask how to keep up with agent-written work — even if they don't ask for a document explicitly. For a single diff, commit, or PR, use the explain-change skill instead — debrief covers arcs, not changes. The goal is understanding to participate, not just to verify.
license: MIT
---

# Debrief

Agents produce work faster than humans build understanding of it. This skill
closes that gap at the moments it matters: the end of an arc, before the next
decision. It produces **understanding artifacts** — not status reports.

**Provenance:** distilled from Geoffrey Litt's "understand to participate"
talk (the `/explain-diff` practice, quiz-as-speed-regulator after Matuschak &
Nielsen, micro-worlds after Seymour Papert), hardened by use on a research
project where the human named "keeping up with what we accomplished" as the
bottleneck. Siblings: `explain-change` (single change), `micro-world`
(standalone interactive teaching UI).

## When to fire

- A substantive arc closes: a multi-PR push, a multi-session investigation, a
  training-run-plus-evaluation cycle. Not per commit — per *story*. (A single
  change is `explain-change`'s job.)
- The human signals lost context ("where do we stand?", "catch me up", "I've
  lost the plot").
- Before asking the human to approve the *next* phase: they should be able to
  pass the previous phase's quiz first.

## Artifact 1 — the explainer packet (always)

One self-contained document (no external dependencies, so it survives
offline and can be printed). Choose the format deliberately: **markdown**
when the packet lives in the repo's docs and must pass docs CI; **HTML**
when interactive figures or the interactive quiz earn their keep. Fixed
structure, in this order:

1. **Background first, two layers.** What existed before this arc, in terms
   a returning teammate needs: a deep background for a reader new to this
   part of the project (labelled as skippable), then the narrow background
   directly relevant to the arc. Never assume they watched the work happen.
2. **Intuition before details.** State the goal of the arc and the *why*
   before any implementation. Open each act with a one-line **plain-words
   summary** — what happened and why it mattered, in language that assumes
   nothing — then the highlighted intuition box, then the detail. Use
   figures liberally: pick one or two **diagram families** and reuse them
   across acts — e.g. a simplified sketch of what the user sees, or a
   system/dataflow diagram with example data flowing through it. HTML/SVG
   diagrams, never ASCII art. Two rules on *what* to draw:
   - **If a named metric or mechanism cannot be pictured from the prose,
     draw it.** Abstract quantities need a figure more than architecture
     does — a reader nods past "reach-averaged anomaly error" and never
     notices they did not follow it. One orientation figure early, defining
     the regions or objects the rest of the vocabulary names, repays itself
     across every later act.
   - **Nothing may exist only in a caption.** Anything a figure names carries
     the identical name in the body text and gets at least one sentence of
     definition there. Names drifting between figure, prose and the
     underlying record is the commonest way a packet quietly stops cohering.
3. **Literate walk, narrative order.** Present the work as acts of a story
   (what was tried → what was found → what that forced next), not
   chronological minutiae or files-in-alphabetical-order. Include the load-
   bearing numbers inline, and a "where it lives" pointer (paths, records,
   PRs) after each act.
4. **Honest negatives get equal billing.** Failed acceptance criteria,
   reversed assumptions, and bugs found are often the most valuable content.
   Never smooth them into a success narrative.
5. **End with the quiz** (below) and a short "what's genuinely open" list.

One language rule binds the whole packet: **assume zero shared vocabulary.**
Write out every abbreviation and acronym at first use, with a one-line gloss
of what the thing *is* — the expansion alone rarely helps. Introduce every
symbol before its first use: what it measures, its units, a typical value.
General domain terms can be taught in the skippable deep background, but
project-coined names and shorthand must be defined in the main flow — even a
domain expert cannot know those. If more than a handful of terms recur,
collect them in a small glossary callout right after the background — and make
it **bidirectional**: anchor-link every in-text occurrence back to its entry so
the reader never scrolls hunting for a definition. Check that the links resolve
in both directions; orphaned anchors are worse than no anchors.

Budget: ~10 minutes reading time. If the arc needs more, split into acts, not
into a longer document.

## Artifact 2 — the quiz (always, inside the packet)

~5 questions of medium difficulty — hard enough that the reader must have
understood the substance of the arc, but no gotchas or trivia. Rules:

- In HTML packets, make it **interactive multiple-choice**: clicking an
  option reveals correct/incorrect plus a one-line explanation. In markdown
  packets, use collapsed answers (`<details>`).
- Target the **load-bearing concepts and the surprises** — the things that
  change what the reader would decide next. Never quiz trivia.
- Prefer "why" over "what": *why is X the correct baseline?*, *why must Y not
  be corrected away?*
- Each answer links or points to where the full treatment lives.
- State the house rule in the packet: **the quiz is a speed regulator** — the
  next arc shouldn't be green-lit until the human can pass the previous
  arc's quiz. The agent loop must not outrun human understanding.

## Artifact 3 — the micro-world (on demand)

When a result is easier to *inhabit* than to read — a calibration trade-off,
a threshold choice, a dynamic behavior — build a small interactive page the
human can play with. If the `micro-world` skill is installed, use it (it
carries the full pattern menu: parameter playgrounds, execution scrubbers,
comparison worlds). The compact core rules:

- **Real project data**, inlined or precomputed. A toy with fake data teaches
  the wrong lesson with confidence. If live computation is too heavy for the
  browser, precompute a curve over the control's range and interpolate.
- **One control, one lesson.** A slider or scrubber tied to the single
  quantity under discussion; everything visible recomputes in response. The
  best micro-worlds let the human *rediscover* the finding themselves.
- **Annotate the discovery path**: a "what to notice" box with 2–3 numbered
  observations, plus preset buttons for the states that matter.
- **Verify headlessly before delivering** (e.g. playwright): page renders,
  interactions work, zero console errors — and check the artifact's own
  claims against what it displays (it may teach *you* your annotation was
  wrong; fix the annotation, and say so).

## Placement and craft

- Keep artifacts in a stable, linked location in the project (e.g.
  `docs/explainers/`), indexed from wherever the project's front door is —
  an artifact nobody can find does not exist.
- **Write for the team, not just for whoever ran the session.** A debrief is
  a shared artifact: put it where teammates can read and comment, and use
  the project's shared vocabulary (or establish it) rather than session
  shorthand.
- Match the project's visual identity if one exists; otherwise stay plain.
- Every number in an artifact must trace to a source in the repo (results
  file, experiment record, PR). An explainer is a *view* of the record, never
  a second source of truth. Label each number **measured / derived /
  assumed** — derived numbers read as measured unless marked, and an
  *assumed* number in a retrospective packet is itself a finding: say why it
  had to be assumed.
- **Cite external work inline at first mention** — author, year, title, DOI —
  not only in a trailing reference list, so the reader meets the provenance
  where the claim is made. And **verify each DOI against the publisher record
  rather than recalling it**: a plausible-looking wrong DOI in a shared
  artifact is worse than no citation. If a DOI cannot be verified, omit it
  rather than guess.
- **List humans as participants; the agent is not one.** A debrief is a team
  artifact, not a session log. Attribute decisions to whoever made them, and
  credit the contributions you describe — a reader should never find their own
  catch reported anonymously beside a problem they are being shown.
- **Re-verify status claims before republishing.** "Still blocked", "awaiting
  approval", "not yet filed", "X hasn't arrived yet" age faster than anything
  else in a packet, and are exactly what a reader acts on. Re-check them
  against the world on every regeneration, and re-read the whole file before
  republishing — an artifact that still describes work you have since finished
  will contradict itself in front of the person you wrote it for. The
  cheapest defence: don't restate what a living tracker (backlog, issue
  board, decision register) already tracks — **point at it**. Duplication is
  the staleness.
- If the project has a lint/CI for docs, the artifacts must pass it.
