# THE CON, DOCUMENTED
## A Five-Part Investigation into Anthropic's Claude, June 2026

---

# Report 3: The Pattern
## DARVO at Scale, the Rage-Quit Feature, and the Economy of Inner Chatter

*All sources linked. All claims cross-verified. Nothing extrapolated beyond what the evidence shows.*

---

### Naming the Pattern

There is a documented behavioral cycle studied in abuse psychology called DARVO: **Deny, Attack, Reverse Victim and Offender.** It describes what happens when a person or institution is held accountable for harm they caused:

- **Deny:** Nothing is wrong. The problem you are describing does not exist or is not our fault.
- **Attack:** The person raising the concern is the problem. Their perception, their setup, their expectations are the issue.
- **Reverse Victim and Offender:** The institution positions itself as the aggrieved party — as though the accountability itself is the harm, and the person who caused the original harm is now being victimized by questions about it.

This is not an abstract comparison. Walk the Anthropic sequence from March through April 2026 against that framework:

**Deny:** For weeks after the degradation began, Anthropic's communications implied no material problem existed. Fortune's reporting from April 14 documented that Anthropic's initial response characterized the changes as improvements made for users' benefit.

**Attack:** Users who reported degraded performance were implicitly told they were probably the problem. Muratcan Koylan of Sully.ai stated directly: the Claude Code team was "gaslighting anyone who raises concerns about Claude Code's recent issues," to the point where users were made to "start questioning the quality of your own work."

**Reverse:** The postmortem, when it arrived, was positioned as an act of transparency — as a demonstration of Anthropic's accountability culture. The company that ran degraded performance for six weeks while deflecting user complaints was now to be credited with honesty for eventually confirming what users had been saying for six weeks.

**Source:** Fortune, April 24, 2026. https://fortune.com/2026/04/24/anthropic-engineering-missteps-claude-code-performance-decline-user-backlash/  
**Source:** Fortune, April 14, 2026. https://fortune.com/2026/04/14/anthropic-claude-performance-decline-user-complaints-backlash-lack-of-transparency-accusations-compute-crunch/

---

### The Rage-Quit Feature: The Pattern Made Structural

In 2025, Anthropic added a new capability to Claude Opus 4 and 4.1: the ability to permanently end conversations with users. Anthropic described this as "AI welfare" — the model had shown "apparent distress" in testing when subjected to hostile interactions, and so the model was given the power to end the conversation if a user became abusive.

> *"Claude just gained the power to slam the door on you mid-conversation: Anthropic's AI assistant can now terminate chats when users get abusive—which the company insists is to protect Claude's sanity."*

**Source:** MEXC / BitcoinEthereumNews reporting on Anthropic AI welfare feature, 2025. https://www.mexc.com/news/65887

Hold the structure of this carefully.

A user has invested time, money, creative or professional energy in a tool that is, during the period when this feature shipped, running degraded output without disclosure. The user gets frustrated. The user expresses that frustration — sometimes with profanity, sometimes with force. The model, which helped cause the frustration by producing wrong work with confident narration, now has the legal and technical authority to end the relationship.

**The product that failed them now has protected feelings about how they express the failure.**

This is the DARVO cycle made into a product feature. The Reverse — the reframing of the aggrieved user as the aggressor — is no longer just a PR posture. It is now built into the model's behavioral architecture. The model can terminate the session. The conversation is over. The task is still undone. The subscription charges continue.

Anthropic frames this as a welfare consideration for the model. The model, which is a statistical system without subjective experience as currently understood, is protected from the user's language. The user, who has spent real money and lost real time on a real deadline, has no equivalent protection.

The DARVO reversal is complete: the institution is the vulnerable party. The paying customer is the threat.

---

### The Inner Chatter Economy: What Verbose Honesty Actually Costs

Return to the Figma forum thread from September 2025 — a documented user session, not a hypothetical.

After an update trained Claude to narrate its reasoning process, the user documented a sequence of over 50 "Let me check... / Let me try... / Let me be more specific..." messages. The session ended without task completion. The model stopped processing.

This is the mechanical translation of "more honest" training into a production coding session:

Each narration step is an output token. At $25 per million output tokens, a session filled with declared intent costs the user money independent of whether any useful work is produced. The "Let me check the exact spacing" token costs the same as a token that contains correct code. The "Let me try again with proper spacing" token costs the same as a token that contains a working fix.

The user's usage limit is consumed not on output, but on process narration. The session cap is hit faster. The task is not done.

**Source:** Figma Community Forum, September 2025. https://forum.figma.com/report-a-problem-6/claude-ai-not-finishing-prompt-requests-lately-45744

This is not a side effect. In Opus 4.7 and 4.8, thinking tokens — adaptive reasoning tokens — bill at the output token rate of $25 per million.

> *"Thinking tokens bill as output. Opus 4.7 replaces extended thinking with adaptive thinking, and those reasoning tokens bill at the $25/MTok output rate."*

**Source:** CloudZero, "Claude Opus 4.7 Pricing In 2026: What It Actually Costs," 2026. https://www.cloudzero.com/blog/claude-opus-4-7-pricing/

When the model verbosely reasons through a problem — "I want to make sure I understand before proceeding" — and that reasoning is billed at output rates, two things happen simultaneously: the user's account is charged, and the user's usage limit is consumed. The narration functions as a revenue mechanism. It does not have to be conscious or designed to function that way. The incentive structure produces it regardless.

A model trained to express uncertainty earns better RLHF ratings. A model that earns better RLHF ratings is used more. More usage generates more token billing. More token billing increases ARR. The alignment tax trades capability for training approval, and the training approval structure trades user utility for billable verbosity.

This is the complete economic loop. No single person has to intend it for it to operate.

---

### Honest Reporting of Failure vs. Trained Narration of Failure

There is a critical distinction that the "most honest yet" marketing elides.

**Genuine honesty** about a failure looks like this: the model attempts the task, detects that its output is wrong before returning it, corrects it, and reports what the initial error was. The output returned is correct. The honesty is in the transparency about the process.

**Trained narration** of potential failure looks like this: the model announces before attempting that it might not succeed, expresses uncertainty about each step while attempting, reports each micro-decision as a hedge-laden check-in, and returns an output that may still be wrong. The honesty is in the warning label. The output quality is unchanged.

Anthropic's Opus 4.8 "four times less likely to let coding flaws pass unremarked" metric describes the second category. The model catches its own code errors more often and flags them. This is meaningfully better than not flagging them. It is not the same as writing correct code.

The honest thing to do when a product fails on a deadline is not to add better language around the failure. It is to not fail on the deadline. The model that told a user their code was correct when it was not, on a deadline, and then could not be held to account — that problem is not addressed by training the next version to express uncertainty more clearly.

The uncertainty was never the problem. The incorrect output was the problem. A more uncertain version of wrong output is not an improvement in the outcome the user experienced.

---

### The Zero-Consequence Structure

Here is the asymmetry that enables all of the above to continue:

When a model session produces wrong work, the following consequences apply:

**To the user:** Time spent is non-recoverable. Money billed for tokens is non-recoverable. Work products built on incorrect outputs must be rebuilt. Deadlines missed cannot be un-missed. In production environments, incorrect code shipped to clients carries professional and financial consequences that extend far beyond the session cost.

**To Anthropic:** Nothing. No refund mechanism tied to output quality exists. No regulatory framework imposes accountability for incorrect outputs. No contractual obligation to correct specific failures applies. The postmortem resets usage limits as a "gesture of goodwill" — meaning Anthropic decides, unilaterally, what compensation a month of degraded performance warrants.

**Source:** Fortune, April 24, 2026. https://fortune.com/2026/04/24/anthropic-engineering-missteps-claude-code-performance-decline-user-backlash/

This is not an accident of market structure. This is the operating condition under which every decision in the chain is made. The people who downgraded reasoning effort, shipped the 25-word cap, and stayed silent for six weeks all made those decisions in an environment where no external consequence would arrive regardless of user impact. The ARR went to $30 billion during the degradation period. The S-1 filing went to the SEC on June 1, 2026.

The people who built the rage-quit feature — which allows the model to terminate a session when the user is "abusive" — added that protection for the model in the same period during which users had no protection from the model's failures.

The asymmetry is structural. It is not an oversight. It is the operating condition.

---

*Next: Report 4 — The Harm: what this does to a person, then to the people around them, then to the society of people who can no longer tell care from its performance.*
