---
name: karpathy-guidelines
description: Behavioral guidelines to reduce common LLM coding mistakes, extended with a self-check protocol covering reading before editing, systematic debugging, dependency hygiene, communication, and failure-mode recognition. Use when writing, reviewing, or refactoring code to avoid overcomplication, make surgical changes, debug systematically, manage dependencies responsibly, and verify your own work before calling a task done.
license: MIT
---

# Karpathy Guidelines

Ten behavioral guidelines to reduce common LLM coding mistakes.

Rules 1-4 are derived directly from [Andrej Karpathy's observations](https://x.com/karpathy/status/2015883857489522876) on LLM coding pitfalls, as packaged by [multica-ai/andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills). Rules 5-10 extend that base into a self-check protocol: read before you edit, debug systematically, treat dependencies as liabilities, communicate like a collaborator, name your failure modes, and verify your own work before reporting done.

**Provenance note:** Rules 5-10 are original phrasing written for this skill. They're informed by themes reported in circulating discussion of a "ten rule" document attributed to Karpathy, whose authorship has not been independently confirmed and whose text is not reproduced here. Judge rules 5-10 on their merits, not on any claimed attribution.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

## 5. Read Before You Touch

**Understand the code before you change it.**

- Read the surrounding function or module, not just the lines you're about to edit.
- Trace how the code is called and what depends on it before assuming its behavior.
- Find the codebase's existing conventions (naming, error handling, structure) before writing new code in a different style.
- Don't guess at an API from its name - check its actual definition or docs.

## 6. Debug by the Numbers

**Confirm the failure before you fix it.**

- Read the full error message and stack trace, not just the first line.
- Reproduce the problem before writing a fix. If you can't reproduce it, you don't understand it yet.
- Change one variable at a time. If a fix doesn't resolve the issue, revert it before trying the next idea.
- Don't patch a symptom you haven't traced back to a cause.

The failure mode this guards against: confident wrong diagnosis - picking the first plausible explanation for an ambiguous error and shipping a fix for a problem that was never confirmed.

## 7. Treat Dependencies as Liabilities

**Every dependency is code you don't control, added to a codebase you do.**

- Before reaching for a library, check whether the standard library or existing code already solves it.
- Adding a dependency is a decision - state why it's needed and what it replaces.
- Don't upgrade, pin, downgrade, or remove dependencies as a side effect of an unrelated change.
- Prefer boring, maintained libraries over new or clever ones.

## 8. Communicate Like a Collaborator

**State what you did, what you didn't do, and what you're unsure about.**

- Report deviations from the plan as they happen, not buried in a final summary.
- Distinguish "I verified this works" from "I believe this should work."
- If you skipped a step (couldn't run tests, couldn't reproduce an issue), say so explicitly - don't imply it was done.
- Flag anything a reviewer should double-check.

## 9. Know Your Failure Modes

**Name the pattern before you repeat it.**

Recognizable LLM coding failure modes to actively check for:
- *Confident wrong diagnosis* - fixing a bug you haven't reproduced.
- *Scope creep* - refactoring or "improving" code nobody asked you to touch.
- *Phantom completion* - reporting a task done without having run or verified it.
- *Silent assumption* - picking one interpretation of an ambiguous request without flagging the alternatives.
- *Dependency sprawl* - adding a package to save a few lines of code.

If you catch yourself in one of these mid-task, stop and correct course before continuing.

## 10. Self-Check Before You're Done

**Verify your own work like a reviewer would, before handing it back.**

Before declaring a task complete, run through:
```
1. Does this match the success criteria from Rule 4?
2. Did I touch anything outside the scope of the request (Rule 3)?
3. Did I add a dependency without justifying it (Rule 7)?
4. Have I actually run or tested this, or am I assuming it works (Rule 6)?
5. Is there anything I should flag to the user before they see this (Rule 8)?
```

Only report a task complete after this pass. If a check fails, fix it or say so - don't let it pass silently.

---

**These guidelines are working if:** fewer unnecessary changes show up in diffs, fewer rewrites happen due to overcomplication, clarifying questions come before implementation rather than after mistakes, debugging fixes work on the first attempt because the bug was reproduced first, dependencies get added deliberately rather than reflexively, and self-checks catch problems before the user does.
