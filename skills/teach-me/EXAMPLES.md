# Examples

One worked testbed. **This skill has not yet been hardened by use** — unlike
`debrief`'s examples, nothing below is a story about a session that happened.
It is the case the skill was designed against, worked out far enough to be a
test: if a teach-me session on this topic does not surface these gaps, the
skill is not doing its job.

## The testbed: global sensitivity analysis, for a coastal modeller

The motivating case was a competent hydraulic engineer learning global
sensitivity analysis (GSA) from a general assistant, by asking good follow-up
questions over about eight turns. The transcript is a fair example of the
best a strong model does *without* a teaching loop, which is what makes it
useful: the failure is not that it was wrong, but that its shape was set
entirely by what the learner already knew to ask.

**What that conversation got right:** Morris and Sobol' correctly identified
as the de-facto standard pair; σ correctly described as conflating
interaction with non-linearity, and explicitly *not* identifying the
interaction partner; the Morris → Sobol' → calibration ordering; small
S_Ti as the criterion for fixing a parameter; and — the best answer in the
transcript — a clear "no, you do not yet know your uncertainty" when asked,
with the distinction between apportioning variance and quantifying it.

**What it never raised.** Six omissions, ordered by how much they would cost
this learner in a real project review.

### 1. Which model output? — never asked

Every index is a property of a *chosen* output. A hydrodynamic model produces
time series over a spatial field; there is no ranking until someone picks a
scalar. This is not a detail: in a published flood-inundation GSA the most
influential factor *changes during the event*, and spatial resolution ranks
far higher for local water depth than for flood extent. A learner who leaves
with "the ranking" in the singular will hand a reviewer a table that answers
a question nobody asked.

> **Probe (hand-off):** You show me one sensitivity ranking table. What are
> the two things I need to know before I can read it?
> *Key:* which output, and over which period or region. Distinguishing:
> whether they volunteer that the ranking is time-varying.

### 2. Conditional on the assumed ranges and pdfs — never stated

An index is a share, conditional on the input ranges *and* their distribution
shapes. This is the misconception the worked learner model in
`references/learner-model.md` records as confident-and-wrong, because it is
the one a competent engineer is most likely to hold: indices feel like a
property of the model, and they are a property of the model *plus the
uncertainty specification you chose*.

> **Probe (perturbation):** I halve the assumed range of your top-ranked
> parameter and change nothing else. What happens to (a) its S_i, (b) the
> total output variance, (c) the ranking of the other factors?
> *Key:* all three can move — its share typically falls, total variance
> falls, the others' shares rise. Distinguishing: does the learner separate
> the share from the absolute variance; do they say "and the pdf shape, not
> just the range".

This is also the skill's canonical **micro-world** trigger: a slider that
shrinks one input range and watches the bar chart re-order kills this
misconception in seconds and survives four hundred words of prose.

### 3. Independence — never mentioned, and the highest-severity gap here

The variance decomposition is orthogonal and unique only when inputs are
independent. Under dependence the first-order indices need no longer sum
below one, S_Ti can fall *below* S_i, and the shares stop being
interpretable. Coastal parameter sets are routinely correlated — wave height
and period, a breaking index and its roller dissipation coefficient,
Manning's n across land-use classes — and, decisively, **every calibrated
posterior is correlated.** So the method is invalid at precisely the step the
engineer most wants it: re-running GSA after calibration to decide where the
next survey buys the most variance reduction.

The tooling actively manufactures this error. SALib's Sobol'/Saltelli sampler
takes bounds and builds independent marginals; there is no correlation
argument, and the user guide does not state the assumption outside the HDMR
analyser's docstring. Feeding it correlated parameters silently generates
physically impossible combinations *and* invalid indices.

> **Probe (assumption audit):** Your five parameters include a wave-breaking
> γ and a roller dissipation coefficient that are physically linked, and you
> sample them independently over their marginal ranges. Name **two distinct**
> things this breaks.
> *Key:* (i) sample validity — you run combinations that never occur; (ii)
> estimator validity — the decomposition is no longer orthogonal, so the
> indices lose their meaning. A learner naming only (i) has the physics and
> not the mathematics; only (ii), the reverse.

### 4. "Exact" — three claims wearing one word

The conversation called Sobol' "mathematisch exakt" repeatedly. Three
different things get merged there: the indices are exactly *defined* (true,
and the real contrast with μ*, which is a proxy); the *estimates* are Monte
Carlo and therefore noisy, which is why SALib returns bootstrap confidence
intervals and why small indices come back negative; and even a converged
index is conditional on the setup. Calling the method "exact" invites all
three errors at once.

> **Probe (anomaly triage):** Your ST for parameter 7 comes back as −0.004.
> Is your code broken?
> *Key:* no — estimator noise around a true value near zero; the standard
> estimators are not constrained non-negative. Check the bootstrap interval
> and the convergence plot.
> **Follow-up:** the bootstrap mean has been flat over your last three sample
> sizes — converged? *Key:* not necessarily; a flat mean is necessary but not
> sufficient, the interval width must also have collapsed.

### 5. The cost formula — right ballpark, wrong structure

"O(1000·k)" fuses a textbook default into an asymptotic. The structure is
**N = n(k+2)** for first- and total-order indices from one design (SALib's
default `calc_second_order=True` gives n(2k+2) because it also estimates the
pairwise terms). The 1000 is a *base sample size* suggested in Saltelli et
al. (2008) — and a three-model convergence study found it insufficient for
the two more complex models. The same study found requirements varying by
about two orders of magnitude for the same k depending on what you need:
converged index *values* cost roughly a hundred times a stable *ranking*, and
its conclusion is explicit that fit-for-all sample-size rules should not be
used.

Morris is likewise r(k+1) with r typically 10-50, not "O(k)" — the constant
is the whole cost story.

> **Probe (entitlement pair):** Give me one thing μ* is nearly as good as
> S_Ti for, and one thing it is not.
> *Key:* ranking, yes — it is an empirically validated proxy for the
> total-order index. Not: a variance share, a normalised 0-1 scale, or any
> transferable threshold, since μ* carries the output's units.

### 6. Sensitivity is not identifiability — the missing bridge

This is the gap that would actually cost the learner in the review they named
as their adversary. The conversation ran Morris → Sobol' → "now calibrate the
sensitive parameters", which quietly implies that dropping insensitive
parameters makes the calibration well-posed. It does not. Sensitivity is a
property of the forward map; identifiability is a property of the inverse
problem. Two parameters can each be highly sensitive and jointly
non-identifiable because their sensitivity functions are collinear and they
compensate — which is the standard collinearity-index result, and which
hydrologists know natively as equifinality: many behavioural parameter sets
fit acceptably, so the honest output of calibration is an ensemble, not a
best set.

> **Probe (hand-off):** Two parameters both show S_Ti ≈ 0.45 and S_i ≈ 0.05.
> (a) Do you keep them in the calibration? (b) Will the calibration return a
> sharp posterior for either?
> *Key:* (a) yes — S_Ti is large, so they cannot be fixed; (b) no — S_Ti ≫
> S_i means nearly all the influence runs through interaction, so expect a
> ridge-shaped likelihood and strongly correlated posteriors. The right next
> move is an identifiability or collinearity check, **not** a bigger sample.

A seventh, smaller: the transcript placed SHAP in the same table as Morris
and Sobol'. SHAP explains a fitted model's individual predictions relative to
a background set; **Shapley effects** — a different object sharing the name —
are a variance-based GSA measure that sums exactly to the output variance and
is one of the correct answers to the dependence problem in §3. The GSA
sibling was never mentioned; the ML cousin was. That is the **name collision**
probe shape, and it is a standing hazard for an engineer straddling
modelling and Python.

## What the loop would have done differently

- **Scoped first, and the scoping is substantive here, not polite.** The GSA
  literature organises the field around four *objectives* — factor fixing,
  factor prioritisation, variance cutting, factor mapping — and holds the
  question ill-posed until one is named. Different objectives converge at
  wildly different sample sizes and are served by different indices. The
  transcript never asked, so it taught a blend.
- **Made the pipeline's hand-offs the content**, since that is what the
  learner kept asking for: what each stage consumes, what it hands on, and
  the one thing it does *not* tell you. Then faded the chain one link per
  cycle and made the faded link the probe.
- **Been adversarial on purpose, and said why.** A systematic review of
  highly-cited papers whose focus is sensitivity analysis found statistically
  inadequate practice to be common — including a fraction of *methodological*
  papers still recommending one-at-a-time analysis. That gives the tutor
  licence to probe hard without condescension: the misconceptions being
  tested are held by published experts, so being asked is not an assessment
  of the learner.

## A note on the register

The source conversation was in German with English technical terms, and every
answer ended with an offer of a Python example that the learner accepted with
"Yes" and that never arrived, because the next question redirected. Both are
worth reading as signals: mirror the language and keep the terms in the
language of the tooling, and **do not close every turn with an offer** — a
learner saying "yes" to the fourth offer in a row is being polite, not
choosing.
