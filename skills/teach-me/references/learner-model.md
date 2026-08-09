# The learner model

- [Cadence](#cadence)
- [Status vocabulary](#status-vocabulary)
- [Schema](#schema)
- [Worked example](#worked-example)
- [Resuming](#resuming)

The file the loop runs on. It exists so a session can end abruptly and still
be resumable, so a diagnosis survives a context compaction, and so the
learner can be shown what you believe about them and dispute it.

## Cadence

**Write** at the end of every cycle — not at the end of the session, because
most sessions end by interruption. **Read** it at resume, after any
compaction, and every few cycles thereafter. Re-reading is what re-anchors
the *state*; the skill body cannot do that, since the harness never re-reads
it.

**Evidence goes in verbatim.** `"said group velocity equals phase velocity in
shallow water, confident"` is resumable. `"struggled with dispersion"` is
not — and compaction discards exactly the specifics that steering depends on.

## Status vocabulary

Five values and the evidence each requires. The point of the ladder is that
the two cheap outcomes are not the same thing, and that `solid` is expensive
on purpose.

| Status | Means | Evidence required |
|---|---|---|
| `untested` | Never probed. | — |
| `shaky` | Probed; wrong, or right for the wrong reason. | One failed probe with the error *named* (which of the five cells). |
| `working` | Can state and explain it. | One correct answer at *explain* level. |
| `solid` | Can apply and judge with it. | **Two independent observations** at *apply* level or above, separated by intervening material on another component. |
| `out-of-scope` | Real, deliberately excluded. | The reason, so a later session does not re-litigate it. |

Two rules that keep this honest:

- **If your chunk is still on screen, a correct answer counts for nothing.**
  In-session performance can run opposite to what a learner retains
  unassisted. Only unassisted observations count toward `solid`.
- Record the observation count in the status cell: `` `working` (n=1) ``.
  One tick is one noisy sample, and a model that flatters the learner retires
  exactly the components that still need work.

## Schema

```markdown
# teach-me — <topic>

**Started:** YYYY-MM-DD · **Last session:** YYYY-MM-DD · **Cycles:** N

## Destination

<3-5 observable capabilities, confirmed by the learner. No "understand" or
"get a feel for". Revised in place when the loop branches — the old version
moves to Log, because a changed destination is itself a finding.>

## Learner context

- **Adjacent expertise:** <what they already own that borders this>
- **Use:** <the decision / artifact / review this feeds>
- **Adversary:** <who challenges the result, and on what>
- **Depth target:** <follow / defend / implement>
- **Retention horizon:** <when they need it — drives the spacing calc>
- **Conventions in play:** <datum, sign, units, notation they work in —
  checked before any answer is called wrong>
- **False-friend risks:** <terms or methods meaning something else in their
  home field>

## Components

| # | Component | Prereq | On path | Status | Evidence (verbatim) | Last probed |
|---|---|---|---|---|---|---|

## Session control

- **Rolling probe outcome (last 6):** ✓ ✓ ✗ ✓ ✓ ✓ → 5/6, at target
- **Assistance:** <component · rung>  (full chain / one link faded /
  setup only / bare problem)
- **Spacing:** horizon <date> → revisit ~<date>  (10-20% of the horizon)
- **Parked:** <component · why · what would unpark it>

## Confirmed misconceptions

<Each: what the learner believed, what is true, which error pattern it is,
whether corrected, whether re-tested. Keep the corrected ones — they are
the first things to re-test, and confident errors are the most likely to
return.>

## Open threads

<Questions the learner raised that were parked, and why.>

## Next

- **Chunk:** <the next component and its assistance rung>
- **Probe:** <the question, verbatim — written before it is sent>
- **Expect:** <the answer you expect>
- **Distinguishing:** <2-3 elements separating real understanding from a
  plausible-sounding reply>
- **Due a re-test:** <component, and why now>

## Log

<One line per cycle: taught / probed / what the answer revealed. Terse.>
```

## Worked example

Mid-session, three cycles in. Component 3 is `shaky` on a *confident* wrong
answer, which is why it — and not the frontier — is what the next cycle
addresses.

```markdown
# teach-me — global sensitivity analysis

**Started:** 2026-08-09 · **Last session:** 2026-08-09 · **Cycles:** 3

## Destination

1. Choose between Morris, Sobol' and a surrogate-based scheme for a given
   model and defend the choice on cost and on what each can answer.
2. State what a sensitivity index is conditional on, and therefore what
   would change it.
3. Explain to a reviewer why a sensitivity analysis does not give you the
   model's uncertainty, and what does.
4. Read a paper's SA methods section and name the assumption it skipped.

*Out of scope for this destination:* FAST/eFAST machinery beyond knowing
when it beats Sobol'; derivative-based measures; the SHAP literature
(different question — but see the name-collision probe in component 8).

## Learner context

- **Adjacent expertise:** coastal/hydraulic modelling, calibration, Python;
  comfortable with Monte Carlo, less so with variance decomposition.
- **Use:** deciding which parameters to calibrate in a hydrodynamic model,
  and defending that choice in a project review.
- **Adversary:** a reviewer who asks "why did you fix that parameter?"
- **Depth target:** defend, and implement with SALib.
- **Retention horizon:** design review 2026-09-15 → revisit ~2026-08-25.
- **Conventions in play:** MSL vs chart datum; still-water vs total depth.
  Check both before calling a numeric answer wrong.
- **False-friend risks:** "OAT" (Morris steps are OAT, the design is not
  local); "exact" (analytic in hydraulics vs a defined-but-estimated
  functional here); "Shapley" (SHAP ≠ Shapley effects).

## Components

| # | Component | Prereq | On path | Status | Evidence (verbatim) | Last probed |
|---|---|---|---|---|---|---|
| 1 | The four GSA settings; SA vs UA | — | yes | `solid` (n=2) | "the 95% band is UA, the 60%-from-roughness is SA" — then applied it unprompted to their own surge model | 2026-08-09 |
| 2 | What counts as a factor; ranges and pdfs | 1 | yes | `working` (n=1) | "grid resolution could be a factor too, not just parameters" | 2026-08-09 |
| 3 | Indices are conditional on the setup | 2 | yes | `shaky` | **Confident** wrong: "the indices are a property of the model". Error pattern: overgeneralisation | 2026-08-09 |
| 4 | Output choice / QoI, scalar vs time-varying | 2 | yes | `working` (n=1) | "you'd have to reduce the time series to a scalar first" | 2026-08-09 |
| 5 | Pick-freeze design (A/B/AB) | 2 | yes | `untested` | — | — |
| 6 | Morris: μ*, σ, r(k+1) | 5 | yes | `untested` | — | — |
| 7 | Sobol': S_i, S_Ti, n(k+2), sum rules | 5 | yes | `untested` | — | — |
| 8 | Convergence, CIs, negative indices, thresholds | 7 | yes | `untested` | — | — |
| 9 | Independence; correlated inputs | 7 | yes | `untested` | — | — |
| 10 | Identifiability, equifinality, the calibration hand-off | 7 | yes | `untested` | — | — |
| 11 | Surrogates (PCE / GP) as a cost trade | 7 | no | `out-of-scope` | Excluded at scoping: their runtime does not force it yet. Revisit if it does | — |

## Session control

- **Rolling probe outcome (last 6):** ✓ ✓ ✓ ✗ ✓ — 4/5, at target
- **Assistance:** component 3 at `full chain`; component 5 will open at
  `setup only` — they already hold Monte Carlo sampling
- **Spacing:** horizon 2026-09-15 → revisit ~2026-08-25
- **Parked:** —

## Confirmed misconceptions

- **"The indices are a property of the model."** They are a property of
  model + chosen output + assumed input ranges and pdfs. Halve a parameter's
  plausible range and its share falls while everyone else's rises. Pattern:
  overgeneralisation. Raised C3, corrected, **not yet re-tested.**
- **"A sensitivity analysis tells me my model's uncertainty."** Corrected C1,
  re-tested successfully C2 → component 1 `solid`.

## Open threads

- Asked whether SA should be redone after calibration. Parked: it depends on
  components 9 and 10, which are downstream. The answer is owed, and it is a
  good one — posteriors are correlated, so the vanilla method is invalid at
  exactly the step they want it.

## Next

- **Chunk:** component 3 again, at `full chain`. Then a micro-world — this is
  a parametric-conditionality component, which is the named trigger.
- **Probe:** "I halve the assumed range of your top-ranked parameter and
  change nothing else. What happens to (a) its S_i, (b) the total output
  variance, (c) the ranking of the other factors?"
- **Expect:** all three can change; the share typically falls, total variance
  falls, the others' shares rise.
- **Distinguishing:** does the learner separate the *share* from the
  *absolute* variance; do they notice the other rankings move; do they say
  "it depends on the pdf, not just the range".
- **Due a re-test:** component 1, in the closing set.

## Log

- **C1** — SA vs UA and the four settings; learner conflated SA and UA,
  corrected → `shaky`.
- **C2** — factors and ranges; re-tested C1, correct and applied to their own
  surge model → `solid` (n=2). C2 → `working`.
- **C3** — output choice → `working`. Pre-probe on conditionality: confident
  wrong → C3 `shaky`, misconception recorded.
```

## Resuming

On firing for a topic that already has a file: read it, then open by stating
what it says the learner holds, what is open, and what you are about to
re-test — and **re-test one earlier component before teaching anything new.**
It re-establishes whether `solid` is still true, which is the only way
spacing does any work, and it gives the learner a chance to correct your
model of them before it steers another session.

Find the file with `Glob docs/learning/teach-me-*.md` and by checking
auto-memory for a pointer. **Leave that pointer when you first create the
file** — without it, a later session has no way to know the topic was ever
started.
