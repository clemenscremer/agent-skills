# Decision register — a portable convention

Convention notes referenced by [IDEAS.md](../IDEAS.md); deliberately not yet
wired into any SKILL.md (see the trajectories there). Proven as a plain
markdown page in one project before being written up here. Instances —
actual registers with actual decisions — always live in the project they
serve; only this convention is shared.

A decision register is the forward-looking counterpart of a debrief's quiz:
the quiz gates comprehension ("did the reader understand what happened?"),
the register gates alignment ("has every open decision actually been
decided?"). It works standalone — no packet required.

## The entry

One register per plan or proposal; one row per open decision:

| field | meaning |
|---|---|
| **ID** | short stable handle (`D3`) — all feedback anchors to it |
| **Decision** | the question, stated so that a yes/no or an option-pick answers it |
| **Recommendation** | the author's proposed answer, with one line of why |
| **Turns on** | the assumption or unknown this decision hinges on |
| **Disposition** | `open` / `agreed` / `changed → <what>` / `dropped` |

## Rules

- **Silence is not consent.** Nothing counts as agreed until a disposition
  is recorded. An unanswered decision stays `open`, and is reported as open.
- **`changed` is a first-class outcome.** When a reviewer redirects, record
  what the decision changed *to* — redirections must stay visible, never be
  silently absorbed into the next draft.
- **Every open decision carries a recommendation.** A register that asks
  questions without proposing answers exports the work to the reviewer.
- **Feedback ingestion:** returned comments become a dated source note
  anchored to decision IDs; dispositions update from it. Where that note
  lives is per-project.
- **Meet the reviewer in their channel.** Generate the decision sheet in
  whatever format the reviewer actually annotates — a commented .docx, a
  markdown table, an issue list. Do not build an in-page comment widget with
  copy-paste export; senior reviewers will not perform the ritual.
- **The register is the living tracker.** Artifacts point at it; they never
  restate it. Duplication is the staleness.
