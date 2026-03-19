# AI Marketplace

A plugin marketplace that works with both **Claude Code** and **Cursor**.

## How It Works

This repo uses a single canonical set of plugin files (manifests, skills, agents) that is
symlinked into both the `.claude-plugin/` and `.cursor-plugin/` directory trees, so
one plugin definition satisfies both tools without duplication.

```
.claude-plugin/marketplace.json          ← canonical marketplace manifest
.cursor-plugin/marketplace.json          → symlink to above

plugins/<name>/plugin.json               ← canonical plugin manifest
plugins/<name>/.claude-plugin/plugin.json → symlink to above
plugins/<name>/.cursor-plugin/plugin.json → symlink to above

plugins/<name>/skills/<skill>/SKILL.md   ← works for both (name + description in frontmatter)
plugins/<name>/agents/*.md               ← works for both (name + description in frontmatter)
plugins/<name>/rules/*.mdc               ← Cursor-only (always-on rules)
```

## Included Plugins

| Plugin | Description |
|--------|-------------|
| `git-workflows` | Commit, PR, CI fix, and merge conflict skills |

## Install in Claude Code

```shell
/plugin marketplace add github:snowflake-eng/ai-marketplace
/plugin install git-workflows@ai-marketplace
```

## Install in Cursor

Add via **Settings > Cursor Tab > Marketplace**, pointing to this repository.

## Add a Plugin

See [docs/add-a-plugin.md](docs/add-a-plugin.md).

## Validate

**Claude Code:**
```shell
claude plugin validate .
```

**Cursor:**
```bash
nix-shell -p nodejs_22 --run "npm run validate"
```
