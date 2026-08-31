# Ideas — the "brief" family

Design notes, not a plan of record. Captured 2026-07-28 after a feedback
round on a real debrief packet raised the question: should there be a
forward-looking sibling? Nothing here is implemented.

> **Status addendum, 2026-07-30.** Three trajectory-independent items below
> have since been implemented: confidence labels promoted into the shared
> craft (`debrief` + `explain-change`), the staleness discipline added to
> `debrief`, and the decision-register convention written up in
> [references/decision-register.md](references/decision-register.md).
> Everything else — plan mode, the T2/T3 choice — remains deliberately
> unimplemented pending the settling signals at the bottom.
>
> **Second addendum, same day.** T2 is now implemented — forward-mode
> dispatch in SKILL.md plus [references/plan.md](references/plan.md) — on
> owner priority, ahead of the reviewer-cycle signal. The trigger-dilution
> question is therefore live and testable; T3 remains open.
>
> **Third addendum, 2026-07-31 — the first real circulation cycle happened,
> and it changed the craft rather than the architecture.** Two plan-mode
> packets were written for real reviewers, and the feedback was not about
> tense or structure. It was that **the packet had the wrong audience baked
> in**: "what this touches" pointers and a named person's workload are
> internal-draft content, and putting them in a document going to a
> supervisor is a defect. Implemented in `plan.md` as an explicit
> internal-versus-circulated flag with a strip rule, cross-referenced from
> SKILL.md so it binds in both tenses, plus a short handover subsection
> (circulated plan brief, reader is an implementer, ends in an executable
> checklist). Also added to shared craft: **typeset equations as MathML**,
> after a sign error in an ASCII-transcribed PDE survived several revisions
> of a packet and was caught only by re-deriving it — an equation printed as
> text reads as notation rather than as a claim.
>
> Two signals for the trajectory question, pulling in opposite directions.
> Toward T3/T6: the audience rule had to be written in `plan.md` and
> *referenced* from SKILL.md because it genuinely applies to both tenses,
> which is exactly the shared-craft duplication T6 exists to solve — the
> second such rule to land in the wrong file. Against urgency: no reviewer
> has yet responded against decision IDs, so the async multi-reviewer case
> is still unevidenced. Lean unchanged: stay at T2, but the next
> both-tenses craft rule should trigger the T6 extraction rather than
> another cross-reference.

## The idea in one paragraph

A brief is a self-contained understanding artifact about a body of work. It
has a tense. Backward-looking (today's debrief) serves understanding and is
gated by a quiz — the reader should be able to pass it before the next phase
is green-lit. Forward-looking (a "plan brief") serves alignment and is gated
by a decision register — every open decision carries an ID, a
recommendation, and a disposition, and nothing counts as agreed until a
disposition is recorded. Most of the craft is shared; only the ending and
the provenance discipline really differ.

## What actually differs between the tenses

Not cosmetic — three structural inversions:

| | backward (debrief) | forward (plan) |
|---|---|---|
| Reader's job | understand | decide |
| Ending | quiz (comprehension gate) | decision register (disposition gate) |
| Provenance rule | every number traces to a record | every number labelled measured / derived / assumed — the assumed ones are what to argue with |
| "Honest negatives" | what went wrong | falsifiers: the cheapest experiment that would kill each assumption, and its cost |
| Extra sections | — | off-ramps / kill criteria; ownership + sequencing |
| "Where it lives" pointers | paths, PRs, records | nothing exists yet → "what this touches" |

Everything else is shared: two-layer background, intuition-first, diagram
families, linked glossary, plain-words act openers, self-contained HTML,
inline citations with verified DOIs, re-verify-status-before-republishing,
placement and craft.

## Trajectories

Roughly in order of increasing churn. T1 is the honest baseline and several
of the others do not clearly beat it.

- **T1 — status quo.** Keep debrief; write plans inline or in plan mode.
  Costs nothing. Gives up the async multi-reviewer case, and leaves the
  decision-register discipline with no home in the skill layer.
- **T2 — additive mode inside debrief.** A short dispatch paragraph plus
  `references/plan.md`. Lowest risk, zero migration, preserves a description
  that demonstrably triggers well. Semantically awkward: "debrief" is the
  wrong word for a forward-looking document.
- **T3 — rename to `brief`, modes in `references/{debrief,plan}.md`.** Clean
  architecture; shared craft lives once; idiomatic progressive disclosure.
  Two costs: trigger dilution (one description spanning both tenses is
  vaguer, and descriptions are the selection mechanism — mitigable by making
  it purely additive and keeping the word "debrief" in it), and `brief` is a
  generic enough word to attract spurious firing, so the description has to
  work harder.
- **T4 — full family refactor.** `brief` with three modes: a single change /
  an arc retrospectively / an arc prospectively, folding in explain-change.
  The coherent end state. Churns a second working skill for less benefit
  than the debrief+plan merge.
- **T5 — separate `proposal` skill, craft duplicated with a "change both"
  marker.** Considered and disliked: ~70% overlap guarantees drift. A
  six-rule craft fix would have needed applying twice.
- **T6 — extract the shared craft into its own reusable unit** (a
  packet-craft skill, or one shared reference that all siblings point at).
  Solves drift without merging trigger surfaces — an orthogonal axis to
  T3/T4. Risk: cross-skill references break when only one skill is
  installed, and it adds a layer of indirection to every read.

## Ideas worth keeping regardless of trajectory

- **Decision register as a portable convention.** IDs, recommendations,
  turns-on clauses, dispositions; silence is not consent; `changed` as a
  first-class outcome so redirections stay visible. Already proven useful as
  a plain markdown page independent of any packet — arguably the highest
  value-per-effort item in this whole family, and the piece most obviously
  wanted across projects.
- **Confidence labels belong in both tenses.** A retrospective packet also
  carries derived numbers that read as measured. The rule should probably be
  promoted into the shared craft rather than living only in plan mode.
- **Falsifiers with costs** — likely the single most valuable plan-mode
  section, and the one most plans omit.
- **Reviewer-channel adapter.** Generate the decision sheet in whatever
  format the reviewer actually annotates (commented .docx, markdown table,
  issue list). Do not build an in-page comment widget with copy-paste
  export — senior reviewers will not perform the ritual.
- **Feedback ingestion pattern.** Returned comments become a dated source
  note anchored to decision IDs. The skill can only state the pattern; the
  destination is per-project.
- **Staleness discipline.** Don't restate a project's living tracker inside
  the artifact — point at it. Duplication is the staleness. Optional
  companion: a verified-date on the artifact plus a docs-CI warning when it
  predates the records it summarises.

## Open questions

- Does trigger reliability measurably degrade when one description spans
  both tenses? Directly testable — ship it and watch whether the skill fires
  when expected.
- Is the full packet worth building at all, or is the register ~80% of the
  value? Unknown until a real reviewer either responds against IDs or
  doesn't.
- Does explain-change fold in, or is "one change" a genuinely different job
  with a different reader?
- Where do cross-project conventions live so they aren't copy-pasted per
  project — in the skill, or in each project's own knowledge base?

## What would settle it

- A reviewer responds in writing, against decision IDs → the async case is
  real → build the packet, go T3.
- Plans keep getting settled in conversation → register-only; stay at T1/T2
  and stop.
- A second project needs the same forward-looking artifact → the
  shared-craft duplication problem multiplies, which strengthens T3/T6
  independently of whether any single reviewer engages in writing. This is
  the cheapest signal to check, because it needs no reviewer at all.

## Current lean

Register first (done, as a plain page in one project). T2 or nothing until
one real reviewer cycle has happened. T3 becomes a mechanical refactor once
plan-mode content is known rather than guessed — and the register already
contains the decision payload a plan brief would present, so the packet is
cheap to add later and expensive to guess at now.

---

## Addendum, 2026-08-02 — self-containment has two halves, and I only had one

The skill reasoned carefully about *network* dependency (that is why it mandates
MathML over a maths CDN) and then told you to build JS-drawn figures and a
JS-gated quiz without noticing those fail the same test. A packet shipped for
review came back with "saw the sliders but nothing else": the reader's viewer
rendered the HTML and silently refused the script, so five of six figures were
blank space and all five quiz answers were unreachable. The file was fine. The
assumption was not.

Two rules now in SKILL.md, both cheap:

1. **Pre-render everything at build time; let the script replace it.** The static
   snapshot is also the printable version, which the skill had been claiming
   without earning.
2. **Verify with `java_script_enabled=False` as well as True**, and require the
   figure counts to match. Two lines of playwright; it is the only way to see what
   a locked-down reader sees.

A third, smaller, from the same session: an interactive control's default must
agree with the static content beside it. A stepped slider snaps to its own grid,
so compute the pre-rendered state at the value the control actually lands on — or
the figure jumps on first touch and the neighbouring prose is briefly wrong.

**Worth generalising.** The failure was not "I forgot a fallback". It was assuming
the delivery environment resembled the authoring one. The audience rule already in
this skill says decide who reads it before drafting; this says decide *where* they
read it, and verify there.


---

## Addendum, 2026-08-31 — T6 fired (inside the skill), and audience became a dial

Two things happened in one session. The trivial one first, because it is the
better story: **the frontmatter had been unparseable since the forward-mode
edit.** `Debrief also has a forward-looking mode: when a plan…` — an unquoted
`: ` inside a plain scalar, which YAML reads as a nested mapping. GitHub
refused to render it (`line 2 column 771`); this harness's own loader is
lenient, so the skill kept working and nobody noticed for a month. Then, while
adding the audience clause to that same description, the same mistake was made
again within the hour (`in both tenses: 'write this up…'`).

Generalisable, and not really about YAML: **a description is the skill's only
selection mechanism and the one part no reader proofreads.** It needs a
mechanical gate, not care. `yaml.safe_load(open(f).read().split('---')[1])`
over every SKILL.md is a one-liner and belongs in whatever CI this repo grows.
Worth pushing up into `writing-skills` as a rule rather than living here.

### T6, as pre-registered

The 2026-07-31 addendum committed to a condition: *the next both-tenses craft
rule triggers the T6 extraction rather than another cross-reference.* Audience
is that rule, so it fired — but **inside `debrief`**, not as a separate craft
skill: [references/audience.md](references/audience.md), pointed at from both
SKILL.md and plan.md, with the audience section deleted from plan.md rather
than duplicated. This takes the de-duplication win while avoiding the risk the
original T6 carried (cross-skill references that break when only one skill is
installed). `explain-change` and `micro-world` still duplicate craft; when the
third consumer needs the same rule, that is the signal for the real extraction.

### What audience.md adds

- **Two orthogonal dials, not a list of document types.** `access`
  (internal/circulated) controls **stripping**; `altitude`
  (specialist/adjacent/non-specialist) controls **demoting**. Rules attach to
  dials, so an invented preset inherits correct behaviour. Five named presets
  are just coordinates.
- **Strip ≠ demote.** A dead pointer is deleted; a number the reader does not
  need is collapsed into `<details>` and keeps its trace to the record. That
  distinction is what lets one authored source serve every altitude.
- **The layers invert with altitude** rather than accumulating. At
  non-specialist the figure carries the argument, the prose supports it, one
  number per act survives in the main flow, and the glossary moves *before* the
  background — a reader who lacks the words cannot read the background that
  teaches them the words.
- **Hard word ceilings replace the reading-time target.** The old "~10 minutes"
  was measured against a real project's artifacts and had failed exactly where
  it mattered most: internal arc explainers 945–1254 main-flow words (fine), the
  document written for the broadest audience **3343** — 4× over, at the altitude
  with the least patience. (The first pass at this addendum quoted 5313, from a
  counter that swept in glossary, captions and collapsed blocks. Defining the
  ceiling and then measuring by a different rule is the obvious way to make a
  ceiling meaningless: the count rule ships beside the numbers.) Ceilings: 2000 / 1200 / 800, handover exempt. Plus a cut
  list, and the count as a ship gate beside the scripts-off check.
- **The ending follows the reader's job.** The quiz gates *the owner's*
  green-light of the next arc, so it has no function pointed at a supervisor or
  a client and reads as patronising there. Circulated non-specialist ends in
  takeaways + the ask + **what would change our mind**. The invariant: the
  internal version always carries the quiz, and the circulated one is derived
  by stripping it — authoring without one silently removes the speed regulator.

### Effect on the open questions

- **Trigger dilution is now doubly live**: one description spans two tenses
  *and* names audience presets (1123 → 1294 chars). Still directly testable by
  watching whether the skill fires when expected; no evidence of degradation
  yet, and it fired correctly on the session that wrote this.
- **T3 (rename to `brief`) is cheaper than it was.** With audience extracted,
  SKILL.md is closer to being just the backward mode, which is what T3 needs it
  to be. Lean unchanged: no rename until a reviewer actually responds against
  decision IDs.
- New question, from the same session that produced the ceilings: **is
  "outward brief" really debrief's job, or a sibling?** It shares the source
  document and the derivation mechanism, which argues it stays. But its
  ending, its ceiling and its voice all differ, and its reader never sees the
  quiz. Watch whether it accumulates rules of its own.
