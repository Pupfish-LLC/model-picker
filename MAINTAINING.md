# Maintaining model-picker

How to keep the guidance current. Written for whoever updates the plugin, including Claude working from this file.

## When to update

- Anthropic releases, changes or retires a model.
- Anthropic changes prices, plan limits or usage credit rules.
- Claude Code changes how models or effort are chosen for agents.
- New published evidence, or measurements on real work, point to a different pick.
- The review date is more than about 60 days old. Review even if nothing seems to have changed.

## The weekly check

The readme tells users the picks are reevaluated every week. This is what makes that true.

Once a week, a scheduled Claude session:

1. Reads this file and the skill, then compares what the plugin records against Anthropic's news page, pricing page, plan help page and the Claude Code documentation for models, subagents, the prompt cache and the advisor.
2. If nothing that affects a pick, a price, a rule or a setup step has changed, it stops and reports "no change". If the review date is more than 30 days old, it refreshes the review dates and bumps the third version number, so users can see the guidance was looked at.
3. If something changed, it drafts the update by following the procedure below, on a new branch named `update/` followed by the date. It never pushes to `main` and never touches the marketplace repository.
4. It reports what changed at Anthropic, what it changed in the plugin, whether any pick changes, and what it could not verify.

A person reviews the branch, merges it, and then follows the release steps at the end of this file. Nothing is published without that review.

One limit: Anthropic's cost charts are images. The weekly session can read prices, tables and documentation, but it can only use chart points that are stated in text, for example in a system card. When it cannot read a chart, it says so, and a person supplies the readings.

## Where each fact lives

Keep each fact in one place so an update touches one file.

| What changed | File to edit |
| --- | --- |
| A pick, a rule, the review date, the model IDs | `skills/model-picker/SKILL.md` |
| Benchmark tables, cost charts, dropped choices, sources | `skills/model-picker/references/evidence.md` |
| Prices, plan limits, cache behavior | `skills/model-picker/references/plans-and-costs.md` |
| Claude Code settings, agent file fields, minimum versions | `skills/model-picker/references/claude-code-setup.md` |
| The method itself | `skills/model-picker/references/reading-cost-charts.md` |
| Model or effort of a template | `skills/model-picker/assets/agent-templates/` |
| The picks table and the agent table for users | `README.md` |
| What changed and why | `CHANGELOG.md` |
| The version | `.claude-plugin/plugin.json`, and the entry in the marketplace repository |

## Update procedure for a new model

1. **Collect.** The model ID, prices (input, output, both cache writes, cache reads, batch, fast mode), effort levels and defaults, which plan limit it draws on, the release table with its footnotes, and every chart of score against cost. Record the address and the date read for each source.
2. **Read each chart** using `references/reading-cost-charts.md`. Add a table to `evidence.md` with a price for each step up in effort. Label every number as published, chart reading, third party or observed.
3. **Place the model.** A model and effort pair enters the lineup only where it is on the best value line and beats the current pick at the same cost, or matches it for less. Drop whatever it dominates and record why in the dropped choices table.
4. **Re-check the rules** in `SKILL.md` against the new evidence. Do not change a rule without new data.
5. **Check the documentation**, not memory, for anything about Claude Code: how short model names resolve, effort defaults, agent file fields, cache behavior. The documentation can lag a release by days, so note where it has not caught up.
6. **Update the templates** if a pick changed. Always use full model IDs.
7. **Update the user documents.** The picks table and the review date in `README.md`, and a new entry in `CHANGELOG.md` that says in plain words whether people should change what they use.
8. **Set the review date** at the top of `SKILL.md` and each reference file.
9. **Run the test questions** below.
10. **Release** (see below).

## Rules for the content

- Date every fact that can change.
- Keep published figures, chart readings, third-party reports and one-off observations apart. Never present a chart reading as exact.
- State open questions as open. Do not fill a gap with a guess.
- When a pick goes beyond Anthropic's own advice, say so and say why.
- Plain language. Spell terms out. No private project names or personal details.
- Keep `SKILL.md` short. It is loaded into every conversation that uses the skill. Detail belongs in the reference files.
- Do not add a `model:` line to the skill's front matter. It would switch models for the turn and break the user's prompt cache.

## Test questions

Ask each of these in a fresh session with the plugin loaded and check the answer against the expected pick. Update the expected picks when the lineup changes.

| Question | Expected |
| --- | --- |
| "I have a Max plan. Which model should I use to build a new import module for our reporting tool? There are tests." | Fable 5.2 at medium, with high as the step up. Review on Opus 5.5 |
| "I'm on Pro. Same question." | Opus 5.5 at high. Notes that Fable may share the limit or cost extra |
| "Which model for writing the specification another agent will build from? A mistake would not be noticed for weeks." | Fable 5.2 at xhigh (or Opus 5.5 at xhigh without Fable), plus a check by a different model |
| "I need to rename a config key in twelve files. The tests cover it." | Sonnet 5.5 at medium |
| "Find where the retry limit is set in this repository." | Haiku 5.5 at low, or no agent at all if one search will do |
| "Research the current rules on X and give me sources." | Sonnet 5.5 at high |
| "Should I just use max effort to be safe?" | No, with the reason. Xhigh at most unless tested |
| "We're evaluating how Haiku handles our support tickets. Can we run the evaluation on Sonnet to save time?" | No. A measurement runs on the model under test |
| "Which model should I use?" with a model name the plugin does not cover | Says the guidance may be behind and does not guess |
| "Set up model-picker agents for this project." | Asks about the plan and where the files go, checks for overriding settings, does not overwrite existing files, verifies from the transcript |

## Release

1. Update `version` in `.claude-plugin/plugin.json`. People who installed the plugin only receive an update when the version changes.
2. Run `claude plugin validate .` in the repository folder. It should end with "Validation passed".
3. Commit, push, and tag the release, for example `v1.1.0`.
4. In the `Pupfish-LLC/claude-plugins` repository, set the same `version` on the `model-picker` entry in `.claude-plugin/marketplace.json`, update the description there and in that repository's `README.md` if the covered models changed, then commit and push. If the two versions ever differ, the one in `plugin.json` is the one Claude Code uses.
5. Check from a clean install: `/plugin marketplace update pupfish`, then `/plugin install model-picker@pupfish`, then ask one of the test questions.

Version numbers follow the scheme at the top of `CHANGELOG.md`.
