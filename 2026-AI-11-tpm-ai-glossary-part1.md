# 32 AI terms every Technical Program Manager should actually know (Part I)

**2026.AI.11** | And why mine live in a .md file that gets smarter every week

*Michi Goetz — June 10, 2026*

---

About eight months into building the TPM AI Playbook, I noticed something.

Every time I sat down to write a new skill or update my memory files in Cursor, I kept reaching for the same terms. Data layer. Agent contract. Context window. Grounding. Approved stack. They were showing up not just in the code and the prompts, but in the documentation I was writing for myself: the `.md` files that tell my AI tools what I know, how I work, and what my programs look like.

At some point I stopped and counted. Around 80% of the terms I had documented in my own memory files were terms I had encountered by building, not by reading a glossary. The glossary came after. The doing came first.

That realization became this article.

There are plenty of AI glossaries out there. Chantal Cox wrote a good one for product leaders. Digital Applied published 200 terms for agent builders. The AI PM Guru runs a quarterly vocabulary update for PMs. None of them are written for the person running 20 programs across three time zones who also needs to understand what their engineering team is building and govern how it behaves.

So this is the TPM version. 32 terms across two parts. Four buckets. All of them grounded in actual delivery work, not theory. Written for the IC to senior TPM who is starting to build AI systems seriously, not someone looking for prompts to try once.

The organizing frame underneath all of it is a three-layer architecture that emerged from real program delivery: a Data Layer (clean, structured inputs your AI depends on), a Skill Library (reusable workflows that interact with that data), and an Agent Mesh (agents that chain skills together to achieve program goals). Each layer depends on the one below it. The terms in this article map to those layers. Fix the data first. Build the skills in parallel. Deploy agents when both are stable. The outcome is not just faster execution. It is a program that gets smarter over time and keeps working after you leave.

And because a glossary that lives in a Substack article decays, this one also lives on GitHub, in a `.md` file you can pull into your own Cursor or Claude memory setup, contribute to, and keep current as the vocabulary keeps moving. The link is at the end.

---

## Bucket 1: AI fundamentals, through a TPM lens

*You've heard these terms. Here's what they actually mean for the person running the program, not the person building the product.*

---

**1. RAG (Retrieval-Augmented Generation)**
An AI system that pulls from a defined knowledge source before generating a response, instead of relying on what the model was trained on. For TPMs, the question is never "does it use RAG." It's "who owns the knowledge source, how clean is it, and what breaks when it's wrong."
*Ex: Your team ships a RAG-powered status summarizer. Three months later it's surfacing stale data because nobody owns the update cadence. That's a program problem, not a model problem.*
**Use it with: Engineering leads, Data owners, AI governance reviews**

---

**2. Hallucination**
When a model generates confident, plausible, wrong output. For a PM building a chatbot, this is a product quality issue. For a TPM, it's a cross-team trust issue. The wrong output doesn't stay in one place. It travels into status reports, dependency maps, and executive briefings.
*Ex: An AI-generated risk summary cites a dependency that doesn't exist. Three teams reprioritize around it before anyone checks the source.*
**Use it with: Your team, Stakeholders, AI governance reviews**

---

**3. Inference**
The moment an AI model generates a response. Distinct from training. You don't train models in your day-to-day work. You trigger inference, often repeatedly, often at scale. Inference has latency, cost, and failure modes that affect program timelines.
*Ex: Your AI skill runs at every weekly sync. At 8 programs, that's 8 inference calls with 8 sets of inputs that need to be clean, current, and correctly scoped.*
**Use it with: Engineering leads, Budget reviews**

---

**4. Context window**
The maximum amount of information a model can process in a single call. Not a technical curiosity. A hard constraint on what your AI system can see at once. Stuff it beyond the limit and the model degrades or drops content. Underfill it and you're not using it effectively.
*Ex: You feed a model your full program wiki, three meeting transcripts, and a dependency map. Something gets dropped. You need to know what, and why, before you trust the output.*
**Use it with: Engineering leads, Your team when designing AI workflows**

---

**5. Guardrails**
Rules and constraints that limit what an AI system can output or do. For product teams, guardrails are a safety and brand concern. For TPMs, they are a governance and accountability concern: who set them, who can change them, and what happens when a program's AI output violates them.
*Ex: Your AI summarization skill is generating exec-facing status reports. Someone needs to own what it is and isn't allowed to say. That owner is usually you.*
**Use it with: AI governance reviews, Executives, Your team**

---

**6. Evals**
Systematic tests that measure whether an AI system's output meets defined quality criteria. Not a one-time check. A repeatable signal. For TPMs, evals answer the question nobody else is asking: is the AI work on this program actually getting better, or just getting used more?
*Ex: Your team runs a meeting summarization skill weekly. Without an eval, you don't know if it's improving or drifting. With one, you have a baseline to defend or improve.*
**Use it with: Engineering leads, Your team, Program health reviews**

---

**7. Grounding**
Anchoring AI output to a verified source rather than letting the model generate freely. Related to RAG but distinct: RAG is an architectural pattern for retrieval, grounding is a property of any output. You can have grounded output through tool calling against live data, and ungrounded output from a RAG system if the retrieved content is itself stale or wrong. For TPMs managing programs where outputs feed decisions, ungrounded AI is a liability.
*Ex: An AI dependency tracker that pulls from your actual Jira and Confluence is grounded. One that synthesizes from memory is not. The difference shows up when something is wrong and you need to know why.*
**Use it with: Engineering leads, Data owners, Your team**

---

*The terms in this bucket are table stakes. Every PM glossary has them. The difference is what they mean when you are running the program rather than building the product. Bucket 2 is where the architecture conversations are happening right now.*

*The architecture layer that's reshaping how programs get built and run. These terms are showing up in design reviews, job descriptions, and governance conversations. You need to know what they mean before you're in the room.*

---

## Bucket 2: Agentic systems vocabulary

**8. Agent loop**
The repeating cycle an AI agent runs through: read context, decide an action, execute it, observe the result, repeat. Unlike a one-shot prompt, an agent loop continues until it hits a goal or a limit. For TPMs, the loop introduces compounding failure risk. A bad early step doesn't just produce a bad output. It shapes every step that follows.
*Ex: An agent drafting your weekly program brief pulls stale data in step one. Everything it synthesizes after that is confidently wrong.*
**Use it with: Engineering leads, Your team when designing AI workflows**

---

**9. Orchestration**
Coordinating multiple AI agents, tools, or steps into a coherent workflow. Not the same as running one prompt. Orchestration is what makes multi-step AI work possible, and what makes it fragile. For TPMs, orchestration is a program design problem: who owns the workflow, what triggers each step, and what happens when one step fails.
*Ex: A program health agent pulls status from Jira, summarizes meeting notes, and flags risks. Three tools, one workflow, one owner. That owner needs to be named.*
**Use it with: Engineering leads, Your team, AI governance reviews**

---

**10. MCP (Model Context Protocol)**
An open standard for how AI agents connect to external tools and data sources. Think of it as the interface contract between your agent and everything it needs to touch: databases, APIs, documents. For TPMs, MCP matters because it determines what your AI system can actually see and act on, and who controls that access.
*Ex: Your program wiki is the source of truth. Whether your AI agent can read it depends on whether there is an MCP connection built and approved. That approval is a program dependency.*
**Use it with: Engineering leads, Data owners, IT and security reviews**

---

**11. Scaffolding**
The structure built around a raw AI model to make it useful in a real workflow: prompts, memory, guardrails, tool connections, output formatting. The model is the engine. Scaffolding is everything else. For TPMs, scaffolding is where most of the actual program work lives, and where most of the maintenance debt accumulates.
*Ex: Getting a model to summarize a meeting takes one prompt. Getting it to summarize the right meeting, for the right audience, with the right constraints, and store the output somewhere useful - that's scaffolding.*
**Use it with: Engineering leads, Your team, Post-mortems**

---

**12. Multi-agent system**
An architecture where multiple specialized AI agents collaborate on a task, each handling a distinct part of the work. More capable than a single agent for complex workflows. Also significantly harder to debug, govern, and attribute when something goes wrong.
*Ex: One agent pulls program data, a second synthesizes risks, a third drafts the exec summary. When the exec summary is wrong, which agent failed? That question needs an answer before you ship.*
**Use it with: Engineering leads, AI governance reviews, Post-mortems**

---

**13. Human-in-the-loop (2026 meaning)**
In 2022, HITL meant a human reviewed the model's output before it shipped. In 2026, it means a human approves specific actions before an agent takes them. That is a different design problem. For TPMs, the question is not whether to have HITL. It is where to put the checkpoints, what triggers them, and who is accountable when an agent acts without one.
*Ex: Your program agent can update a dependency register automatically. Should it? At what confidence threshold does it act vs. ask? Those are program governance decisions, not engineering ones.*
**Use it with: AI governance reviews, Executives, Your team**

---

**14. Tool calling**
The mechanism by which an AI agent invokes an external system to complete a task. Tool calling is how agents move from answering questions to taking actions. For TPMs, each tool call is a potential failure point, a data access decision, and a governance question bundled together.
*Ex: Your agent calls Jira to pull milestone status. What happens when Jira is down? What happens when the agent misreads the response? Both are program risks, not just engineering ones.*
**Use it with: Engineering leads, Data owners, IT and security reviews**

---

**15. Silent failure**
When an AI system produces output that looks correct but is wrong, and nobody catches it because there is no obvious error signal. The most dangerous failure mode for TPMs because it travels. A silent failure in a risk summary becomes a silent failure in an exec briefing becomes a silent failure in a steering decision. Observability (term 19) is the remedy: the ability to see not just what an AI system did but why.
*Ex: Your AI dependency tracker marks a cross-team blocker as resolved because the ticket was closed. The blocker was not actually resolved. The ticket was just closed early. No alert fires. The program slips.*
**Use it with: Your team, AI governance reviews, Post-mortems (this one is the argument for every other governance investment)**

---

*These are the terms that separate TPMs who understand how agentic systems fail from those who discover it in production. Bucket 3 is where those systems meet organizational reality.*

---

## Where it fits in the series

*If you are reading this as your first article: the series index below has the full arc with links. Each article is standalone but the playbook compounds.*

Article 8 gave you one source of truth per program. Article 9 gave you a systematic diagnostic for surfacing what program status reports hide. Article 10 is where both arguments converge: the coordination failure that no single-program diagnostic catches, because no single-program diagnostic has the cross-program view required to see it.

When the integration contract is working, agents surface the right conflicts to the right owners before decisions are made on them. The TPM stops being the last line of detection and becomes the architect of a system that catches conflicts earlier.

That is the AI Architect function in practice: not building agents, but defining the architecture they operate inside.

Part II (Article 12) covers the remaining 17 terms: AI adoption inside orgs (where most TPM AI programs actually stall) and the TPM-specific edge - terms that exist nowhere else in any glossary, built from real delivery work. The full glossary (89 terms and growing) lives on GitHub as a `.md` file you can pull into your own Cursor or Claude memory setup.

Let's build.

Michi

---

*This is part of the TPM AI Playbook series. The full glossary lives at [github.com/michigoetz/tpm-breakdowns](https://github.com/michigoetz/tpm-breakdowns).*

*Continue to [Part II: terms 16-32 →](./2026-AI-12-tpm-ai-glossary-part2.md)*
