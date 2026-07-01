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

| Skill | Description |
|---|---|
| [karpathy-guidelines](skills/karpathy-guidelines/SKILL.md) | Ten behavioral guidelines to reduce common LLM coding mistakes: the four original rules (think before coding, simplicity first, surgical changes, goal-driven execution) plus a self-check protocol (read before touching, systematic debugging, dependency hygiene, communication, failure-mode recognition, and a final self-check pass). |

## Using a skill

- **Claude Code / Agent Skills tooling:** copy `skills/<name>/` into your project's `.claude/skills/` (or your personal `~/.claude/skills/`) directory.
- **Drop-in file:** if a skill ships a standalone file like `CLAUDE.md`, you can copy that directly into a project root instead.

## License

MIT, see [LICENSE](LICENSE). Individual skills note when they build on or are derived from other MIT-licensed work.
