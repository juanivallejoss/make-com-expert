# Make.com Expert — Claude Skill

Expert-level [Make.com](https://www.make.com/) (formerly Integromat) skill for Claude. Provides complete knowledge of Make.com's expression language, all built-in functions, date/time tokens, common patterns, and critical syntax rules so Claude can help you write, debug, and optimize Make.com formulas.

## What's included

- **SKILL.md** — Core skill prompt covering syntax rules, all function categories, common patterns, and the most frequent mistakes
- **references/functions-reference.md** — Complete reference for every built-in function (general, math, text, date/time, array) with signatures and examples
- **references/datetime-tokens.md** — Full token tables for `formatDate` and `parseDate`
- **make-com-functions.skill** — Ready-to-import skill file for Claude Desktop (bundles all of the above)

## Installation

### Claude.ai (Web)

1. Go to [claude.ai](https://claude.ai)
2. Open **Settings** → **Capabilities** → **Custom Instructions**
3. Copy the entire contents of [`SKILL.md`](SKILL.md) and paste it into the custom instructions field
4. Save

This gives every new conversation Make.com expertise. For a heavier setup with the full function reference, create a **Project** instead:

1. Create a new Project
2. Upload all three files (`SKILL.md`, `references/functions-reference.md`, `references/datetime-tokens.md`) to the project knowledge
3. Start conversations inside that project

---

### Claude Desktop App (Import .skill file)

The easiest way for Claude Desktop:

1. Download [`make-com-functions.skill`](make-com-functions.skill) from this repo
2. Open Claude Desktop → **Settings** → **Capabilities** → **Skills**
3. Click **Import Skill** and select the downloaded `.skill` file
4. Done — the skill is now active in all your conversations

---

### Claude Code (CLI) & Claude Desktop App (Manual)

Skills can also be installed manually by placing files in the right directory. Works for both Claude Code and Claude Desktop.

#### Option A: Personal skill (available in all projects)

```bash
git clone https://github.com/juanivallejoss/make-com-expert.git ~/.claude/skills/make-com-expert
```

#### Option B: Project-specific skill (available only in one project)

From your project root:

```bash
mkdir -p .claude/skills
git clone https://github.com/juanivallejoss/make-com-expert.git .claude/skills/make-com-expert
```

#### Option C: Manual copy-paste

If you prefer not to use git:

1. Download or copy the contents of this repo
2. Place them in one of these directories:

| Scope | Path |
|---|---|
| Personal (all projects) | `~/.claude/skills/make-com-expert/` |
| Project-specific | `<your-project>/.claude/skills/make-com-expert/` |

The directory should look like this:

```
make-com-expert/
├── SKILL.md
└── references/
    ├── functions-reference.md
    └── datetime-tokens.md
```

3. Restart Claude Code or Claude Desktop.

## Usage

Once installed, just ask Claude anything about Make.com formulas. The skill activates automatically when you mention Make.com topics. Examples:

- *"Write a Make.com formula that formats a phone number"*
- *"How do I calculate the number of days between two dates in Make?"*
- *"Debug this Make.com expression: `if(1.status === "active", "yes", "no")`"*
- *"Convert this JavaScript to a Make.com formula"*

## Why this skill exists

Make.com has its own expression language that **looks like JavaScript but isn't**. The most common source of errors is applying JavaScript syntax (commas, `===`, ternary operators, `.methods()`) where Make.com expects its own syntax (semicolons, `=`, `if()` functions, standalone functions). This skill teaches Claude the differences so it stops guessing and starts giving correct Make.com formulas.

## License

MIT
