# Plans, prices and token costs

Last reviewed 2026-11-09. Plan rules and prices change often. When the answer matters, tell the user to check their own usage page and Anthropic's pricing page.

## Contents

1. Prices per million tokens
2. Price per token against cost per task
3. Plan limits
4. Usage credits and fast mode
5. The prompt cache
6. Token overhead of agents
7. How a user can measure their own usage

## 1. Prices per million tokens

List prices in US dollars, from Anthropic's pricing page.

| Model | Input | Output | Cache write, 5 minutes | Cache write, 1 hour | Cache read | Batch input | Batch output |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Fable 5.2 (`claude-fable-5-2`) | $8 | $40 | $10 | $16 | $0.20 | $4 | $20 |
| Opus 5.5 (`claude-opus-5-5`) | $4 | $20 | $5 | $8 | $0.20 | $2 | $10 |
| Sonnet 5.5 (`claude-sonnet-5-5`) | $2 | $10 | $2.50 | $4 | $0.10 | $1 | $5 |
| Haiku 5.5 (`claude-haiku-5-5`), prompts up to 100,000 tokens | $0.10 | $0.50 | $0.125 | $0.20 | $0.01 | $0.05 | $0.25 |
| Haiku 5.5, prompts over 100,000 tokens | $0.50 | $2.50 | $0.625 | $1 | $0.05 | $0.25 | $1.25 |
| Fable 5.1 (`claude-fable-5-1`), for comparison | $10 | $50 | $12.50 | $20 | $0.25 | $5 | $25 |

Notes:

- Sonnet 5.5 is half of Opus 5.5 on every line. Fable 5.2 is twice Opus 5.5 on input and output, and the same on cache reads.
- Haiku 5.5 is the only model with a price step. A request whose prompt is over 100,000 tokens, counting cached tokens, is charged the higher rates. So a fortieth of Opus's price becomes an eighth on long contexts. Keep Haiku agents short.
- The other current models include the full one-million-token context at standard prices.
- Fast mode: Fable 5.2 at $16 and $80, Opus 5.5 at $8 and $40. Not available with batch.
- Batch is half price on input and output.
- US-only inference costs 1.1 times on every line.
- Fable 5.2 has a one-million-token context and up to 128,000 output tokens (third party).

## 2. Price per token against cost per task

- A model that costs twice as much per token can cost less per task if it needs fewer tokens or fewer attempts. Fable 5.2 at high costs about half of Opus 5.5 at max per task on FrontierCode 2.0, despite twice the price per token.
- Agent work is mostly cache reads. Fable 5.2 and Opus 5.5 charge the same for those, and Sonnet 5.5 half. Token counts worked out from dollar figures are rough for this reason.
- Fable 5.2 against Fable 5.1 per task on FrontierCode 2.0: cheaper at low and medium, more expensive from high up, despite the lower price per token.
- Each benchmark has its own cost scale. Opus 5.5 at high costs about $2.4 per task on FrontierCode 2.0 and about $3.9 per attempt on Terminal-Bench 4.0. Only compare costs within one chart.

## 3. Plan limits

On a subscription the real currency is the plan's allowance, not dollars.

Unless a line says otherwise, the facts in sections 3 and 4 were read on 2026-11-09 and read a second time the same day to check them. A fact that was read only once says so.

### Limits by plan

Source: Anthropic help article 11145838, "Use Claude Code with your Pro, Max, or Ultra plan", https://support.claude.com/en/articles/11145838. The Fable share is from article 15424964, below.

| Plan | Limits |
| --- | --- |
| Pro | A five-hour session limit and a weekly limit |
| Max | A five-hour session limit and a weekly limit. Fable can use up to 50 percent of the weekly limit |
| Ultra | A weekly limit. Fable can use up to 50 percent of it. Verified Ultra accounts have no five-hour limit |

- These limits are shared between the Claude apps and Claude Code.
- Team and Enterprise seats have a per-seat allowance on a rolling five-hour window and a weekly window, sized by seat tier (read once, 2026-11-09).
- The Free plan is outside this lineup. It has no Opus, no Fable, no Claude Code and no usage credits (Anthropic's plan pricing page, https://claude.com/pricing, read 2026-11-09).

### Where Fable is included, and where it bills to usage credits

Source: Anthropic help article 15424964, "Claude Fable models on your plan", https://support.claude.com/en/articles/15424964.

| Plan or seat | How Fable is paid for |
| --- | --- |
| Max, Ultra, premium seats on Team plans, premium seats on legacy seat-based Enterprise plans | Included in the plan. Fable draws from the plan's regular weekly limit and uses it faster than other Claude models. Up to 50 percent of the weekly limit can go to Fable at no extra cost. After that, the choice is to keep using Fable with usage credits or to switch to another model |
| Pro, standard seats on Team plans, standard seats on legacy seat-based Enterprise plans | Not included in the plan's usage limits. Fable bills to usage credits. Standard Enterprise seats can use Fable only if the organization has enabled usage credits |
| Usage-based Enterprise plans, and the Claude Platform | Billed at standard API rates |

- The Fable share is a cap inside the weekly limit. It is not a separate pool. In Anthropic's words: "your use of other models draws from the same usage limits and you can never use more than your weekly limit."
- The clearest proof is the worked example in help article 17506494 (below): someone who has used 80 percent of the weekly limit, 50 on Fable and 30 on other models, is back at 30 percent after a Fable limit reset.
- So on an included plan, every piece of Fable work uses up the same weekly limit that Opus, Sonnet and Haiku work draws on, and uses it faster.
- This is why included plans have their own picks, the Included profile in the skill. Substantial building defaults to Opus 5.5 at high. Fable 5.2 is kept for the highest-stakes work, at xhigh, and, at high, for building work where Opus 5.5 clearly tried and was still wrong. That is the plugin owner's choice, made on 2026-11-09.
- Help articles 11145838 and 12429409 still say that Max and Ultra have "a separate weekly limit for Fable". That fits the facts above if it means the 50 percent cap, which the usage page shows as its own bar. It does not mean a second pool of usage.
- The plan pricing page agrees (read 2026-11-09). It lists Fable on Max and Ultra as "50% of weekly limits". On Pro it says "Fable, paid with usage credits" on the plan card and "Usage credits" in the comparison table.
- Versions of this plugin before 2.0.0 treated the Fable limit on Max and Ultra as a separate weekly limit and advised spreading work across the two. The help article says otherwise.

### The launch week on Pro and standard Team

Source: Anthropic help article 17506494, "Claude Fable 5.2 launch offers", https://support.claude.com/en/articles/17506494. Read 2026-11-09 and re-verified the same day.

- On Pro plans and standard Team seats, Fable is included for up to 50 percent of weekly limits from the release on 2026-11-09 through 2026-11-16 at 11:59 pm Pacific time. After that 50 percent is used, or once the week ends, Fable on those plans bills to usage credits.
- This confirms the end date that the previous version of this file had only from a third party. The release post says "this week" and gives no date (read once, 2026-11-09).
- What the usage page and the `/model` picker show on those plans during the launch week was not checked.

### Fable limit resets

Same article, re-verified 2026-11-09.

- A reset gives back the usage spent on Fable models against the weekly limit. Usage on other models stays.
- It also refills the whole five-hour window, on accounts that have one.
- Max, Ultra and premium seats get 1 reset if subscribed for under 6 months, 2 for 6 to 12 months, and 3 for over 12 months. These resets expire on 2027-03-08 at 11:59 pm Pacific time.
- Pro and standard Team seats get 1 reset. It expires on 2026-11-16 at 11:59 pm Pacific time.
- Only accounts with paid billing in place before 2026-11-09 at 10:00 am Pacific time get resets.

### Where Fable is not offered

- Under zero data retention, an arrangement where Anthropic does not keep an organization's prompts and responses, Fable 5.2 is not available unless expressly authorized by Anthropic. It needs 30-day data retention (Claude Platform release notes, https://platform.claude.com/docs/en/release-notes/overview).
- On Enterprise plans, Fable 5.2 stays off until an admin enables it. Seven days after launch it is added to every role that has any Fable model enabled, unless an admin opts out first (help article 15424964).
- Where an organization cannot use Fable, the Fable row in the `/model` picker is grayed out with a note. Where a model allowlist or an organization restriction excludes it, the row is missing (Claude Code model configuration documentation).

### Not confirmed

- How plans weigh models against each other inside the weekly limit. Anthropic says only that Fable models use the limit "faster than other Claude models".
- How much faster Fable draws the weekly limit than Opus. The charts give Fable's cost in dollars per task. What the same work costs in plan allowance is not published.

Observed once (Ultra plan, 2026-11-09): the usage page showed "Weekly, all models" and "Weekly, Fable" as two bars that reset together. About 38,000 tokens of Fable work moved neither bar by a whole percent. Read together with the help article, the Fable bar tracks Fable's capped share of the one weekly limit. It is not a second allowance.

Practical advice:

- To learn what Fable costs on a given plan, read both bars before and after the first real piece of Fable work. Fable work counts against the weekly limit as well as against its own cap.
- Do not plan as if heavy building on Fable left the weekly limit free for other work. Fable work, and coordination, review and helper work on other models, all draw on the same limit, and Fable draws it faster.
- A weekly allowance unused at the reset is lost. If the weekly limit is heading to end the week well under its cap, step the default up one level. Before moving work to Fable on an included plan, check the Fable bar as well, because Fable stops being included at 50 percent of the weekly limit.
- If the weekly limit is running out early because of Fable work and a Fable limit reset is available, use it before stepping the important work down. A reset gives back only the Fable usage.

## 4. Usage credits and fast mode

- Usage credits bill at standard API rates, which are the per-token prices in section 1 (Anthropic help article 12429409, "Manage usage credits for paid Claude plans", https://support.claude.com/en/articles/12429409, read once on 2026-11-09).
- With usage credits switched on, work continues past a plan limit and is billed that way. Switch them off unless that is wanted.
- Where Fable bills to usage credits (section 3), the `/model` picker in Claude Code shows "Requires usage credits" on the Fable row. In an interactive session Claude Code can also show a consent prompt (Claude Code model configuration documentation).
- A user who sees either is on the Opus profile unless they choose to pay. Someone who chooses to pay for Fable with usage credits pays per token for that work, so situation 2 and the Fable profile apply to it.
- Through `claude -p`, which runs one prompt without an interactive session, Claude Code never asks. It bills Fable to usage credits where the plan needs them. In an application built on the Agent SDK, Anthropic's kit for building agents in code, whether the consent prompt appears is up to that application. If it does not show the prompt, the same applies (same documentation).
- Monthly API credits included with Max and Ultra plans cannot be used in Claude Code or the Claude apps, including for usage credits (help article 11145838).
- Fast mode costs about double and, on a subscription, draws on usage credits. Keep it off for agent work.
- If an `ANTHROPIC_API_KEY` environment variable is set, Claude Code uses it instead of the subscription and the work is billed per token.

## 5. The prompt cache

Claude Code resends the whole conversation on every request. The cache lets the unchanged part be reread at the cheap cache-read price. Anything that breaks the cache makes the next request reread everything at full price once.

Breaks the cache:

- **Switching models.** Each model has its own cache. This is why a long session should not change model midway.
- **An automatic fallback from Fable.** A request that a Fable model's safety checks flag, most often on cybersecurity or biology, is run again on an older Opus model: Opus 5 for biology and Opus 4.8 for cybersecurity. That is a model switch, and the session stays on that model until the user runs `/model` (Claude Code model configuration and prompt caching documentation, read twice on 2026-11-09).
- A skill or command whose front matter names a `model` different from the session's. It switches models for that turn.
- The `opusplan` setting, at every switch into and out of plan mode.
- Turning fast mode on (once per conversation).
- Compacting the conversation, by design.
- A break longer than the cache lifetime.

Keeps the cache:

- **Changing effort** on Fable 5.1 and later, Opus 5.5, Sonnet 5.5 and Haiku 5.5, when signed in with a Claude subscription or a Claude Platform key (Claude Code prompt caching documentation, https://code.claude.com/docs/en/prompt-caching, read twice on 2026-11-09). This now covers Fable 5.2. Changing effort still breaks the cache on other models, on Amazon Bedrock and Google Cloud, through a Claude apps gateway (the documentation's term), under a configuration for HIPAA, the United States health privacy law, and when `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS` is set. Microsoft Foundry is not in that list, so check before relying on either behavior there.
- Turning the advisor on or off.
- Starting a subagent. It has its own separate cache.
- Loading a skill, entering plan mode, editing files.

Cache lifetime:

| Requests | Subscription, within plan usage | Usage credits, a key, or a cloud provider |
| --- | --- | --- |
| Main conversation | One hour | Five minutes |
| Subagents and other background requests | Five minutes | Five minutes |

- To give a subagent a one-hour cache, set `experimental.cacheTtl: 1h` in its agent file, or the `subagentPromptCacheTtl` setting. A one-hour cache costs more to write, so it only pays for agents that pause for more than five minutes between turns.

## 6. Token overhead of agents

Observed once in Claude Code, November 2026:

- A helper agent that did not load project instruction files used about 5,000 to 10,000 tokens for a one-line task. An agent that loaded them used about 16,000 to 34,000.
- Seven trivial agent checks used about 97,000 tokens in all.

So starting an agent has a fixed cost. Do not start one for a lookup a single tool call can do.

From Anthropic's documentation:

- Agent teams use about seven times the tokens of a single session when teammates run in plan mode.
- A session open for hours uses more than its activity suggests, because the whole conversation is reread on every request. Clear between unrelated tasks.

## 7. How a user can measure their own usage

- In Claude Code, `/usage` shows the plan's limits and a breakdown of what used them, including the share from subagents, skills and plugins.
- Read the weekly limit, and the Fable bar where there is one, before and after a representative piece of work.
- The measures worth tracking: tokens per accepted result, and how often a helper's output is used as is, fixed, or redone.
