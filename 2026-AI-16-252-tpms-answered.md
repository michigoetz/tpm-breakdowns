# We asked 252 TPMs, PgMs, PMs, EMs how they use AI. Here's what happened since.

**2026.AI.16** | *The month I spent living those numbers, including watching a TPM on my team do what used to take an engineer.*

*Michi Goetz - July 2026*

---

In January, I wrote a note that traveled further than anything I'd published before it.

The premise was one paragraph. Lenny Rachitsky surveyed 1,750 tech workers about AI. Stack Overflow covered 49,000 developers. GitHub measured 15 million Copilot users. Product managers had data. Engineers had data. TPMs appeared in none of it.

If you cannot measure AI productivity for TPMs, you cannot improve it.

The honest version of what happened next: complaining worked, briefly. The note resonated, people nodded, and nothing changed, because nobody was going to run that survey for us. So six of us ran it ourselves: Liana Gevorgyan, Malvika Sinha, Aadil Maan, James, Josh Teter, and I created the survey and shared the results on [AI for TPMs](https://aifortpms.substack.com). Eight weeks of collection. 252 TPMs, Program Managers, and Engineering Program Managers. The most comprehensive dataset on TPM AI adoption that exists.

This article is two things at once: my personal read of the survey - the five numbers I keep quoting, the two findings that surprised the people who ran it - and doubling down harder than before at the company I work at, building the workflows the data says TPMs want most. The full report, both parts, lives on [AI for TPMs](https://aifortpms.substack.com).

> **One ask before the data:** I'm collecting examples of TPMs and their teams building real AI *systems* - not prompts, systems that ship work that used to need an engineer. If you have one, I want to see it. The full ask is at the end, and it's the seed of whether we run a second survey.

---

## Who answered, and why that matters

Before the numbers: 96% of respondents were TPMs, PgMs, or EPMs. 75% individual contributors. 69% with twelve or more years of experience. 63% from enterprises with 3,000+ employees.

Read that composition again, because it's the credibility of everything that follows. These are not AI enthusiasts who happen to have opinions about program management. These are senior practitioners running programs at scale, and 39% of them have 16+ years - enough technology waves to know the difference between hype and durable value. When this population says AI is delivering, the signal carries weight it wouldn't carry from a survey of early adopters.

## The five numbers I keep quoting

**70% save 2+ hours a week with AI.** The peak bucket is 2-4 hours (36%), and the distribution skews right: 15% save a full day or more. Across a 20-person TPM org, the floor of that range is a full-time equivalent of reclaimed capacity, every week.

**63% rate themselves Beginner or Developing. 95% want to learn more.** Sit with that pair. The population is early on the curve and almost universally hungry - 82% rated their upskilling interest 5 out of 5. This is not a skeptical profession. It's a blocked one.

**Literacy predicts outcomes. Seniority doesn't.** ICs and Leaders score nearly identically on quality impact (3.78 vs 3.70 out of 5). But Beginners save 2+ hours at a 54% rate and Intermediates at 88% - the steepest jump in the data. The ROI on AI training isn't a nice-to-have line item. It's the highest-leverage investment a TPM org can make right now, and it beats every seniority-based assumption about who will benefit.

**The barriers are organizational, not motivational.** Integration issues, company policy, and paid-tool access: ~41% each, statistically tied. Culture and skepticism: 9%. Only 2% of respondents - four people out of 252 - identified as not using or trusting AI. The resistance narrative is dead. The access problem is alive.

**The want-list doesn't match the use-list.** Meeting summarization: 83% use it, 31% want more - solved. Cross-program dependency management: 38% use it, 57% want more. Technical risk and dependency mapping: the single most-wanted use case in the entire survey. TPMs have automated the communication layer and are pointing at the core of the job.

---

## What surprised us

Two findings I didn't see coming when we designed the instrument.

**The productivity curve accelerates exactly where the work changes character.** Saving 4+ hours weekly: 15% of Beginners, 37% of Developing, 40% of Intermediate - then 63% at Advanced. That break in the curve isn't more prompting skill. Advanced users are doing different work: agents, multi-step workflows, AI upstream in problem framing rather than downstream in document polish. The ceiling breaks when AI stops being a feature and becomes infrastructure. (That architecture is where this series goes next.)

**The verification tax scales with ambition, not usage.** 50% cite hallucinations, 45% spend real time reviewing and fixing outputs. But the burden isn't uniform - it concentrates exactly in the use cases TPMs want most. A wrong meeting summary costs you a correction. A wrong dependency map costs you a steering committee decision. The things we most want to automate are the things that most require expert validation. Anyone selling you effortless AI for risk management has not used it at scale.

---

## The month I spent living these numbers

I didn't just read this data. Before the survey I was getting my team on AI, into AI and enabling them (shoutout to Clara from my team for doing a fantastic job), and after the survey pushed even more.

**I moved myself into the 15%.** The survey's top savers reclaim a full day a week. Last month I shipped the thing that put me there: a portfolio view that rebuilds itself every hour, so the 90-minute Monday collection ritual became a few minutes of scanning. A year ago I was in the 0% bucket. The number moved because the work changed, not because I got faster at it. ([The Daily 360](https://michigoetz.substack.com/p/tpm-portfolio-management-operating-system))

**The sharpest ceiling-break I saw this month wasn't mine - it was a TPM on my team.** The survey's finding is that savings jump when AI stops being a feature and becomes infrastructure. Here's what that looked like on the ground. We surfaced a backlog of cryptic error messages that get surfaced to our customers - the kind that say "column not found" and tell an end user nothing about which column or what to do next. A year ago, fixing that meant activating an engineer: scope it, find capacity, wait in the sprint queue. This time a TPM on my team built the fix. Not a prompt: an actual agentic system, with defined triggers, guardrails, skills, a memory layer, and humans in the loop. It scanned the codebase, rewrote the ambiguous errors with the missing context, created a Jira ticket, and opened pull requests with before/after diffs - a bare "column not found" became "the query needs column X; add it to the source table and re-run." Engineers reviewed, two sign-offs before merge, monitoring confirmed the error rate dropped. A handful of pull requests shipped, authored by a system a TPM built. That is the ceiling breaking: work that used to require pulling in an engineer, now designed and shipped by a TPM. The agentic architecture will be revealed in one of the next posts.

**I paid the verification tax in public.** 45% of us spend real time reviewing AI output, and the survey says that tax concentrates in the use cases we want most. A reader asked me last month how long it took to trust the false-positive rate. The honest answer is that trust never came from a better model. It came from drawing a hard line: the system parses what must be deterministic and only synthesizes the part a human still reviews. The most-wanted use cases, risk and dependencies, are exactly the ones that need that line drawn before you ship them.

---

## If you are leading TPMs: what I'd do Monday

If I ran your TPM org and had only this dataset, three moves, in order.

**Audit access before funding training.** 41% of your people are blocked by policy or tooling - a problem training doesn't touch. Find out what your team can actually reach. Escalate the gap. This is the cheapest intervention on the list and it unblocks every other one.

**Train to Intermediate, deliberately.** The Beginner-to-Intermediate jump is worth 34 percentage points of 2+ hour savers. That's not a course - it's expanding the range of tasks people bring AI into, with TPM-specific use cases, until confident multi-use-case work is normal. Generic AI tutorials won't do it; 34% of respondents said they don't know how to use AI effectively, and what they mean is nobody has shown them their job with AI in it.

**Define the human-in-the-loop boundaries in writing.** 45% are paying the verification tax ad hoc. Decide explicitly: which outputs ship with a skim, which need line-by-line validation, which never leave without human sign-off. The orgs that skip this step will learn it from an incident.

---

## What this survey cannot tell you

Honest limits, because a survey I co-ran deserves the same scrutiny I'd give anyone else's.

**Self-selection is real.** People who answer an AI survey from an AI-focused community skew toward engagement with AI. The 2% skeptic number is probably the floor, not the census. Directionally, though, the barrier data holds - even this engaged population reports being blocked by access, not conviction.

**Literacy is self-rated.** Our scale measures tool proficiency, not judgment. A TPM who evaluated AI for their risk register and deliberately decided against it scores as a Beginner in our framework - and might be one of the most sophisticated practitioners in the dataset. The instrument encodes adoption as the destination. Reality is more conditional than that.

**Time saved is reported, not measured.** Nobody ran a stopwatch. The numbers are practitioner perception at scale - valuable, consistent, and still perception.

---

## So what?

Six months ago the complaint was: TPMs are missing from every AI survey. That's no longer true.

The same logic applies one level down, to you. Nobody is going to measure your team's AI reality for you. The survey we ran is the industry baseline; your version is a one-question form and two weeks of patience, observation, and asking peers: where is AI actually saving you time, and where is it still painful? That baseline becomes your backlog. It did for us.

If you want the raw dataset behind these numbers - the IC vs Leader split, the tool value-ratio table, the voices from the field - it's on [AI for TPMs](https://aifortpms.substack.com), the survey I ran with that group.

Two asks to close, and they're the same logic that started all this.

**First: send me your examples.** If you've built - or your team has built - an AI system that did work that used to require an engineer, I want to see it. Reply, or drop it in the comments. I'm collecting them because the next round of this should be built on receipts, not vibes.

**Second: should we run that second survey?** The first one existed only because six practitioners decided the data should. If you'd answer a Wave 2, and help shape what it asks, tell me - and let's build it together.

---

*The TPM AI Playbook - 40+ skills, the NovaGrid sandbox, and the 8-layer reference architecture - is open on GitHub: [github.com/michigoetz/tpm-breakdowns](https://github.com/michigoetz/tpm-breakdowns)*

*Let's build.*

*Michi*
