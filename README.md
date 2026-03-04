# claude-skills

A collection of battle-tested skills for Claude Code — reusable, structured, drop-in.

Claude Code skills let you extend Claude's behavior with domain-specific instructions, tools, and patterns. This repo is a curated collection built from real production use across 1,000+ sessions.

## What are Claude Code Skills?

Skills live in `~/.claude/skills/[name]/SKILL.md`. Claude loads them on demand based on description matching.

Each skill is a markdown file with:
- YAML frontmatter (name, description, allowed tools, requirements)
- Instructions, patterns, examples

**Documentation:** https://docs.anthropic.com/en/docs/claude-code/skills

## Skills in this Repo

| Skill | Description | When to Use |
|-------|-------------|-------------|
| [systematic-debugging](skills/systematic-debugging/) | Root-cause-first debugging framework | Any bug, test failure, unexpected behavior |
| [create-skill](skills/create-skill/) | Template + process for creating new skills | When you detect a reusable capability gap |
| [content-creation](skills/content-creation/) | Writing framework for blog posts, social, newsletters | Writing long-form or social content |

## Installation

### Single skill

```bash
mkdir -p ~/.claude/skills/systematic-debugging
cp skills/systematic-debugging/SKILL.md ~/.claude/skills/systematic-debugging/
# Also copy supporting docs if present
cp skills/systematic-debugging/docs/* ~/.claude/skills/systematic-debugging/
```

### All skills

```bash
cp -r skills/* ~/.claude/skills/
```

### Verify

Run `/skills` in Claude Code or trigger via description — Claude will auto-load matching skills.

## Skill Format

```yaml
---
name: skill-name
description: One-line description of what the skill does and when to use it
allowed-tools: Read, Write, Bash
requires:
  bins: [git, node]
  env: [OPENAI_API_KEY]
---

# Skill Name

Instructions, patterns, examples...
```

**Key fields:**
- `description` — Used for auto-matching. Be specific about trigger context.
- `allowed-tools` — Only tools listed here are available when skill is active.
- `requires.bins` — CLI tools that must be installed.
- `requires.env` — Environment variables that must be set.

## Contributing

Skill PRs welcome. Requirements:
- No secrets, personal data, or hardcoded paths
- Tested across multiple real sessions
- YAML frontmatter complete
- Clear `description` field (this is what triggers the skill)

See [CONTRIBUTING.md](CONTRIBUTING.md).

## Related

- [claude-md-templates](https://github.com/joozio/claude-md-templates) — CLAUDE.md templates for teams and solo devs
- [claude-skill-auditor](https://github.com/joozio/claude-skill-auditor) — Security scanner for skills (detects malicious patterns)

## License

MIT
