# AI Council - Multi-Model Deliberation System

The AI Council is a set of three prompts that enable Claude, GPT, and Gemini to collaborate on complex topics through structured deliberation.

## How It Works

The council uses a shared session file in the `/council/` folder to maintain conversation state across models. Each council member:

1. **Reads** the current session state
2. **Analyzes** previous contributions from other members
3. **Adds** their own perspective and arguments
4. **Proposes** or **votes** on consensus when appropriate

## Running a Council Session

Due to GitHub Copilot limitations, models cannot invoke each other automatically. You must manually run each council prompt in sequence:

1. **Start the session**: Run any council prompt (e.g., `/council-claude`) with your topic
2. **Rotate models**: After each response, run the next council prompt (e.g., `/council-gpt`, then `/council-gemini`)
3. **Continue until consensus**: Keep rotating through the prompts until the council reaches agreement

### Example Workflow

```
You: /council-claude "Should we use microservices or a monolith for our new project?"
[Claude creates session file and provides initial analysis]

You: /council-gpt
[GPT reads the session, responds to Claude's points]

You: /council-gemini
[Gemini adds perspective, possibly proposes consensus]

You: /council-claude
[Claude votes on proposal or continues discussion]

... continue until consensus is reached
```

## Session Files

Sessions are stored in `/council/` with the format `council-session-YYYY-MM-DD-HHMMSS.md`. Each session tracks:

- The topic being discussed
- All contributions from each model
- Consensus proposals and votes
- Final decisions

## Best Use Cases

- **Architecture decisions** requiring multiple perspectives
- **Complex technical problems** benefiting from diverse reasoning
- **Risk analysis** where different viewpoints reveal blind spots
- **Strategy development** requiring thorough deliberation
- **Brainstorming** where varied approaches help

## The Three Council Members

| Prompt | Model | File |
|--------|-------|------|
| `/council-claude` | Claude Sonnet 4.5 | [council-claude.prompt.md](../.github/prompts/council-claude.prompt.md) |
| `/council-gpt` | GPT-5 | [council-gpt.prompt.md](../.github/prompts/council-gpt.prompt.md) |
| `/council-gemini` | Gemini 3 Pro | [council-gemini.prompt.md](../.github/prompts/council-gemini.prompt.md) |

## Design Principles

- **Independence**: Each model thinks independently and cannot be pressured into agreement
- **Ownership**: Models only modify their own contributions, never others'
- **Transparency**: All reasoning is documented in the session file
- **Consensus-driven**: Decisions require unanimous agreement from all three models
