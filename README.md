# 🌌 Nightjar Skyworks: Agent-Powered Business Assistant

EECE 503P/798S, Agentic Systems, C3 assignment.

**Vega** is the virtual night-sky concierge of *Nightjar Skyworks*, a fictional Lebanese company that runs guided stargazing tours, astrophotography workshops and school field nights in the Ehden highlands. It is built on the Gemini API (`google-genai`) and demoed through Gradio.

## What it does
| Requirement | Where |
|---|---|
| Business identity (PDF + TXT) | `me/about_business.pdf`, `me/business_summary.txt` |
| Persona and instructions, labeled separately | Notebook §3 (`PERSONA`, `INSTRUCTIONS`) |
| Router (general question / lead / feedback) | Notebook §5: LLM classifier with structured output and a keyword fallback; each intent gets its own guidance, tool set and tool forcing |
| Tools: `record_customer_interest`, `record_feedback` | Notebook §4: print a push notification and append to `logs/*.jsonl`, documented with MCP-style `inputSchema` / `outputSchema` |
| System prompt + chat loop with history and tools | Notebook §6–7 |
| **Bonus:** reflection with logged draft and revision | Notebook §8, `logs/reflections.jsonl` |
| Gradio `ChatInterface` | Notebook §10, with a live agent-trace panel (route, tool calls, reflection) |

## Run it
```bash
pip install -r requirements.txt
cp .env.example .env        # then put your GEMINI_API_KEY in .env
jupyter notebook business_agent.ipynb   # Run All; the Gradio app opens at http://127.0.0.1:7860
```

The free Gemini tier allows only about 20 requests per day **per model**, and each chat turn makes 2 to 3 calls. That is why the router, the agent and the reflection step each use a different model (configurable in `.env`).

## Project structure
```
business_bot/
├── me/
│   ├── about_business.pdf
│   └── business_summary.txt
├── business_agent.ipynb
├── logs/                  # leads.jsonl, feedback.jsonl, reflections.jsonl (created at runtime)
├── .env.example
└── requirements.txt
```
