# Prior art

What already exists, what this skill took from it, and what it deliberately
rejected. Written because a teaching skill assembled from nothing would
repeat mistakes that other people have already made in public, and because
several rules in `SKILL.md` are counter-intuitive enough that a future reader
deserves to see where they came from.

Surveyed 2026-08-09. Everything below was checked against a primary source;
where a claim could not be verified it is marked as such rather than dropped,
because an unverified claim you can see is safer than one you cannot.

## The landscape

| Cluster | Representatives | The reusable core |
|---|---|---|
| **Official Anthropic** | [`doc-coauthoring`](https://github.com/anthropics/skills/blob/main/skills/doc-coauthoring/SKILL.md), [`skill-creator`](https://github.com/anthropics/skills/blob/main/skills/skill-creator/SKILL.md), [`learning-output-style`](https://github.com/anthropics/claude-code/tree/main/plugins/learning-output-style) | An interview phase before producing anything is legitimate and has a stated exit condition; shorthand answers explicitly legal; ask only where a genuine trade-off exists |
| **Engineered tutors** | [`mhingston/agent-skills teach-me`](https://github.com/mhingston/agent-skills), [`cdmorozov/claude-tutors`](https://github.com/cdmorozov/claude-tutors) | Goal-backwards concept graph; a mastery ladder with named evidence per rung; confidence taken before the verdict; a hard question budget |
| **Interview engines** | Matt Pocock's `grill-me`, `superpowers/brainstorming` | Every question ships with your recommended answer; one question per message |
| **Diagnosis** | Exam-prep distractor libraries; Barton's diagnostic questions | Every wrong option maps to a *named* misconception |
| **Shipped tutors** | LearnLM / Gemini Guided Learning, ChatGPT Study Mode, Claude Learning Mode, Khanmigo | Pedagogy as a tunable parameter rather than a fixed persona; a mode-switch gate out of tutoring; never let the model check its own arithmetic |
| **Tutor-turn rubrics** | MRBench (arXiv:2412.09416); BEA 2025 shared task | Four scoreable dimensions — mistake identification, mistake location, providing guidance, actionability |

Two structural facts worth knowing before adding another teaching skill:

- **The official catalogue contains no teaching skill.** Seventeen skills in
  `anthropics/skills` as of August 2026; none pedagogical. There is no
  canonical implementation to defer to — the design freedom is real, and so
  is the burden.
- **The name collides.** At least two other public skills are called
  `teach-me`. That is fine: it is the phrase people type. Differentiate in
  the `description`, not the name.

## What this skill took

| Taken | From | Why it survived |
|---|---|---|
| **Interview about the destination, never the level** | Reconciling `cdmorozov` against the brief for this skill | `cdmorozov` argues, correctly, that quizzing a learner about what they know before giving them anything is obstruction. The resolution is that a *destination* interview is not a level interview — and level falls out of how they answer it |
| **Shorthand is a complete answer, demonstrated** | `doc-coauthoring` | It is what stops a senior professional abandoning a stack of open questions |
| **Every question ships with a recommended answer** | `grill-me` | The single highest-leverage line for interviewing someone about a topic they do not yet know: they cannot generate a destination, but they can react to one |
| **Interview exit condition** | `doc-coauthoring`, adapted | Theirs: enough context when edge cases can be discussed without explaining basics. Ours: when you can pose a trade-off question the learner's stated decision would turn on |
| **Ask only where a real trade-off lives** | `learning-output-style` | Its when-to-ask / when-not-to-ask split is the discipline that stops a teaching skill degenerating into busywork quizzing |
| **Backward decomposition by necessity** | `mhingston`, and Wiggins & McTighe underneath | Copying chapter headings produces coverage, which is not the goal |
| **Confidence after the answer, before the verdict** | `mhingston` | Reveal the verdict first and what comes back is a rationalisation |
| **Menus may navigate, never probe** | `mhingston` | Recognition masquerading as recall is the failure this prevents |
| **"Does that make sense?" banned by name** | `cdmorozov/references/pedagogy.md` | Yes/no under social pressure toward yes; the tutor receives zero information either way |
| **Correct by contradiction** | `cdmorozov/references/obstacles.md` | Being told you are wrong changes less than watching your own rule produce a result you know is false |
| **An `Implication:` line after every principle** | `cdmorozov/references/pedagogy.md` | The right way to carry learning science in a reference file without writing an essay |
| **Description names outcome and triggers, never the procedure** | [`obra/superpowers/writing-skills`](https://github.com/obra/superpowers/blob/main/skills/writing-skills/SKILL.md) | Their reported test: a description summarising "code review between tasks" made an agent perform **one** review though the skill specified two. A skill whose value is a disciplined loop must not leak a runnable summary of that loop |

## What it rejected, and why

- **Default-on withholding.** Every shipped tutor examined either ships an
  escape hatch or gets bypassed and resented without one. Anthropic's own
  Learning Mode instructions are the clearest case: they ask explicitly for a
  *"balance between pure Socratic dialogue and direct instruction"*, and for an
  immediate switch to direct-assistant mode the moment the user's ask is a
  concrete artifact. Standing rule 1 and the stand-down section are this skill's
  version. Khanmigo is the counter-example — forced withholding produced a
  documented cheating workaround and, per Sal Khan, *"for a lot of students, it
  was a non-event."*
- **Trusting the model's own arithmetic.** Khan Academy's stated root cause is
  that a language model predicts *"the most probable numbers to come next,"*
  and *"the most probable number in the training data is not always the correct
  answer."* Their fix was to route calculation through a deterministic tool.
  Standing rule 6 is the same rule.
- **Pure Socratic withholding.** The measured failure of frontier models
  asked to tutor is *leaking* the answer, not withholding it — on the
  standard pedagogical benchmark a strong model identifies mistakes correctly
  around 94% of the time while revealing the answer in roughly half its
  turns. Standing rule 1 answers direct questions directly; the leak check in
  `references/probes.md` guards the real risk.
- **A spaced-repetition algorithm (FSRS and relatives).** It models memory
  decay; the problem here is conceptual gaps. The *scheduling trigger* was
  kept as an offer at closure; the algorithm was not.
- **Per-cycle HTML artifacts.** The chunk stays conversational, because that
  is where the loop's signal lives and an artifact would replace generation
  with reading. Artifacts appear on two named predicates only: a micro-world
  when the frontier component is a conditional or parametric relationship,
  and the study pack at closure.
- **A skill-plus-output-style pairing.** Output styles are the only harness
  mechanism that re-anchors instructions *every turn*, which is exactly the
  drift problem here — but they are Claude-Code-specific and would break
  portability. Worth knowing as an option; not shipped.
  *(Correction to a claim made during research: output styles are not
  deprecated. They were deprecated in v2.0.30 and un-deprecated four days
  later in v2.0.32; only the standalone `/output-style` command was removed.)*
- **A `context: fork` or subagent-driven teaching loop.** A fork does not see
  the conversation history, which for a tutor is fatal regardless of tools.
  Research delegation to a subagent is fine and is the largest available
  context-budget lever; the *teaching and grading stay on the main thread*,
  which also enforces mechanically that nothing but the main thread can
  question the learner.

## Evidence behind the counter-intuitive rules

Only the load-bearing ones. Each was verified against the source; the hedges
are part of the record.

- **Open the cycle with a probe, before teaching.** The pretesting effect
  holds even for items the learner fails to retrieve, and VanLehn's impasse
  work reports that learning from a tutorial explanation was uncommon when
  the student was not at an impasse. Together these say a failed pre-probe is
  not a wasted turn.
- **Ask for a step, not an answer.** Tutoring meta-analyses put answer-based
  interaction near d≈0.3 and step-based near d≈0.75, with finer granularity
  buying nothing.
- **Assistance must fall as prior knowledge rises.** Expertise-reversal
  meta-analysis, 60 studies / 176 effects / N=5,924: high assistance is
  d=+0.505 for low prior knowledge and **d=−0.428** for high. For an
  adjacent-domain expert, over-scaffolding is actively harmful, not merely
  slow.
- **Do not fold under pushback.** SycEval reports 58.19% sycophancy overall,
  14.66% of it *regressive* (a correct answer flipped to wrong), flips
  persisting 78.5% of the time, and **citation rebuttals producing the
  highest regressive rate** (Z=6.59, p<0.001). The honest limit: sycophancy
  is a preference-training artifact, so a prompt rule reduces it and does not
  remove it — which is why the answer key is durable and auditable, and why
  the learner is told verdicts are disputable.
- **Write the answer key first.** LLM graders show measured optimistic bias,
  over-scoring incorrect and underdeveloped answers. The same study concludes
  human oversight remains necessary — this skill has none above it, so the
  key is the only available check.
- **Enumerate the routes before calling an answer wrong.** Khan Academy
  reported its tutor making evaluation errors — misjudging whether a student
  was right — even when its own calculation was correct, and its shipped fix
  was to write out all the ways the student may have reached the answer.
- **Two unassisted observations for `solid`.** In a controlled study, a
  tutor-style arm improved performance +127% *during practice* while a
  plain-assistant arm scored −17% on the unassisted exam. In-session
  performance can run opposite to retention.
- **Make the learner synthesise at least once.** Seven experiments,
  N=10,462, found LLM-synthesised learning shallower than link-based with
  content held identical, and preregistered replications adding real-time
  links did not restore depth. **Hedge:** the depth outcome is substantially
  self-report, with the objective leg being third-party ratings of advice
  participants wrote. Well-motivated, not settled.
- **Target ~85% correct.** From optimal-difficulty work on simpler learning
  tasks. **The trigger thresholds in `probes.md` — three right to raise, two
  wrong to drop, a rolling window of six — are a working convention, not a
  finding.**
- **Do not label your own probes by difficulty.** The stronger published
  result is about *discrimination*: models struggle to judge whether an item
  separates learners who hold a concept from those who do not, which is the
  entire job of a probe.
- **Spacing at 10-20% of the retention horizon.** From a large lag study —
  but on verbatim retention of simple material, extrapolated here to
  conceptual understanding. Presented in the skill as a rule of thumb.

## Claims deliberately not made

- That any of this is *absent everywhere*. The absence findings were
  established by enumerating GitHub repositories and two curated lists. That
  is a claim about GitHub, not about the world.
- That the anti-sycophancy rules make the verdict trustworthy. They make it
  better and auditable. The learner is told it is disputable because it is.
- That the evidence base fits this learner. Almost every empirical anchor
  above is drawn from children or undergraduates; the stated target is an
  expert-adjacent adult professional. The one meta-analysis that genuinely
  fits that learner is expertise reversal. Everything else transfers by
  argument, not by measurement.
- That this design has been validated in use. It has not. Nothing here was
  graded against real transcripts before shipping; the first sessions are the
  test, and the rules most likely to be wrong are the invented thresholds.
