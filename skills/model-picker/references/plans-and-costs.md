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

Confirmed on Anthropic's help page (read 2026-11-09):

| Plan | Limits |
| --- | --- |
| Pro | A five-hour session limit and a weekly limit |
| Max | A five-hour session limit, a general weekly limit, and a separate weekly limit for Fable |
| Ultra | A general weekly limit and a separate weekly limit for Fable. Verified Ultra accounts have no five-hour limit |

- These limits are shared between the Claude apps and Claude Code.
- Team and Enterprise seats have a per-seat allowance on a rolling five-hour window and a weekly window, sized by seat tier.

From the Fable 5.2 release (2026-11-09):

- Fable is included for up to 50 percent of weekly usage limits on Pro plans and standard Team seats.
- Plans and seats that include Fable get one to three Fable limit resets, depending on how long the person has subscribed.

Not confirmed:

- One third-party summary says the Pro and standard Team share is a launch offer that ends 2026-11-16, after which Fable on those plans bills to usage credits. Anthropic's page, as read, does not state an end date. Treat Fable on Pro and standard Team as something that may cost extra, and check.
- How large the Fable weekly limit is on Max and Ultra, and whether Fable work also counts against the general limit. One third-party summary says "up to 50 percent of weekly limits".
- How plans weigh models against each other inside the general limit.
- What a Fable limit reset clears.

Observed once (Ultra plan, 2026-11-09): the usage page showed "Weekly, all models" and "Weekly, Fable" as two bars that reset together. About 38,000 tokens of Fable work moved neither bar by a whole percent.

Practical advice:

- To learn what Fable costs on a given plan, read both limits before and after the first real piece of Fable work.
- Spread work across both limits where there are two: heavy building on the Fable limit, and coordination, review and helpers on the general one.
- A weekly allowance unused at the reset is lost. If a limit is heading to end the week well under its cap, step the default up one level.
- If a limit is running out early and a free limit reset is available, use it before stepping the important work down.

## 4. Usage credits and fast mode

- With usage credits switched on, work continues past a plan limit and is billed at per-token rates. Switch them off unless that is wanted.
- On some plans choosing Fable bills to usage credits. Claude Code shows a consent prompt the first time. If the user sees that prompt, they are on the Opus profile unless they choose to pay.
- Fast mode costs about double and, on a subscription, draws on usage credits. Keep it off for agent work.
- If an `ANTHROPIC_API_KEY` environment variable is set, Claude Code uses it instead of the subscription and the work is billed per token.

## 5. The prompt cache

Claude Code resends the whole conversation on every request. The cache lets the unchanged part be reread at the cheap cache-read price. Anything that breaks the cache makes the next request reread everything at full price once.

Breaks the cache:

- **Switching models.** Each model has its own cache. This is why a long session should not change model midway.
- A skill or command whose front matter names a `model` different from the session's. It switches models for that turn.
- The `opusplan` setting, at every switch into and out of plan mode.
- Turning fast mode on (once per conversation).
- Compacting the conversation, by design.
- A break longer than the cache lifetime.

Keeps the cache:

- **Changing effort** on Opus 5.5, Sonnet 5.5, Haiku 5.5 and Fable 5.1, when signed in with a subscription or a Claude Platform key. The documentation had not yet been updated for Fable 5.2 at the review date. On other models and on cloud providers, changing effort breaks the cache.
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
- Read both weekly limits before and after a representative piece of work.
- The measures worth tracking: tokens per accepted result, and how often a helper's output is used as is, fixed, or redone.
