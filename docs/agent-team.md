# Agent team

For Mona's Project Pulse dashboard, I will use a small custom agent team orchestrated through GitHub Copilot CLI in a Codespace. The team is designed to split planning, UX, implementation, and coordination into clear responsibilities.

- Orchestrator — Target model: Claude Opus 5.5 (copilot). Responsibility: coordinates the full workflow, breaks the dashboard work into phases, delegates tasks to specialists, and verifies that the integrated result fits the project goals. Definition: `.github/agents/orchestrator.agent.md`.
- Planner — Target model: Claude Opus 5.5 (copilot). Responsibility: researches the repository, checks dependencies and edge cases, and produces a practical implementation plan with file ownership, sequencing, validation expectations, and risks. Definition: `.github/agents/planner.agent.md`.
- Coder — Target model: GPT-5.5 (copilot). Responsibility: implements the code for the dashboard within the assigned file scope, including support files when needed for a runnable app such as the Project Pulse preview. Definition: `.github/agents/coder.agent.md`.
- Designer — Target model: Gemini 3.7 Flash (copilot). Responsibility: shapes the dashboard experience, focusing on visual hierarchy, accessibility, usability, responsive design, and polished project-status presentation. Definition: `.github/agents/designer.agent.md`.

This setup lets the Orchestrator manage the work through GitHub Copilot CLI in the Codespace while the specialized agents handle research, design, and implementation without overlapping responsibilities.
