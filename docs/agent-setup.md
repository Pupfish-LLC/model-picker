# Setting up agents

Optional. The plugin works without this.

## When this is useful

Set this up if any of these sound like you:

- You work in long sessions on an expensive model, and Claude does a lot of searching and small jobs along the way.
- You run larger builds where Claude hands work to several helper agents.
- You want building and reviewing done by separate agents, each on a suitable model.

If you mostly ask questions or do short tasks, skip it.

## Why bother

Claude can hand a piece of work to a helper agent, such as a file search or a review. Unless told otherwise, the helper uses the same model as your session. So a quick file search runs on your most expensive model.

An agent file fixes that. It is a short text file that gives a helper a name, a job, and its own model and effort level.

## The agent files

The plugin comes with eight.

| Agent | What it is for | Model and effort |
| --- | --- | --- |
| `builder-critical` | Work that must be correct | Opus 5.5, xhigh |
| `builder` | Other substantial building | Opus 5.5, high |
| `auditor` | A fresh review of `builder-critical` work | Opus 5.5, xhigh |
| `reviewer` | A fresh review of `builder` work | Opus 5.5, high |
| `general-purpose` | One clearly specified change, or sifting a log | Sonnet 5.5, medium |
| `researcher` | Research with sources | Sonnet 5.5, high |
| `summarizer` | Summarize, classify, extract | Haiku 5.5, medium |
| `Explore` | Searching your files | Haiku 5.5, low |

You do not need all eight. `Explore` and `general-purpose` alone stop quick searches and small jobs from running on your session's model. Add the others when you run larger builds.

## Set it up

Ask Claude:

> Set up model-picker agents.

Claude will:

1. Ask [how you pay for Claude](../README.md#the-first-thing-it-needs-to-know), and whether the agents are for this project or all your projects. If Fable suits how you pay, it moves one or both of the builder agents up to Fable.
2. Check for settings that would override the agent files, and tell you what it finds.
3. Copy the files you want. It asks before replacing anything you already have.
4. Test each agent and tell you which model and effort it really ran on.

Nothing is copied until you ask. If the agents do not show up afterward, restart and try again.

## Using the agents

Most of the time you do nothing. Claude hands work to an agent on its own when the job matches what the agent is for.

If you want a particular agent, name it in your request:

> Use the Explore agent to find where the invoice total is calculated.

> Have the builder agent make this change, then have the reviewer agent check it.

> Use the researcher agent to find the current prices, with sources.

For a larger build, ask Claude to give every piece of work an agent role in the plan. See [in a multi-agent build](../README.md#in-a-multi-agent-build).

## More detail

The full technical notes that Claude follows are in [`claude-code-setup.md`](../skills/model-picker/references/claude-code-setup.md).
