# GitHub Copilot Toolkit

![GitHub Copilot Toolkit Hero Image](img/github-copilot-toolkit-hero-image.jpg)
This repository contains my collection of GitHub Copilot [prompts](#included-prompts), [agents](#included-agents), and other tools designed to help enterprises maximize value from GitHub Copilot, especially in large, complex, and legacy codebases.

These resources are:
- **Constantly evolving** – updated based on real-world usage and feedback
- **Enterprise-focused** – optimized for complex organizational needs

## Recommended prerequisites
- VS Code with GitHub Copilot enabled and access to custom prompts/agents. See [official setup guide](https://code.visualstudio.com/docs/copilot/getting-started).
- Basic familiarity with using custom prompts and agents in GitHub Copilot. See [official documentation](https://code.visualstudio.com/docs/copilot/customization/overview).
- A codebase or project where you can test and adapt these tools.

## How to use
- Clone or download this repo, then copy any folders you want (`.github/agents`, `.github/prompts`) into your workspace or profile locations.

- See the diagram below for an example workspace structure:

  ![Agents and Prompts Workspace Structure](img/chatmodes-prompts-workspace.png)
If you want to keep the agents and/or prompts locally without sharing them in your repo, store them in the current [VS Code profile](https://code.visualstudio.com/docs/configure/profiles).

### Prompts

1. Enable prompt files via `setting(chat.promptFiles)`.

   ![Prompt Files Setting](img/vs-code-prompt-files.png)

2. Run the prompts with `/prompt-name` (for example `/why-this-way.prompt.md`) in the chat window.

   ![Run Prompt Command](img/run-prompt-in-chat.png)

3. More information about working with prompts is available in the [official documentation](https://code.visualstudio.com/docs/copilot/customization/prompt-files).

### Custom agents

1. Select an agent by clicking the agent picker in the chat window.

   ![Agent Picker](img/select-custom-chat-mode.png)

2. You can simply start chatting with the selected mode active. Even a message like `Start` is enough to trigger the agents's behavior.

   ![Start Agent](img/start-chat-mode.png)

3. More information about working with custom agents is available in the [official documentation](https://code.visualstudio.com/docs/copilot/customization/custom-agents)

## Included Agents

![Dead Code Detective](img/dead-code-detective.jpg)
**[Dead Code Detective](.github/agents/dead-code-detective.agent.md)**: Systematically identifies unused code, functions, classes, and dependencies using a safety-first approach that checks for dynamic invocation, reflection, and configuration-driven usage patterns. Categorizes findings by confidence level and includes handoffs to review results, create removal plans, and execute cleanup safely.

![Monolith Splitter](img/monolith-splitter.jpg)
**[Monolith Splitter](.github/agents/monolith-splitter.agent.md)**: Analyzes monolithic codebases to suggest modularization seams, domain cuts, and incremental extraction strategies. Measures coupling metrics, identifies global state traps, and generates detailed Split Blueprints with phased rollout plans, safety nets, and rollback procedures. Supports any monolith type with handoffs for planning, execution, and iterative analysis.

## Included Prompts

![Why This Way?](img/why-this-way.jpg)
**[Why This Way?](.github/prompts/why-this-way.prompt.md)**: Investigates puzzling code by analyzing its purpose, reviewing git history, and examining architectural context. Generates a report explaining what the code does, why it exists, and whether refactoring would be beneficial.

![Legacy Architecture Map](img/legacy-architecture-map.jpg)
**[Legacy Architecture Map](.github/prompts/legacy-architecture-map.prompt.md)**: Systematically explores codebases to create or refine architecture maps, identifying entry points, modules, layers, data flow, and dependencies. Works in both initial analysis and refinement modes, producing structured documentation with Mermaid diagrams.

![Dependency Chain Analyzer](img/dependency-chain-analyzer.jpg)
**[Dependency Chain Analyzer](.github/prompts/dependency-chain-analyzer.prompt.md)**: Traces complete dependency chains for the active file in both directions, mapping transitive relationships multiple levels deep. Identifies circular dependencies, calculates blast radius, and supports iterative refinement of existing analyses.

![AI Feature Ideation](img/ai-feature-ideation.jpg)
**[AI Feature Ideation](.github/prompts/ai-feature-ideation.prompt.md)**: Guides teams to elicit priorities, scan opportunity areas, and produce a sequenced AI feature roadmap (low-lift wins → bigger bets) with data needs, guardrails, and success signals tailored to the application.

![AI Council](img/ai-council-prompt.jpg)
**[AI Council](docs/ai-council.md)**: A multi-model deliberation system where Claude, GPT, and Gemini collaborate through structured debate to reach consensus on complex topics. Requires manual rotation between three prompts (`/council-claude`, `/council-gpt`, `/council-gemini`). See the [documentation](docs/ai-council.md) for usage instructions.

## Contributing
- Issues and PRs are welcome; please include context, repro steps (if applicable), and which prompt/agent you’re adjusting.
- Keep additions consistent with the existing format (frontmatter, headings, images, and concise descriptions).

## Licensing
- Content in this repo is provided under the terms of the accompanying [`LICENSE`](LICENSE) file.