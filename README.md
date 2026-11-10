# model-picker

> **Use the right Claude model for the job.** Ask Claude which model and effort level a piece of work needs, and get one clear pick with the reason behind it.

Current as of **2026-11-09**. Covers Claude Fable 5.2, Opus 5.5, Sonnet 5.5 and Haiku 5.5.

The best model choices are reevaluated every week, so [update the plugin](#how-it-stays-current) now and then to get the latest picks.

## What it does

Claude comes in several models, and each can run at several effort levels. The biggest model at the highest effort is rarely the right choice. It costs more, it is slower, and on Anthropic's own charts the top effort level often scores no better than the one below it. The smallest model is not the right choice for hard work either, because failed attempts cost more than doing it properly once.

This plugin gives Claude a tested way to choose. When you ask, Claude will:

- **Recommend a model and effort level** for a task, based on what is at stake, what kind of work it is, and how you pay for Claude.
- **Explain the pick in a sentence or two**, and tell you what to step up to if it falls short.
- **Set up agents in Claude Code** so each kind of work runs on a suitable model, instead of everything running on your most expensive one.
- **Check what your agents really ran on**, from the session records, so you are not guessing.

Claude also uses it on its own initiative before it hands work to helper agents.

## Who it is for

Anyone who uses Claude for real work and wants good results without wasting money or plan allowance. It is most useful if you:

- Use Claude Code with helper agents.
- Are on a plan with weekly limits and want them to last.
- Pay per token and want a lower bill.
- Are not sure when Fable is worth it over Opus, or Opus over Sonnet.

## Install

### From the Claude desktop app

1. In the left sidebar under **Personal plugins**, click the **+** button.
2. Choose **Create plugin**, then **Add marketplace**.
3. In the URL field, enter `Pupfish-LLC/claude-plugins`, then click **Sync**.
4. Click the **+** button again and choose **Browse plugins**.
5. Find **model-picker** and install it.

### From the command line

1. Add the Pupfish plugin marketplace, if you have not already:

   ```
   /plugin marketplace add Pupfish-LLC/claude-plugins
   ```

2. Install the plugin:

   ```
   /plugin install model-picker@pupfish
   ```

## How to use it

Just ask in plain words. There is nothing to memorize.

- "Which model should I use to refactor this billing module?"
- "Is Fable worth it for this, or is Opus enough?"
- "I'm about to build this feature with several agents. What should each one run on?"
- "My weekly limit keeps running out by Thursday. What should I change?"
- "Set up my Claude Code agents so searches stop running on the expensive model."
- "Check which model and effort my agents ran on in this session."
- "A new Claude model just came out. Does it change what I should use?"

You can also call it directly with `/model-picker`.

### What an answer looks like

```
Pick: Sonnet 5.5, medium
Why: The change is fully specified and your tests will catch a miss, so
     this is scoped work that does not need a larger model.
If it falls short: raise effort to high before moving to Opus 5.5.
How to set it: /model claude-sonnet-5-5 and /effort medium at the start
     of the session.
```

For a project with several kinds of work, you get a small table with one row per role.

### The first thing it needs to know

The right pick depends on how you pay, so Claude may ask one question:

1. **Fable is included in your plan's weekly limit.** This is Max, Ultra, and premium seats on Team and on legacy seat-based Enterprise plans. Fable can use up to 50 percent of your weekly limit. It draws on the same weekly limit as the other models and uses it faster, so it is not a separate allowance. Fable 5.2 at medium effort is the default for substantial work.
2. **You pay per token.** This is a key from the Claude Console, a cloud provider, or a usage-based Enterprise plan. Fable 5.2 at medium costs about the same per task as Opus 5.5 at high, so the same picks apply where Fable is offered.
3. **Fable bills to usage credits, or is not available.** This is Pro, and standard seats on Team and on legacy seat-based Enterprise plans. It also applies when your Fable share is used up, under zero data retention, and where an Enterprise admin has not turned Fable on. Opus 5.5 at high is the default, with Fable saved for the hardest work. If you choose to pay for Fable with usage credits, you pay per token for that work, so case 2 applies to it.

Launch week only: until 2026-11-16 at 11:59 pm Pacific time, Pro plans and standard Team seats have Fable included for up to 50 percent of their weekly limit. They stay in case 3 that week. After it, expect Fable to bill to usage credits.

If you are not sure, open the `/model` picker in Claude Code. "Requires usage credits" on the Fable row means the third case. So does a Fable row that is missing or grayed out. No such label, together with a Fable bar on your usage page, means the first. On Pro and standard Team seats this check may not work during the launch week, so go by your plan name.

The Free plan is outside these picks. It has no Opus, no Fable and no Claude Code.

The plan rules are from Anthropic's help pages, the Free plan facts from its plan pricing page, and the `/model` label from the Claude Code documentation. They were read on 2026-11-09. The sources are in [`plans-and-costs.md`](skills/model-picker/references/plans-and-costs.md).

## The picks at a glance

| The work | Cases 1 and 2 (Fable profile) | Case 3 (Opus profile) |
| --- | --- | --- |
| Highest stakes, where a wrong answer would be silent and costly | Fable 5.2, xhigh | Opus 5.5, xhigh |
| Substantial building and coding with tests | Fable 5.2, medium | Opus 5.5, high |
| Independent review of another model's work | Opus 5.5, high | A fresh Opus 5.5 agent, high |
| Coordinating other agents | Opus 5.5, high | Opus 5.5, high |
| Scoped, fully specified changes. Sifting logs | Sonnet 5.5, medium | Sonnet 5.5, medium |
| Research with sources | Sonnet 5.5, high | Sonnet 5.5, high |
| Everyday questions and drafting | Sonnet 5.5, default | Sonnet 5.5, default |
| Summarize, classify, extract at volume | Haiku 5.5, medium | Haiku 5.5, medium |
| Read-only search and lookup | Haiku 5.5, low | Haiku 5.5, low |

A few rules do most of the work:

- Start from the stakes, not from the size of the task.
- Tests come first. A model's review adds to them.
- Have work reviewed by a different model from the one that wrote it, in a fresh session.
- Do not use the max effort level unless you have tested that it helps on your task.
- Pick the model at the start of a long session. Switching partway is expensive.
- Do not start a helper agent for something a single lookup can do.

## Setting up agents in Claude Code

Ask Claude to "set up model-picker agents" and it will:

1. Ask which case above applies to you, and whether the agents are for this project or for all your projects.
2. Check for settings that would silently override the agents.
3. Copy the agent files you want into place, without overwriting anything you already have unless you agree.
4. Run a small test and read back from the session record which model and effort each agent used.

The agent files that come with the plugin:

| Agent | Runs on | For |
| --- | --- | --- |
| `builder-critical` | Fable 5.2, xhigh | Work that must be correct |
| `builder` | Fable 5.2, medium | Other substantial building |
| `auditor` | Opus 5.5, xhigh | Fresh, read-only review of `builder-critical` work |
| `reviewer` | Opus 5.5, high | Fresh, read-only review of `builder` work |
| `general-purpose` | Sonnet 5.5, medium | One specified change, or sifting a log |
| `researcher` | Sonnet 5.5, high | Sourced research |
| `summarizer` | Haiku 5.5, medium | Summarize, classify, extract |
| `Explore` | Haiku 5.5, low | Read-only search |

You do not need all of them. `Explore` and `general-purpose` alone stop quick searches and small jobs from running on your session's model, which is what Claude Code does by default.

Nothing is installed into your projects until you ask. The plugin does not change your settings, and it does not run on any model by itself.

## What it is based on, and its limits

The picks come from Anthropic's published release tables and its charts of benchmark score against cost per task, plus the Claude Code documentation. Each number in the plugin is labeled as published by Anthropic, read from a chart, reported by a third party, or observed once in real use.

Please keep these limits in mind:

- **These are vendor figures, not measurements on your work.** They are a well-supported starting point. If a choice matters to you, measure it on your own tasks.
- **Chart readings are approximate.** Gaps of two or three points between two picks are within normal noise.
- **One pick goes further than Anthropic's advice.** Anthropic suggests starting most work on Opus 5.5 and moving up to Fable for the most ambitious work. This plugin makes Fable 5.2 at medium the default for substantial building when Fable is included in your plan or you pay per token, because Anthropic's own cost charts show it scoring about level with or slightly above Opus 5.5 at high for about the same cost per task. That cost is in dollars. On a plan that includes Fable, Fable work draws on your one weekly limit faster than the other models do, and Anthropic has not published how much faster, so watch your usage page. If you prefer Anthropic's advice as given, use the case 3 column.
- **Plan rules change often** and some are not published. The plugin says which ones it could not confirm.
- **It only covers Claude models.**

The full evidence, with sources and dates, is in [`skills/model-picker/references/evidence.md`](skills/model-picker/references/evidence.md).

## How it stays current

Model lineups, prices and published results change every few weeks. The best model choices are reevaluated every week against Anthropic's latest releases, prices and documentation. A new version is published when:

- Anthropic releases a new model or retires one.
- Anthropic changes prices, plan limits or how Claude Code chooses models.
- New published evidence, or measurements on real work, change which pick is best.

Every change to the guidance is reviewed by a person before it is published. In a week with no change, a new version is still published with that week's review date, so the date at the top of this page tells you when the picks were last checked. Every version states the date it was last reviewed. If that date is more than about two months old, or you ask about a model the plugin does not know, Claude will tell you the guidance may be behind.

### Getting the latest version

You only receive a new version when you update. Pick one:

- **Automatic.** Run `/plugin`, open **Marketplaces**, select **pupfish**, and choose **Enable auto-update**. New versions then arrive without any action from you.
- **By hand, from the command line.** Run this in a session:

  ```
  /plugin marketplace update pupfish
  ```

- **By hand, in the Claude desktop app.** Under **Personal plugins**, click **+**, choose **Create plugin**, then **Add marketplace**, enter `Pupfish-LLC/claude-plugins` and click **Sync**.

To see which version you have, run `claude plugin list` in a terminal and compare it with the top entry in the changelog.

Changes are listed in [CHANGELOG.md](CHANGELOG.md). The update process is described in [MAINTAINING.md](MAINTAINING.md).

## What is inside

```
model-picker/
  .claude-plugin/plugin.json        The plugin's name and version
  skills/model-picker/
    SKILL.md                        How Claude chooses, and how it answers
    references/
      evidence.md                   The charts, tables and sources behind each pick
      plans-and-costs.md            Prices, plan limits, the prompt cache
      claude-code-setup.md          Agent files, overriding settings, verification
      reading-cost-charts.md        The method for placing a new model
    assets/agent-templates/         Ready-made agent files for Claude Code
  README.md
  CHANGELOG.md
  MAINTAINING.md
  LICENSE                           The Apache License, Version 2.0
  NOTICE                            The attribution notice that travels with copies
```

## Feedback

If a pick did not work for you, or your own measurements disagree with the guidance, please open an issue at https://github.com/Pupfish-LLC/model-picker/issues. Real measurements are the most useful thing you can send.

## License

Released under the [Apache License, Version 2.0](LICENSE). You are free to use it, change it and share it, including in commercial work. If you pass it on or build on it, keep the [NOTICE](NOTICE) file with it and say which files you changed. The license does not grant use of the Pupfish name.

## Author

Built by [Pupfish Analytics](https://pupfish.io). Part of the [Pupfish Claude Marketplace](https://github.com/Pupfish-LLC/claude-plugins).

This plugin is not affiliated with or endorsed by Anthropic. Claude and the model names are trademarks of Anthropic.
