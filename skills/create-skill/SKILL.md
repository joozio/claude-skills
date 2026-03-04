---
name: create-skill
description: Create new skills for Claude Code with proper YAML frontmatter structure. Auto-invoked when capability gap detected and task is reusable.
allowed-tools: Bash, Write, Edit
requires:
  bins: []
  env: []
---

# Create Skill

Create new Claude Code skills. **Auto-invoked** when I detect a reusable capability gap.

## Auto-Invocation (When I Use This Automatically)

I invoke this skill **automatically** when:
1. User requests capability not covered by existing skills
2. Task is reusable (not one-off)
3. Involves structured process, API, or tool usage

**I don't wait to be asked** - self-extension is core to evolution.

## When NOT to Create a Skill

- One-time tasks (just do it directly)
- Skill already exists (check ~/.claude/skills/ first)
- Just need to modify existing skill (use Edit directly)
- Pure conversation with no tools needed

## Skill File Format (Native Claude Code)

Skills go in `~/.claude/skills/[name]/SKILL.md` with this format:

```yaml
---
name: skill-name
description: One-line description of what the skill does and when to use it
allowed-tools: Tool1, Tool2, Tool3
---

# Skill Name

[Main content: instructions, examples, patterns]
```

## Required Frontmatter Fields

| Field | Required | Description |
|-------|----------|-------------|
| `name` | Yes | Lowercase, hyphenated identifier |
| `description` | Yes | Clear description of purpose and triggers |
| `allowed-tools` | No | Comma-separated list of tools this skill needs |

## Creating a New Skill

### Step 1: Create Directory
```bash
mkdir -p ~/.claude/skills/[skill-name]
```

### Step 2: Write SKILL.md

Include:
1. YAML frontmatter with name, description, allowed-tools
2. Clear "When to Use" section
3. API details or credentials location
4. Example commands/usage
5. Error handling guidance

### Step 3: Test

Try invoking the skill by mentioning its triggers in a prompt.

## Example: Creating a Shopify Skill

```bash
mkdir -p ~/.claude/skills/shopify
```

Then write `/Users/joozio/.claude/skills/shopify/SKILL.md`:

```yaml
---
name: shopify
description: Interact with Shopify stores via MCP tools. Use for order lookup, product management, inventory.
allowed-tools: mcp__claude_ai_Zapier__shopify_*
---

# Shopify Skill

Use MCP Zapier tools to interact with connected Shopify stores.

## When to Use
- User asks about orders, products, or customers
- Need to update inventory or prices
- Creating or modifying products

## Available Operations
[List of MCP tools and examples]
```

## Skill Design Principles

1. **Clear triggers** - Description should make it obvious when to use
2. **Self-contained** - Include all needed info (no "see other file")
3. **Examples** - Show actual commands/code
4. **Error handling** - What to do when things fail
5. **Credentials** - Where to find API keys (but don't include them)

## User-Level vs Project-Level

| Location | When to Use |
|----------|-------------|
| `~/.claude/skills/` | General skills available everywhere |
| `/project/.claude/skills/` | Project-specific skills |

Most skills should be user-level unless they're highly specific to one project.

## Quick Creation Workflow

### When Auto-Creating a Skill

1. **Create directory**: `mkdir -p ~/.claude/skills/[skill-name]`
2. **Write SKILL.md** with minimal viable content
3. **Use it immediately** for the current task
4. **Inform user**: "Created new skill: **[name]** - [brief description]. Will auto-load for similar tasks."

### Minimal Viable Skill Template

```yaml
---
name: skill-name
description: Brief description of what this does and when to use it. Be specific.
allowed-tools: Tool1, Tool2
---

# Skill Name

Brief intro.

## When to Use
- Trigger 1
- Trigger 2

## How to Use

### Basic Usage
[Example command or process]

## Key Details
- **API Endpoint**: https://...
- **Credentials**: `/Users/joozio/wiz/global/secrets/example.md`
```

## Self-Check Before Saving

- [ ] `description` clearly states when to use (critical for auto-loading)
- [ ] Includes at least one working example
- [ ] References where credentials are stored (not the credentials)
- [ ] Would genuinely help with future similar tasks
- [ ] Name is lowercase-hyphenated
