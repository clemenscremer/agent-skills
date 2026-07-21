# Examples

Two real instances from the project where this practice was hardened
(a storm-surge research codebase where the human named "keeping up with what
we accomplished" as the bottleneck):

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
