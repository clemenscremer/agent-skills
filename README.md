# agent-skills

A collection of [Agent Skills](https://code.claude.com/docs/en/claude-code-on-the-web) for coding agents - written for Claude but not Claude-specific.

## Structure

Each skill lives in its own directory under `skills/`:

```
skills/
  <skill-name>/
    SKILL.md       # required: YAML frontmatter (name, description, license) + guidance
    ...            # optional supporting files (examples, drop-in configs, references)
```

`SKILL.md` is the canonical file any Agent Skills-compatible tool will load. Some skills also ship a plain drop-in file (e.g. `CLAUDE.md`) for agents or workflows that prefer a single file over the skill format.

## Skills

### Understanding

Skills that keep human understanding in step with agent output — based on Geoffrey Litt's ["Understanding is the new bottleneck"](https://www.geoffreylitt.com/2026/07/02/understanding-is-the-new-bottleneck) (explainer documents, quiz-as-speed-regulator, micro-worlds). They share one premise: the goal is understanding to *participate* in the next decision, not just to verify the last one.

| Skill | Fires on | Description |
|---|---|---|
| [explain-change](skills/explain-change/SKILL.md) | one change (diff / commit / branch / PR / revision) | Self-contained HTML explainer: layered background, intuition with reusable diagrams, literate walkthrough in execution order, interactive 5-question quiz as approval gate. |
| [debrief](skills/debrief/SKILL.md) | close of a work arc (multi-PR / multi-session) | Background-first explainer packet with honest negatives and a check-your-understanding quiz; committed to the project's docs. |
| [micro-world](skills/micro-world/SKILL.md) | behavior easier to inhabit than to read | Single-purpose interactive teaching page on real project data: parameter playground, execution scrubber, or comparison world. |

### Coding discipline

| Skill | Description |
|---|---|
| [karpathy-guidelines](skills/karpathy-guidelines/SKILL.md) | Ten behavioral guidelines to reduce common LLM coding mistakes: the four original rules (think before coding, simplicity first, surgical changes, goal-driven execution) plus a self-check protocol (read before touching, systematic debugging, dependency hygiene, communication, failure-mode recognition, and a final self-check pass). |

## Using a skill

- **Claude Code / Agent Skills tooling:** copy `skills/<name>/` into your project's `.claude/skills/` (or your personal `~/.claude/skills/`) directory.
- **Drop-in file:** if a skill ships a standalone file like `CLAUDE.md`, you can copy that directly into a project root instead.

## License

MIT, see [LICENSE](LICENSE). Individual skills note when they build on or are derived from other MIT-licensed work.
