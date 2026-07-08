# Sample n8n Agentic Workflows

Two production-ready agentic workflows built with [n8n](https://n8n.io), demonstrating multi-agent orchestration, LLM tool use, and real-world API integrations.

---

## Workflows

### 1. J.A.R.V.I.S. - Agentic Personal Assistant

A multi-agent orchestration workflow built around a Master Agent that delegates tasks to three specialized sub-agents via natural language chat.

**Architecture:**
- **Master Agent** - receives chat input, routes requests to the right sub-agent
- **Email Agent** - reads, drafts, sends, replies to, and deletes Gmail messages
- **Calendar Agent** - queries availability, creates and deletes Google Calendar events; uses a Date & Time tool for temporal reasoning
- **Meeting Agent** - fetches meeting transcripts via HTTP (Zoom / meeting notes integration)

**Key patterns:**
- Agent-to-agent delegation via `agentTool` nodes
- Windowed memory per agent (each sub-agent maintains its own context window)
- Shared OpenAI Chat Model (GPT-4) across all agents
- Real-time date/time awareness via the DateTime tool

**Integrations:** OpenAI, Gmail, Google Calendar, HTTP (meeting transcript API)

**Trigger:** Chat interface (`chatTrigger`)

---

### 2. Customer Support Triage Bot

A webhook-invoked agentic workflow that receives a customer support request from a front-end, classifies and responds using an AI agent, logs the interaction to Google Sheets, and optionally sends a follow-up email - all before returning the response to the caller.

**Architecture:**
- **Webhook trigger** - receives POST request from front-end
- **AI Agent** - classifies intent, generates response using GPT-4
- **Google Sheets tool** - appends each interaction to a tracking sheet
- **Gmail tool** - sends follow-up email where appropriate
- **Respond to Webhook** - returns the agent's response to the front-end

**Key patterns:**
- Synchronous webhook request/response loop (front-end waits for agent reply)
- Tool-augmented agent with write access to Sheets and Gmail
- Stateless per-request design (no persistent memory needed)

**Integrations:** OpenAI, Google Sheets, Gmail

**Trigger:** Webhook (POST)

---

## How to Use

1. Import the JSON file into your n8n instance: **Workflows → Import from file**
2. Add your own credentials for each integration (OpenAI, Gmail, Google Calendar, Google Sheets)
3. Update any placeholder values marked `YOUR-CREDENTIAL-ID` or `your-email@gmail.com`
4. Activate the workflow

> These workflows were built and used in real environments. API keys, personal emails, and internal IDs have been removed. Credential setup is required before use.

---

## Tech Stack

- [n8n](https://n8n.io) - workflow automation
- [OpenAI GPT-4](https://openai.com) - LLM backbone
- Gmail, Google Calendar, Google Sheets - via Google OAuth
- HTTP Request - for external API calls (meeting transcripts)

---

Built by [Azmina Janmohamed](https://azmina.vercel.app) - Senior Technical Program Manager specializing in AI-integrated delivery.
