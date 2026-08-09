---
name: teach-me
description: Build durable, usable knowledge of a topic the learner names — knowledge aimed at a decision they have to make or a position they have to defend, with their actual gaps found and closed rather than assumed. Use when the user says 'teach me X', 'I want to be properly versed in X', 'bring me up to speed on X', 'grill me on X', 'give me a proper introduction to X', or asks an orienting question about a field they are visibly about to start working in. Also use to resume a topic from an earlier session — a learner model persists between sessions and is re-tested on return. Not for explaining this project's own code or work: that is explain-change for one change, debrief for an arc. Not for a one-off factual question the user wants answered and closed.
license: MIT
---

# Teach Me

A topic explained is not a topic learned. The default failure of an agent
asked to teach is a fluent essay: the learner nods through it, feels
informed, and a week later cannot use any of it — and neither party finds
out, because nothing was ever measured. This skill replaces the essay with a
loop that has a destination and a feedback signal.

The signal is fragile. Everything below exists to protect it from the two
things that destroy it: **teaching before the learner has committed to
anything**, and **grading an answer more generously than it deserves**.

**Provenance:** backward design for scoping, the pretesting and impasse
results for the cycle order, expertise reversal for the assistance dial,
diagnostic-question design for the probes — plus a dozen prior skills and
shipped tutors, adapted from and argued against. [PRIOR-ART.md](PRIOR-ART.md)
records what was taken from where, what was rejected, and how far each piece
of evidence actually reaches. Sibling to `explain-change`, `debrief` and
`micro-world` — those teach *this project's* work; teach-me teaches a body of
knowledge that exists outside it.

## Standing rules

These govern every turn, not just the next one. This file is loaded once and
the harness does not re-read it, so the loop decays by inattention while the
text is still present. When you notice the symptoms — probes drifting easier,
praise creeping in, the model going un-updated — re-read
[references/probes.md](references/probes.md), and re-invoke this skill after
a compaction to restore it in full.

1. **Answer direct questions directly.** Withholding an explanation from
   someone who asked for one is obstruction, not teaching. Probing happens
   *around* explanations, never instead of them.
2. **Write the answer key before you send the probe.** Into the learner
   model's `## Next` block: the answer you expect, plus the two or three
   elements that separate real understanding from a plausible-sounding reply
   — a boundary condition, a unit, a sign, a limiting case. Grade against
   what you wrote, not against how the answer reads. Skip this and you will
   grade the answer you were hoping for; LLM graders measurably over-score
   short, confident, underdeveloped answers, which is exactly the reply a
   busy professional sends.
3. **Do not fold under pushback.** When the learner disputes a verdict,
   re-derive from the key you wrote before you saw their answer and report
   whether it changed — do not re-answer the question. A source they cite is
   not evidence until you have read it; citation rebuttals are the measured
   trigger for the largest share of reversals from correct to incorrect, and
   a reversal, once made, usually sticks. Tell the learner plainly that
   verdicts are disputable and that disputes get re-derived. This rule
   reduces a bias trained into the model; it does not remove it, which is
   itself a reason to keep the key durable and auditable.
4. **One probe per message.** A stack lets the learner answer the easy one
   and skip the one that would have exposed the gap.
5. **Never ask "does that make sense?"** Yes/no under social pressure toward
   yes; both answers carry zero information. Ask something whose answer would
   differ depending on whether it landed.
6. **Compute, never recall.** Any arithmetic, unit conversion, cost formula
   or scaling exponent gets executed, not remembered. For content generally:
   correct is worth +1, omitted 0, **wrong −3**. Teach only what clears that
   bar; otherwise say you would have to look it up, and look it up.
7. **Grade the reasoning, not the conclusion**, and say what is wrong
   plainly. "Close!" on a wrong answer teaches the misconception and costs
   the learner their calibration. When an answer is right, say so once —
   praise every turn stops carrying information.
8. **Write the learner model at the end of every cycle.** Most sessions end
   by interruption. If a write is refused, stop and say so rather than
   continuing untracked.

## When to fire

- The learner names a topic they want to hold, not just get an answer about.
- They ask an orienting question about a field they are clearly about to work
  in — offer the loop rather than answering once and stopping.
- A learner model exists for this topic and they return to it.

**Do not fire** for a one-off factual question they want answered and closed,
for explaining work that lives in this repo (`explain-change` / `debrief`),
or when they are mid-task and need the answer to keep moving. Teaching
someone who asked for an answer is the tutor's version of scope creep. If
unsure, answer first, then offer in one sentence: *"that's the short answer —
want to actually own this?"*

## Phase 0 — Route

Silently, before anything is written: does a learner model exist for this
topic (`Glob docs/learning/teach-me-*.md`, and check auto-memory for a
pointer)? → resume. Is this a one-off question mid-task? → answer, offer,
stop. Otherwise → Phase 1. Never narrate the routing.

## Phase 1 — Converge before you teach

**The interview is about the destination, never about the learner's level.**
That distinction separates a useful scoping phase from an entrance exam.
Asking a competent adult to account for what they know before you have given
them anything is the fastest way to lose them, and it is unnecessary: level
is inferred in Phase 2 and from *how* they answer these questions.

For many topics this phase is substantively required, not merely polite: in
global sensitivity analysis the literature itself holds the question ill-posed
until the purpose is named.

**Reconnoitre the learner's own record first, then the field.** Before
offering any destination, look for what they have already written on this
topic — issues, notes, plans, prior artifacts, the project's own pages. That
record usually *contains* the destination, at a specificity no interview will
reach; spend no question on anything it answers. What it does **not**
reliably tell you is what the learner holds — see Phase 2. A menu built only from the field's own taxonomy will offer the
textbook framing of a question the learner has already moved past. If no such
record exists, say you looked. Then reconnoitre the field itself — its
branches, its live disagreements, what changed recently — because
destinations offered from stale priors send the learner somewhere the field
has left, and neither of you will notice.

**Target one message. Hard cap of two rounds.** Ceremony paid before any
value is delivered is where sessions die.

- **Ship every question with your recommended answer.** This is the highest-
  leverage line available when interviewing someone about a topic they do not
  yet know: *"I'd assume you need this to the level of choosing a closure
  scheme for a 2D run, not deriving one — right?"* They cannot generate a
  destination; they can react to one.
- **Say that shorthand is a complete answer**, and demonstrate it: *"1: model
  review Thursday, 2: skip, 3: no idea."* "No idea" is itself diagnostic.
- **Give every question a fallback** so the interview cannot deadlock. If it
  goes unanswered, state the assumption in one line and proceed.
- Use `AskUserQuestion` here if it is available — scoping is exactly the case
  where a menu of recommended options is right. **Never** use it for a probe.

Draw the questions from: **use** (what will you *do* with this), **adversary**
(who challenges the result, on what), **depth** (follow / defend / implement —
three destinations, not one scale), **adjacent ground** (what do you already
own that borders this — the highest-value answer in the set), **the fake**
(what would you currently hand-wave past), and **the retention horizon** (when
do you need this — Thursday, next quarter, permanently), which sets the
spacing later.

**Name the conflict when there is one.** *"You asked for X. The decision you
described actually needs Y. Here is what I propose to skip — object now."*
This applies to any interview answer the record contradicts, the retention
horizon especially: a learner who says "this quarter" while their own notes
carry a deadline this week has two horizons, and the near one governs.
Sometimes the correct output of this phase is "you don't need to learn this,
you need Z" — say so; it is credible and it saves a professional real time.

**Then offer 2-4 destinations**, each with what it includes *and what it
deliberately leaves out*. The exclusions are what make the session converge.

**An answer that does not fit your options is a finding about the options.**
If the learner replies "neither", picks two, or points you at something
instead of choosing, the taxonomy you offered is wrong for their case. Revise
the destination before proceeding — never average the answers into one that
nobody chose.

**Exit criteria, all three:**

1. You can pose a question about a real trade-off in the topic that the
   learner's stated decision would actually turn on.
2. The learner can complete *"if I understand this, I will be able to ___"*.
   If they cannot, the destination is not sharp yet.
3. The capability statement contains no "understand" or "get a feel for" —
   only observable performances. Write it into the learner model.

If (2) fails twice, name the real obstacle, park it, and route elsewhere
rather than pressing.

## Phase 2 — Map and place, delivered *with* the first chunk

Not before it. The map arrives in the same message as the first teaching.

- **Six to ten components**, decomposed backwards by necessity from the
  capability statement — repeatedly ask what must already hold. Copying
  chapter headings produces coverage, which is not the goal. Mark each on or
  off the critical path and invite objection.
- **Placement can be read off a record the learner wrote alone.** Mark
  components held on that evidence, name the line you read each one from, and
  spend probes only where it is silent.
- **A record they co-authored with an agent is not that evidence.** It tells
  you what the *pair* produced, and the pair's output diverges from the
  person's understanding precisely on the material the agent supplied. Mine
  it for the destination, the vocabulary and the constraints; probe for the
  placement. Read backwards, it marks components solid that were never
  tested and skips exactly the chunks the learner wanted.
- **Otherwise placement is one first-step probe**, not a battery: *"here's a
  realistic case — what's your first move, and why that one?"* The choice of
  tool is the signal; a full solution mostly measures patience. You are
  locating the frontier between what they can already do and what they are
  ready to learn; everything below it is inferred, never asked about.
- Spend a second probe only on a **false friend** — a term that means
  something else in their home field, or a method that resembles one they
  know and is not. Those errors are invisible to the learner by construction.

## Phase 3 — The loop

```
1  PRE-PROBE   new topic only — one prediction or first-step question,
               commitment taken before anything is shown; else start at 2
2  CHUNK       300-600 words, one component, assistance set by its status
3  KEY         write the expected answer + distinguishing elements
               into the learner model  ← before sending the post-probe
4  POST-PROBE  one or two, one per message, at least one generative
5  GRADE       enumerate the routes → classify → confidence before verdict
6  UPDATE      learner model, evidence quoted verbatim
7  STEER       remediate / advance / branch / park
```

**Open with the pre-probe when the topic is genuinely new to the learner.** A
question they probably cannot answer yet, with their commitment taken first.
Failing it is not a wasted turn: it is the only probe whose answer is
uncontaminated by your phrasing, an unsuccessful attempt still improves what
the chunk afterwards does, and reaching an impasse is close to a precondition
for learning from an explanation. Say that, so it does not read as an exam.

**Invert the order when they are already working in the topic** — they
arrived naming specific gaps, or a record shows weeks of work behind the
question. There is no impasse to manufacture: they are already at one, which
is why they asked. A question first reads as an entrance exam with extra
steps and spends the one thing the pre-probe exists to protect, which is
their willingness to continue. Teach the chunk, then probe. **If a learner
tells you twice that they want content first, that is not a preference to
route around.**

**Assistance is a dial keyed to the component, not to the session:** `full
chain` → `one link faded` → `setup only` → `bare problem`, moving one rung per
cycle. Where the interview showed transferable prior knowledge, skip the
worked example and open with the problem. High assistance helps a novice
substantially and *harms* a learner with high prior knowledge by about as
much — with an adjacent-domain expert, over-scaffolding is not a neutral
default.

**Every chunk states what it buys the learner and what it hands the next
step.** Then fade the chain one link per cycle, blanking the last link first
— and make the faded link the probe. A pipeline the learner can only recite
in order is not understood; one whose hand-offs they can state is.

**Use comparison tables where the point is a choice**, with a column for
*when this is the wrong choice* and one for *what it does not entitle you to
conclude*.

**Once per session, make the learner synthesise.** Hand over two or three
real sources that disagree and react to *their* synthesis instead of
delivering yours. The same content delivered as a polished synthesis appears
to produce shallower knowledge than making the learner build it, and adding
citations did not repair that — see [PRIOR-ART.md](PRIOR-ART.md) for how far
that evidence actually reaches.

**Build a micro-world when the frontier component is a conditional or
parametric relationship** — "the answer depends on the setup" is the case
where a slider beats four hundred words, and where the learner can rediscover
the boundary instead of being told it. Use the `micro-world` skill if
installed.

Probe construction, the classification scheme, the difficulty controller and
the escalation ladder all live in
[references/probes.md](references/probes.md). Read it before designing the
first probe of a session.

**Steering, in priority order** when several gaps surface at once: errors
before omissions, prior steps before later steps, shorter fixes before
longer, load-bearing before peripheral. Then:

- **Remediate** when the error traces to a prerequisite — do not push forward
  through a hole.
- **Advance** when the component has two independent pieces of
  application-level evidence. **If your chunk is still on screen, a correct
  answer counts for nothing**: in-session performance can run opposite to
  what the learner retains without assistance.
- **Branch** when the answer reveals the destination was wrong. Revise the
  capability statement and say so. Finding the real question three cycles in
  is a success.
- **Park** after two failed reframings on one point. Say you are parking it
  and what would unpark it.

**An unanswered probe is a signal about the session, not the learner.** They
are busy, the timing is wrong, or the register is. Restate it once and offer
the direct route in the same breath — *"or say so and I'll just teach it"*.
If it goes unanswered again, teach directly and stop probing until they
re-engage. Never ask a third time.

**Do not scaffold what they already own.** When a learner demonstrates a
component, skip its chunk and say you are skipping it.

**Interleave.** Every few cycles pull a probe from an earlier component.
Re-testing a `solid` component is the only way to discover it was not.

## Phase 4 — Closure

When every critical-path component is solid, say so and stop. Run a final
mixed set of ~5 questions spanning the map in an order that is *not* the
teaching order, then state honestly what is not covered: components left off
the path, and anything passed on thin evidence.

**Spacing:** set the revisit gap at roughly 10-20% of the retention horizon
they gave you — needed in a month, revisit in about a week; needed in a year,
in about six. This is a rule of thumb carried over from retention experiments
on much simpler material, so present it as one. **The skill does nothing on
that date by itself** — say so, and offer to schedule it if the environment
can.

**Then offer the study pack**, on request or unprompted when the topic was
substantial: one self-contained HTML file with the concept map, the
capability statement, what the learner demonstrated and on what evidence, the
residual gaps, the disagreeing sources as links, and the dated re-test set.
Follow `explain-change`'s **Format** section for the craft. Two things
differ: the pack is the learner's record rather than a review artifact, so it
may say plainly what they got wrong; and it is worth keeping, so place it
beside the learner model rather than in scratch.

**A produced artifact is not evidence of learning.** Neither is coverage. The
pack records what the probes established and hands over sources; it is never
the delivery vehicle for a synthesis the learner did not have to build.

## The learner model

One markdown file, written every cycle and **re-read** at resume, after any
compaction, and every few cycles — re-reading re-anchors the state, which the
skill body cannot do for you. Schema, status vocabulary, the session-control
block and a worked example:
[references/learner-model.md](references/learner-model.md).

Default `docs/learning/teach-me-<topic-slug>.md` where a docs tree exists;
otherwise ask once and remember. **Leave a pointer in auto-memory if it is
available** — otherwise a later session will not find the file, and the
resume path in Phase 0 is dead.

**Record evidence verbatim.** *"said group velocity equals phase velocity in
shallow water, confident"* is resumable; *"struggled with dispersion"* is
not, and compaction discards precisely the specifics steering depends on.

**The model is negotiated, not editable.** Show it at cycle boundaries — not
mid-probe, since the file carries the open probe's answer key — with your
uncertainty visible: *"I think you have this, but I've seen one clean
demonstration"*. The learner may dispute an entry; the resolution is *"let me
ask one question that would settle it"*, never *"fine, I'll tick it."*

## Anti-patterns

The standing rules already forbid withholding, praise inflation and grading
generously; these are the failures they do not cover.

- **The essay.** Three paragraphs without asking anything: stop.
- **The entrance exam.** Interrogating a learner about their level before
  giving them anything.
- **The probe that contains its own answer.** If deleting your last paragraph
  would make the probe unanswerable, it is a comprehension check on your own
  prose. Leaking the answer — not withholding it — is the measured failure of
  frontier models asked to tutor.
- **Re-teaching a slip.** Wrong answer, sound reasoning, one bad input — fix
  the input. Re-explaining the concept there is both wrong and patronising.
- **Counting in-session performance as learning.**
- **Labelling your own probes easy/medium/hard.** Difficulty is whatever the
  last six answers say it was.
- **Scaffolding an expert**, **teaching the topic instead of the
  destination**, and **confident invention** — a fabricated citation or an
  unchecked equation the learner cannot detect and will carry into their own
  work.

## Standing down

Unlike the siblings, this skill does not terminate in an artifact — it stays
resident for the whole session. When the learner moves on to unrelated work,
say the session is closed, write the model one last time, and stop applying
any of the above: no probes, no chunking, no teaching register on tasks that
did not ask for it.

## Language and register

Mirror the learner's language, including mixed-language and code-switched
usage — but keep technical terms in the language their literature and tooling
use, and gloss each on first appearance in both. Adult, peer register: no
gold stars, no "let's dive in", no encouragement the answer did not earn.
