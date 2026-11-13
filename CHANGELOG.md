# Changelog

All notable changes to the `model-picker` plugin are recorded here. Each entry says what changed in the guidance and why, so you can tell whether an update changes what you should use.

Version numbers:

- **First number** changes when a pick in the lineup changes for a common kind of work, or when the way the picker decides changes, such as the payment situations it asks about.
- **Second number** changes when a model is added, or evidence or rules are updated without changing the common picks.
- **Third number** changes for corrections and wording, and for each weekly review that found nothing to change. So the third number tells you roughly how many quiet weeks have passed since the guidance last changed.

## Weekly reviews with no change

The guidance is reviewed in full every week. In a week where nothing needed to change, only the review date and the version move. Those weeks are listed on the one line below, with the version published that week, and get no entry of their own.

Since 2.1.0: none yet.

## [2.1.0] - 2026-11-12

No pick changes. The one thing to check is that your own agent files set an `effort:` line, as the last bullet below explains. This release adds a large set of figures that Anthropic published, records honestly where they support the picks and where they do not, and updates how Claude Code chooses effort for subagents.

### Should you change what you use?

- **No.** Every pick in the table is the same as in 2.0.1, and so are the eight agent templates.
- **If you pay per token, know that the building default is a close call.** Fable 5.2 at medium and Opus 5.5 at high are level in score and cost on two coding benchmarks. Two others point different ways. Claude now names Opus 5.5 at high as the close alternative when it gives that pick.
- **If you want to spend less on building, Anthropic's own advice is now more specific.** It is to start on Opus 5.5 at medium and rerun only the failures at high. On Anthropic's figures that costs less than running everything at high, where tests reliably show a failure. The plugin still picks high, and now says that this goes beyond Anthropic's advice and why.
- **If your agent files set no `effort:` line, add one.** From Claude Code 2.1.317 an agent on a different model from the session runs at that model's saved effort level or its default, which may not be the level you want. The templates in this plugin already set it.

### Added: Anthropic's cost guide

Anthropic's page "Optimizing for cost and intelligence" was read on 2026-11-12. It publishes scores and costs by effort level for the current models on several benchmarks. `evidence.md` has a new section 5 with the tables, each figure labeled with its source, its unit and whether it is a single run.

- On Anthropic's subset of SWE-bench Pro, Opus 5.5 solved 92.8% of tasks at medium for $0.21 per task, 95.3% at high for $0.29, and 96.7% at xhigh for $0.74 (a single run). Fable 5.2 at high solved 96.3% for $1.39 per solved task. Anthropic's reading is that Opus 5.5 at xhigh is level with Fable 5.2 at high for a little over half the cost.
- On Anthropic's internal agentic-coding benchmark, Fable 5.2 at medium scored 88.9% for $1.34 per attempt (a single run) and Opus 5.5 at high scored 88.4% for $1.38.
- On a research benchmark, DeepResearch Bench II, Sonnet 5.5 at high was the cheapest setting run. Opus 5.5 at medium scored 2.4 points higher for 1.5 times the cost. Fable 5.2 scored no higher than either.
- Haiku 5.5 at medium now has published cost figures.
- Running at a lower effort and rerunning only the failures at high cost less than everything at high on the SWE-bench Pro subset. This is Anthropic's calculation from its runs, not a separate run.

### Reviewed and left unchanged

Each pick was checked against the new figures, using the rule that a pick changes only when another choice beats it at the same cost or matches it for less.

- **Fable 5.2 at medium for building when you pay per token.** Not changed. The new figures back it on one benchmark and point the other way on cost on another, where Fable 5.2 at medium was not run. Its evidence is now rated "moderate, and close".
- **Fable 5.2 at high as the step up when you pay per token.** Not changed. Its evidence is now rated moderate, down from strong. Against Opus 5.5 at xhigh the two are close.
- **Opus 5.5 at high for building, review and coordination.** Not changed. High scored above medium on all five benchmarks that show both, by about 2 to 7 points for about 20 to 65 percent more cost per task. The gain on the three published benchmarks is about 2 points.
- **Fable 5.2 at xhigh for the highest stakes.** Not changed. One caveat is recorded: on the research benchmark Fable 5.2 scored no higher than Opus 5.5.
- **Sonnet 5.5 and Haiku 5.5 picks.** Not changed. The new figures support Sonnet 5.5 at high for research and Haiku 5.5 at medium for narrow work. They also show Sonnet 5.5 at medium failing much more often than high on open-ended coding, so that pick stays limited to scoped changes with a check.

Five open questions are added to `evidence.md` for these, and two older ones are marked as partly answered.

### Changed in the skill

- The paragraph on why the profiles differ now gives the new evidence for and against the pay-per-token default, and tells Claude to name Opus 5.5 at high as the close alternative.
- A new paragraph says where the building picks go beyond Anthropic's advice, which names Opus 5.5 at medium as the starting point, and describes Anthropic's approach for people who prefer it.
- The delegation section notes the 2.1.317 change to subagent effort.

### Updated facts

- Claude Code, in `claude-code-setup.md`, from the Claude Code changelog read on 2026-11-12:
  - From 2.1.317, a subagent or teammate on a different model from the main conversation uses that model's saved effort level or its default, not the session's level. This answers a gap the previous version listed as not stated.
  - From 2.1.316, the `CLAUDE_CODE_SUBAGENT_EFFORT` environment variable sets the effort subagents run at when nothing else names one. Its exact place in the order is not confirmed.
  - The documentation pages had not caught up with either change on 2026-11-12, so the changelog is the only source for them.
- Also in `claude-code-setup.md`: effort levels are saved per model. By default 20 subagents can run at once, and subagents can nest three layers deep. A saved Fable 5.1 choice moves on Ultra as well as Pro and Max. The advisor note now cites Anthropic's published figures.
- Plans, in `plans-and-costs.md`, from Anthropic's help pages read on 2026-11-12:
  - Usage credits bought on or after 2026-12-07 generally expire after 12 months.
  - A wrap-up allowance lets Claude Code finish the step in progress when the five-hour limit is reached. It is rolling out gradually.
  - Claude Code now calls the five-hour window the "5-hour limit".
  - The launch offer on Pro and standard Team seats is unchanged and still ends on 2026-11-16.
- Prices were read again and every figure matched. The 128,000-token output limit is now sourced to Anthropic and applies to all four models.
- `reading-cost-charts.md`: it now carries a review date like the other reference files. Three cautions added, on cost per task against cost per solved task, on benchmarks near their ceiling and on single runs. The price-per-point thresholds now carry a note that they do not transfer to benchmarks where a task costs cents.
- `MAINTAINING.md`: the expected answer to the pay-per-token test question now names Opus 5.5 at high as the close alternative.

### Not changed

- Every pick, the payment situations, the eight agent templates, the model IDs and the prices.
- The rules that decide close calls.

### Known gaps

- Fable 5.2 at medium has no published figure on the SWE-bench Pro subset, and its figure on the internal agentic-coding benchmark is a single run. So the pay-per-token building default cannot be settled from published evidence.
- Whether to make "start lower and rerun the failures at high" a rule is undecided. The saving is published for one benchmark only.
- How much faster Fable uses the shared weekly limit than Opus, and how plans weigh the other models against each other, were still unpublished on 2026-11-12.
- The exact order between `CLAUDE_CODE_SUBAGENT_EFFORT` and a model's saved effort level was not tested.

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
- The readme's agent setup section is now its own page, [`docs/agent-setup.md`](docs/agent-setup.md), rewritten in plainer language with examples of how to ask for an agent. The readme keeps a short section near the end that links to it. The agent files and the setup steps are unchanged.

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
