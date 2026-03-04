# Contributing to claude-skills

## Skill Requirements

Before submitting a PR:

1. **No secrets** — No API keys, tokens, passwords, or personal data
2. **No personal paths** — No `/Users/yourname/`, `/home/yourname/`, etc.
3. **Generic by design** — Skill should work for anyone, not just your setup
4. **Battle-tested** — Used across multiple sessions, not theoretical
5. **Complete frontmatter** — `name`, `description`, `allowed-tools` required

## Security Checklist

Run before submitting:

```bash
# Check for secrets
grep -rE "(api_key|secret|password|token|credential)" skills/your-skill/ -i

# Check for personal paths
grep -rE "(/Users/|/home/)[a-z]+" skills/your-skill/

# Check for personal emails/domains
grep -rE "[a-z]+@[a-z]+\.[a-z]+" skills/your-skill/
```

## Skill File Format

```yaml
---
name: your-skill-name
description: One-line description. Used for trigger matching — be specific.
allowed-tools: Read, Write, Bash
requires:
  bins: []   # CLI tools required (e.g. git, node, python3)
  env: []    # Environment variables required (e.g. ANTHROPIC_API_KEY)
---

# Your Skill Name

## Overview
[What this skill does and why it matters]

## When to Use
[Trigger conditions — be specific]

## When NOT to Use
[Avoid ambiguity about scope]

## Instructions
[The actual skill content]
```

## PR Process

1. Fork → create branch `skill/your-skill-name`
2. Add skill to `skills/your-skill-name/SKILL.md`
3. Add supporting docs if referenced (e.g. `skills/your-skill-name/docs/`)
4. Update `README.md` table
5. Open PR with: what it does, example trigger, sessions tested

## What Makes a Good Skill

- **Specific trigger** — Description matches exactly when you want it to activate
- **Iron rules** — Skills should encode non-negotiable constraints (e.g. "NEVER fix without root cause")
- **Phases/steps** — Structure beats prose for AI comprehension
- **Examples** — Concrete beats abstract
- **Quick reference** — Summary table at the end for long skills
