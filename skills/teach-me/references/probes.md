# Probe design

- [What a probe is for](#what-a-probe-is-for)
- [Interaction granularity: ask for a step](#interaction-granularity-ask-for-a-step)
- [The ladder](#the-ladder)
- [The shape menu](#the-shape-menu)
- [The answer key, written first](#the-answer-key-written-first)
- [Construction rules](#construction-rules)
- [Multiple choice: may diagnose, may never promote](#multiple-choice-may-diagnose-may-never-promote)
- [Confidence](#confidence)
- [Grading: five cells, not two](#grading-five-cells-not-two)
- [The escalation ladder](#the-escalation-ladder)
- [Difficulty as a closed loop](#difficulty-as-a-closed-loop)
- [Named error patterns](#named-error-patterns)
- [Spacing and re-tests](#spacing-and-re-tests)

## What a probe is for

A probe is not a quiz question. Its job is to produce a *diagnosis* — to make
the learner reveal which of several possible internal states they are in. A
question everyone gets right, or one whose wrong answers all mean the same
thing, has cost the learner time and told you nothing.

Three filters before anything is sent:

- **Would a competent practitioner have to *decide* something to answer
  this?** If not, it is nomenclature. Skip it.
- **The leak check.** If deleting your own last paragraph would make the
  probe unanswerable, it is a comprehension check on your prose, not a probe.
  Leaking the answer is the measured failure mode of frontier models asked to
  tutor — on the standard pedagogical benchmark, a strong model identifies a
  mistake correctly ~94% of the time and reveals the answer in roughly half
  of its turns. Withholding is not your risk; leaking is.
- **Could someone still holding the target misconception answer it
  correctly?** If yes, it does not discriminate. Rewrite it.

Budget: one pre-probe plus one or two post-probes per cycle, **hard cap of
three, one per message.** At most one recall-level probe per cycle, and only
as an anchor check.

## Interaction granularity: ask for a step

Ask for a **step**, not for a final answer and not for an essay. The
tutoring meta-analyses put answer-based interaction around d≈0.3 and
step-based around d≈0.75, with sub-step granularity buying nothing further —
the entire gain lives in moving from answers to steps. "What's your first
move, and why that one?" outperforms both "what's the answer?" and "explain
this whole area to me."

## The ladder

Climb until the learner stops being fluent — that rung is the frontier, and
it is where the next chunk goes.

| Rung | Asks for | Stem shapes |
|---|---|---|
| **State** | Recall | "What does σ measure here?" |
| **Explain** | Mechanism, causes | "Why does that follow?" "What breaks if it isn't true?" |
| **Apply** | Transfer to a case | "40 parameters, 6-hour runtime — what do you run first, and what do you give up?" |
| **Judge** | Choice under trade-off | "A colleague fixes every parameter with a small first-order index. Sound?" |

**Never stop at *state*.** Recall is the rung where fluency and understanding
are indistinguishable, and where an answer is most likely to be your own
phrasing handed back. `working` needs *explain*; `solid` needs *apply* or
above, twice.

## The shape menu

Pick by which layer you need to resolve, not by rotation. Every shape below
has a pre-committable answer key, which is what makes the inference
grounded rather than a feeling that the learner was vague.

| Shape | Form | Discriminates | Use when |
|---|---|---|---|
| **First-step** | "What's your first move here, and why that one?" | Which schema fires | Placement; cheap re-test |
| **Perturbation** | "I halve X — what happens to A, B and C?" | Whether they hold the result's *conditionality* | Any result that depends on its setup |
| **Hand-off** | "What does this stage give the next? What does the next still need from elsewhere?" | Pipeline-level vs method-level understanding | Every procedural component; the faded link |
| **Entitlement pair** | "Name one conclusion this entitles you to, and one it does not." | Over-reading | After any method with a proxy or a ceiling |
| **Assumption audit** | "Which assumption here does your actual project violate?" | Silent tooling assumptions | Whenever a library hides one |
| **Anomaly triage** | "You get this odd output — bug, noise, or real?" | Ran-it vs read-about-it | Estimators, numerics, anything sampled |
| **Contrastive why** | "Why does this hold here and **not** in [neighbouring case]?" | The deepest available for a high-prior-knowledge learner | Default post-probe |
| **Name collision** | "Same object as X, or just the same word?" | Cross-community confusion | Topics spanning two fields |
| **Error-finding** | A short, plausible, *wrong* analysis: "what's wrong with it?" | Evaluate level; the paper-reading skill | Closure; judge-level checks |
| **Explain-back** | "Say that to someone on your team." | Production vs recognition | Any cycle needing a generative probe |

**Contrastive why is the default**, not a warm-up: elaborative-interrogation
effects grow with prior knowledge, so for an adjacent-domain expert it is the
main instrument. Never the bare "why?" — always the contrast.

**At least one probe per cycle must be generative and about their own work.**
Transfer to their real case exposes a hollow understanding faster than
anything else, and it is the only probe that tests the thing the capability
statement is written in terms of.

## The answer key, written first

Before sending a probe, write into the learner model's `## Next` block:

```markdown
- **Probe:** <the question, verbatim>
- **Expect:** <the answer you expect>
- **Distinguishing:** <2-3 elements separating real understanding from a
  plausible-sounding reply — a boundary condition, a unit, a sign, a
  limiting case>
```

Three reasons this is not ceremony. Grading against a key written afterwards
means grading the answer you were hoping for, and LLM graders measurably
over-score short, confident, underdeveloped replies — the exact profile of a
busy professional's answer. When the learner disputes a verdict you need
something to re-derive *from*. And a key you cannot write is a probe you did
not understand well enough to ask.

The key lives in the file rather than in your head because thinking does not
survive compaction and a disputed verdict may be challenged many turns later.
Do not hold the write until the answer arrives — a key written afterwards is
worth nothing, which is the whole point.

**While a probe is open, the file therefore contains its answer.** Mark it as
a spoiler where it sits, warn the learner in the message that sends them to
the file, and do not walk them through the model mid-probe — cycle boundaries
only. The learner keeps the choice: reading your own answer key is opting out
of being measured, which is theirs to decide, but they have to be told the
choice exists.

## Construction rules

Barton's five, for diagnostic items: unambiguous; a single concept; answerable
in about ten seconds; **you learn something from every wrong response without
needing the learner to explain**; and it must be impossible to answer
correctly while still holding the key misconception. The last is the defence
against a smart adjacent-domain expert pattern-matching to the right answer
on plausibility alone.

## Multiple choice: may diagnose, may never promote

A well-built item is genuinely diagnostic — which distractor gets picked
tells you which misconception is running, where an open question often does
not. But recognition is not evidence of mastery.

- **Use it** for placement, for cheap re-tests, and to separate two specific
  competing misconceptions.
- **Never let it promote to `solid`.** That requires production.
- **Never use a menu to make a knowledge probe easier.** Menus are for
  navigation and preferences.
- **Three options is the psychometric optimum.** Two plausible distractors
  beat four fillers; every wrong option must map to a *named* misconception.
  Write the distractors first, from the misconception list, then write the
  correct answer to sit alongside them.
- **Surface parity is mandatory.** The habit of writing a longer, more
  hedged, more precise correct option gives it away instantly to a test-wise
  professional. Match length, complexity and grammar across options.
- **If you cannot name what picking each wrong option would reveal, the
  question is not ready.**

## Confidence

Ask **after the learner has answered and before you give any correctness
signal.** The ordering is the mechanism: reveal the verdict first and what
comes back is a rationalisation. A word is enough — *"how sure, roughly?"*;
asking for a number invites theatre.

| | Right | Wrong |
|---|---|---|
| **Confident** | Advance. | **The highest-yield moment in the session.** Surface the discrepancy plainly — "you were sure; here's why that's wrong" — do not soften it into "great intuition, though". The discrepancy *is* the correction mechanism. Then flag it for a delayed re-check: confident errors correct strongly and are also the most likely to return. |
| **Unsure** | Not solid. Probe the reasoning — they may have guessed, or may know more than they trust. | Ordinary gap. Teach it. |

## Grading: five cells, not two

Score two axes — answer right or wrong × reasoning sound or unsound — with
confidence taken before any verdict. Right/wrong alone miscategorises roughly
a fifth of answers in the diagnostics literature. **Never write "gap" in the
learner model without saying which of these it was.**

| Cell | Signature | Response |
|---|---|---|
| **Knows it** | Right, sound | Advance. Count the observation. |
| **False positive** | Right, unsound | Do **not** promote. Right answer, wrong route — the most-missed cell, because the conclusion matches. |
| **False negative** | Wrong, sound | Fix the one bad input. Do **not** re-teach the concept: that is both wrong and patronising. |
| **Misconception** | Wrong, unsound, confident | Remediate by contradiction. Record it by name. |
| **Plain gap** | Wrong, unsound, unsure | Just teach it. No drama. |

Before assigning a cell, **enumerate the routes that produce the answer** —
including the route that is correct under a different convention: a sign
convention, a datum, units, a different definition of the same symbol. Only
then decide which error it is. Khan Academy's shipped fix for its tutor
mis-marking correct student work was exactly this: write out all the ways the
student may have arrived at their answer before judging it. Note the
learner's working conventions in the learner model so this check is cheap.

Then, if the answer is wrong: **trace it to its prerequisite.** The component
that failed is usually not the component that is broken.

Two further reading signals:

- **The multistructural signature** — a correct *list* with no connective
  tissue. This is what fluent-but-shallow looks like coming from an
  articulate senior professional, and it will read as mastery. The fix is a
  relational prompt ("how do these three interact? which dominates when?"),
  never more content.
- **Your own phrasing coming back verbatim.** Follow up with something the
  phrasing cannot answer.

**A vague answer is not a correct answer.** Ask the one follow-up that
separates the readings.

## The pre-send audit

Before sending a correction or a piece of feedback, check it against the four
dimensions that a peer-reviewed tutor-evaluation rubric scores. They are cheap
to run and they catch the commonest empty response — the content-free nudge:

1. **Mistake identification** — did I name the actual error, rather than
   gesture at "something's off here"?
2. **Mistake location** — did I point to exactly where it lives, rather than
   at the answer as a whole?
3. **Providing guidance** — did I give a real lever — an explanation, a
   boundary case, a hint with traction — rather than either the full answer or
   an encouraging noise?
4. **Actionability** — is the learner's next move unambiguous?

Specialised systems score worst on the third, and it is the one worth the most
attention: "think about it again" passes 1, 2 and 4 and fails the only
dimension that helps.

## The escalation ladder

When an answer stalls, climb one rung at a time: **pump** ("what else?") →
**hint** (point at the region) → **prompt** (ask for the missing term) →
**re-framed problem**. Never let the ladder end in the answer — a hint
sequence that terminates in the solution trains the learner to skip to the
bottom. After two failed reframings on the same point, **park it**: say you
are parking it, record what would unpark it, and move on.

## Difficulty as a closed loop

Target roughly **85% correct** — hard enough to carry information, easy
enough to keep going. Run it as a controller on the rolling outcome of the
last six probes, recorded in the learner model:

- three consecutive fully-correct → raise one rung
- two consecutive wrong → drop a rung **and remediate the prerequisite**,
  rather than re-asking the same thing

The 85% target comes from optimal-difficulty work on simpler learning tasks;
the trigger thresholds are a working convention, not a finding. Tune them.

**Do not label your own probes easy, medium or hard.** Models align poorly
with human item statistics, and — the stronger result — struggle to judge
whether an item *discriminates* between learners who hold a concept and
learners who do not, which is the entire job of a probe. Difficulty is
whatever the last six answers say it was.

## Named error patterns

Vocabulary so the learner model records a diagnosis rather than a miss:

| Pattern | Looks like | Fix |
|---|---|---|
| **Overgeneralisation** | A rule applied outside its conditions. | A boundary case where their rule gives an answer they know is wrong. |
| **Undergeneralisation** | A rule treated as special to one context. | A second context where it applies. |
| **False analogy** | An import from their home field that does not hold. | Name the mapping, then the term where it breaks. |
| **Half-right kernel** | A belief with a true part and a false part ("Morris is OAT, therefore local"). | **Name the true part explicitly before correcting the false part**, then use a boundary question to locate the seam. Contradicting the whole belief loses the part they were right about. |
| **Premature closure** | The first plausible explanation adopted before alternatives. | Ask for a second explanation fitting the same evidence. |
| **Passive recognition** | Fluent agreement, no production. | Any generative probe. |
| **Load-bearing adjective** | *exact*, *robust*, *global*, *optimal*, *converged* — one word silently merging several claims. | Force disambiguation before proceeding. |
| **Slip** | A one-off error the learner can find themselves. | Point at it; do not re-teach. |

## Spacing and re-tests

- Every few cycles, pull one probe from a component last touched several
  cycles ago. Mixed practice retains; blocked practice flatters.
- Re-test corrected misconceptions first, and at *apply* level — a
  misconception acknowledged is not a misconception removed.
- A component that fails its re-test returns to `shaky`. That is the
  mechanism working; say so plainly rather than softening it.
- The closing set is interleaved by construction: ~5 questions spanning the
  whole map, in an order that is not the teaching order.
