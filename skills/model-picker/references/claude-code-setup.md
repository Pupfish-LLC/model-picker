# Setting models and effort in Claude Code

Last reviewed 2026-11-09 against the Claude Code documentation. Version numbers below are the minimum Claude Code version for that feature.

## Contents

1. The short version
2. Setup procedure
3. The agent templates
4. How an agent's model and effort are decided
5. Settings that silently override agent files
6. The built-in helper agents
7. When changes take effect
8. Verify from the transcript
9. The main session
10. The advisor
11. Notes for cloud providers

## 1. The short version

- Set both the model and the effort in an agent file, using the full model ID. Short names such as `opus` move to a new version with each release, sometimes late, so a full ID is the only way to know what will run.
- Do not pass a model on the call that starts an agent. That argument accepts only short names and overrides the agent file.
- Check for settings that override every agent before trusting the files.
- Prove what ran from the transcript, not from what the agent says about itself.

## 2. Setup procedure

Follow these steps when the user asks to set up or fix agent models.

1. **Choose the profile** (Fable or Opus) as in the main skill file. Ask if it is not clear, because writing Fable into agent files on a plan without a Fable allowance can bill to usage credits.
2. **Choose where the files go.** Ask the user.
   - `.claude/agents/` in the project: applies to this project and is shared with everyone who works in it.
   - `~/.claude/agents/` in the user's home folder: applies to all their projects.
3. **Look before writing.** List any agent files already there. Never overwrite one without showing the user the difference and getting a yes. If an existing agent already does a role well, only adjust its `model:` and `effort:` lines.
4. **Check for overrides** (section 5). Report any that are set and what they do. Do not change the user's settings without asking.
5. **Copy the templates** the user wants from `assets/agent-templates/` into the chosen folder. For the Opus profile, change the two builder files as shown in section 3. Adjust the body text to the project if the user wants, and keep it short.
6. **Tell the user when it takes effect** (section 7). A new agents folder needs a restart.
7. **Verify** (section 8). Start one trivial task on each new agent and read the model and effort from its transcript. Report what ran, not what was configured.

The user does not need every template. A project with no multi-agent build may only want `Explore` and `general-purpose`, so that quick searches stop running on the session's expensive model.

## 3. The agent templates

In `assets/agent-templates/`:

| File | Agent name | Fable profile | Opus profile | Role |
| --- | --- | --- | --- | --- |
| `builder-critical.md` | `builder-critical` | `claude-fable-5-2`, xhigh | `claude-opus-5-5`, xhigh | Work where a silent wrong answer would be costly |
| `builder.md` | `builder` | `claude-fable-5-2`, medium | `claude-opus-5-5`, high | Every other substantial piece of building |
| `auditor.md` | `auditor` | `claude-opus-5-5`, xhigh | same | Fresh review of `builder-critical` work. Read-only |
| `reviewer.md` | `reviewer` | `claude-opus-5-5`, high | same | Fresh review of `builder` work. Read-only |
| `general-purpose.md` | `general-purpose` | `claude-sonnet-5-5`, medium | same | One fully specified change, or sifting a log. Replaces the built-in |
| `researcher.md` | `researcher` | `claude-sonnet-5-5`, high | same | Sourced findings from files and the web |
| `summarizer.md` | `summarizer` | `claude-haiku-5-5`, medium | same | Summarize, classify, extract |
| `Explore.md` | `Explore` | `claude-haiku-5-5`, low | same | Read-only search. Replaces the built-in |

The templates ship with the Fable profile. For the Opus profile, edit only `builder-critical.md` and `builder.md`.

On the Opus profile the reviewer and the author are the same model. A fresh agent still helps, because it never saw the work being written, but it shares the author's blind spots. Lean harder on tests.

The session that coordinates the agents is not an agent file. Set it with `/model` and `/effort` (section 9). The pick is Opus 5.5 at high.

## 4. How an agent's model and effort are decided

Model, first match wins (2.1.251 or later):

1. A model passed on the call that starts the agent. Only short names are accepted there.
2. The `model:` line in the agent file. `inherit` means the main session's model.
3. The `CLAUDE_CODE_SUBAGENT_MODEL` environment variable.
4. The main session's model.

Effort:

- The `effort:` line in the agent file overrides the session's effort level.
- It does not override the `CLAUDE_CODE_EFFORT_LEVEL` environment variable.
- An agent with no effort of its own takes the session's level.
- If a model does not support a level, Claude Code uses the highest supported level at or below it.

Agents started by other agents use their own agent file's model and effort (observed).

Useful front matter fields in an agent file:

| Field | Purpose |
| --- | --- |
| `name`, `description` | Required. The description tells Claude when to hand work to this agent |
| `model` | A full model ID such as `claude-opus-5-5`, a short name, or `inherit` |
| `effort` | `low`, `medium`, `high`, `xhigh` or `max` |
| `tools` | Limits the agent's tools. Use it to make reviewers and searchers read-only |
| `omitClaudeMd` | `true` stops the agent loading the user's, project's and local `CLAUDE.md` files (2.1.271). Saves tokens and stops project reading rules from making a helper read whole documents |
| `experimental.cacheTtl` | `5m` or `1h` for the agent's prompt cache (2.1.248). Must be nested under `experimental` |

Where agent files are found, highest priority first: managed settings, the `--agents` command-line flag, the project's `.claude/agents/`, the user's `~/.claude/agents/`, then agents that come with plugins. When two share a name, the higher one wins.

## 5. Settings that silently override agent files

Check these before relying on agent files. Look in the environment and in the user, project and managed settings files.

| Setting | Effect |
| --- | --- |
| `CLAUDE_CODE_EFFORT_LEVEL` | Overrides every agent's effort |
| `CLAUDE_CODE_SUBAGENT_MODEL` | Used for agents that set no model |
| `CLAUDE_CODE_SUBAGENT_MODEL_FORCE=1` | Makes the variable above override every agent's model (2.1.257) |
| `availableModels` and related allowlist settings | A blocked model is swapped for a permitted one |
| `maxEffortLevel` (managed settings) | Caps the effort level |
| `fastMode` | Runs at about double the price |
| `ultracode` | Turns on a workflow mode that starts more agents |
| `advisorModel` | Adds a second model that agents inherit (section 10) |
| `ANTHROPIC_DEFAULT_OPUS_MODEL` and the matching Sonnet, Haiku and Fable variables | Change what the short names mean |

## 6. The built-in helper agents

Claude Code has built-in agents that it uses without being asked. By default they follow the session, so a quick search in an expensive session is expensive.

| Built-in | Model by default |
| --- | --- |
| `Explore` | The main session's model. If the main model is Fable on a subscription, it runs on the current Opus instead |
| `Plan` | The main session's model |
| `general-purpose` | `CLAUDE_CODE_SUBAGENT_MODEL` if set, otherwise the main session's model |

A user or project agent file with the same name replaces a built-in and keeps its own model. The documentation states this for `Explore`. It was observed to work for `general-purpose` as well.

The built-in `Explore` and `Plan` skip `CLAUDE.md` files. A replacement should set `omitClaudeMd: true` to keep that behavior.

## 7. When changes take effect

According to the documentation, Claude Code watches the project and user agent folders, picks up new and edited files within a few seconds, and uses them on the next hand-off. A restart is still needed when:

- The first agent file is created in a folder that did not exist when the session started.
- The agent is in a folder added with `--add-dir`.
- The session was started with slash commands turned off.

One observation disagrees. In the desktop app on 2026-11-09, four edited agent files kept their old model and effort until the app was restarted. So do not assume. Verify from the transcript, and restart if the change has not taken effect.

## 8. Verify from the transcript

Each agent's transcript is a file at:

```
~/.claude/projects/<project>/<session>/subagents/agent-<id>.jsonl
```

Each request in it records the model that ran. In the maintainer's sessions it recorded the effort as well (observed). To check an agent, start it on a trivial task, then search its transcript for `"model"` and `"effort"`.

Do not ask the agent. Agents asked about their own effort gave a number, a guess or "not stated". The transcript was exact every time (observed).

Transcripts are deleted after 30 days by default.

`claude plugin validate <folder>` and `claude --debug` report agent files that were skipped because of a missing name or front matter that does not parse.

## 9. The main session

- `/model <name>` sets the model. `/effort <level>` sets the effort. Do both at the start of a session, because a later model switch rereads the whole conversation at full price.
- The `model` and `effortLevel` settings set defaults. `effortLevel` accepts low, medium, high and xhigh, not max. Max applies to the current session only.
- Defaults at the review date: Opus 5.5 is the default model on Pro, Max, Team and Enterprise accounts. Opus 5.5, Sonnet 5.5, Haiku 5.5 and Fable 5.2 default to medium effort in Claude Code. No Fable model is the default on any plan.
- Do not put a `model:` line in the front matter of a skill used in the middle of a long session. It switches models for that turn and breaks the cache. Hand the work to an agent instead.
- Minimum versions: Haiku 5.5 as the `haiku` short name needs 2.1.293. Anthropic did not state a minimum version for Fable 5.2. If `claude-fable-5-2` is not accepted, update Claude Code.

## 10. The advisor

The advisor lets the main model consult a second, usually stronger, model at key moments. It suits long tasks where most turns are routine but the plan decides the outcome. It is a way to get stronger judgment without running the stronger model throughout.

- Turn it on with `/advisor opus`, the `advisorModel` setting, or `--advisor` at launch. Turn it off with `/advisor off`.
- It is experimental and works only when signed in to Anthropic directly, not through a cloud provider.
- The advisor must rank at or above the main model. A Fable main session accepts only a Fable advisor. Sonnet 5.5 accepts Fable, Opus 5 or later, or Sonnet 5.5. Opus 5.5 accepts Fable or Opus 5 or later. Haiku 5.5 accepts Fable, recent Opus, Sonnet 5 or later, or Haiku 5.5.
- Each consultation rereads the whole conversation at the advisor's price with no cache discount.
- Subagents inherit the configured advisor.
- Turning it on or off does not break the main session's cache.
- A Fable advisor bills the way Fable does on the user's plan.

A sensible use on the Opus profile: Sonnet 5.5 as the main model with an Opus advisor for long routine builds. There are no published figures for the current models, so treat it as something to test.

## 11. Notes for cloud providers

- On Amazon Bedrock, Google Cloud and Microsoft Foundry the short names can point to older models. At the review date the documentation showed `sonnet` and `haiku` resolving to the 4.5 or 4.6 versions on those providers. Use full model IDs and check which models the provider offers.
- The advisor is not available there.
- Changing effort breaks the cache there.
- Billing is per token, so cost per task is what matters, and the cache lifetime is five minutes.
