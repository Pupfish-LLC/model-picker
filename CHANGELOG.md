# Changelog

All notable changes to the `model-picker` plugin are recorded here. Each entry says what changed in the guidance and why, so you can tell whether an update changes what you should use.

Version numbers:

- **First number** changes when a pick in the lineup changes for a common kind of work, or when the way the picker decides changes, such as the payment situations it asks about.
- **Second number** changes when a model is added, or evidence or rules are updated without changing the common picks.
- **Third number** changes for corrections and wording, and for each weekly review that found nothing to change. So the third number tells you roughly how many quiet weeks have passed since the guidance last changed.

## Weekly reviews with no change

The guidance is reviewed in full every week. In a week where nothing needed to change, only the review date and the version move. Those weeks are listed on the one line below, with the version published that week, and get no entry of their own.

Since 2.0.1: none yet.

## [2.0.1] - 2026-11-09

No pick changes, so there is nothing to do differently. This release explains how to use the plugin in a multi-agent build and shortens the readme.

### Added

- The readme's "How to use it" section now has two parts, "In a conversation" and "In a multi-agent build". The second has two lines of sample wording for a project's instructions: one to decide as agents are started, and one to give every work package an agent role in the plan.
- The skill has a matching section, "Planning a multi-agent build", so Claude assigns roles in the plan, starts agents by role, checks the agent files against the current picks at the start of each phase, and confirms what ran from the transcript.
- A test question for a planned build in `MAINTAINING.md`.

### Changed

- The readme heading "The picks at a glance" is now "The current picks at a glance".
- The word "vendor" is replaced by "Anthropic" wherever it appeared.
- The readme is shorter. The file listing is removed and the update instructions are condensed.
- The `NOTICE` file adds one sentence: "That is all that we ask."
- The readme's rule on review now says "by a different model when you can", to match the picks table, where work built on Opus 5.5 is reviewed by a fresh Opus 5.5 agent.

## [2.0.0] - 2026-11-09

One pick changes for people whose plan includes Fable. The way the picker sorts people by how they pay has changed as well.

### Should you change what you use?

- **On Max, Ultra, and premium seats on Team and on legacy seat-based Enterprise plans: yes, for substantial building.** The default for substantial building and coding with tests moves from Fable 5.2 at medium to Opus 5.5 at high. When that falls short, follow the usual order. If it skipped checks or stopped early, raise effort to xhigh. If it had the context, clearly tried and was still wrong, move to Fable 5.2 at high. The highest-stakes pick stays Fable 5.2 at xhigh. If you installed the `builder` agent file, change it to `claude-opus-5-5` with effort `high`.
- **Review on those plans.** Work built on Opus 5.5 is now reviewed by a fresh Opus 5.5 agent, so the author and the reviewer are the same model. Lean harder on tests. Highest-stakes work built on Fable is still audited on Opus 5.5 at xhigh.
- **If you pay per token: no change.** Fable 5.2 at medium stays the default for substantial building, with high as the step up.
- **On Pro and standard Team seats: no change to the picks.** Opus 5.5 at high stays the default. Expect Fable to bill to usage credits after 2026-11-16. Until 11:59 pm Pacific time that day, Fable is included for up to 50 percent of your weekly limit as a launch offer. Usage credits bill per token at standard API rates. If you choose to pay for Fable that way, the pay-per-token picks apply to that work.
- **How to tell which case you are in.** Open the `/model` picker in Claude Code. "Requires usage credits" on the Fable row means Fable is not included in your plan. No such label, together with a Fable bar on your usage page, means it is included. The one exception is Pro and standard Team seats during the launch week, so go by your plan name that week.

Why the pick changed. Earlier versions said Max and Ultra had a separate weekly Fable allowance and that Fable work did not draw down the general limit. Anthropic's help page says otherwise. Fable can use up to 50 percent of your weekly limit. It draws on the same weekly limit as the other models and uses it faster, and Anthropic does not publish how much faster. Anthropic's own advice is to start most work on Opus 5.5. So plans that include Fable now spend it where it matters most, on the highest-stakes work, and on building work where Opus 5.5 clearly tried and was still wrong. For people who pay per token the cost is in dollars, and there Fable 5.2 at medium costs about the same per task as Opus 5.5 at high on Anthropic's charts (a chart reading). This is the plugin owner's choice.

The plan facts above are from Anthropic's help pages, and the `/model` label is from the Claude Code documentation. They were read on 2026-11-09 and checked a second time the same day. The sources are in `plans-and-costs.md`.

### Changed: the payment situations and their picks

Before, two sets of picks:

1. A plan with its own weekly Fable allowance (Max and Ultra). Fable picks.
2. Pay per token. Fable picks.
3. A plan where Fable shares the weekly limit or bills to usage credits (Pro and standard Team), or the allowance is spent, or Fable is not offered. Opus picks.

Now, three sets of picks:

1. Fable is included in the plan's weekly limit: Max, Ultra, premium seats on Team, and premium seats on legacy seat-based Enterprise plans. Included picks: Fable 5.2 at xhigh for the highest stakes, Opus 5.5 at high for substantial building, and the Opus picks for everything else. When Opus 5.5 at high falls short on building work, xhigh comes first, then Fable 5.2 at high.
2. Pay per token: a key from the Claude Console, a cloud provider, or a usage-based Enterprise plan. Fable picks, unchanged.
3. Fable bills to usage credits: Pro, standard Team seats, and standard seats on legacy seat-based Enterprise plans. Also when the Fable share is spent, or Fable is not offered (zero data retention, or an Enterprise admin has not enabled it). Opus picks, unchanged.

The Free plan is outside the lineup. It has no Opus, no Fable and no Claude Code (Anthropic's plan pricing page, read 2026-11-09).

The change appears in steps 2 and 3 of the skill, `plans-and-costs.md`, `evidence.md`, `claude-code-setup.md`, the two builder agent templates, and the matching sections of the readme.

### Changed: the builder agent templates

- `builder` now ships as `claude-opus-5-5` at high, and `builder-critical` as `claude-opus-5-5` at xhigh. Before, both shipped on Fable 5.2.
- The reason is that these picks never bill Fable to usage credits on any plan. A file copied by hand on Pro could bill Fable to usage credits, and through `claude -p` it would do so without asking.
- The upgrades are in a comment at the top of each file: `builder-critical` to `claude-fable-5-2` at xhigh for cases 1 and 2, and `builder` to `claude-fable-5-2` at medium for case 2. Setup still asks which case applies and makes these changes.
- If you copied the builder files by hand on Pro or a standard seat, set them to `claude-opus-5-5`.

### Corrected

- Every statement that Fable work does not draw down the general limit, or sits in a separate pool, in the skill, `plans-and-costs.md`, `evidence.md`, `reading-cost-charts.md` and the readme. The advice to spread work across two limits is removed.
- A subagent with no effort of its own takes the session's effort level only when it runs on the session's own model. On another model that level does not apply. Earlier versions said it always took the session's level.

### Updated facts

- Plan limits in `plans-and-costs.md`: the launch-week end date, the size of the Fable share, what a Fable limit reset clears, how many resets each plan gets and when they expire. These replace items that were listed as not confirmed. Usage credits bill at standard API rates.
- Claude Code in `claude-code-setup.md`: Fable 5.2 needs version 2.1.321. From that version `fable` means Fable 5.2 and `best` means the same model as `opus`. An effort can be passed on the call that starts an agent (2.1.292). The `autoCompactWindow` agent field (2.1.296). The advisor rule for Fable 5.2. `/model` shows "Requires usage credits". Fable through `claude -p` bills usage credits without asking, and so does an Agent SDK application that does not show the consent prompt. A request that a Fable model's safety checks flag is run again on an older Opus model and the session stays there, which breaks the prompt cache.
- Changing effort keeps the prompt cache on Fable 5.2. The notes that the documentation had not been updated for Fable 5.2 are removed where it now has been.
- `evidence.md`: three open questions closed, one added, and the new sources listed with the dates they were read.
- `MAINTAINING.md`: the expected answers to the Max and Pro test questions, and a new test question for pay per token.

### Not changed

- The picks for people who pay per token, and for plans where Fable bills to usage credits or is not offered.
- Every pick on the rows that are the same for everyone: coordination, scoped changes, research, everyday questions, summarizing and lookup.
- The six agent templates other than the two builders. The model IDs and the prices.
- The rules that decide close calls, apart from rule 10. It now says to judge by the weekly limit, which every model draws on, and to check the Fable bar before moving work to Fable on an included plan.

### Known gaps

- How much faster Fable uses the shared weekly limit than Opus is not published. So the plugin can state what Fable work costs in dollars per task, and cannot state what it costs in plan allowance.
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
