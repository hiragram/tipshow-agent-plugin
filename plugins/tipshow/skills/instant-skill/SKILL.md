---
name: instant-skill
description: >
  Search tips.how knowledge base for relevant tips and save them as reusable skill files
  in the project's .claude/skills/ directory. Use this skill when:
  (1) Starting work on a new task — automatically search for relevant knowledge based on
  the task description, target code/tech stack, and plan files
  (2) User explicitly requests knowledge loading (e.g., "load tips", "search knowledge",
  "find relevant tips")
  (3) Working on an unfamiliar domain or technology where tips.how might have useful guidance
  Triggers: manual invocation OR when beginning a task that could benefit from domain knowledge.
---

# Instant Skill

Search tips.how for relevant tips and persist them as skill files for the current project.

## Workflow

### 1. Gather Context

Collect search context from these sources (use whichever are available):

- **User's task instructions** — extract key topics, technologies, and goals
- **Plan files** — read `plan.md` or similar planning documents in the project root
- **Target code** — identify the tech stack, frameworks, and patterns from the codebase (e.g., package.json, Podfile, build.gradle, CLAUDE.md)

### 2. Search tips.how

Use the MCP tools to find relevant tips:

1. **Discover available tags** — call `mcp__plugin_tipshow_tips_how__tags_in_brain` to see what knowledge exists
2. **Narrow by tags** — if relevant tags are found, use `mcp__plugin_tipshow_tips_how__tags_in_brain_and` or `mcp__plugin_tipshow_tips_how__tags_in_brain_or` to explore tag combinations
3. **Semantic search** — call `mcp__plugin_tipshow_tips_how__search_tips` with queries derived from the context (multiple queries with different angles are encouraged)
4. **Get full details** — for promising results, call `mcp__plugin_tipshow_tips_how__get_tip` to retrieve the full tip content

### 3. Evaluate Results

- Discard tips that are too generic or not relevant to the current task
- Group related tips together — they will be combined into a single skill file
- If no relevant tips are found, report that and do not create empty skill files

### 4. Check for Existing Skills

Before saving, check `.claude/skills/` for existing skill files that might overlap:

- Read existing SKILL.md files and compare content
- If overlap is found, ask the user whether to update, merge, or skip

### 5. Save as Skill

Create a skill directory under `.claude/skills/` with the following structure:

```
.claude/skills/<skill-name>/
└── SKILL.md
```

**Naming**: Derive the skill name from the task content in kebab-case (e.g., `swift-concurrency-tips`, `react-testing-patterns`).

**SKILL.md format**:

```markdown
---
name: <skill-name>
description: >
  <Concise description of what knowledge this skill provides and when to use it.
  Include relevant technology names and use cases.>
---

# <Skill Title>

<Synthesized content from multiple tips, organized by topic.
Transform raw tip content into actionable guidance.
Include code examples where available.
Attribute tips by linking to their source when possible.>
```

**Guidelines for content**:
- Synthesize and reorganize — do not just concatenate tips
- Use imperative/infinitive form for instructions
- Keep it concise; remove redundant or obvious information
- Preserve code examples and specific configurations
- Add a "Sources" section at the end listing the original tip titles and IDs

### 6. Report

After saving, briefly report:
- How many tips were found and used
- The skill file path created
- A one-line summary of the knowledge captured
