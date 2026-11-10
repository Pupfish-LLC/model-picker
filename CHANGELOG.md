# Changelog

All notable changes to the `model-picker` plugin are recorded here. Each entry says what changed in the guidance and why, so you can tell whether an update changes what you should use.

Version numbers:

- **First number** changes when a pick in the lineup changes for a common kind of work, or when the way the picker decides changes, such as the payment situations it asks about.
- **Second number** changes when a model is added, or evidence or rules are updated without changing the common picks.
- **Third number** changes for corrections and wording, and for each weekly review that found nothing to change. So the third number tells you roughly how many quiet weeks have passed since the guidance last changed.

## Weekly reviews with no change

The guidance is reviewed in full every week. In a week where nothing needed to change, only the review date and the version move. Those weeks are listed on the one line below, with the version published that week, and get no entry of their own.

Since 2.0.0: none yet.

## [2.0.0] - 2026-11-09

The way the picker sorts people by how they pay has changed. The picks themselves have not. The first version number moved because you may need to answer the payment question differently.

### Should you change what you use?

- **The picks are unchanged.** Every model and effort level in the picks table is the same as in 1.0.2. So are the eight agent files.
- **What changed is how to tell which column you are in.** Open the `/model` picker in Claude Code. "Requires usage credits" on the Fable row means Fable is not included in your plan, and the Opus column applies. No such label, together with a Fable bar on your usage page, means Fable is included, and the Fable column applies. The one exception is Pro and standard Team seats during the launch week: they stay in the Opus column, so go by your plan name that week.
- **On Max and Ultra, Fable shares your weekly limit.** Earlier versions said these plans had a separate weekly Fable allowance and that Fable work did not draw down the general limit. Anthropic's help page says otherwise. Fable can use up to 50 percent of your weekly limit. It draws on the same weekly limit as the other models and uses it faster. If you moved heavy work to Fable expecting your weekly limit to be untouched, watch your usage page. The same applies to premium seats on Team and on legacy seat-based Enterprise plans.
- **On Pro and standard Team seats, expect Fable to bill to usage credits after 2026-11-16.** Until 11:59 pm Pacific time that day, Fable is included for up to 50 percent of your weekly limit as a launch offer. Usage credits bill per token at standard API rates. The pick for these plans was already the Opus column, and still is. If you choose to pay for Fable with usage credits, you are paying per token for that work, and the Fable column applies to it.

One thing to know plainly. The rule in 1.0.2 sent any plan where Fable shares the weekly limit to the Opus column. Max and Ultra turn out to be such plans. This version keeps them in the Fable column, because the reason in dollars per task still holds, and says what is not known about the cost in plan allowance. Whether to move them is the plugin owner's decision and has not been made.

The plan facts above are from Anthropic's help pages, and the `/model` label is from the Claude Code documentation. They were read on 2026-11-09 and checked a second time the same day. The sources are in `plans-and-costs.md`.

### Changed: the payment situations

Before:

1. A plan with its own weekly Fable allowance (Max and Ultra). Fable column.
2. Pay per token. Fable column.
3. A plan where Fable shares the weekly limit or bills to usage credits (Pro and standard Team), or the allowance is spent, or Fable is not offered. Opus column.

Now:

1. Fable is included in the plan's weekly limit: Max, Ultra, premium seats on Team, and premium seats on legacy seat-based Enterprise plans. Fable column.
2. Pay per token: a key from the Claude Console, a cloud provider, or a usage-based Enterprise plan. Fable column.
3. Fable bills to usage credits: Pro, standard Team seats, and standard seats on legacy seat-based Enterprise plans. Also when the Fable share is spent, or Fable is not offered (zero data retention, or an Enterprise admin has not enabled it). Opus column.

The Free plan is outside the lineup. It has no Opus, no Fable and no Claude Code (Anthropic's plan pricing page, read 2026-11-09).

The change appears in step 2 of the skill, `plans-and-costs.md`, and the two matching sections of the readme.

### Corrected

- Every statement that Fable work does not draw down the general limit, or sits in a separate pool, in the skill, `plans-and-costs.md`, `evidence.md`, `reading-cost-charts.md` and the readme. The advice to spread work across two limits is removed.
- The reason given for making Fable 5.2 at medium the default. One half of it was the separate allowance, which does not exist. The other half stands: on Anthropic's charts Fable 5.2 at medium scores about level with or slightly above Opus 5.5 at high for about the same cost per task. The Opus figure is a chart reading and the gap is within normal noise.
- A subagent with no effort of its own takes the session's effort level only when it runs on the session's own model. On another model that level does not apply. Earlier versions said it always took the session's level.

### Updated facts

- Plan limits in `plans-and-costs.md`: the launch-week end date, the size of the Fable share, what a Fable limit reset clears, how many resets each plan gets and when they expire. These replace items that were listed as not confirmed. Usage credits bill at standard API rates.
- Claude Code in `claude-code-setup.md`: Fable 5.2 needs version 2.1.321. From that version `fable` means Fable 5.2 and `best` means the same model as `opus`. An effort can be passed on the call that starts an agent (2.1.292). The `autoCompactWindow` agent field (2.1.296). The advisor rule for Fable 5.2. `/model` shows "Requires usage credits". Fable through `claude -p` bills usage credits without asking, and so does an Agent SDK application that does not show the consent prompt. A request that a Fable model's safety checks flag is run again on an older Opus model and the session stays there, which breaks the prompt cache.
- Changing effort keeps the prompt cache on Fable 5.2. The notes that the documentation had not been updated for Fable 5.2 are removed where it now has been.
- `evidence.md`: three open questions closed, one added, and the new sources listed with the dates they were read.
- `MAINTAINING.md`: the expected answer to the Pro test question now says Fable on Pro bills to usage credits.

### Not changed

- The picks, the agent templates, the model IDs and the prices.
- The rules that decide close calls, apart from rule 10. It now says to judge by the weekly limit, which every model draws on, and for Fable work also by the Fable bar.

### Known gaps

- How much faster Fable uses the shared weekly limit than Opus is not published. So the plugin can state what the Fable default costs in dollars per task, and cannot state what it costs in plan allowance.
- How plans weigh Opus, Sonnet and Haiku against each other inside the weekly limit is still not published.
- What the `/model` picker and the usage page show on Pro and standard Team during the launch week was not checked.

## [1.0.2] - 2026-11-09

Documentation only. The guidance is unchanged.

### Changed

- The readme now says the best model choices are reevaluated every week, and explains the three ways to get the latest version.
- `MAINTAINING.md` describes the weekly check.
- The `NOTICE` file now asks that it be kept with any copy or adaptation.

## [1.0.1] - 2026-11-09

License change only. The guidance is unchanged, so there is nothing to do differently.

### Changed

- The plugin is now released under the Apache License, Version 2.0, in place of the earlier proprietary license. Anyone may use, change and share it.
- Added a `NOTICE` file. It must be kept with any copy that is passed on or built upon.

## [1.0.0] - 2026-11-09

First release. Guidance reviewed against Anthropic's sources on 2026-11-09, the day Claude Fable 5.2 was released.

### Models covered

- Claude Fable 5.2, Opus 5.5, Sonnet 5.5 and Haiku 5.5.

### The lineup

- Fable 5.2 at xhigh for the highest-stakes work.
- Fable 5.2 at medium as the default for substantial building, with high as the step up, for people with a Fable allowance or who pay per token.
- Opus 5.5 at high as the default without Fable, and for independent review and coordination. Opus 5.5 at xhigh for audits.
- Sonnet 5.5 at medium for scoped, fully specified work. Sonnet 5.5 at high for research with sources.
- Haiku 5.5 at medium for summarizing, classifying and extracting at volume. Haiku 5.5 at low for read-only search.

### Included

- One skill, `model-picker`, with four reference files: the evidence, plans and costs, Claude Code setup, and the method for reading cost charts.
- Eight agent templates for Claude Code, installed into a project or user folder only on request.

### Known gaps

- No per-effort cost table for Haiku 5.5, because Anthropic's charts for it carry no labeled values.
- The size of the weekly Fable allowance, and how plans weigh models against each other, are not published.
- The Claude Code documentation had not yet been updated for Fable 5.2 at the review date.
