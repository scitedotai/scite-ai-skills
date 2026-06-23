# Scite AI Skills

A shared collection of [**Agent Skills**](https://docs.claude.com/en/docs/claude-code/skills) for use with Claude and Claude Code at Scite / Research Solutions.

## What is a Skill?

A Skill is a folder of instructions, and optionally scripts and resources, that teaches an AI agent how to do a specific task well. Instead of re-explaining the same conventions in every conversation, you package that knowledge once and the agent loads it automatically whenever it's relevant.

Each Skill is a directory containing a `SKILL.md` file with:

- **YAML frontmatter** — a `name` and a `description`. The description is what the agent reads to decide *when* to use the Skill, so it spells out the triggers.
- **Instructions** — the body of the Markdown file, telling the agent how to perform the task.
- **Resources (optional)** — supporting files such as templates, reference docs, or scripts, kept in subfolders like `references/`.

Skills are model-invoked: you don't call them manually. When your request matches a Skill's description, the agent pulls in the instructions on its own. This keeps the base context small while making deep, specialized know-how available on demand.

Learn more in Anthropic's [Agent Skills documentation](https://docs.claude.com/en/docs/claude-code/skills).

## Available Skills

| Skill | What it does |
|---|---|
| [`academic-dashboard`](skills/academic-dashboard) | Renders research dashboards and data views in a clean, journal/preprint visual language, with a locked color encoding for Scite Smart Citations (supporting / contrasting / mentioning). Use it whenever building an HTML dashboard or report from Scite / research literature data. |

## How to install a Skill

Skills live in a `skills/` directory under one of two locations:

- **Personal** — `~/.claude/skills/` — available to you across every project.
- **Project** — `.claude/skills/` inside a repo — shared with everyone who works in that project (commit it to version control).

A Skill is just a folder, so installing one means copying its directory into the right place.

### Option 1 — Clone and copy

```bash
# Clone this repo
git clone https://github.com/scitedotai/scite-ai-skills.git
cd scite-ai-skills

# Install a single skill for your own use (personal)
mkdir -p ~/.claude/skills
cp -r skills/academic-dashboard ~/.claude/skills/

# …or install it into a specific project (shared with the team)
mkdir -p /path/to/your/project/.claude/skills
cp -r skills/academic-dashboard /path/to/your/project/.claude/skills/
```

### Option 2 — Download a single skill without cloning

```bash
# Replace ACADEMIC-DASHBOARD with the skill you want
mkdir -p ~/.claude/skills
git clone --depth 1 https://github.com/scitedotai/scite-ai-skills.git /tmp/scite-ai-skills
cp -r /tmp/scite-ai-skills/skills/academic-dashboard ~/.claude/skills/
rm -rf /tmp/scite-ai-skills
```

After copying, restart Claude Code (or start a new conversation) and the Skill will be picked up automatically. You can confirm it loaded by running `/help` or by asking Claude what skills are available.

## Repository layout

```
scite-ai-skills/
├── README.md
└── skills/
    └── academic-dashboard/
        ├── SKILL.md            # frontmatter + instructions
        └── references/
            └── template.html   # supporting resource
```

## Contributing a Skill

1. Create a new folder under `skills/` named for your skill (kebab-case).
2. Add a `SKILL.md` with `name` and `description` frontmatter. Write the description so it clearly states *when* the skill should trigger.
3. Put any templates, scripts, or reference docs in subfolders (e.g. `references/`).
4. Add a row to the **Available Skills** table above.
5. Open a pull request.

Keep skills focused, self-contained, and portable, so anyone on the team can drop the folder into their `~/.claude/skills/` and have it work.
