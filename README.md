# model-picker

> **Use the right Claude model for the job.** Ask Claude which model and effort level a piece of work needs, and get one clear pick with the reason behind it.

Current as of **2026-11-09**. Covers Claude Fable 5.2, Opus 5.5, Sonnet 5.5 and Haiku 5.5.

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

- **Your plan has its own weekly Fable allowance** (Max and Ultra at the time of writing). Fable work does not draw down your general limit, so Fable 5.2 at medium effort becomes the default for substantial work.
- **You pay per token.** Fable 5.2 at medium costs about the same per task as Opus 5.5 at high, so the same picks apply where Fable is offered.
- **Fable shares your weekly limit, costs extra, or is not available.** Opus 5.5 at high is the default, with Fable saved for the hardest work.

If you are not sure, look at your usage page. A separate weekly limit labeled Fable means the first case.

## The picks at a glance

| The work | With a Fable allowance | Without |
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
- **One pick goes further than Anthropic's advice.** Anthropic suggests starting most work on Opus 5.5 and moving up to Fable for the most ambitious work. This plugin makes Fable 5.2 at medium the default for substantial building when you have a Fable allowance or pay per token, because Anthropic's own cost charts show it scoring about level with or slightly above Opus 5.5 at high for about the same cost. If you prefer Anthropic's advice as given, use the "without" column.
- **Plan rules change often** and some are not published. The plugin says which ones it could not confirm.
- **It only covers Claude models.**

The full evidence, with sources and dates, is in [`skills/model-picker/references/evidence.md`](skills/model-picker/references/evidence.md).

## How it stays current

Model lineups, prices and published results change every few weeks. This plugin is updated when:

- Anthropic releases a new model or retires one.
- Anthropic changes prices, plan limits or how Claude Code chooses models.
- New published evidence, or measurements on real work, change which pick is best.

Every version states the date it was last reviewed. If that date is more than about two months old, or you ask about a model the plugin does not know, Claude will tell you the guidance may be behind.

To get updates, turn on auto-update for the Pupfish marketplace under **Marketplaces** in `/plugin`, or run:

```
/plugin marketplace update pupfish
```

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
  LICENSE
```

## Feedback

If a pick did not work for you, or your own measurements disagree with the guidance, please open an issue at https://github.com/Pupfish-LLC/model-picker/issues. Real measurements are the most useful thing you can send.

## Author

[Pupfish Analytics](https://pupfish.io)

This plugin is not affiliated with or endorsed by Anthropic. Claude and the model names are trademarks of Anthropic.
