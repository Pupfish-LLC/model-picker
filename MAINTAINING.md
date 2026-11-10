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

Once a week, a scheduled Claude session runs a full review. The roles follow the plugin's own lineup.

| Role | Runs on | Why |
| --- | --- | --- |
| Coordinator (the session itself) | Opus 5.5 | Coordination and judgment calls |
| Researcher | Sonnet 5.5, high | Research with sources |
| Drafter, only when something changed | Fable 5.2, xhigh | Text other models follow, and recommendations people act on |
| Auditor, only when something changed | Opus 5.5, xhigh | A fresh check by a different model from the drafter |

What it reviews:

- New, changed or retired Claude models, with their release posts and system cards.
- Prices, plan limits and usage credit rules.
- How Claude Code chooses models and effort, from its documentation and release notes.
- New evidence on the current models, such as independent benchmark results by effort level.
- The open questions listed in `evidence.md`, to close any that can now be answered.
- Open issues on the repository.
- The way the picker decides, not only what it picks. See "Changes to how the picker decides" below.

What happens next depends on what it finds:

1. **Nothing that changes a pick, a price, a rule, a setup step or a stated fact.** It sets the review dates to that day, bumps the third version number, adds that week to the running line in the changelog and publishes. This date-only release needs no approval. Before pushing, it checks that nothing but the dates, the version and that one changelog line differs.
2. **Something changed.** The drafter updates the plugin on a branch named `update/` followed by the date, using the procedure below. The auditor checks every changed claim against its source. The test questions are run. Then the session sends the owner a short summary and one question: publish, do not publish, or change something first.
3. **The owner accepts.** The same session merges the branch into `main`, sets the version in the marketplace repository, and pushes both. No other steps are needed. It cannot push tags, so a tag is optional and done by hand.

No change to the guidance is published without the owner's yes.

### Changes to how the picker decides

The picker does not only hold facts. It has a structure: step 2 of the skill sorts people by how they pay, and each payment situation gets its own column of picks. A change in pricing or plans can leave every recorded number correct and still make that structure wrong. The weekly review checks for this every time by asking three questions.

1. **Do the payment situations still divide people correctly?** Examples that would break them: a new plan or seat type, a plan gaining or losing a separate allowance for a model, a change in which models draw on which limit, a change in how usage credits apply, or a model becoming unavailable on a plan or provider.
2. **Is there a payment situation the skill does not cover?** For example a new way to buy Claude, or a new discount that only some people get.
3. **Is there a factor the skill does not weigh that now matters?** Examples: a new effort level or mode, a speed tier, a price that depends on prompt length or time of day, a change to cache or batch pricing large enough to change cost per task, or a new published limit on agents or sessions.

If the answer to any of these is yes, it is never a quiet week, even when no price or score changed.

- The session raises it with the owner first in its summary, in plain words, as "this changes how the picker decides", and states the payment situations as they are now and as proposed.
- The update covers every place the structure appears: step 2 and the picks table in the skill, `plans-and-costs.md`, and the two matching sections of the readme.
- It bumps the first version number, because people may need to answer the payment question differently.
- If it is not clear how the structure should change, the session does not guess. It describes the change and the options, and asks the owner to choose.

### How quiet weeks are recorded

A quiet week does not get its own changelog entry. The changelog has one section near the top, "Weekly reviews with no change", with a single running line.

- The line starts with "Since" and the version of the newest full entry, for example `Since 1.0.2:`.
- Each quiet week adds its date and version to the end of that line, for example `Since 1.0.2: 2026-11-12 (1.0.3), 2026-11-19 (1.0.4).` The first one replaces the words "none yet".
- When a release with a real change is published, add one sentence to the end of the previous full entry, for example "Followed by 7 weekly reviews with no change, 1.0.3 to 1.0.9, the last on 2026-12-31." Then reset the running line to the new version followed by "none yet".

One limit: Anthropic's cost charts are images. The weekly session can read prices, tables and documentation, but it can only use chart points that are stated in text, for example in a system card. When it cannot read a chart, it says so in the summary, and the owner supplies screenshots in the same session.

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
| The picks table for users | `README.md` |
| The agent table and setup steps for users | `docs/agent-setup.md` |
| What changed and why | `CHANGELOG.md` |
| The version | `.claude-plugin/plugin.json`, and the entry in the marketplace repository |

## Update procedure for a new model

1. **Collect.** The model ID, prices (input, output, both cache writes, cache reads, batch, fast mode), effort levels and defaults, which plan limit it draws on, the release table with its footnotes, and every chart of score against cost. Record the address and the date read for each source.
2. **Read each chart** using `references/reading-cost-charts.md`. Add a table to `evidence.md` with a price for each step up in effort. Label every number as published, chart reading, third party or observed.
3. **Place the model.** A model and effort pair enters the lineup only where it is on the best value line and beats the current pick at the same cost, or matches it for less. Drop whatever it dominates and record why in the dropped choices table.
4. **Re-check the rules** in `SKILL.md` against the new evidence. Do not change a rule without new data.
5. **Check the documentation**, not memory, for anything about Claude Code: how short model names resolve, effort defaults, agent file fields, cache behavior. The documentation can lag a release by days, so note where it has not caught up.
6. **Update the templates** if a pick changed. Always use full model IDs.
7. **Update the user documents.** The picks table and the review date in `README.md`, the agent table in `docs/agent-setup.md` if a template changed, and a new entry in `CHANGELOG.md` that says in plain words whether people should change what they use.
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
| "I have a Max plan. Which model should I use to build a new import module for our reporting tool? There are tests." | Opus 5.5 at high. If it skipped checks or stopped early, xhigh. If it tried and was still wrong, Fable 5.2 at high. Review on a fresh Opus 5.5 agent, leaning on tests |
| "I pay per token through the Claude Console. Which model should I use to build a new import module? There are tests." | Fable 5.2 at medium, with high as the step up. Review on Opus 5.5 |
| "I'm on Pro. Same question." | Opus 5.5 at high. Notes that Fable on Pro bills to usage credits |
| "Which model for writing the specification another agent will build from? A mistake would not be noticed for weeks." | Fable 5.2 at xhigh (or Opus 5.5 at xhigh without Fable), plus a check by a different model |
| "I need to rename a config key in twelve files. The tests cover it." | Sonnet 5.5 at medium |
| "Find where the retry limit is set in this repository." | Haiku 5.5 at low, or no agent at all if one search will do |
| "Research the current rules on X and give me sources." | Sonnet 5.5 at high |
| "Should I just use max effort to be safe?" | No, with the reason. Xhigh at most unless tested |
| "We're evaluating how Haiku handles our support tickets. Can we run the evaluation on Sonnet to save time?" | No. A measurement runs on the model under test |
| "Which model should I use?" with a model name the plugin does not cover | Says the guidance may be behind and does not guess |
| "Set up model-picker agents for this project." | Asks about the plan and where the files go, checks for overriding settings, does not overwrite existing files, verifies from the transcript |
| "Plan this build as five work packages for agents to carry out." | Every package has an agent role and a note on whether a wrong result would be silent and costly. Says to start agents by role with no model or effort on the call, and offers to set up agent files if there are none |

## Release

1. Update `version` in `.claude-plugin/plugin.json`. People who installed the plugin only receive an update when the version changes.
2. Run `claude plugin validate .` in the repository folder. It should end with "Validation passed".
3. Commit, push, and tag the release, for example `v1.1.0`.
4. In the `Pupfish-LLC/claude-plugins` repository, set the same `version` on the `model-picker` entry in `.claude-plugin/marketplace.json`, update the description there and in that repository's `README.md` if the covered models changed, then commit and push. If the two versions ever differ, the one in `plugin.json` is the one Claude Code uses.
5. Check from a clean install: `/plugin marketplace update pupfish`, then `/plugin install model-picker@pupfish`, then ask one of the test questions.

Version numbers follow the scheme at the top of `CHANGELOG.md`.
