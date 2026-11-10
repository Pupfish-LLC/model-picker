# Changelog

All notable changes to the `model-picker` plugin are recorded here. Each entry says what changed in the guidance and why, so you can tell whether an update changes what you should use.

Version numbers:

- **First number** changes when a pick in the lineup changes for a common kind of work.
- **Second number** changes when a model is added, or evidence or rules are updated without changing the common picks.
- **Third number** changes for corrections and wording, and for each weekly review that found nothing to change. So the third number tells you roughly how many quiet weeks have passed since the guidance last changed.

## Weekly reviews with no change

The guidance is reviewed in full every week. In a week where nothing needed to change, only the review date and the version move. Those weeks are listed on the one line below, with the version published that week, and get no entry of their own.

Since 1.0.2: none yet.

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
