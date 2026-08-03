# Forward mode — the plan brief

Read this together with SKILL.md: all shared craft applies unchanged —
two-layer background, intuition before details, diagram families,
plain-words openers, the zero-shared-vocabulary rule, linked glossary,
self-contained document, verified inline citations, staleness discipline.
What changes is the reader's job: not *understand what happened* but
*decide what should happen*.

## Three structural inversions

1. **The ending is a decision register, not a quiz.** Follow
   [decision-register.md](decision-register.md). The register is the
   disposition gate: every open decision carries an ID, a recommendation,
   and a "turns on" clause, and nothing counts as agreed until a
   disposition is recorded — silence is not consent. There is no quiz.
2. **Provenance becomes confidence.** Every number carries its
   measured / derived / **assumed** label (shared craft), but in a plan the
   assumed ones are the point: they are what the reviewer should argue
   with. Each load-bearing assumption maps to a register entry's "turns on"
   clause — an assumption no decision turns on is either not load-bearing
   or missing its decision.
3. **Honest negatives become falsifiers with costs.** For each load-bearing
   assumption: the cheapest experiment that would kill it, and what that
   experiment costs. This is the section most plans omit, and the one that
   makes a plan arguable rather than aspirational.

## Sections a plan brief adds

- **Off-ramps / kill criteria.** The conditions under which the plan should
  be abandoned or descoped, stated before work starts — they are
  near-impossible to state honestly afterwards.
- **Ownership and sequencing.** Who carries each piece, what depends on
  what, and the first concrete step.
- **"What this touches"** replaces "where it lives": nothing exists yet, so
  each act points at the systems, records, and people the work would touch.
  **Internal only** — see the audience rule below.

## Audience: internal draft vs circulated document

A plan brief has two audiences and they want different documents. Decide
which you are writing *before* drafting, and say so at the top, because two
sections are conditional on the answer.

**Internal draft** — for the author and whoever shares their knowledge base.
Keeps everything, including the pointers and the capacity judgements. This is
a working document.

**Circulated document** — a brief, proposal, or handover going to
collaborators, supervisors, or reviewers. Two things come out:

1. **Cut the "what this touches" pointers.** They name files, records, and
   internal IDs in one person's knowledge base. To everyone else they are
   dead links that imply a shared substrate the reader has no access to, and
   they push the reader's eye to plumbing instead of the argument. If an act
   genuinely depends on an external artifact the reader can open, cite it
   normally in the prose. (Same rule for the backward tense: "where it
   lives" is internal.)
2. **Never publish a named person's capacity as a claim about them.** "X's
   workload is the binding constraint" is a judgement about a colleague,
   written where they and their supervisor will both read it — and in a
   handover it is not even actionable. State the *scheduling* constraint
   instead ("this phase needs one person's undivided attention for ~3 weeks
   and cannot be parallelised"), and let the humans allocate. Ownership rows
   say what a person would *carry*, never how much they have left.

The two are one document with a flag, not two documents — write the internal
version, then strip. Deriving the circulated version from the internal one
keeps them from drifting; maintaining two drafts guarantees they do.

## Handovers

A handover is a circulated plan brief whose reader is an *implementer*, not a
decider. The inversions above all hold, plus:

- **Assume no knowledge-base access at all.** Every number, equation, and
  dataset the implementer needs is restated in the document. A handover that
  requires the author to be reachable has failed.
- **The register becomes a "decisions someone else must make" list.** The
  implementer must not silently resolve them; say which are theirs and which
  are not.
- **End in an executable checklist** with a pass condition per step, so
  "done" is checkable by the implementer rather than adjudicated by the
  author.

## The review loop

- **Meet the reviewer in their channel.** Generate the decision sheet in
  whatever format the reviewer actually annotates — commented .docx, a
  markdown table, an issue list. No in-page comment widgets with copy-paste
  export; senior reviewers will not perform the ritual.
- **Feedback ingestion:** returned comments become a dated source note
  anchored to decision IDs; dispositions update from it; `changed` is a
  first-class outcome and stays visible — redirections are never silently
  absorbed into the next draft.
- **The register outlives the packet.** After the first feedback round the
  register is the living tracker: republished packets point at it rather
  than restating it, and carry a verified-date.
