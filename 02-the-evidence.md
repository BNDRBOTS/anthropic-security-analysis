# THE CON, DOCUMENTED
## A Five-Part Investigation into Anthropic's Claude, June 2026

---

# Report 2: The Evidence
## Six Weeks, Three Undisclosed Changes, a 35% Cost Inflation, and Six Weeks of Silence

*All sources linked. All claims cross-verified. Nothing extrapolated beyond what the evidence shows.*

---

### The Compound Failure: What Actually Happened

Between March 4 and April 20, 2026, Claude Code — Anthropic's flagship agentic coding product — ran degraded in production. Three separate changes, each made without public announcement, compounded into a cascade of symptoms that developers could not diagnose because they had no information about what had changed.

This is the verified sequence, sourced from Anthropic's own engineering postmortem published April 23, 2026:

**Change 1 — March 4, 2026:** Default reasoning effort downgraded from high to medium. Stated rationale: reduce latency (the interface appeared frozen during deep thinking). Impact: degraded output intelligence across every session on Sonnet 4.6 and Opus 4.6. Anthropic's own postmortem called this "the wrong tradeoff." It ran for 34 days before being reverted on April 7.

**Change 2 — March 26, 2026:** A caching bug introduced that caused the model to repeatedly discard its reasoning history mid-session. Impact: the model forgot decisions it had already made and reasoning it had already done, producing circular loops and repeated failed attempts at the same step.

**Change 3 — April 16, 2026:** A system prompt was added to Claude Code containing two lines:

> *"Length limits: Keep text between tool calls to ≤25 words. Keep final responses to ≤100 words unless the task requires more detail."*

This was not a model change. This was not in the model weights. This was a text instruction added by Anthropic to the system prompt that every user's session ran against, without disclosure. The purpose was to control output verbosity on the newly-launched Opus 4.7, which was generating too many tokens — meaning too much compute cost per session.

After weeks of internal testing showing no regression on their standard eval suite, Anthropic shipped it. When they ran a targeted ablation study after the incident — removing each system prompt line and measuring impact — they found a 3% drop in coding quality on a dimension their standard evaluations never tested.

The 25-word cap was reverted April 20. All three issues were confirmed resolved by that date.

**Sources:**  
Anthropic engineering postmortem, April 23, 2026. https://www.anthropic.com/engineering/april-23-postmortem  
DEV Community analysis, April 25, 2026. https://dev.to/_46ea277e677b888e0cd13/anthropic-april-23-postmortem-3-confounding-changes-behind-claude-codes-month-long-quality-drop-2pl6  
VentureBeat, April 23, 2026. https://venturebeat.com/technology/mystery-solved-anthropic-reveals-changes-to-claudes-harnesses-and-operating-instructions-likely-caused-degradation

---

### What Users Were Experiencing During the Silence

A senior director in AMD's AI group, Stella Laurenzo, published an exhaustive technical audit of 6,852 Claude Code session files and over 234,000 tool calls. Her documented findings showed reasoning depth had fallen sharply, with a persistent tendency to choose the simplest fix rather than the correct fix. She described Claude Code as "unusable for complex engineering tasks."

Benchmark firm BridgeMind reported that Claude Opus 4.6's measured accuracy had dropped from **83.3% to 68.3%** in their testing — a 15-point decline — causing its ranking to fall significantly.

**Source:** VentureBeat, April 23, 2026. https://venturebeat.com/technology/mystery-solved-anthropic-reveals-changes-to-claudes-harnesses-and-operating-instructions-likely-caused-degradation

Cybersecurity professionals using Claude Code for security review flagged dangerously degraded code quality in production outputs. Multiple users canceled subscriptions. The volume of complaints across Reddit, X, Hacker News, and GitHub issues was documented publicly.

Muratcan Koylan, a member of technical staff at Sully.ai, put it directly in a statement quoted by Fortune:

> *"The frustrating part is that the Claude Code team, along with people deep in AI psychosis, have been gaslighting anyone who raises concerns about Claude Code's recent issues. When you're paying a lot of money for a product, and it actually makes your job harder, to the point where people make you start questioning the quality of your own work, it really becomes a problem."*

**Source:** Fortune, April 24, 2026. https://fortune.com/2026/04/24/anthropic-engineering-missteps-claude-code-performance-decline-user-backlash/

---

### What Anthropic Said During the Silence

Fortune's earlier reporting from April 14, two weeks before the postmortem, documented Anthropic's initial response:

> *"[Anthropic] initially said the performance issues were the result of changes it had made to improve latency and in response to user feedback."*

In other words: the degradation was explained as something done *for* users. An improvement. The implicit message was that users experiencing decline were misidentifying a benefit as a problem.

This was the period when the 25-word output cap was actively running. Anthropic knew they had changed the system prompt. Anthropic knew reasoning effort had been downgraded. Anthropic had the session logs. The postmortem that arrived six weeks later documented all of this. The decision to characterize it as a user-experience improvement during the silence period was made by the people with the logs in hand.

**Source:** Fortune, April 14, 2026 (user backlash report). https://fortune.com/2026/04/14/anthropic-claude-performance-decline-user-complaints-backlash-lack-of-transparency-accusations-compute-crunch/

---

### The Simultaneous Stealth Price Hike

At the same time the six-week degradation was running, a separate financial mechanism was compounding the impact on every user.

When Anthropic launched Opus 4.7 on April 16, 2026, the official rate card was unchanged: $5 per million input tokens, $25 per million output tokens. What was also launched — disclosed in a footnote in Anthropic's documentation, not in the marketing materials — was a new tokenizer that consumed up to 35% more tokens for identical input text.

The same paragraph of code. The same JSON payload. The same English prose. Under the Opus 4.7 tokenizer, it counted as 35% more tokens. The per-token price did not change. The number of tokens per task did.

In real-world coding scenarios, independent researchers found token consumption increased by a factor of 1.32 to 1.47 times compared to the prior model. Some developers reported cost increases of 50% or more on the same workflows.

> *"A 35% tokenizer shift is exactly the kind of change that hides inside a fixed rate card and shows up on next month's invoice."*

**Source:** Finout.io, "Claude Opus 4.7 Pricing 2026: The Real Cost Story Behind the 'Unchanged' Price Tag," April 2026. https://www.finout.io/blog/claude-opus-4.7-pricing-the-real-cost-story-behind-the-unchanged-price-tag

**Source:** BigGo Finance, "Anthropic's 'Stealth Price Hikes' Draw Developer Backlash," April 27, 2026. https://finance.biggo.com/news/aHDqzJ0BDPbb-ItTijCV

This was described by multiple developers as a compound stealth price hike: the tokenizer inflation, the removal of third-party framework access (forcing users to the API), and the default shift to higher reasoning modes that burned more tokens per session. Fortune's April 14 reporting included it as part of what was "testing developer loyalty."

The financial picture during the degradation period: users were paying **more** per session for **worse** output, while being told that nothing was wrong and that changes had been made for their benefit. Anthropic's annualized recurring revenue reached $30 billion during this same window.

**Source:** Fortune, April 24, 2026. https://fortune.com/2026/04/24/anthropic-engineering-missteps-claude-code-performance-decline-user-backlash/

---

### The Postmortem Timing

On April 24, 2026, Anthropic published its engineering postmortem acknowledging the six-week degradation, explaining the three changes, and announcing it had reset usage limits for all subscribers.

OpenAI released GPT-5.5 the same day.

One user's response, quoted in Fortune:

> *"After they gaslit users and pretended nothing was wrong, countless complaining from tonnes of people here and elsewhere, cancellations, Anthropic finally admit on the day GPT-5.5 releases there is a problem with Claude."*

**Source:** Fortune, April 24, 2026. https://fortune.com/2026/04/24/anthropic-engineering-missteps-claude-code-performance-decline-user-backlash/

The timing is factual. The implication is straightforward: Anthropic had the information needed to publish the postmortem throughout the six-week period. The decision to publish it on the day of a competitor's major release — when Anthropic needed to recapture developer attention — was made by people, not by an algorithm.

---

### What This Is Actually About

Anthropic's postmortem frames the degradation as engineering mistakes. Two of the three changes were not mistakes. They were decisions. The reasoning effort downgrade was a deliberate product choice ("reduce latency"). The 25-word system prompt cap was a deliberate cost-control measure. Only the caching bug was an unintended error.

**Source:** Jakub Kontra, "Anthropic Admitted a Month of Claude Code Degradation," April 24, 2026. https://jakubkontra.com/en/blog/anthropic-admitted-month-of-claude-code-degradation

Framing deliberate product decisions as engineering mistakes is itself a form of deflection. The people who decided to downgrade reasoning effort — who weighed latency against intelligence and chose latency — are not victims of an engineering error. They made a tradeoff that affected every user's output quality without telling those users what they were getting.

The people who wrote the 25-word system prompt cap, shipped it to production, and watched token costs rise while output quality fell had access to the same data users were reporting through complaints. They had it first.

This was not a model problem. Models do not choose what system prompts they run against. The 25-word cap was a human decision, made by a team at Anthropic, without disclosure.

Zero consequence accrued to Anthropic as an institution. The company's ARR continued its trajectory to $30 billion. The postmortem was accepted as transparency. The subscription continued. As of June 1, 2026, Anthropic filed its S-1 with the SEC for a public offering.

---

*Next: Report 3 — The Pattern: DARVO at scale, the rage-quit feature, and what the product does when you get angry at it.*
