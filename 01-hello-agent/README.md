# Hello Agent

A conversational AI agent built in n8n, powered by Google Gemini 2.0 Flash. This is the foundational project in my agentic AI portfolio - a minimal but complete pattern that demonstrates how triggers, agents, and language models connect to form a working autonomous workflow.

**Built by Trevor Kauyu** · [LinkedIn](https://www.linkedin.com/in/trevor-kauyu/) · [Portfolio](#)

---

## What it does

Hello Agent is a chatbot that accepts a user message, routes it to Google Gemini through n8n's AI Agent node, and returns a response. A system message defines the agent's personality and behavior, so responses stay consistent in tone and length across conversations.

It is intentionally simple. The point is not to impress - it is to demonstrate fluency with the building blocks every more complex agent shares.

## Architecture

```
User message
    │
    ▼
[ Chat Trigger ]  ──►  [ AI Agent ]  ──►  Response
                            │
                            ▼
                    [ Gemini 2.0 Flash ]
                       (Chat Model)
```

Three nodes. Two connections. One working agent.

| Component | Role |
|---|---|
| Chat Trigger | Entry point - fires when a user sends a message via n8n's built-in chat UI |
| AI Agent | Orchestrates the call to the language model, applies the system message, returns the structured response |
| Google Gemini 2.0 Flash | The reasoning model - handles the actual language understanding and generation |

## Stack

- **n8n** (self-hosted via Docker on Windows 11) - workflow orchestration
- **Google Gemini 2.0 Flash** - language model (free tier)
- **Docker Desktop** - local container runtime

## What this project demonstrates

- Setting up and self-hosting n8n locally
- Configuring API credentials inside n8n
- Connecting a language model to an AI Agent node
- Using system messages to control agent behavior
- The core trigger → agent → model pattern that every subsequent project in my portfolio builds on

## Run it yourself

### Prerequisites

- Docker Desktop installed and running
- A Google AI Studio API key (free at [aistudio.google.com](https://aistudio.google.com))

### Steps

1. **Start n8n in Docker:**
   ```bash
   docker run -d --name n8n --restart unless-stopped \
     -p 5678:5678 \
     -v ${HOME}/n8n-data:/home/node/.n8n \
     -e GENERIC_TIMEZONE="America/Phoenix" \
     -e TZ="America/Phoenix" \
     docker.n8n.io/n8nio/n8n
   ```

2. Open `http://localhost:5678` and create your owner account.

3. In n8n, go to **Credentials** → **Add credential** → search for **"Google Gemini(PaLM) API"** → paste your API key → save.

4. **Import the workflow:** in n8n, go to **Workflows** → **Import from File** → select `workflow.json` from this repo.

5. Open the imported workflow, attach your Gemini credential to the Chat Model node if not already linked.

6. Click the **Chat** button at the bottom of the workflow editor and start a conversation.

## Files

- `workflow.json` - the exported n8n workflow (drop it into n8n via Import)
- `screenshots/` - screenshots of the canvas and a sample conversation
- `README.md` - this file

## What I learned

- The AI Agent's "Chat Model" connects underneath the agent node, not in the main left-to-right flow. Once I understood this as "the brain attached to the agent," the visual model clicked.
- The system message has more impact on output quality than I expected. Without it, responses felt generic. With one clear sentence of instruction, the agent felt purposeful.
- Self-hosting n8n via Docker was less intimidating than I expected - one command, one folder, done. The reverse (paying monthly for a SaaS) would have been easier on day one but locks me out of running unlimited experiments.

## What's next

This is the foundation. From here, the portfolio adds:

- **Email triage and routing** - classifying inbound messages and routing them to the right destination
- **Structured output extraction** - turning free-form text into clean, validated data
- **Multi-step agents with tool use** - agents that call external systems and act on the results

Each project builds on the trigger → agent → model pattern shown here.

---

## Contact

Trevor K · [trevor@email.com](#) · [LinkedIn](https://www.linkedin.com/in/trevor-kauyu/) · [GitHub](https://github.com/Travoltah)

Open to conversations about agentic AI workflow automation, no-code AI tooling, and operational automation projects.
