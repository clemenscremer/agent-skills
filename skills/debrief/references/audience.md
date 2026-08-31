# Audience — the two dials

Shared craft for **both tenses**. Read together with
[../SKILL.md](../SKILL.md) (backward) or [plan.md](plan.md) (forward):
everything there about two-layer background, intuition-first, diagram
families, self-containment, provenance labels, verified citations and
staleness applies unchanged. This file decides *who the document is for*,
and the four things that follow from the answer: what gets stripped, what
gets demoted, how long it may be, and how it ends.

## Declare the preset before drafting

One line, first thing, in the document itself:

> *Team read-out · backward · internal · adjacent — state as of 2026-08-31*

Deciding audience after drafting does not work: every rule below changes
what goes in the main flow, and retrofitting them means rewriting. **If you
cannot name the reader, you are writing the internal specialist version** —
say so and move on, rather than inventing a general audience you have not
got.

## The dials

Two, orthogonal, both new; tense already exists in SKILL.md.

| dial | values | what it controls |
|---|---|---|
| **access** | `internal` / `circulated` | what gets **stripped** (deleted) |
| **altitude** | `specialist` / `adjacent` / `non-specialist` | what gets **demoted** (collapsed) |

`adjacent` means a technical colleague from a neighbouring field: fluent in
models and statistics, innocent of *this* project's vocabulary. It is the
most common real reader and the one most often written past.

The reader's job — understand / decide / implement — is not a third dial. It
falls out of tense and access: backward → understand, forward+internal →
decide, forward+circulated → decide or implement (see plan.md § *Handovers*).

**Strip and demote are different operations, and the distinction is
load-bearing.** Stripping deletes: a where-it-lives pointer is a dead link
for an outside reader, so it goes. Demoting collapses: a σ-calibration
number an outside reader does not need still traces to the record, so it
moves into `<details>` rather than out of the file. One authored source
serves every altitude; two drafts drift.

## Presets

| preset | tense | access | altitude | ends in |
|---|---|---|---|---|
| **arc explainer** | backward | internal | specialist | quiz, 5 questions |
| **team read-out** | backward | internal | adjacent | quiz, 3 questions |
| **outward brief** | backward | circulated | non-specialist | takeaways + the ask |
| **plan brief** | forward | either | adjacent | decision register |
| **handover** | forward | circulated | specialist | executable checklist |

Rules attach to the **dials**, not to the presets — so a preset you invent
(a circulated adjacent read-out for a partner team, say) inherits the right
behaviour without a new rule being written.

## access = circulated → strip

1. **Where-it-lives pointers** (paths, PR numbers, record IDs, "what this
   touches"). Dead links that imply a substrate the reader cannot open, and
   they pull the eye to plumbing instead of the argument. If an act depends
   on an artifact the reader *can* open, cite it normally in prose.
2. **Any named person's capacity.** State the scheduling constraint ("this
   phase needs one person's undivided attention for ~3 weeks and cannot be
   parallelised"), never the judgement about the person. Ownership rows say
   what someone would *carry*, never how much they have left.
3. **Session shorthand and internal identifiers** — `exp15`, `R3`, `gate A`
   — unless the document defines them and they earn their keep. Prefer the
   thing over its handle: "the deployment checkpoint", not "exp15".

Write the internal version, then strip. Deriving keeps them from drifting.

## altitude → the layers invert

Not "add more glosses". At broader altitude the plain layer *becomes* the
document and the technical layer demotes beneath it.

| | specialist | adjacent | non-specialist |
|---|---|---|---|
| main-flow prose | technical | technical, each act opened by one plain-words line | plain throughout |
| figures | support the prose | ≥1 per act | **carry the argument**; prose supports |
| glossary | if more than a handful of terms recur | mandatory, after the background | mandatory, **before** the background |
| numbers per act | every load-bearing one | the load-bearing ones | **one** |
| equations | inline MathML | inline MathML | demoted |
| method detail | main flow | main flow | `<details>`, labelled *for the record* |

Two notes on the ends of that table:

- **Glossary position is not cosmetic.** A reader who lacks the words cannot
  read the background *that teaches them the words* — at non-specialist
  altitude the glossary comes first, and stays bidirectionally anchored
  (SKILL.md's rule) so no one scrolls hunting.
- **"One number per act" is a discipline, not a limit on rigour.** Pick the
  number that would change the reader's mind and demote the rest. Three
  numbers in a paragraph a non-specialist reads once are zero numbers.

## Terseness — ceilings, not targets

"Aim for ~10 minutes" failed in practice. Measured across eight artifacts of
one real project, the internal arc explainers came in at 945–1254 main-flow
words — comfortable — while the document written for the broadest audience
reached **3343**, four times what that audience needed and the longest thing in
the set. The pattern is not an accident: broad-audience documents attract
background, and background is where padding hides. A target you can overshoot
fourfold is not a constraint. Use ceilings.

| preset | ceiling |
|---|---|
| arc explainer · specialist | ≤ 2000 words |
| team read-out · adjacent | ≤ 1200 words |
| outward brief · non-specialist | ≤ 800 words |
| plan brief | ≤ 1500 words + the register |
| handover | no ceiling — completeness beats brevity for an implementer |

**Counted:** main-flow prose only. Figure captions, the glossary, demoted
`<details>` blocks, the quiz and the register do not count — otherwise the
demote rule and the ceiling fight each other.

**Over ceiling → split into acts or cut. Never a longer document.** Count
before shipping; it belongs beside the scripts-off check in SKILL.md's
verification, and it is one line:

```python
# count main-flow prose only
t = open(path, encoding='utf-8').read()
t = t[t.index('<body>'):]
t = re.sub(r'<(script|style|svg|figcaption|details)\b.*?</\1>', ' ', t, flags=re.S)
for cls in ('gloss', 'meta', 'foot', 'qz'):          # glossary, declaration
    t = re.sub(r'<(\w+)[^>]*class="[^"]*\b%s\b[^"]*".*?</\1>' % cls, ' ', t, flags=re.S)
print(len(re.sub(r'<[^>]+>', ' ', t).split()))
```

The ending — quiz, register, checklist — is excluded as apparatus. **The
takeaways/ask ending of an outward brief is not**: it is prose the reader
reads, and exempting it would let the shortest document quietly grow the
section that matters most.

### The cut list — delete on sight

- Prose restating what a figure already shows.
- Chronology that changed no decision. ("Then we tried X, then Y" is only
  worth words if X's failure is why Y exists.)
- Hedging stacks: *appears to suggest that it may potentially*. Pick one
  hedge or none; an honest negative stated plainly is shorter and stronger.
- A second example making the point the first one made.
- Method detail with no consequence for the reader — demote it.
- Any sentence that survives its own deletion.
- Preamble announcing what the document will do. The document does it.

Terseness never buys itself with omitted negatives, missing provenance
labels, or an unstated assumption. Those are the content; verbosity is the
packaging.

## Endings

| preset | ending | gates |
|---|---|---|
| arc explainer | quiz, 5 questions | your green-light of the next arc |
| team read-out | quiz, 3 questions | the same, cheaper |
| outward brief | 3 takeaways + **the ask** + **what would change our mind** | the reader knowing what you want from them |
| plan brief | decision register ([decision-register.md](decision-register.md)) | alignment — silence is not consent |
| handover | executable checklist, pass condition per step | done-ness, checkable without you |

**Invariant: the internal version always carries the quiz.** The quiz
regulates *your* loop — the next arc is not green-lit until the human can
pass the previous arc's quiz — so it is about the owner, not the reader.
Quizzing a supervisor or a client has no gating function and reads as
patronising, so the circulated version drops it. Dropping it is a **strip
from a version that had one**, never an authoring shortcut: a circulated
brief written without an internal quiz behind it has silently removed the
speed regulator.

An outward brief's ending carries a specific weight the quiz does not:
**what would change our mind.** It is what makes a confident summary
arguable rather than promotional, and it is the section a reader with
authority actually engages with.

## Worked example — one finding at three altitudes

From the atmo-scale temporal-interpolation project: a model interpolates
6-hourly reanalysis wind to hourly, sampled trajectories restore the storm
peaks that deterministic prediction smooths away — and then a review found
the sampling noise is spatially uncorrelated, so the gain does not reach the
storm-surge numbers the catalogue exists to produce. Same finding, three
documents.

**specialist** (arc explainer, main flow, all numbers):

> Sampled AR(1) trajectories at the measured residual correlation
> (ρ ≈ 0.65 / 0.67 / 0.55 for u10 / v10 / msl) damp the top-0.1 % wind peak
> by −0.51 m/s against −0.72 deterministic and −1.58 linear. But ε is drawn
> per pixel: adjacent-pixel correlation ≈ −0.005 (measured). Over a surge
> fetch the perturbation area-averages out, and the gate-A runs show it —
> sampled median ≡ predictive mean at Helgoland (−3.7 cm both). Pointwise
> extreme realism does not transfer to spatially integrated quantities;
> surge-level spread would need a fitted spatial scale in the noise model,
> which is an escalation, not a tuning.

**adjacent** (team read-out — plain-words opener, then the technical line,
one figure, internal pointers kept):

> *In plain words: the randomness we add fixed the peaks at each individual
> grid point, but it cancels out when you average over a whole storm — so
> the water-level numbers never saw the improvement.*
>
> The sampler adds temporally correlated noise per pixel and no spatial
> correlation, so area-integrated wind stress is effectively the predictive
> mean. Peak damping improves 0.72 → 0.51 m/s pointwise; the surge peak does
> not move (−3.7 cm, sampled ≡ mean). Recorded as a caveat on the method
> page rather than fixed: a spatially correlated noise model is a
> substantive change and nothing yet requires surge-level spread.

**non-specialist** (outward brief — figure carries it, one number, method
demoted):

> Coarse weather data smooths storms out, and a smoothed storm makes a
> smaller flood. Our model rebuilds the missing detail, and the rebuilt
> storms drive water levels within **±5 cm** of the real ones. One caveat we
> found ourselves: the part of the fix that restores gusts works point by
> point, so it improves wind statistics without changing the flood numbers —
> those come out the same as before. That is a limit on what the method
> claims, not a fault in the water levels.
> <details><summary>For the record — how the wind detail is restored</summary>
> …spatially white AR(1) noise, ρ ≈ 0.65, adjacent-pixel r ≈ −0.005…
> </details>

Note what stayed constant: the honest negative is in all three. Altitude
changes vocabulary, figure load and how many numbers survive — never whether
the reader is told the bad news.
