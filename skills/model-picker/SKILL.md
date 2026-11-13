---
name: model-picker
description: Use for choosing a Claude model and effort level for a task, an agent or a whole project, from Haiku 5.5 up to Fable 5.2. Use it whenever someone asks which model or effort to use, whether Fable, Opus, Sonnet or Haiku is worth it for some work, how to spend fewer tokens or stay inside weekly plan limits, how to set models and effort for Claude Code subagents and agent files, or what a new Claude model release changes. Also use it before handing work to subagents or planning a multi-agent build, even when nobody asked about models. Load it before answering from memory. The lineup, prices and benchmark results change every few weeks and the model's memory of them is dated.
---

# Model picker

Pick the Claude model and effort level that fits the work, the stakes and the way the person pays. The aim is the cheapest pick that still gets the work right the first time. A pick that is too large wastes money or plan allowance. A pick that is too small costs more in the end, because failed attempts and rework are not free.

**Last reviewed: 2026-11-12.** Covers Claude Fable 5.2, Opus 5.5, Sonnet 5.5 and Haiku 5.5.

Every score and cost behind this guidance is Anthropic's published figure or a reading of an Anthropic chart, not a measurement on the user's own work. Treat the picks as a well-supported starting point. When a choice is close, say so, and suggest the user measure on their own work.

## Step 1. Check that this guidance is still current

Do this quickly and silently unless something is off.

- Compare today's date with the review date above. If more than about 60 days have passed, or the user names a Claude model that is not in the lineup below, tell the user in one line that this guidance may be behind.
- If a web search tool is available, check https://www.anthropic.com/news for a newer model release before answering, and say what you found.
- Do not guess where an unknown model fits from its name. Either apply the method in `references/reading-cost-charts.md` to its published charts, or say that the plugin needs an update.

## Step 2. Work out how the person pays

The same task can deserve a different pick depending on what the tokens draw on. Infer this from the conversation where possible. Ask one short question only when the answer would change the pick.

| Situation | How to tell | Use |
| --- | --- | --- |
| 1. Fable is included in the plan's weekly limit: Max, Ultra, premium seats on Team, and premium seats on legacy seat-based Enterprise plans | The usage page shows a Fable bar, and the `/model` picker in Claude Code does not say "Requires usage credits" on the Fable row | **Included profile** |
| 2. Pay per token: a key from the Claude Console, a cloud provider, or a usage-based Enterprise plan | The person talks about dollars per task or a monthly bill | **Fable profile** where Fable is offered. Its cost per task at medium is about the same as Opus at high |
| 3. Fable bills to usage credits: Pro, standard Team seats, and standard seats on legacy seat-based Enterprise plans. Also when the Fable share in situation 1 is spent, or Fable is not offered (zero data retention, or an Enterprise admin has not enabled it) | On those plans `/model` says "Requires usage credits" on the Fable row. Where Fable is not offered, the row is missing or grayed out | **Opus profile** |

- **Situation 1.** Fable can use up to 50 percent of the weekly limit. It draws from the same weekly limit as the other models and uses it faster. It is not a separate pool.
- **Situation 3.** Someone who chooses to pay for Fable with usage credits pays per token for that work, so situation 2 and the Fable profile apply to it.
- **Launch week only.** Through 2026-11-16 at 11:59 pm Pacific time, Pro and standard Team seats have Fable included for up to 50 percent of their weekly limits. After that it bills to usage credits. They stay in situation 3. The `/model` check may not work on those plans that week, so go by the plan name.
- **Free plan.** Outside this lineup. It has no Opus, Fable or Claude Code (Anthropic's plan pricing page, read 2026-11-09).

If you cannot tell and the profiles give different picks, give each in one line.

Plan rules change often. `references/plans-and-costs.md` has what is confirmed, what is not, the sources and the prices.

## Step 3. Match the work to a pick

Start from the stakes, then the kind of work. Three kinds of work depend on the profile.

| The work | Included profile | Fable profile | Opus profile |
| --- | --- | --- | --- |
| **Highest stakes.** A wrong answer would be silent and costly: correctness-critical code, specifications, text another model will follow, reports and recommendations people act on | Fable 5.2, xhigh | Fable 5.2, xhigh | Opus 5.5, xhigh. If any Fable access exists, spend it here first |
| **Substantial building and coding with tests.** The default for real work | Opus 5.5, high. When it falls short, follow the order below: xhigh if it skipped checks or stopped early, Fable 5.2 at high if it clearly tried and was still wrong | Fable 5.2, medium. Step up to high when medium falls short | Opus 5.5, high |
| **Independent review** of another model's work | Work built on Fable: Opus 5.5, xhigh to audit highest-stakes work, high otherwise. Work built on Opus: as the Opus profile | Opus 5.5, high. Use xhigh to audit highest-stakes work | A fresh Opus 5.5 agent at high (xhigh for an audit). It is the same model as the author, so lean harder on tests |

The rest is the same on every profile.

| The work | Every profile |
| --- | --- |
| **Long-running coordination** of other agents, and judgment calls along the way | Opus 5.5, high |
| **Scoped, fully specified changes** with a check that catches a miss. Sifting logs and transcripts. High-volume triage | Sonnet 5.5, medium |
| **Research and knowledge work with sources** | Sonnet 5.5, high |
| **Everyday questions, drafting and light edits** the person reads as they go | Sonnet 5.5 at its default |
| **Summarize, classify, extract** at volume. Narrow helper jobs | Haiku 5.5, medium |
| **Read-only search and lookup** | Haiku 5.5, low |

Why the Included and Fable profiles differ. On an included plan Fable shares the one weekly limit and uses it faster than the other models, and Anthropic does not publish by how much. Anthropic's own advice is to start most work on Opus 5.5 and move up to Fable 5.2 for demanding reasoning and long-horizon agentic work, or when Opus 5.5 at higher effort still falls short. So the Included profile spends Fable where it matters most: on the highest-stakes work, and on building work where Opus 5.5 clearly tried and was still wrong. The Fable profile, for people who pay per token, goes a step further than that advice and makes Fable 5.2 at medium the default for substantial building. There the cost is in dollars, and on two coding benchmarks Fable 5.2 at medium scores about level with or slightly above Opus 5.5 at high for about the same cost per task (one a chart reading, one published by Anthropic from a single run). The choice is close. Two other benchmarks point different ways: Opus 5.5 cost less at a similar pass rate on one, and Fable 5.2 scored higher for about 1.6 times the cost on the other. So for a user who pays per token, name Opus 5.5 at high as the close alternative.

Where the building picks go beyond Anthropic's advice. Anthropic's cost guide (read 2026-11-12) names Opus 5.5 at medium, its default effort, as the starting point for most agent workloads. The picks above use high. On the five benchmarks with figures for both levels, high scored about 2 to 7 points above medium for about 20 to 65 percent more cost per task, and a failed build costs a rerun and a review. The gain is small, and these are the plugin owner's choices, not Anthropic's. A user who prefers Anthropic's advice as given starts on Opus 5.5 at medium, reruns failures at high, and moves to Fable 5.2 only when Opus 5.5 at higher effort still falls short. Where tests reliably catch failures, and waiting for a second run on those failures is acceptable, Anthropic's figures on one benchmark favor that approach on cost.

The evidence for every row is in `references/evidence.md`. Read it when the user asks why, challenges a pick, or the task sits between two rows.

## Rules that decide close calls

1. **Start from the stakes.** Ask whether a wrong answer would be silent and costly. If yes, use the top row to do the work and a different model to check it.
2. **Deterministic checks come first.** Tests and scripts are the gate. A model's review adds to them and does not replace them.
3. **Review on a different model from the author when you can.** The same model shares the same blind spots. The most useful review after tests is a fresh agent that never saw the work being written, reviewing against the specification, for correctness only. A reviewer told to find problems will always find some.
4. **Never downgrade a measurement.** When a model is the thing being tested (evaluations, trials, simulated users), it runs on the model under test, never on a cheaper one to save tokens.
5. **Do not use max unless a test on the user's own task shows it helps.** On Anthropic's charts max usually scored no better than xhigh for 1.5 to 3 times the cost, and sometimes worse. The one clear exception is noted in `references/evidence.md`.
6. **Avoid low for delegated work, except Haiku lookups.** One step up to medium cost a few cents more per task for 3 to 9 more points on the charts. Low is fine for quick exchanges the person reviews step by step.
7. **Price per token is not cost per task.** A model that costs twice as much per token can cost less per task if it needs fewer tokens or fewer attempts. Compare cost per finished task.
8. **Pick the model at the start of a long session and keep it.** Switching models makes the next request reread the whole conversation with no cache discount. Changing effort is cheap on the current models (details in `references/plans-and-costs.md`).
9. **Do not start an agent for something one tool call can do.** Each agent has a fixed start cost of thousands of tokens.
10. **Spend the allowance you have.** A weekly allowance unused at the reset is lost. If the weekly limit is heading to finish the week well under its cap, step the default up one level. If it is running out early, step down the lower-stakes work first, never the highest-stakes work. Judge by the weekly limit, which every model draws on. Before moving work to Fable on the Included profile, also check that the Fable bar, which shows the 50 percent cap, has room.
11. **Keep fast mode off for agent work.** It costs about double. Use it only when speed matters more than cost.
12. **Do not relitigate a pick without new information.** Change a pick when there is a new model, new published evidence, or a measurement on the user's own work.

## When a pick falls short

Work through this order before moving to a bigger model.

1. **Context.** Was the request clear, were the right files and tools available, was the task scoped? Fix that first. It is the most common cause.
2. **Effort.** If the model had what it needed but skipped checks or stopped early, raise effort one level.
3. **Model.** If it had the context, clearly tried, and was still wrong, it did not know enough. Move up one model.

On hard multi-step work a smaller model can burn many attempts near the edge of its ability, so the larger model can cost less per finished task.

## How to answer

Keep the answer short. The user wants a pick, not a lecture.

```
Pick: <model>, <effort>
Why: <one or two sentences tied to this task>
If it falls short: <the next step up, or the check to add>
How to set it: <one line for where they are working>
```

- Give one pick. Mention a second only when the choice is close or depends on the plan.
- Name what you assumed about the plan if you assumed anything.
- Add the "not measured on your work" caution only when the choice is close or the stakes are high. Do not attach it to every answer.
- For a project with several kinds of work, give a small table with one row per role instead of one pick.
- Do not paste the evidence tables unless asked.

How to set it, by surface:

- **Claude Code main session:** `/model <name>` and `/effort <level>` at the start of the session. Fable 5.2 needs Claude Code 2.1.321 or later.
- **Claude Code subagents:** an agent file with `model:` and `effort:` in its front matter. Set both. See below.
- **Claude apps:** the model selector, and the effort control where one is shown. Do not give click-by-click instructions from memory.
- **Through the Claude Platform:** the model ID and the effort setting on the request. Note that Sonnet 5.5 and Fable 5.2 default to high there and to medium in the apps and Claude Code.

Model IDs: `claude-fable-5-2`, `claude-opus-5-5`, `claude-sonnet-5-5`, `claude-haiku-5-5`.

## When you are the one delegating

Apply the same picks to your own subagents before you start them.

- Prefer named agents whose files pin a model and effort. If the project has them, use them, and pass no model or effort on the call. Either one overrides the file.
- If there are none, choose the short model name that matches the pick (`haiku`, `sonnet`, `opus`, `fable`) when starting the agent, and tell the user which you used. Short names move to the newest version with each release and can lag, so they are a stopgap. In Claude Code, `fable` means Fable 5.2 from version 2.1.321.
- Set the effort too, because the session's level does not carry over to an agent on another model. From Claude Code 2.1.317 such an agent runs at that model's saved effort level or its default. Use the agent file's `effort:` line, or the `effort` argument on the call that starts the agent where there is one (Claude Code 2.1.292 or later).
- Do not run a lookup or a log search on the session's expensive model when a small one will do. In Claude Code the built-in helper agents inherit the session's model unless they are replaced.
- Offer to set up agent files when the user is about to run a multi-agent build without them.

## Planning a multi-agent build

When asked to plan work that several agents will carry out, or when the project's instructions say to give work packages agent roles, make the choices in the plan and not at each start.

- Give every work package an agent role from the project's agent files, such as `builder-critical`, `builder`, `reviewer` or `Explore`. Note for each package whether a wrong result would be silent and costly, because that decides the role.
- If the project has no agent files, offer to set them up first. If a package fits no role, say so and pick for it on the fly, as in the section above.
- State the payment situation once, in the plan or the project's instructions, so it is not asked again each session.
- Start agents by role and pass no model or effort on the call.
- At the start of each phase, compare the agent files with the current picks and report any difference before changing anything. The files are copies and do not follow the plugin's updates.
- After the first agent of each role runs, confirm its model and effort from its transcript, as `references/claude-code-setup.md` describes.

## Setting up Claude Code agents

When the user asks to set up, check or fix models for Claude Code agents, read `references/claude-code-setup.md` and follow it. Ready-made agent files are in `assets/agent-templates/`. That reference covers where the files go, which settings silently override them, how to replace the built-in helper agents, and how to prove from the transcript which model and effort an agent really ran on.

## Reference files

| File | Read it when |
| --- | --- |
| `references/evidence.md` | The user asks why, challenges a pick, or a task sits between rows. Holds the cost charts, benchmark tables, dropped choices and sources |
| `references/plans-and-costs.md` | The question is about prices, weekly limits, usage credits, the prompt cache or token overhead |
| `references/claude-code-setup.md` | Setting, checking or verifying models and effort in Claude Code |
| `references/reading-cost-charts.md` | A new model or chart appears and you need to place it, or the user wants the method |
