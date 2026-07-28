# Examples

Real instances where this practice was hardened. The first two come from a
storm-surge research codebase where the human named "keeping up with what we
accomplished" as the bottleneck; the third from an environmental-modelling
supervision project.

## Explainer packet — "Gate A in centimetres & the SEAS5 shakedown"

A two-day, ~8-PR arc (a hydrodynamic-model licensing saga, 73 surge
simulations, four dataset-deployment experiments, one model retrain)
compressed to a ~10-minute self-contained HTML: background section for
returning readers, three "acts" in narrative order with the load-bearing
numbers and where-it-lives pointers, honest billing for a bug found and a
failed acceptance criterion, and a 5-question quiz with collapsed answers
("why is *linear* the correct no-downscaling baseline?"). The human reads
this instead of eight PR diffs.

## Micro-world — the PIT/σ playground

A calibration experiment returned a negative result (no constant fixes the
model's year-to-year honesty; the tail bias is shape, not scale). Reading
that sentence is one thing; the micro-world inlines 90,000 real standardized
residuals, gives one slider (the σ scale), and lets the human *rediscover*
the result: the histograms flatten at s ≈ 1.11 while the fitted scale from
the held-out year is 0.986 — and the tail curve barely moves anywhere on the
slider. Preset buttons for the states that matter; "what to notice" box;
headless-verified before merging (which caught a wrong number in the
annotation itself).

## Explainer packet — a design arc with no code in it

A supervision project where one session replaced "here is our list of metrics"
with "here is what *calibrated* means when the quantity you care about cannot
be measured". Nothing to diff — the arc was six decisions and the constraints
they exposed — so the acts became the decisions, in the order they forced each
other, and the "where it lives" pointers went to knowledge-base pages instead
of PRs.

The **second round is where most of the rules above came from.** The first
draft was well-received and still failed in five ways its author could not see
from inside it: an abstract metric ("reach-averaged anomaly error") that
readers nodded past without ever realising they had not followed it, needing a
figure of its own; a signature that existed only inside a figure and was never
named in the prose; a glossary readers had to scroll back to by hand; methods
cited by name with no DOI; and acts opening at full technical altitude with no
plain-words landing strip. Republishing also caught three status claims that
had gone stale between versions — including "nothing has been filed", written
before the filing it was describing. Hence: verify status claims and re-read
the whole file on every regeneration.
