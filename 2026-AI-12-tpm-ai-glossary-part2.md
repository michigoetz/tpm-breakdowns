# 32 AI terms every Technical Program Manager should actually know (Part II)

**2026.AI.12** | The TPM AI vocabulary: terms 16-32

*Michi Goetz — June 17, 2026*

---

*Part of the TPM AI Playbook series. This is Article 12. If you missed Part I, start there - it covers the AI fundamentals and agentic systems vocabulary every TPM needs before this one lands properly. [Read Part I →](./2026-AI-11-tpm-ai-glossary-part1.md)*

---

Last week, Part I covered the first 15 terms across two buckets.

Bucket 1 redefined the AI fundamentals: RAG, hallucination, inference, context window, guardrails, evals, grounding. All through the lens of someone running a program, not someone building a product. The question is never "does it use RAG." It is "who owns the knowledge source and what breaks when it is wrong."

Bucket 2 went into agentic systems vocabulary: agent loop, orchestration, MCP, scaffolding, multi-agent systems, HITL, tool calling, silent failure. Terms showing up in architecture reviews and governance conversations right now, before most TPMs have the vocabulary to participate in them.

Before continuing: this is a good moment to step back.

The TPM AI Playbook series has been moving fast. Articles 1 through 10 covered adoption strategy, AI skill design, program health agents, the data layer, NotebookLM as a program second brain, and the survey of what 252 TPMs are actually doing with AI. Article 11 (Part I of this glossary) started anchoring the vocabulary underneath all of it.

This article completes that anchor. Buckets 3 and 4 are where the vocabulary gets specific to program delivery inside real organizations, and where the terms that exist nowhere else in any glossary live. After this, the series returns to use cases, with a shared vocabulary that makes those use cases easier to reason about, build, and govern.

The full glossary (89 terms and growing) lives on GitHub as a `.md` file you can pull into your own Cursor or Claude memory setup. The link is at the end.

---

*These are the terms that separate TPMs who understand how agentic systems fail from those who discover it in production. Bucket 3 is where those systems meet organizational reality.*

*The layer between the technology and the team. Where most TPM AI programs actually stall. Not because the tools aren't good enough, but because the organizational conditions aren't right.*

---

## Bucket 3: AI adoption inside organizations

**16. Approved stack**
The set of AI tools that have cleared your organization's legal, security, and procurement review. Not the optimal stack. The available stack. For TPMs, the approved stack is a hard constraint that shapes every AI program decision: what you can build, what data you can use, and how fast you can move.
*Ex: The tool your team wants is not approved. The tool that is approved is less capable. You build for what cleared procurement, not what won the benchmark. Six months later, you have something that works in your actual environment.*
**Use it with: Your team, IT and security reviews, Executives**

---

**17. Data layer**
The infrastructure of inputs your AI system depends on: where it lives, how clean it is, how current it is, and who owns it. The data layer is the most common failure point in TPM AI work. Not the model, not the prompt. The data the model is fed.
*Ex: Your AI program health tool is only as accurate as the Jira tickets, meeting notes, and status updates flowing into it. If those are stale, inconsistent, or owned by nobody, the tool fails regardless of how good the model is.*
**Use it with: Engineering leads, Data owners, Your team**

---

**18. Context engineering**
Deciding what information goes into an AI system's context window, in what form, and at what point. Not the same as prompt engineering. Prompt engineering is what you ask the model to do. Context engineering is what the model knows when it answers: what you select, compress, and exclude.
*Ex: You have a program wiki, three weeks of meeting notes, and a dependency map. You cannot fit all of it into one context window. What you choose to include determines what the model can reason about. That choice is yours, not the model's.*
**Use it with: Engineering leads, Your team when designing AI workflows**

---

**19. Observability**
The ability to see not just what an AI system did, but why it made the decisions it made: logs, traces, and output monitoring. For TPMs, observability is what lets you diagnose a silent failure (term 15), prove an AI system is improving, and hold the system accountable when a program decision goes wrong.
*Ex: Your AI risk summarizer flagged the wrong workstream as critical. Observability tells you which input caused it, which step amplified it, and what to fix. Without it, you are guessing.*
**Use it with: Engineering leads, AI governance reviews, Post-mortems**

---

**20. AgentOps**
The emerging discipline of managing AI agents in production: monitoring performance, tracking failures, managing versions, and maintaining reliability over time. For TPMs, AgentOps is where AI programs graduate from experiments to infrastructure.
*Ex: Your team has three agents running across five programs. Who monitors them? Who gets paged when one fails silently? Who decides when to roll back a prompt change that degraded output quality? That function is AgentOps.*
**Use it with: Engineering leads, Your team, Executives**

---

**21. Non-determinism**
AI models do not produce the same output for the same input every time. For TPMs, this is a governance and trust challenge. Non-deterministic output means you cannot assume yesterday's result tells you anything about today's.
*Ex: You run the same program risk prompt on Monday and Friday. You get different risk lists. Both are plausible. Neither is wrong. Which one do you act on? That question needs an answer built into your process, not resolved ad hoc every week.*
**Use it with: Your team, Stakeholders, AI governance reviews**

---

**22. AI governance**
The policies, decision rights, and accountability structures that define how AI is used inside a program or organization. Not a compliance document. A delivery system. For TPMs, AI governance determines who approves an agent's action space, who owns its outputs, and who is accountable when it gets something consequentially wrong.
*Ex: Your program uses an AI agent to draft dependency updates. Governance defines whether that agent acts autonomously, requires review, or only suggests. Without it, the answer changes person by person, week by week.*
**Use it with: Executives, AI governance reviews, Steering committee**

---

**23. Prompt engineering**
Crafting the instructions that guide what an AI model does: the task, the format, the constraints, the tone. The entry point for most TPMs into AI work. Valuable for one-off tasks. Insufficient as the only AI skill a TPM develops.
*Ex: "Summarize this meeting for engineering leads, focus on blockers and decisions, under 200 words." That is prompt engineering. It works once. Turning it into a repeatable skill that runs across all your programs is something else.*
**Use it with: Your team, Engineering leads**

---

*Most AI programs stall somewhere in this bucket. The tools are available, the use cases are identified, and nothing scales. The reason is almost always organizational, not technical. Bucket 4 is the vocabulary for building past that stall.*

---

## Bucket 4: The TPM-specific edge

*Terms that either originate in this work or exist nowhere else in this form. You will not find these in the Cox glossary, the agent builder docs, or the PM vocabulary lists. This is the vocabulary the community is building.*

---

**24. Tracker / Orchestrator / AI Architect**
The three stages of TPM AI maturity. Trackers use AI on discrete tasks: meeting notes, status drafts. Orchestrators design how AI works across the team: backlogs, shared skills, coordinated workflows. AI Architects encode institutional knowledge into systems that outlast any individual TPM. Most teams are stuck at Tracker. The gap to Orchestrator is a program design problem, not a tool problem.
*Ex: If your AI work disappears when you leave the program, you are a Tracker. If the system keeps running without you, you are moving toward Architect.*
**Use it with: Your team, Job interviews, Executives**

---

**25. Attrition test**
A diagnostic for whether your AI program work is institutionalized or personal. The question: what happens to your program's AI systems when you leave? If the answer is they stop working, the work was never really a program. It was a habit. The attrition test is the sharpest measure of whether AI adoption has taken root.
*Ex: You have built three agents that run weekly across your program portfolio. Document them, hand them to a new TPM, and see if they still run in month two. That result tells you more than any adoption metric.*
**Use it with: Your team, Executives, Job interviews**

---

**26. Judgment layer**
The decisions an AI system cannot and should not make: organizational dynamics, trust, risk tolerance, escalation calls. The layer that sits above the agent and requires a human. For TPMs, owning the judgment layer is the answer to what is left for us when agents handle the overhead.
*Ex: Your agent flags three risks every week. Which one gets escalated, to whom, and how - that is the judgment layer. The agent surfaces. The TPM decides.*
**Use it with: Executives, Your team, Job interviews**

---

**27. Skill**
A discrete, reusable AI workflow built for a specific TPM task: a prompt, its inputs, its output schema, and the logic connecting them. Not a one-off prompt. A versioned, repeatable unit of work that can be shared across a team and improved over time.
*Ex: A stakeholder map skill takes a program charter as input and returns a structured map of stakeholders, influence levels, and communication needs. Any TPM on the team can run it. Any TPM can improve it.*
**Use it with: Your team, Engineering leads**

---

**28. Hook**
A trigger that fires automatically when a defined event occurs in a program: a milestone update, a status change, a new risk. Hooks connect your AI skills to your program's live data without requiring a human to initiate each run. The difference between AI that assists and AI that operates.
*Ex: A risk hook fires every time a Jira ticket moves to blocked. It runs a risk assessment skill and posts the output to your program channel. No prompt needed. No human trigger required.*
**Use it with: Engineering leads, Your team**

---

**29. Agent contract**
The explicit definition of what an AI agent is authorized to do, what data it can access, what it cannot touch, and what requires human approval before action. Not a technical spec. A governance document that lives at the program level.
*Ex: Your program agent can read Jira and Confluence, draft status updates, and flag risks. It cannot close tickets, send external communications, or update the dependency register without review. That boundary is the contract.*
**Use it with: AI governance reviews, Executives, Engineering leads**

---

**30. Institutional knowledge encoding**
The process of converting what a TPM carries in their head into structured, machine-readable artifacts that an AI system can use. The hardest part of building a real TPM AI operating system. Also the part with the most leverage.
*Ex: Six months of program decisions, pivots, and escalations sitting in a TPM's memory is context an AI cannot access. The same information in a versioned program wiki, structured as markdown, is context an agent can reason from.*
**Use it with: Your team, Executives, Job interviews**

---

**31. Agent Mesh**
The top layer of the three-layer TPM AI architecture: Data Layer, Skill Library, Agent Mesh. A network of agents that chain skills together to achieve broader program goals. Distinct from the generic "multi-agent system" (term 12 in Part I): a multi-agent system is any architecture where agents collaborate; an Agent Mesh is the specific orchestration layer built on top of your Skill Library and Data Layer, where agents share the same program context and compound each other's outputs. Fix the data first. Build the skills in parallel. Deploy the Mesh when both are stable.
*Ex: Four agents running across your program portfolio: dependency tracking, risk synthesis, stakeholder communications, program health scoring. Sharing the same data layer and skill library. That is a Mesh. Four separate prompts saved in a Notion doc is not.*
**Use it with: Executives, Engineering leads, Job interviews**

---

**32. Agent harness**
The runtime layer that wraps a skill and manages its execution: input validation, context injection, output parsing, error handling, logging, and trigger logic. Distinct from scaffolding (term 11 in Part I): scaffolding is the structural wrapper built around a raw model to make it useful; the harness is the execution runtime built around a skill to make it operate reliably in a live program environment. Without a harness, a skill is a prompt. With one, it is a production workflow.
*Ex: Your risk synthesis skill is a well-crafted prompt. The harness takes the Jira export, validates the format, injects it into context, runs the inference call, parses the output, checks it against the schema, logs the run, and writes the result to Confluence. The skill defines the intelligence. The harness makes it operate reliably.*
**Use it with: Engineering leads, Your team**

---

## Where it goes from here

A Substack article is a snapshot. The full glossary (89 terms and growing) lives on GitHub as a `.md` file structured for direct import into Cursor or Claude project memory. The same way I maintain my own terminology file: it updates as the vocabulary earns new entries through real delivery work.

The TPMs who will lead in the next three years are not the ones who read the most glossaries. They are the ones who use the vocabulary to build systems, test them against real programs, and update the vocabulary when the systems teach them something new. That loop is what this file is for.

**[TPM AI Playbook on GitHub](https://github.com/michigoetz/tpm-breakdowns)**

---

*This is Article 12 of the TPM AI Playbook series. Article 13 returns to use cases, with this vocabulary as the foundation.*

*If you are reading this as your first article: the series index below has the full arc with links. Each article is standalone but the playbook compounds.*

- **AI.01-02** — Why TPMs are absent from AI adoption data ([michigoetz.substack.com/t/practical-ai](https://michigoetz.substack.com/t/practical-ai))
- **AI.03** — Seven program failure patterns AI can surface faster than any status meeting ([Program Fruit Bowl](https://michigoetz.substack.com/p/the-program-fruit-bowl-an-anatomy))
- **AI.04** — Why every program needs a second brain ([NotebookLM article](https://michigoetz.substack.com/p/why-i-think-every-program-needs-a))
- **AI.05** — The Tracker → Orchestrator → AI Architect evolution ([Tracker. Orchestrator. AI Architect.](https://michigoetz.substack.com/p/tracker-orchestrator-ai-tpm))
- **AI.06** — Four skills, one comms agent, one delivery workflow ([TPM Delivery Agent](https://michigoetz.substack.com/p/the-tpm-had-a-risk-register-agent-skills))
- **AI.07** — 30 power questions no agent can ask for you ([Power Questions](https://michigoetz.substack.com/p/what-ai-reads-what-you-have-to-ask))
- **AI.08** — The data layer that makes everything above it work - or fail ([Data Layer](./2026-AI-08-all-about-templates-data-layer.md))
- **AI.09** — The Fruit Bowl skill: how a label becomes a defensible diagnostic ([Fruit Bowl skill](./2026-AI-09-fruit-bowl-skill.md))
- **AI.10** — The coordination problem one layer above the data layer ([Agent Coordination](./2026-AI-10-the-agent-coordination-problem.md))
- **AI.11** — TPM AI vocabulary Part I: terms 1-15 ([Part I](./2026-AI-11-tpm-ai-glossary-part1.md))
- **AI.12** — This article. Terms 16-32: organizational AI adoption and the TPM-specific edge.
