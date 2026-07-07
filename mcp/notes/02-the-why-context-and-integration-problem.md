# The Why: MCP and the N×M Integration Problem

**Course:** mcp · **Video:** [The Why](https://youtu.be/Zmy439spZB4) · **Watched:** 2026-07-07

## TL;DR
As chatbots got the ability to call external tools, every AI client ended up writing its own custom integration for every service it needed — an N×M problem (N chatbots × M services = N×M functions to build and maintain). MCP fixes this by standardizing a client-server protocol where the *service* builds one server that any MCP-compliant AI client can use, turning N×M into N+M and moving that integration work off the client entirely.

## Core Concepts
- **Context** (see [`_meta/glossary.md`](../_meta/glossary.md)) — everything an AI can see when generating a response. In a simple chat it's just conversation history; in real professional work it's scattered across a Jira ticket, a codebase, a database schema, a Google Doc, and a Slack thread. MCP's name (Model *Context* Protocol) points directly at this problem.
- **The fragmentation problem** — after ChatGPT's API let every piece of software bolt on AI (Copilot in Office, AI in Google Workspace, Cursor, Perplexity), each tool's AI became its own island: Notion's AI has no idea what Slack's AI is discussing. The vision was one unified AI agent that sees your *whole* work; the reality was five disconnected AI silos, each needing manual copy-paste to bridge — turning developers into "human APIs" assembling context by hand. Not scalable past a handful of tools.
- **Function/tool calling** (see glossary; OpenAI, mid-2023) — let an LLM call an external function instead of just chatting, automating context-fetching (e.g. "check if I have a new Jira ticket" instead of copy-pasting the ticket). This genuinely solved the copy-paste problem — until it hit scale.
- **The N×M integration problem** — once companies had multiple chatbots (a general one, a coding agent, an analytics agent) each needing to connect to many services (Jira, GitHub, MySQL, Drive, Slack...), every chatbot × service pair needed its own hand-written function: its own auth, its own data format handling, its own error handling. 3 chatbots × 20 services = 60 integrations to build *and* maintain — a full team's job, ironically making the "make devs' lives easier" project require hiring more devs. One upstream API change breaks every integration built against it, and credentials scattered across 60 files is a security liability.
- **MCP's fix** (see glossary) — two entities, **client** (the AI chatbot — Claude, Cursor, Perplexity) and **server** (the service — GitHub, Drive, Slack), talking a shared protocol. The key shift: **the server does all the heavy lifting** — auth, rate limiting, data-format translation, error handling — while the client just connects (one JSON config entry, no integration code). This reduces N×M to N+M, and even that N+M work shifts onto the service providers themselves (GitHub writes its own official MCP server once; every AI client reuses it), rather than every chatbot builder repeating it per service.
- **Why it's compounding into a standard** — popular clients (Claude Desktop, Cursor, Perplexity) publicly supporting MCP pressures services to ship official MCP servers; more servers make MCP more valuable to the *next* new chatbot (connect to thousands of servers on day one, zero code) — a network effect. Not adopting MCP means being cut off from that ecosystem and writing custom integrations the old way.

## How This Connects
- [[01-trailer-ai-newsletter-demo]] — the "config, not code" pattern from the newsletter demo (one JSON entry per tool in `claude_desktop_config.json`) is this video's core claim made concrete: the client did nothing but connect; the server (Drive, GitHub, Twitter's MCP server) did the heavy lifting.
- [[../langgraph/notes/02-what-is-agentic-ai]] — "context awareness" and tool use as agent characteristics map directly onto this video's "context" and "function calling" definitions.
- Added to [`_meta/glossary.md`](../_meta/glossary.md): **Context (LLM)**, **Function Calling / Tool Calling**, **MCP (Model Context Protocol)** — later notes should link back rather than re-explain these.

## Self-Test
- Q1 — Function/tool calling already let an LLM fetch its own context automatically. What specifically broke at scale, and why?
- Q2 — In MCP, which side (client or server) owns auth, rate limiting, and error handling — and what does that mean for the code you write when adding a new tool to your chatbot?
- Q3 — Why does N×M → N+M matter for *who* writes the integration, not just how many exist?

---
