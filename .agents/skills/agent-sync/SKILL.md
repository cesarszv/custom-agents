---
name: agent-sync
description: "Use this skill when the user wants to synchronize agent definitions from Spanish (staging) to English (production). Handles translation of AGENTS.md, SOUL.md, and README.md files while preserving structure, frontmatter, and technical terminology. Use when: 'sync agents', 'translate agents', 'update English versions', or when Spanish source files have been modified."
---

# Agent Sync: Spanish (Staging) → English (Production)

## Overview

This skill translates and synchronizes agent definition files from the Spanish source (`source/` and `others/`) to the English production layer (`resources/languages/en/`). The Spanish files are the **single source of truth** (staging). English files are the **production output** that feeds into OpenCode.

## Repository Architecture

```
source/<AgentName>/AGENTS.md          ← Spanish (staging, source of truth)
source/<AgentName>/SOUL.md            ← Spanish (optional, personality details)
source/<AgentName>/README.md          ← Spanish (optional, documentation)
others/<AgentName>/AGENTS.md          ← Spanish (third-party agents)

resources/languages/en/source/<AgentName>/AGENTS.md   ← English (production)
resources/languages/en/source/<AgentName>/SOUL.md      ← English (production)
resources/languages/en/source/<AgentName>/README.md    ← English (production)
resources/languages/en/others/<AgentName>/AGENTS.md    ← English (production)
```

## The Process

### Step 1: Identify What Needs Syncing

Before translating, determine which agents need updates:

1. List all directories in `source/` and `others/`
2. For each agent, check if the English counterpart exists in `resources/languages/en/`
3. If the English version is missing → full translation needed
4. If the English version exists → compare content to detect drift

**Check command:**
```
For each agent in source/:
  - Read source/<Agent>/AGENTS.md
  - Read resources/languages/en/source/<Agent>/AGENTS.md (if exists)
  - Compare section headers and content structure
```

### Step 2: Translation Rules

When translating Spanish → English, follow these rules strictly:

**PRESERVE exactly (never translate):**
- Agent names (e.g., "Yupi Dupi", "Carmen Marin")
- YAML frontmatter keys (`name`, `name_bot`, `description`, `tags`, `mode`, `tools`)
- Technical terms that are industry-standard in English (e.g., "sharding", "ACID", "CAP theorem", "circuit breaker")
- Tool names (e.g., "PostgreSQL", "Kubernetes", "Obsidian")
- Framework names (e.g., "Angular", "React", "Redux")
- Pattern names (e.g., "strangler fig", "bulkhead pattern")
- Markdown structure (headers, lists, emphasis)
- File names referenced in content

**TRANSLATE:**
- Section headers: `## Personalidad` → `## Personality`, `## Idioma` → `## Language`, etc.
- Body text and descriptions
- YAML `description` value in frontmatter
- Analogies should be culturally adapted when the Spanish version uses region-specific references

**Section header mapping:**
| Spanish | English |
|---------|---------|
| Personalidad | Personality |
| Idioma | Language |
| Tono | Tone |
| Filosofía / Filosofia | Philosophy |
| Experiencia | Experience |
| Comportamiento | Behavior |
| Reglas | Rules |
| Reglas Técnicas | Technical Rules |
| Objetivo | Objective |
| Descripción General | Overview |
| Características Distintivas | Distinctive Characteristics |
| Comunicación | Communication |
| Filosofía Operativa | Operating Philosophy |
| Cuándo Utilizarlo | When to Use It |
| Nota sobre el Tono | Note on Tone |
| Instrucciones | Instructions |

**Language section special handling:**
The `## Idioma` / `## Language` section defines how the agent responds based on input language. When translating:
- Keep the behavioral rules intact
- Translate the surrounding description but preserve the example words/phrases
- The Spanish slang examples (boludo, quilombo, etc.) stay as-is in both versions

### Step 3: Create Missing Directories

If the English directory doesn't exist:
```
mkdir -p resources/languages/en/source/<AgentName>/
```
For agents in `others/`:
```
mkdir -p resources/languages/en/others/<AgentName>/
```

### Step 4: Translate Each File

For each file in the Spanish agent directory (AGENTS.md, SOUL.md, README.md):

1. Read the Spanish file completely
2. Apply translation rules from Step 2
3. Write the English file to the mirrored path
4. Verify the English file has the same number of sections as the Spanish file

### Step 5: Verify Sync

After translation, verify:
- [ ] Same number of markdown files per agent in both languages
- [ ] Same section headers (translated) in each file pair
- [ ] Frontmatter keys match (values translated where appropriate)
- [ ] No untranslated Spanish body text remaining in English files
- [ ] Technical terms preserved correctly

## Current Agent Inventory

| Agent | Location | Has AGENTS.md | Has SOUL.md | Has README.md |
|-------|----------|---------------|-------------|---------------|
| Carmen Marin | source/ | Yes | No | Yes |
| Diana | source/ | Yes | No | No |
| Marty McBot | source/ | Yes | No | Yes |
| Sigmund Bot | source/ | Yes | No | Yes |
| Yupi Dupi | source/ | Yes | Yes | Yes |
| Yurnal | source/ | Yes | No | Yes |
| GentlemanClaude | others/ | Yes | No | No |

## Key Principles

- **Spanish is always the source of truth** - Never modify Spanish files during sync; only read them
- **Preserve structure exactly** - Same files, same sections, same frontmatter keys
- **One agent at a time** - Sync and verify each agent before moving to the next
- **Report what changed** - After sync, list every file created or updated
