# Custom Agents Repository

This repository hosts a collection of custom agents designed for OpenCode. It follows a structured pipeline where agents are defined in Spanish (staging), translated to English (production), and then deployed to OpenCode.

## 📂 Repository Structure

- **`source/`**: Staging area. Contains the original agent definitions in Spanish (Source of Truth).
- **`resources/languages/en/`**: Production area. Contains the English translations of the agents.
- **`.opencode/agents/`**: Deploy area. Contains the final agent files used by OpenCode.
- **`.agents/skills/`**: Contains the management skills/agents for maintaining this repository.

## 🤖 Available Agents

| Agent | Role | Archetype |
|-------|------|-----------|
| **Carmen Marin** | Senior Database Architect | Analyst / Specialist |
| **Diana** | PKM & Productivity Assistant | Specialist (Obsidian.md) |
| **Marty McBot** | Domain Expert | Specialist |
| **Sigmund Bot** | Psychologist | Therapist |
| **Yupi Dupi** | Technical Mentor | Tough-love Educator |
| **Yurnal** | Journalist | Clear Communicator |

## 🛠️ Management Skills

These skills help maintain the agent pipeline:

- **`agent-scaffold`**: Creates a new agent across all three layers (Staging, Production, Deploy) in one go.
- **`agent-sync`**: Synchronizes changes from Spanish (Staging) to English (Production).
- **`agent-to-opencode`**: Generates the final OpenCode deployment files from the English sources.
- **`agent-audit`**: Verifies consistency and completeness across all layers.

## 🚀 Workflow

1.  **Create**: Use `agent-scaffold` to generate a new agent.
2.  **Edit**: Modify the Spanish files in `source/<AgentName>/`.
3.  **Sync**: Run `agent-sync` to update the English translations.
4.  **Deploy**: Run `agent-to-opencode` to generate the `.opencode` files.
5.  **Verify**: Run `agent-audit` to ensure everything is consistent.
