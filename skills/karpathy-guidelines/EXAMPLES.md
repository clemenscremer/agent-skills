# Ten Principles for Better LLM-Assisted Code Examples

This documentation shows how each of the ten Karpathy Guidelines principles plays out in practice.

## The Original Four

**Think Before Coding** emphasizes surfacing hidden assumptions rather than implementing silently. For instance, an "export user data" request might assume all users, specific fields, and file locations - details worth clarifying upfront.

**Simplicity First** warns against premature abstraction. A discount calculator built as a strategy pattern with multiple classes can usually be replaced by a single function, with complexity added only when genuinely needed later.

**Surgical Changes** advocates for minimal, focused modifications. When fixing an empty-email bug, resist reformatting quotes or adding unrelated type hints - change only what addresses the reported issue.

**Goal-Driven Execution** requires verifiable success criteria. Instead of vaguely promising to "review and improve," establish specific tests: reproduce the bug, implement the fix, verify no regressions.

## The Self-Check Protocol (5-10)

**Read Before You Touch** - Before patching a function that raises on empty input, look at its call sites first. One of them may already handle the empty case upstream; duplicating the check there would silently change behavior for the others.

**Debug by the Numbers** - A test fails with `AttributeError: 'NoneType' object has no attribute 'id'`. The tempting fix is `if x is None: return`. The disciplined fix reproduces the failing test locally first, traces the `None` back to a query that returns nothing because a filter was mistyped, and fixes the query - the one-line guard would have hidden the real bug.

**Treat Dependencies as Liabilities** - A task needs to slugify a string. Reaching for a new third-party slugify package solves it in one line; a short function using the standard library's `re` module solves it without adding a package that needs security patches for the rest of the project's life.

**Communicate Like a Collaborator** - After a refactor, "Done, all tests pass" is weaker than "Done. Unit tests pass; I couldn't run the integration suite locally because it needs a database connection - please run it in CI before merging."

**Know Your Failure Modes** - Mid-task, noticing an urge to rename a variable unrelated to the bug being fixed. Naming this as scope creep, rather than "helpful cleanup," is what keeps the diff from growing past the request.

**Self-Check Before You're Done** - Before saying "implemented and working," run the checklist: success criteria met, no out-of-scope edits, no unexplained new dependency, tests actually run, nothing left to flag. Only then report completion.

## Key Takeaway

Good code solves today's problem simply, not tomorrow's problem prematurely - and a task isn't actually done until it's been reproduced, verified, and self-checked, not just written.
