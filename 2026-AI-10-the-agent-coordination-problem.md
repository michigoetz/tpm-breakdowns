# The Agent Coordination Problem No One Has Named Yet

**2026.AI.10** | *Why your data layer works for one program and breaks at scale - and what the TPM owns at the boundary.*

*Michi Goetz — May 27, 2026*

---

You're the TPM watching a steering committee recommendation fall apart in real time.

The risk assessment came back clean. One conflict flagged. NEXUS IAM delivering July, HORIZON needing June. A four-week gap. Fixable.

Then you open the other program masters.

ATLAS had an Auth0 workaround gated on the same July delivery. SHIELD had 14 compliance controls staked on that date, with its August SOC 2 audit window moving the moment July slips. PULSE needed the OTel migration from NEXUS before it could instrument reliability. What the agent flagged as one conflict was five. Each one invisible to an agent reading a single program file. Each one visible only from the seat looking across all of them.

The model didn't fail. It read exactly what it was given. The problem was the architecture sitting above the individual program files: the layer where one program's output becomes another program's input, where dependency dates get consumed differently across four different programs, and where nobody had assigned an owner to watch the boundary.

That boundary is the next problem in the series.

---

## But I already have risk and dependency management tools

Before the architecture argument: the objection every practicing TPM will raise immediately.

You have a risk register in Jira. A dependency matrix in Confluence. A RAID log. A SteerCo deck updated every two weeks. Cross-program dependency management has been core TPM work for years. Risk registers, RAID logs, dependency matrices. These aren't new concepts. The tools exist. The practice exists. What's changing?

The agent is.

Those tools were built for humans to read. A TPM opens Confluence, reads the dependency matrix, applies judgment, and produces a synthesis. The synthesis lives in their head and surfaces in the steering committee meeting. That workflow functions because the TPM is the integration layer. They reconcile inconsistencies in real time. They know which Jira filter is current and which one the team stopped updating in March. They know the Confluence page is authoritative for one program and informational for another. They know the SteerCo deck from two weeks ago has a date that was already superseded in a Slack thread.

Agents don't know any of that. An agent pointed at Jira reads whatever Jira returns. An agent pointed at Confluence reads whatever is on that page. If those two reads disagree on a date, the agent has no mechanism to determine which is canonical. It picks one, or flags a conflict without context on how to resolve it.

This is also the honest answer to why tools like Cowork, Glean, or any AI assistant operating across your existing tool stack don't solve this on their own. Those tools read what exists. If what exists is six systems with no canonical authority rules between them, the tool reads six fragmented sources and produces a synthesis with no stable foundation. Your existing tools are retrieval systems. Every steering committee, you re-derive the cross-program picture from raw sources. The integration contract is the compiled alternative. Built once, kept current, readable by every agent without re-derivation.

The institutional knowledge that made the old workflow function lived in the TPM's head. It was never encoded anywhere an agent can reach. The markdown file doesn't replace your Jira risk register or your Confluence dependency matrix. It tells agents which system is authoritative for which fact, what to do when two systems disagree, and where to escalate when neither can resolve the conflict. Your existing tooling becomes more useful, not less, when the canonical sources are explicit. That's the layer that was always missing, because until now a human was providing it in real time.

---

## The failure that looks like success

You have six programs. One of them, NEXUS, owns the IAM infrastructure work. Four others (ATLAS, SHIELD, HORIZON, PULSE) each depend on NEXUS delivering something different, on a different date, for a different reason.

HORIZON needs the IAM handoff in June. ATLAS needs an Auth0 workaround in April and full delivery in July. SHIELD has 14 compliance controls gated on the same July delivery, with an August SOC 2 audit window that moves the moment July slips. PULSE needs the OTel migration from NEXUS before it can instrument reliability, which means PULSE's reliability commitments are downstream of NEXUS's delivery pace.

Each program maintains its own markdown file. Each file is internally consistent. Each was validated this week.

Now a risk assessment agent runs against the portfolio. It reads NEXUS's program master as the canonical source for IAM delivery. The date it finds is July. HORIZON's program master says it needs June. The agent flags one dependency conflict.

What it cannot see: the same July date is simultaneously gating ATLAS's pilot timeline, collapsing SHIELD's SOC 2 audit window, and blocking PULSE's reliability sequencing. One stale read in NEXUS's master doesn't create one conflict. It creates five. Each one invisible to the agent reading a single program file. Each one visible only from the seat looking across all of them.

*One fact. Five consuming programs. Five different failure modes.*

The model didn't fail. The architecture did. Six programs, one canonical provider, no integration contract between them, and no role assigned to watch the boundary.

That last part is the problem worth naming.

---

## Why this only becomes visible from one seat

The NEXUS program owner is looking at NEXUS. The SHIELD program owner is looking at SHIELD. The engineering lead on IAM is looking at the ticket. Each of them has a locally consistent view. None of them has a reason to compare five program masters against each other.

The TPM does. Not because of a tool or a process. Because of position.

No other role sits simultaneously across program state, cross-functional dependencies, the technical context that makes a date meaningful, and the humans who will act on the output. The engineering lead knows the IAM work. The PM knows the compliance deadline. The TPM knows that the same July date lives in five different files, that four of them consume it differently, and that a steering committee recommendation is about to be built on reads that have never been reconciled.

This is not a claim about TPM value. It's a claim about information flow. The conflict only surfaces at the intersection of programs. The only role whose job requires that intersection is the TPM's.

When the conflict is caught before the steering committee, it looks like good program management. When it isn't, it looks like an AI problem. It's neither. It's a distributed state consistency problem at the program layer, the same failure mode that appeared in the early days of microservices. Every service owned its data. Every service was internally consistent. The integration layer, the contracts between services and source of truth for shared state, was nobody's explicit job until the inconsistencies became expensive enough to force the conversation.

The program management version is structurally identical. Each program owns its markdown. Each program is internally consistent. The boundary between programs is where the stale reads accumulate: the set of dependencies, shared resources, and authority decisions that one program's agent reads from another program's state. And it's owned by whoever is watching the boundary.

Right now, in most organizations, nobody is.

> **Ownership without attention is governance theater.**

---

## The integration contract

Above your individual program folders, one file: `cross-program-dependencies.md`.

Not a dashboard. Not a governance framework. A markdown file at the repo root that makes the boundary explicit and gives every agent a common reference point alongside `domain-context.md`. It detects conflicts. It doesn't prevent them. That distinction matters.

The AI Architect function, the organizational role that governs cross-program data contracts, is currently unowned in most teams. This file is how you make it explicit before the absence becomes expensive.

The organizational standing question is one to answer before you need it: what gives the TPM the right to declare that the NEXUS program master is canonical for ATLAS's dependency, and that ATLAS cannot maintain its own conflicting view? The answer isn't technical. Three mechanisms work in practice: include the integration contract as a standard item in program kickoff agreements, so every new program accepts canonical status for the facts it owns as part of joining the portfolio rather than as a special negotiation; establish it as portfolio policy at the Head TPM level so canonical authority is a structural expectation, not a case-by-case request; or embed it directly in the program charter template, in the section that defines program ownership responsibilities. Whichever fits your organization, the principle is the same: establish authority explicitly at the program boundary, before the cascade that makes everyone wish it existed.

Here's the complete file structure:

```markdown
# cross-program-dependencies.md
# Purpose: Canonical authority registry for cross-program dependencies.
# Agents: load this file before any cross-program risk sweep or SteerCo prep.
# Owner: [TPM name]
# Last updated: [date]
# Review trigger: new program joins portfolio | dependency authority changes | cascade incident resolved

---

## Dependency Registry

| Program | Artifact | Canonical path | Last validated | Depends on | Risk ID | Notes |
|---------|----------|----------------|----------------|------------|---------|-------|
| SHIELD | IAM delivery (14 controls gated) | `/nexus/program-master.md` | 2026-05-21 | NEXUS | DEP-005 | Jul IAM delivery blocks 14 SHIELD controls. Aug SOC 2 audit at risk. |
| HORIZON | IAM handoff date | `/nexus/program-master.md` | 2026-05-21 | NEXUS | DEP-001 | NEXUS Jul vs HORIZON Jun need. 4-week gap. |
| ATLAS | Auth0 workaround + full delivery | `/nexus/program-master.md` | 2026-05-21 | NEXUS | DEP-003 | Apr workaround + Jul full delivery. Pilot timeline gated. |
| PULSE | OTel migration handoff | `/nexus/program-master.md` | 2026-05-18 | NEXUS | DEP-006 | PULSE reliability instrumentation blocked until NEXUS OTel migration complete. |

## Shared Resource Conflicts

| Resource | Programs competing | Total commitment | Decision owner | Status |
|----------|--------------------|-----------------|----------------|--------|
| Model Serving (12 people) | ATLAS + SPARK | 190%+ | VP Engineering | 🔴 Unresolved — DEP-007 |
| Security Engineering (8 people) | SHIELD + ATLAS + NEXUS | 170% | Engineering leadership | 🔴 Active |

## Canonical Authority Rules

1. When two programs reference the same fact with different values, the provider program's master is canonical. The consuming program defers.
2. If the provider's master is stale (last validated beyond your threshold), flag it before consuming.
3. Conflicts not resolvable by rules 1-2 escalate to the TPM owner listed in this file's header.

---
# Maintenance: Update when a dependency row changes. Validate all rows on SteerCo cadence.
# A stale row in this file is worse than no file. It gives agents false confidence.
```

*One file. Every agent reference point in one place.*

Six fields in the dependency registry answer what every agent and every human needs: who owns this fact, where does it live, when was it last confirmed, who's downstream if it changes, and which risk record tracks it.

The `Risk ID` column connects to your existing RAID log. An agent running a risk sweep cross-references DEP-005 against open risks without being told the link exists. Your Jira risk register doesn't disappear. It gets connected.

When a consuming program depends on artifacts from multiple providers simultaneously, list each provider as a separate row. The canonical authority rules apply per row, not per consuming program.

The shared resource conflicts table captures the second layer of cross-program dependency that no individual program master holds. Date conflicts are visible if you look. Capacity conflicts are invisible until someone maps total commitment across programs simultaneously. 190% allocation on Model Serving doesn't appear in any single program's risk register. It only exists at the portfolio level.

"Last validated" means a human has opened the canonical path, confirmed it reflects current program state, and updated the date. The Claude Code diagnostic prompt at the end automates the staleness check. It does not replace the confirmation.

That third canonical authority rule is where the human judgment boundary lives. Rules one and two resolve most conflicts automatically. What's left (DEP-007, Model Serving at 190%, decision owner: VP Engineering) is a judgment call the agent can surface but cannot make.

The agent tells you the allocation is impossible. The TPM brings it to the VP with the right framing. The VP decides which program gets priority. That's not a coordination story. It's a decision quality story. The TPM is not managing a dependency log. The TPM is ensuring a resource allocation decision reaches the right owner with the right information.

**On the staleness threshold:** set it to match your shortest decision cycle. If a dependency gates a weekly SteerCo decision, validate it every three to four days. Under delivery pressure, decision cycles compress. So should your review frequency.

The integration contract is most valuable under delivery pressure and hardest to maintain under delivery pressure. Name that paradox with your team before it arrives. The three moments where rebuilding it pays the highest return: when a new program joins the portfolio, when dependency authority over a shared resource changes hands, and immediately after a cascade incident, when the failure is fresh and everyone can see exactly which row was missing or stale.

---

## What this requires to work

Two dimensions govern whether the integration contract stays useful or quietly reverts to another document nobody reads.

**Event-driven triggers, not calendar-driven reviews.**

Calendar-driven reviews happen whether or not anything changed. Event-driven reviews happen when dependencies are most likely to have shifted. The minimum viable trigger set: a new cross-program dependency is identified in any weekly sync, a milestone date changes in any provider program's master, a shared resource decision changes authority, or a cascade incident just resolved. Any of these events means the integration contract is potentially stale. The cost of reading a stale contract is higher than the cost of updating it now.

Calendar reviews add maintenance burden. Event-driven triggers reduce it: you update when something actually changed, not when the cadence says to check.

**Ownership structure that doesn't collapse under scale.**

In a single-TPM portfolio, the TPM owns both sides (provider programs and consuming programs) and the integration contract is their personal audit surface. In a multi-TPM team, the TPM who owns the affected dependency updates the file when a new cross-program dependency is identified. The portfolio-level TPM validates the whole file on a SteerCo cadence. That division prevents the file from becoming one person's maintenance burden and prevents it from becoming everyone's assumption that someone else is maintaining it.

The failure mode to name explicitly with your team at the start: under delivery pressure, the file reverts. Milestone dates slip, team communication compresses, and the integration contract is the first artifact nobody has time to update. That's precisely when an agent reading a stale contract produces its worst output: confident, specific, and wrong.

The failure looks like this: NEXUS IAM slipped three weeks ago. The program master was updated. The integration contract was not - the incident absorbed everyone's attention and nobody updated the boundary artifact. HORIZON's agent runs its weekly risk sweep, reads July in the integration contract, marks the NEXUS dependency green, and two days later the HORIZON TPM presents a steering committee recommendation built on a fact that is three weeks stale. Everyone assumes the integration contract was validated. It was. It was just wrong.

The early warning signal is not staleness alone. It is the combination of high delivery pressure and extended quiet: when a provider program is moving fast and the integration contract row hasn't changed in two weeks, that is not evidence the dependency is stable. It is evidence the maintenance habit has lapsed. Under pressure, teams update their program master. The boundary artifact is the first thing to go unmaintained.

This failure mode is harder to recover from than having no integration contract at all. With no contract, agents flag the gap explicitly - they surface what they cannot confirm. With a stale contract, agents report confidence. The question "is this dependency validated?" gets a false yes instead of a visible no. False confidence from a stale-but-believed-current contract is a harder problem to detect and a harder failure to recover from than the baseline of no contract. That's the failure worth naming with your team before it happens.

The protection is not discipline. It is making the three forcing functions above the explicit team agreement: new program, authority change, cascade resolved.

---

## Not just for TPMs

The integration contract matters beyond the TPM seat.

**Engineering Managers** get a clear destination for cross-program conflicts that currently surface as ad hoc Slack threads or heated SteerCo moments. When an EM's team is blocked on another team's decision, the integration contract names the canonical path, the authority rule, and the escalation owner. A political conversation becomes a documented one.

**Software Engineers** stop getting woken up for incidents caused by a contract that didn't exist. The OTel migration gap in PULSE doesn't surface as a 2am page if the dependency row existed and was validated. The integration contract is the technical spec for the layer between programs.

**Product Managers** can scope programs with explicit boundary agreements. "ATLAS depends on NEXUS IAM by July" in a PM's roadmap is an assumption. "ATLAS depends on NEXUS IAM by July, canonical path `/nexus/program-master.md`, last validated 2026-05-21" is a fact with an owner.

---

## Where to start

If you have more than one program running right now, you likely already have this problem. You just haven't seen it yet because the conflict hasn't surfaced in a decision.

The minimum viable version:

Pick your two most interdependent programs. Open both program masters. Find one artifact where they reference each other. Check if the facts match.

If they match, you're fine for now. If they don't, you've found a cross-program dependency conflict that your agents are reading as two different truths, and you now know which one is canonical.

Build `cross-program-dependencies.md` for those two programs first. Start with the header block: purpose, owner, last-updated, review trigger. One row per shared dependency. Add the shared resource conflicts table if more than two teams are competing for the same resource. Agree on canonical sources. Set a review cadence. Run it for two weeks before you scale.

Then run this in Claude Code:

```
Load cross-program-dependencies.md and domain-context.md.

For each row in the Dependency Registry:
  - Open the canonical path listed
  - Confirm the artifact exists at that path
  - Check whether last-validated date is within the staleness threshold
  - Flag any row where the path is missing, the artifact is absent, or the date is stale

For each row in the Shared Resource Conflicts table:
  - Check whether a decision has been recorded against the Risk ID
  - Flag any 🔴 rows with no recorded decision

Cross-reference all Risk IDs against the open RAID log.
Report: stale rows, missing paths, unresolved capacity conflicts, disconnected Risk IDs.
```

*In a well-maintained integration contract, this diagnostic runs in under a minute. The first run will find rows that need validation, paths that have drifted, Risk IDs without open RAID log entries. That's not a failure. It's the diagnostic doing its job.*

The underlying principle is worth stating separately from any particular tool or model: explicit canonical authority matters regardless of what AI capability is available. Whether the agent is reading Jira, Confluence, GitHub, or a purpose-built retrieval stack, it reads what exists. If what exists has no declared authority structure, the agent either picks a source arbitrarily or flags conflicts without context to resolve them. The integration contract makes the authority structure machine-readable and stable. The diagnostic prompt operationalizes it. The speed follows from the structure, not the other way around.

---

## Where this fits in the series

Article 8 gave you one source of truth per program. Article 9 gave you a systematic diagnostic for surfacing what program status reports hide: the two-round Fruit Bowl workflow that turns a label into a defensible finding. Article 10 is where both arguments converge: the coordination failure that no single-program diagnostic catches, because no single-program diagnostic has the cross-program view required to see it.

When the integration contract is working, agents surface the right conflicts to the right owners before decisions are made on them. The TPM stops being the last line of detection and becomes the architect of a system that catches conflicts earlier. That's the outcome that changes.

That's the AI Architect function in practice: not building agents, but defining the architecture they operate inside.

Article 11: the TPM AI vocabulary - 32 terms, built from real delivery work.

---

*Templates, program masters, and skills live in the open repo: [github.com/michigoetz/tpm-breakdowns](https://github.com/michigoetz/tpm-breakdowns)*

*Let's build.*

*Michi*

---

**Where this fits in the series**

- **AI.01-02** — Why TPMs are absent from AI adoption data, and why the same person who plans vacations with Claude won't use it at work ([michigoetz.substack.com/t/practical-ai](https://michigoetz.substack.com/t/practical-ai))
- **AI.03** — Seven program failure patterns AI can surface faster than any status meeting ([Program Fruit Bowl](https://michigoetz.substack.com/p/the-program-fruit-bowl-an-anatomy))
- **AI.04** — Why every program needs a second brain and why NotebookLM is a practical starting point ([NotebookLM article](https://michigoetz.substack.com/p/why-i-think-every-program-needs-a))
- **AI.05** — The Tracker → Orchestrator → AI Architect evolution and the 7-step adoption playbook ([Tracker. Orchestrator. AI Architect.](https://michigoetz.substack.com/p/tracker-orchestrator-ai-tpm))
- **AI.06** — Four skills, one comms agent, one delivery workflow - and what it found that the TPM missed ([TPM Delivery Agent](https://michigoetz.substack.com/p/the-tpm-had-a-risk-register-agent-skills))
- **AI.07** — 30 power questions no agent can ask for you, in two modes: situational lookup and AI governance pre-flight ([Power Questions](https://michigoetz.substack.com/p/what-ai-reads-what-you-have-to-ask))
- **AI.08** — The data layer that makes everything above it work - or fail ([The data layer article](https://michigoetz.substack.com/p/the-agent-didnt-fail-your-data-layer))
- **AI.09** — The Fruit Bowl skill: how a label becomes a defensible diagnostic, and what the portfolio scan found ([Fruit Bowl skill article](./2026-AI-09-fruit-bowl-skill.md))
- **AI.10** — This article. The coordination problem that appears one layer above the data layer, and what the TPM owns at the boundary.
