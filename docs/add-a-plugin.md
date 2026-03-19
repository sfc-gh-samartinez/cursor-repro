# Add a Plugin

Follow these steps to add a new plugin that works in both Claude Code and Cursor.

## 1. Create the plugin directory

```bash
PLUGIN=my-plugin

mkdir -p plugins/$PLUGIN/.claude-plugin
mkdir -p plugins/$PLUGIN/.cursor-plugin
mkdir -p plugins/$PLUGIN/assets
mkdir -p plugins/$PLUGIN/skills
mkdir -p plugins/$PLUGIN/agents
```

## 2. Create the shared plugin manifest

Create `plugins/$PLUGIN/plugin.json`:

```json
{
  "name": "my-plugin",
  "displayName": "My Plugin",
  "version": "0.1.0",
  "description": "What this plugin does.",
  "author": {
    "name": "Your Org"
  },
  "license": "MIT",
  "keywords": ["keyword1", "keyword2"],
  "logo": "assets/logo.svg"
}
```

Then symlink it into both tool directories:

```bash
ln -s ../plugin.json plugins/$PLUGIN/.claude-plugin/plugin.json
ln -s ../plugin.json plugins/$PLUGIN/.cursor-plugin/plugin.json
```

## 3. Add a logo

Create `plugins/$PLUGIN/assets/logo.svg` (or `.png`). The Cursor validator checks
that this path resolves.

## 4. Add skills

Skills are slash commands. Each skill lives in its own subdirectory.

Create `plugins/$PLUGIN/skills/my-skill/SKILL.md`:

```markdown
---
name: my-skill
description: One-sentence description of what this skill does and when to invoke it.
---

# My Skill

Detailed instructions for the AI here.
```

**Frontmatter rules:**
- `name` — required by Cursor, harmless in Claude Code
- `description` — required by both

## 5. Add agents (optional)

Agents are sub-agents with a specific persona. Create `plugins/$PLUGIN/agents/my-agent.md`:

```markdown
---
name: my-agent
description: What this agent specializes in and when to invoke it.
---

You are a specialist in ...
```

## 6. Add Cursor-only rules (optional)

Rules are always-on instructions applied when file globs match. They are Cursor-specific
and ignored by Claude Code.

Create `plugins/$PLUGIN/rules/my-rule.mdc`:

```markdown
---
description: Short description of what this rule enforces.
globs: src/**/*.ts
alwaysApply: false
---

Instructions that apply when the glob matches...
```

## 7. Register in the marketplace manifest

Edit `.claude-plugin/marketplace.json` and add an entry to the `plugins` array:

```json
{
  "name": "my-plugin",
  "source": "my-plugin",
  "description": "What this plugin does."
}
```

The `source` value is the folder name under `plugins/` (the `pluginRoot` prefix is
applied automatically by both tools).

## 8. Validate

```bash
# Claude Code
claude plugin validate .

# Cursor
node scripts/validate.mjs
```

Fix all errors before committing.

## Compatibility Checklist

- [ ] `plugin.json` satisfies both schemas (has `name`, `displayName`, `version`, `description`, `author`, `logo`)
- [ ] `.claude-plugin/plugin.json` and `.cursor-plugin/plugin.json` are symlinks to `../plugin.json`
- [ ] All `SKILL.md` files have both `name` and `description` in frontmatter
- [ ] All agent `.md` files have both `name` and `description` in frontmatter
- [ ] Logo path in `plugin.json` resolves to a real file
- [ ] Plugin is registered in `.claude-plugin/marketplace.json`
