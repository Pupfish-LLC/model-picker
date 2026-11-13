# Evidence behind the picks

Last reviewed 2026-11-12.

## Contents

1. How to read this file
2. FrontierCode 2.0: score against cost per task
3. Terminal-Bench 4.0: score against cost per attempt
4. Other cost findings from the Fable 5.2 release
5. Anthropic's cost guide: scores and costs by effort
6. Fable 5.2 release table
7. Sonnet 5.5 release table
8. Haiku 5.5
9. What each pick rests on
10. Choices that were dropped, and why
11. Other Anthropic guidance worth keeping
12. Open questions
13. Sources

## 1. How to read this file

Each number carries one of four labels. Keep them apart when quoting.

- **Published.** A figure Anthropic states in text or in a table.
- **Chart reading.** A value read off one of Anthropic's charts. The cost axes are log scales, so these are approximate.
- **Third party.** Reported by someone other than Anthropic. Named where used.
- **Observed.** Seen once by the plugin's maintainer in real use in November 2026. One observation, not a study.

None of it is a measurement on the user's own work. Benchmarks of this kind typically carry a few points of noise, so a gap of two or three points between two picks is not a reliable difference.

Unless a row says otherwise, release-table scores use each model's highest available effort (Anthropic's footnote on the Fable 5.2 table).

## 2. FrontierCode 2.0: score against cost per task

Source: the Fable 5.2 release (2026-11-09). FrontierCode is run by Cognition. It measures whether a model's code changes to open-source repositories would be merged by the maintainers. Version 2.0 rebuilt the tasks and grading, so its scores cannot be compared with version 1.1.

Fable 5.2's points are published in the system card. Opus 5.5's max point and Fable 5.1's xhigh point are published. The other Opus 5.5 and Fable 5.1 points are chart readings, taken as low to max from left to right, which the published points confirm.

| Effort | Fable 5.2 | Opus 5.5 | Fable 5.1 |
| --- | --- | --- | --- |
| Low | $2.10, 34.2% | about $0.75, 14.7% | about $3.0, 20.6% |
| Medium | $2.48, 37.6% | about $1.7, 30.1% | about $3.9, 21.5% |
| High | $6.72, 45.3% | about $2.4, 34.5% | about $5.4, 25.7% |
| Xhigh | $14.19, 49.1% | about $5.2, 43.4% | $8.68, 32.4% |
| Max | $44.70, 45.7% | $12.82, 45.5% | about $11.5, 31.7% |

What each step up costs:

| Step | Points gained | Extra cost | Cost per point |
| --- | --- | --- | --- |
| Fable 5.2 low to medium | +3.4 | +$0.38 | about $0.11 |
| Opus 5.5 medium to high | +4.4 | +$0.7 | about $0.16 |
| Opus 5.5 high to xhigh | +8.9 | +$2.8 | about $0.31 |
| Fable 5.2 medium to high | +7.7 | +$4.24 | about $0.55 |
| Fable 5.2 high to xhigh | +3.8 | +$7.47 | about $1.97 |
| Opus 5.5 xhigh to max | +2.1 | +$7.6 | about $3.60 |
| Fable 5.2 xhigh to max | -3.4 | +$30.51 | never worth it |

Readings:

- Fable 5.2 at high is about level with Opus 5.5's best score for roughly half the cost per task (published by Anthropic).
- Fable 5.2 at xhigh has the highest score of any released model on the chart (published).
- Fable 5.2 at medium sits about 3 points above Opus 5.5 at high for about the same cost. The Opus point is a chart reading and the gap is within normal noise, so read this as "about level, possibly slightly ahead".
- Opus 5.5 at xhigh sits close to Fable 5.2's line.
- Fable 5.1 is below both at every cost.
- GPT-6 Astra (best 42.8%) and Gemini 4 Carbon (best 41.1% at medium) are on the same chart, below Fable 5.2 and Opus 5.5.
- Third party: on 2026-11-09 Cognition's live board listed Fable 5.2's costs exactly 25 percent higher at every effort ($2.62, $3.10, $8.40, $17.73 and $55.87) than the system card. That ratio matches the old Fable price of $10 and $50 against the new $8 and $40, so the board was probably still priced at Fable 5.1's rates. This is an inference, not something either source states. Use the system card figures.

## 3. Terminal-Bench 4.0: score against cost per attempt

Source: the Sonnet 5.5 release (2026-09-28). Terminal-Bench scores agentic tasks in a command-line terminal. All values are chart readings except the top scores, which are published. Opus 5.5's points are read as low to max, which the table's footnote confirms (66.4% at xhigh).

| Effort | Sonnet 5.5 | Opus 5.5 |
| --- | --- | --- |
| Low | about $0.76, 20% | about $1.3, 38.5% |
| Medium | about $0.83, 28.8% | about $2.9, 57.6% |
| High | about $1.9, 43% | about $3.9, 64.2% |
| Xhigh | about $5.3, 61.5% | about $7.3, 66.4% |
| Max | about $12.5, 70.6% | about $11.2, 64.7% |

What each step up costs:

| Step | Points gained | Extra cost | Cost per point |
| --- | --- | --- | --- |
| Sonnet 5.5 low to medium | +8.8 | +$0.07 | about $0.01 |
| Sonnet 5.5 medium to high | +14.2 | +$1.07 | about $0.08 |
| Opus 5.5 low to medium | +19.1 | +$1.6 | about $0.08 |
| Opus 5.5 medium to high | +6.6 | +$1.0 | about $0.15 |
| Opus 5.5 high to xhigh | +2.2 | +$3.4 | about $1.55 |
| Opus 5.5 xhigh to max | -1.7 | +$3.9 | never worth it |

Readings:

- Sonnet 5.5 at low and medium are the cheapest points on the best value line.
- Sonnet 5.5 at high is a cheap step up, but at that price a mix of Opus 5.5 at low and medium would score about 46% against 43%, so Sonnet at high sits a little below Opus's line on this chart.
- Sonnet 5.5 at xhigh is beaten outright by Opus 5.5 at high, which is cheaper and scores higher.
- Sonnet 5.5 is the only model on this chart whose max beats its xhigh, and it takes the chart's top score.
- Opus 5.5 at high is a good step on both charts (about $0.15 a point here and $0.16 on FrontierCode 2.0). That is why it is the default without Fable. Section 5 adds three benchmarks with published figures for the same step.
- Opus 5.5's effort curve differs by task. On FrontierCode 2.0 it gains most from high to xhigh. Here it gains most from low to medium and flattens after high. Any effort choice made from one chart is softer than it looks.

## 4. Other cost findings from the Fable 5.2 release

All published by Anthropic in the release text. They support the pattern that Fable 5.2 at low or medium effort often matches Opus 5.5's best.

- Agentic search (WANDR): Fable 5.2 at medium matches Opus 5.5's top score for about 40 percent of the cost per attempt.
- Humanity's Last Exam: Fable 5.2 at low matches Opus 5.5's top score for less than a tenth of the cost per task.
- Chart reading (Chartography): Fable 5.2 at medium scores 66.4%, ahead of Opus 5.5 at max (64.4%), for less than a tenth of the cost per task.
- Fable 5.2 at medium uses fewer tokens than Fable 5.1.

## 5. Anthropic's cost guide: scores and costs by effort

Source: Anthropic, "Optimizing for cost and intelligence", https://platform.claude.com/docs/en/about-claude/models/optimizing-for-cost-and-intelligence, read 2026-11-12. Unless a line says otherwise, every figure in this section is published by Anthropic in that page's text, tables or benchmark notes.

How to read these figures:

- They are Anthropic's own internal runs. Anthropic calls them "directional, not guarantees".
- Costs are in US dollars at the list prices in effect when each benchmark ran. Each benchmark has its own cost scale, so compare costs only within one table.
- Watch the unit. A cost per task or per attempt counts every try. A cost per solved task divides the spend by the tasks that passed.
- Many points are a single run. The tables say which.

### SWE-bench Pro subset

Long software engineering tasks from the SWE-bench Pro benchmark by Scale AI. Anthropic uses its own 482-problem subset, and counts the Opus 5.5 and Sonnet 5.5 figures over 478 of them. It says the scores cannot be compared with the public leaderboard. The Opus 5.5 runs are from 2026-09-19 and 2026-09-20, and the Sonnet 5.5 runs from 2026-09-24. Each score pools two runs unless the row says otherwise.

Opus 5.5 by effort, on the 478 problems:

| Effort | Tasks solved | Cost per task | Cost per solved task |
| --- | --- | --- | --- |
| Low | 87.4% | $0.11 | $0.12 |
| Medium (its default) | 92.8% | $0.21 | $0.22 |
| High | 95.3% | $0.29 | $0.31 (chart label) |
| Xhigh | 96.7% (a single run) | $0.74 | not in the page's text |

Other models on the 478 problems:

| Model and effort | Tasks solved | Cost per solved task |
| --- | --- | --- |
| Sonnet 5.5, high (its default on the Claude Platform) | 87.6% | $0.11 |
| Fable 5.1, high (its default) | 92.3% (a single run) | $1.19 |

- Sonnet 5.5 at medium scored "about 7 points lower" than at high "for about 59% of the cost per task" (two runs each).
- Published as point labels on the page's "Compare models" chart, not in its prose or tables (478 problems, two runs per setting): Sonnet 5.5 at medium 80.3% at $0.07 per solved task. Opus 5.5 at high 95.3% at $0.31 per solved task.

Fable 5.2 was run on 463 of the 478 problems, the ones whose reference solutions also pass with no network access. Anthropic sets these figures beside it, all per solved task on those 463 problems:

| Model and effort | Tasks solved | Cost per solved task |
| --- | --- | --- |
| Opus 5.5, medium | 93.1% | $0.22 |
| Opus 5.5, high | 95.5% | $0.30 |
| Fable 5.2, low | 94.6% (a single run) | $0.39 |
| Opus 5.5, xhigh | 96.5% (a single run) | $0.75 |
| Fable 5.1, high | 92.4% (a single run) | $1.17 |
| Fable 5.2, high (its default on the Claude Platform) | 96.3% (a single run) | $1.39 |

- Anthropic's reading: "At a similar pass rate, Claude Opus 5.5 still costs less per solved task on these problems". Opus 5.5 at xhigh is "level with Fable 5.2 at `high` for a little over half the cost".
- Fable 5.2 at medium and at xhigh were not run on this benchmark.
- The Opus 5.5 figures differ a little between the first and third tables because they count different sets of problems. Both are Anthropic's figures, and neither is adjusted here.
- Limits Anthropic states. The Fable 5.2 costs are estimates. A cap of 16,384 output tokens per turn cut off 8 of the 463 Fable 5.2 attempts at high, and those count as failures. The Fable 5.2 runs were graded with no network access and the Opus 5.5 runs with it, so "only the problem set is matched, not the grading setup".
- Anthropic also says "Opus 5.5 and Fable 5.1 both largely saturate the SWE-bench Pro subset". This file's reading: with scores from 93 to 97 percent, this benchmark shows cost differences more clearly than it shows which of the strongest models is more capable.

Rerunning failures. Anthropic worked out, task by task from the same Opus 5.5 runs, what it would cost to run every task at a lower effort and rerun only the failures at high. This is a calculation from existing runs, with the benchmark's own tests as the failure signal. The ranges are across pairings of runs.

| Policy | Tasks solved | Cost per task |
| --- | --- | --- |
| Low, failures rerun at high | about 97% (96.4% to 97.5%) | about $0.17 |
| Medium, failures rerun at high | about 97% (96.0% to 97.1%) | about $0.24 |
| Everything at high | 95.3% (94.8% to 95.8%) | $0.29 |
| High, failures rerun at high | 96.9% | $0.31 |

- Anthropic's advice: "Use this policy for the saving, not the lift. Most of the small lift is the second attempt".
- Anthropic's two conditions. There must be a failure signal, because "a checker that passes bad work lets those failures through". And every first failure takes two runs' worth of time.

### Internal agentic-coding benchmark

An Anthropic-internal set of 370 repository tasks, graded by the repositories' own tests. Costs are per attempt. Opus 5.5 ran on 2026-09-19 and 2026-09-20, and Sonnet 5.5 on 2026-09-24. The page does not date the Fable 5.2 runs.

| Effort | Opus 5.5 | Fable 5.2 | Sonnet 5.5 |
| --- | --- | --- | --- |
| Low | 74.8%, $0.35 | 88.9%, $1.05 | not run |
| Medium | 86.6%, $0.84 | 88.9%, $1.34 | 62.7%, $0.16 |
| High | 88.4%, $1.38 | 93.5%, $5.39 | 77.8%, $0.33 |
| Xhigh | 91.1%, $4.11 | not run | not run |

- Opus 5.5 at medium and at high had five attempts per task. Every other point had one attempt per task, so treat it as a single run.
- For comparison, Fable 5.1 at high scored 85.7% (one attempt per task, 2026-10-07).

What each step up costs:

| Step | Points gained | Extra cost per attempt | Cost against the level below |
| --- | --- | --- | --- |
| Sonnet 5.5 medium to high | +15.1 | +$0.17 | about 2.1 times |
| Opus 5.5 low to medium | +11.8 | +$0.49 | 2.4 times |
| Opus 5.5 medium to high | +1.8 | +$0.54 | about 1.6 times |
| Opus 5.5 high to xhigh | +2.7 | +$2.73 | about 3.0 times |
| Fable 5.2 low to medium | 0.0 | +$0.29 | about 1.3 times |
| Fable 5.2 medium to high | +4.6 | +$4.05 | about 4.0 times |

Readings:

- Fable 5.2 at medium (88.9% at $1.34) and Opus 5.5 at high (88.4% at $1.38) are level in score and in cost. One of two published comparisons of these settings. On the defect-search benchmark below, Fable 5.2 at medium scored 2.7 points higher for 1.6 times the cost. The Fable 5.2 point is a single run.
- Fable 5.2 at low scored the same as at medium for about a fifth less.
- Fable 5.2 at high has the top score, 2.4 points above Opus 5.5 at xhigh for about 31 percent more per attempt.
- Sonnet 5.5 at high costs slightly less than Opus 5.5 at low and scores 3 points higher.

### Internal defect-search benchmark

An Anthropic-internal test of work larger than one context window: finding 130 planted defects in about 22 million tokens of source code, split into 201 parts. The score is the mean F1 over ten runs, shown here as points out of 100. F1 combines how many of the defects were found with how many of the reports were right. Costs are per run. The runs are from 2026-10-27 to 2026-11-04.

| Configuration | Score | Cost per run |
| --- | --- | --- |
| Haiku 5.5 alone, medium | 57.7 | $25 |
| Opus 5.5 alone, low | 48.9 | $38 |
| Opus 5.5 at high coordinating Haiku 5.5 subagents | 67.7 | $47 |
| Fable 5.2 at high coordinating Haiku 5.5 subagents | 71.6 | $85 |
| Sonnet 5.5 alone, high | 76.0 | $103 |
| Opus 5.5 at high coordinating Sonnet 5.5 subagents | 83.1 | $139 |
| Fable 5.2 at high coordinating Sonnet 5.5 subagents | 83.3 | $165 |
| Opus 5.5 alone, medium | 82.7 | $200 |
| Opus 5.5 alone, high | 85.0 | $236 |
| Fable 5.2 alone, low | 86.6 | $357 |
| Fable 5.2 alone, medium | 87.7 | $378 |
| Fable 5.2 alone, high | 90.9 | $563 |

- Alone, each model ran one session per part. Subagents ran at their model's default effort on the Claude Platform, which is high for Sonnet 5.5 and medium for Haiku 5.5.
- Differences Anthropic reports, with 95 percent intervals. Opus 5.5 at high over medium: 2.3 points (0.7 to 3.9). Fable 5.2 at medium over Opus 5.5 at high: 2.7 points (1.5 to 3.8) for 1.6 times the cost. Fable 5.2 at low over Opus 5.5 at high: 1.6 points (0.3 to 2.9) for 1.5 times the cost. Fable 5.2 at high over Opus 5.5 at high: 5.9 points (4.7 to 7.1) for 2.4 times the cost.
- Coordination. Opus 5.5 with Sonnet 5.5 subagents scored about the same as Opus 5.5 alone at medium for about a third less. "Claude Fable 5.2 as the orchestrator in Claude Opus 5.5's place cost 19% more and scored about the same."

### DeepResearch Bench II

Research tasks done with search tools and graded against rubrics drawn from expert reports. Anthropic ran a 50-task subset on 2026-11-03, three runs per setting, and scores the 44 tasks that every setting answered. Costs are per task on those 44 tasks.

| Model and effort | Rubric score | Cost per task |
| --- | --- | --- |
| Sonnet 5.5, high | 57.2% | $1.13 |
| Fable 5.2, low | 54.5% | $1.50 |
| Opus 5.5, medium | 59.6% | $1.68 |
| Fable 5.2, medium | 55.0% | $2.20 |
| Fable 5.1, low | 60.2% | $3.85 |
| Fable 5.1, medium | 62.1% | $4.77 |
| Fable 5.2, high | 57.7% | $4.86 |
| Fable 5.1, high | 62.5% | $6.10 |

- The page's effort table gives Fable 5.2's costs as $1.49, $2.16 and $4.82. Those are counted over the 46 tasks it ran.
- Anthropic's reading: Opus 5.5 scored 2.4 points above Sonnet 5.5 for 1.5 times the cost per task. Fable 5.2 "cost 4.3 times as much as Claude Sonnet 5.5 for no measurable gain in score, and 2.9 times as much as Claude Opus 5.5 for a score 1.9 points lower". Fable 5.2 at medium was not measurably higher than at low.
- Limits Anthropic states. A Claude model is the judge, and "an Anthropic judge may favor the house style". Fable 5.2 was run before its release. In further runs on 2026-11-06 and 2026-11-07, Fable 5.2 at high scored 0.9 points below Opus 5.5 in one setup (95 percent interval from 1.0 above to 2.7 below) and 1.9 points below in the other (0.0 to 3.7 below).

### Haiku 5.5

- GPQA Diamond, 198 graduate-level science questions, run on 2026-10-07. Haiku 5.5 at medium, its default, scored 85%, against 91% for each of Opus 5.5 and Sonnet 5.5, at "about a twentieth of Claude Opus 5.5's cost per correct answer and about a tenth of Claude Sonnet 5.5's".
- Claude Managed Agents task set, 79 scripted agent tasks, run on 2026-10-07. Haiku 5.5 at medium passed 93% of attempts (a single run) at about $0.011 per passed attempt. About 5 percent of its requests had prompts over 100,000 tokens, which are charged the higher rates, "and they carried 73% of its cost".
- Haiku 5.5 as a subagent on coding tasks. Adding Haiku 5.5 subagents to Opus 5.5 at medium on an internal coding benchmark cut the cost per attempt by 32 percent and the pass rate by about 4 points. Anthropic's reading: "an alternative to lowering effort, not better".

### Other findings on the page

- Opus 5.5 at low against medium: 13.3 points lower on DRACO, a research benchmark by Perplexity, 3.4 lower on Humanity's Last Exam and 14.0 lower on an internal set of physics problems. On the defect-search benchmark it scored 34 points lower for about a fifth of the cost.
- The advisor, a setup where a cheaper model consults a stronger one. Opus 5.5 at high with a Fable 5.1 advisor scored 90.1% on the internal agentic-coding benchmark at $2.92 per attempt. That is 1.7 points over Opus 5.5 at high alone, "at the edge of run-to-run noise", for about 2.1 times the cost. Anthropic's reading: "the advisor bought about what more effort does". On GPQA Diamond, Haiku 5.5 and Sonnet 5.5 never consulted their Opus 5.5 advisor. On 20 SWE-bench Pro problems, Sonnet 5.5 at high did not consult it either, and at xhigh consulted on 3 or 4 of the 20.

### Anthropic's guidance on the page

- "For most agent workloads, start with Claude Opus 5.5 at its default effort (`medium`)."
- "Use Claude Fable 5.2 for demanding reasoning and long-horizon agentic work, or when your evals on Claude Opus 5.5 at higher effort still fall short."
- "Price every candidate in cost per completed task on your own traffic, including Claude Opus 5.5 at its default effort and the frontier model at reduced effort."
- "Sweep two or three effort levels on a sample of your own traffic, each in a separate session".
- Where outputs can be checked, run at a low effort and rerun the failures at high.
- "High-volume work with outputs you can check": try Haiku 5.5 first.
- Default effort on the Claude Platform: high on most models, and medium on Opus 5.5 and Haiku 5.5.

### How these figures bear on the picks

Checked at the 2026-11-12 review against the rule in `reading-cost-charts.md`: a pick changes only where the evidence shows another choice beating it at the same cost or matching it for less. No pick changed. Section 9 has the detail by pick. The three findings that matter most:

1. **Fable 5.2 at medium against Opus 5.5 at high**, the two building defaults. Four benchmarks now compare the two models, and they do not agree. On FrontierCode 2.0 and on the internal agentic-coding benchmark the two settings are level in score and in cost. On the defect-search benchmark Fable 5.2 at medium scored 2.7 points higher for 1.6 times the cost. On the SWE-bench Pro subset Fable 5.2 at medium was not run, and the points that were run put Opus 5.5 ahead on cost at a similar pass rate. So the Fable profile's default is neither confirmed nor overturned. It stays, the choice is close, and the question is open in section 12.
2. **Opus 5.5 at high against medium.** Anthropic now names medium as the starting point. High scored above medium on all five benchmarks that show both: by 2.5, 1.8 and 2.3 points on the three with published figures (SWE-bench Pro subset, internal agentic-coding, defect search), and by about 4.4 and 6.6 points on the two chart readings (FrontierCode 2.0 and Terminal-Bench 4.0). High cost about 20 to 65 percent more per task. Medium does not match high, so the pick stays. The gain on the published figures is small. On the defect-search benchmark Anthropic's 95 percent interval for it is 0.7 to 3.9 points.
3. **Rerunning failures.** On the SWE-bench Pro subset, running Opus 5.5 at medium and rerunning only the failures at high solved slightly more tasks than everything at high, for about 17 percent less. Starting at low saved about 40 percent. The skill does not make this a rule. It is a calculation on one benchmark, with a failure signal that real projects often lack, and each failure costs a second run. It is recorded as Anthropic's alternative and is open in section 12.

## 6. Fable 5.2 release table

Published by Anthropic, 2026-11-09.

| Benchmark | Fable 5.2 | Fable 5.1 | Opus 5.5 | GPT-6 Astra | Gemini 4 Carbon |
| --- | --- | --- | --- | --- | --- |
| Agentic coding, FrontierCode 2.0 | 49.1% (xhigh) | 32.4% (xhigh) | 45.5% | 42.8% | 41.1% (medium) |
| Agentic coding, FrontierSWE v2 | 69.9% | 56.3% | 62.3% | 65.5% | 61.2% |
| Business workflows, AutomationBench | 51.4% | 31.4% | 42.5% | 41.4% | 53.9% |
| Scientific research, Terminal-Bench-Science 0.1 | 74.6% | 52.6% | 58.7% | 68.1% | 64.8% |
| Agentic search, WANDR (relaxed score) | 82.1% | 68.7% | 72.3% | not reported | not reported |
| Computer use, OSWorld 2.1 (offline set, partial) | 89.3% | 83.5% | 87.2% | 79.5% | 81.5% |
| Robotics, RoboDojo Sim | 64.9% | 27.6% | 39.4% | 29.8% | not reported |
| Knowledge work, AA-Briefcase v1.1 (rubric) | 66.1% | 61.5% | 61.2% | 52.0% | 61.8% |
| Knowledge work, AA-Briefcase v1.1 (Elo) | 1785 | 1669 | 1800 | 1569 | 1611 |
| Knowledge work, Remote Labor Index | 41.3% (high) | 17.9% | 21.3% | 20.8% | not reported |
| Reasoning, Humanity's Last Exam (with tools) | 74.2% | 65.6% | 67.7% | 57.2% | not reported |
| Chart recognition, Chartography (no tools) | 73.4% | 44.8% | 64.4% | 71.0% | 72.5% |

Where Fable 5.2 does not lead: business workflows (Gemini 4 Carbon), and the knowledge-work Elo score (Opus 5.5 by 15 points, while the rubric score for the same benchmark favors Fable).

The table also has cybersecurity and protein design rows scored on Mythos 5.2, the restricted version of the same model. They are left out here because Mythos is not generally available.

## 7. Sonnet 5.5 release table

Published by Anthropic, 2026-09-28.

| Benchmark | Sonnet 5.5 | Sonnet 5 | Opus 5.5 | GPT-6 Sol |
| --- | --- | --- | --- | --- |
| Agentic coding, Terminal-Bench 4.0 | 70.6% | 10.3% | 66.4% (xhigh) | not reported |
| Agentic coding, FrontierCode 1.1 (main) | 52.1% (xhigh), 46.2% (max) | 42.4% | 54.4% | 49.3% |
| Agentic coding, CursorBench 4.0 | 55.5% | 34.1% | 57.8% | not reported |
| Knowledge work, GDPval-AA v2.1 (Elo) | 1844 | 1449 | 1846 | 1487 |
| Knowledge work, AA-Briefcase v1.1 (Elo) | 1811 | 1359 | 1822 | 1483 |
| Reasoning, Humanity's Last Exam (with tools) | 64.5% | 54.9% | 67.7% | not reported |
| Computer use, OSWorld 2.1 (partial) | 80.1% | 57.0% | 81.8% | not reported |
| Chart recognition, Chartography (no tools) | 61.6% | 15.6% | 64.4% | 53.6% |

Notes:

- Anthropic's footnote: Sonnet 5.5 scored lower at max than at xhigh on FrontierCode 1.1. At max it more often ran a review step that used many subagents, which in the cases examined caused a timeout or edits outside the task.
- Anthropic's text: Sonnet 5.5 at max performs comparably to Opus 5.5 on several evaluations, but Opus 5.5 stays clearly ahead on complex, open-ended work that needs sustained judgment.
- Anthropic's text: Sonnet 5.5 at medium beats Sonnet 5's best AA-Briefcase score at about a ninth of the cost per task.
- Elo scores are relative to each page's pool of models. Opus 5.5 is 1800 on the Fable page and 1822 on the Sonnet page for the same benchmark. Do not compare Elo across pages.

## 8. Haiku 5.5

Released 2026-10-07. Anthropic published a table and cost charts, but the charts carry no labeled values, so there is no per-effort cost table here. Section 5 has Anthropic's published scores and costs for Haiku 5.5 at medium, from its cost guide.

Published by Anthropic (scores at max effort):

| Benchmark | Haiku 5.5 | Haiku 4.5 | Sonnet 5.5 | GPT-6 Luna |
| --- | --- | --- | --- | --- |
| Knowledge work, GDPval-AA v2.1 (Elo) | 1620 | 735 | 1840 | 1437 |
| Knowledge work, AA-Briefcase v1.1 (Elo) | 1578 | 614 | 1824 | 1336 |
| Computer use, OSWorld 2.1 (offline set) | 72.4% | 15.7% | 83.9% | 48.9% |
| Reasoning, Humanity's Last Exam (no tools) | 45.9% | 10.2% | 56.9% | not reported |
| Reasoning, Humanity's Last Exam (with tools) | 57.4% | 18.7% | 64.5% | not reported |
| Agentic coding, Terminal-Bench 4.0 | 39.2% | 0.0% | 70.6% | 16.4% |
| Agentic coding, FrontierCode 1.1 (main) | 46.4% | not reported | 52.1% (xhigh) | 42.4% |
| Chart recognition, Chartography (no tools) | 46.4% | 6.4% | 61.6% | 29.1% |

What Anthropic says it is for: high-volume, cost-sensitive work such as summaries, compaction, database queries and classification, plus subagent work and speed-sensitive tasks. Anthropic says Sonnet 5.5 and Opus 5.5 remain the better choices for complex agentic coding, and that Haiku 5.5 pairs well with them as a subagent.

How effort changes Haiku 5.5 (all third party):

- Cursor reports 48.4% on CursorBench at max and 30.9% at low.
- Artificial Analysis scores it 43 on its Intelligence Index at max and 34 at the default medium. Running the index took about 440 million output tokens at max against 54 million at medium, and cost about $0.21 per task against $0.05.
- One small independent test of eight coding tasks found low, medium and high all solved eight of eight, while max solved seven and used about twenty times the tokens of low.

What this means for picking:

- Haiku 5.5 is a real step below Sonnet 5.5 on agentic coding (39.2% against 70.6% on Terminal-Bench 4.0, both at max). Keep it to narrow jobs.
- Its effort curve is steep and its max is expensive. Medium is the sensible working level. Low is for plain lookups where a miss is cheap and easy to see.
- Above 100,000 tokens of prompt its price rises five times. Keep Haiku agents on short contexts.

## 9. What each pick rests on

| Pick | Evidence | Strength |
| --- | --- | --- |
| Fable 5.2, xhigh for highest stakes, on the Fable and Included profiles | Top FrontierCode 2.0 score (49.1%), 3.6 points above Opus 5.5's best for about 11 percent more cost per task. Leads most rows of the release table. In the cost guide (section 5) Fable 5.2 at high has the top score on the internal agentic-coding and defect-search benchmarks, and is level with Opus 5.5 at xhigh on the SWE-bench Pro subset. The guide has no figure for Fable 5.2 at xhigh | Strong for code, specifications and text other models follow. Published. Weaker for research reports: on DeepResearch Bench II, the one published research benchmark with costs, Fable 5.2 at high scored 1.9 points below Opus 5.5 at medium |
| Fable 5.2, medium as the default when paying per token (Fable profile) | For it. About level with or slightly above Opus 5.5 at high for about the same cost on FrontierCode 2.0 (the Opus point is a chart reading) and on the internal agentic-coding benchmark (published: 88.9% at $1.34 against 88.4% at $1.38, the Fable point a single run). On the defect-search benchmark it scored 2.7 points higher for 1.6 times the cost (published). Matches Opus's top score on search and beats it on chart reading at medium. Against it. On the SWE-bench Pro subset Opus 5.5 costs less at a similar pass rate, and Fable 5.2 at medium was not run there (published). On two benchmarks Fable 5.2 at low scored as well as medium for less (published) | Moderate, and close. Reviewed on 2026-11-12 and left unchanged. The new figures back "about level for about the same cost" on one benchmark and point the other way on cost on another. Anthropic itself advises starting on Opus 5.5. The comparison is in dollars per task, which is what a person who pays per token pays |
| Fable 5.2, high as the step up on the Fable profile | About level with Opus 5.5 at max for about half the cost per task on FrontierCode 2.0 (published). Against Opus 5.5 at xhigh it is about 2 points ahead for about 30 percent more cost on FrontierCode 2.0 (the Opus point is a chart reading) and on the internal agentic-coding benchmark (published). On the SWE-bench Pro subset the two are level and Opus 5.5 at xhigh costs a little over half as much (published) | Moderate. It was rated strong on 2026-11-09, when the only comparison was with Opus 5.5 at max. Against Opus 5.5 at xhigh the two are close |
| Opus 5.5, high as the default on included plans (Included profile). When it falls short, xhigh if it skipped checks or stopped early, Fable 5.2 at high if it tried and was still wrong | The plugin owner's choice, made on 2026-11-09. Fable draws the shared weekly limit faster than Opus by an amount Anthropic has not published, so the dollar comparison above does not show what Fable costs in plan allowance. Anthropic advises starting most work on Opus 5.5. On FrontierCode 2.0, raising Opus 5.5 from high to xhigh gains 8.9 points for about $2.8 more per task, about $0.31 a point. Moving from Opus 5.5 at high to Fable 5.2 at high gains about 10.8 points for about $4.3 more per task, about $0.40 a point, and reaches the higher score (45.3% against 43.4%). The Opus figures are chart readings. On the internal agentic-coding benchmark (published) the same two steps gain 2.7 points for 3.0 times the cost and 5.1 points for 3.9 times. Anthropic's cost guide gives the same order: use Fable 5.2 "when your evals on Claude Opus 5.5 at higher effort still fall short" | A judgment call. No published figure compares the two models in plan allowance. The order is the skill's own: more effort when the model skipped checks, a larger model when it tried and was still wrong |
| Opus 5.5, high as the default on the Opus profile, and for review and coordination | A good step on both cost charts (about $0.15 to $0.16 a point). On three benchmarks in the cost guide, high scored 1.8 to 2.5 points above medium for about 20 to 65 percent more cost per task (published). As the coordinator of Sonnet 5.5 subagents on the defect-search benchmark, Opus 5.5 at high scored about the same as Fable 5.2 in that role, which cost 19 percent more (published). On a plan that includes Fable, Opus draws the shared weekly limit more slowly than Fable (published by Anthropic, without a figure) | Moderate. Five benchmarks agree on the direction, two of them chart readings. The gain on the three published ones is small. This pick goes beyond Anthropic's advice, which names medium as the starting point. Where tests reliably catch a failure, Anthropic's rerun figures favor starting at medium (section 5) |
| Opus 5.5, xhigh for audits | +8.9 points over high on FrontierCode 2.0 at about $0.31 a point (chart reading). The gain is smaller elsewhere: 2.2 points on Terminal-Bench 4.0 (chart reading), 2.7 points for 3.0 times the cost on the internal agentic-coding benchmark, and 1.0 to 1.4 points for about 2.5 times the cost on the SWE-bench Pro subset (both published) | A judgment call. Three of four benchmarks show a small gain from this step. It is kept for audits and highest-stakes work, where a missed error costs more than the extra effort |
| Sonnet 5.5, medium for scoped work | Cheapest point on Terminal-Bench 4.0's best value line. Half Opus's price on every line. Anthropic describes medium as good for scoped engineering work. On coding benchmarks in the cost guide, medium trails high by about 7 points on the SWE-bench Pro subset and about 15 points on the internal agentic-coding benchmark, for 59 and 48 percent of the cost (published) | Moderate. Keep it to scoped changes with a check that catches a miss. On open-ended coding it fails much more often than high, so raise the effort to high first when it misses |
| Sonnet 5.5, high for research | Nearly level with Opus 5.5 on both knowledge-work Elo scores at half the price. Effort buys more reading and checking, which is what research needs. On DeepResearch Bench II, Sonnet 5.5 at high is the cheapest setting that was run. Opus 5.5 at medium scored 2.4 points higher for 1.5 times the cost, and Fable 5.2 at high cost 4.3 times as much for no measurable gain (published) | Moderate. One published research benchmark with costs now supports it. Sonnet 5.5 at medium was not run there, so high against medium is still open |
| Haiku 5.5, medium for narrow volume work | Anthropic's stated purpose for the model. Medium is its default. In the cost guide, 85% on GPQA Diamond against 91% for Opus 5.5 and Sonnet 5.5 at about a twentieth of Opus's cost per correct answer, and 93% of attempts passed on a 79-task agent set at about $0.011 per passed attempt (published). Alone on the defect-search benchmark it scored far below Sonnet 5.5, 57.7 against 76.0, which is why it is kept to narrow jobs | Moderate |
| Haiku 5.5, low for lookup | Cheapest option. Solved simple tasks at low in a small third-party test | Weak. Use only where a miss is cheap and easy to see. If it misses, go to medium, then to Sonnet 5.5 at medium |

## 10. Choices that were dropped, and why

| Dropped | Why | Exception |
| --- | --- | --- |
| Fable 5.1, every effort | Below Fable 5.2 at every cost on FrontierCode 2.0 and on every row of the release table, at a higher price per token | None |
| Any model at max, as a default | No better than xhigh, often worse, for 1.5 to 3 times the cost | Sonnet 5.5 at max has Terminal-Bench 4.0's top score (70.6%, against 61.5% at xhigh). On FrontierCode 1.1 its max fell below its xhigh. Consider it only for long command-line work that changes no repository, and test first. Anthropic also suggests max for very hard problems such as finding security flaws, with the advice to test before adopting it widely |
| Fable 5.2 at low | On FrontierCode 2.0, medium costs about $0.38 more per task for 3.4 points. On the defect-search benchmark, medium costs 6 percent more for 1.1 points. The case is weaker than it was: on the internal agentic-coding benchmark and on DeepResearch Bench II, medium scored no measurably higher than low for about 30 and 45 percent more (published). Open in section 12 | Short reasoning and lookup questions, where Anthropic shows low matching Opus's best |
| Sonnet 5.5 at low | Medium costs a few cents more for about 9 more points | None |
| Sonnet 5.5 at xhigh | Opus 5.5 at high is cheaper and scores higher on Terminal-Bench 4.0 | None |
| Opus 5.5 at low | Loses about 19 points to medium on Terminal-Bench 4.0 for $1.6 (chart reading). Published figures agree: 5.4 points lower on the SWE-bench Pro subset, 11.8 on the internal agentic-coding benchmark and 34 on the defect-search benchmark. On the first two, Sonnet 5.5 at high scores the same or better for about the same cost | None as a fixed setting. Anthropic's rerun approach uses it as a first pass, with the failures rerun at high (section 5). The skill has not adopted that |
| Opus 5.5 at medium, as a pick | High scored above it on all five benchmarks that show both, by 1.8 to 6.6 points for about 20 to 65 percent more cost per task. Sonnet 5.5 at medium is cheaper for scoped work | It is Anthropic's default and, in the cost guide read on 2026-11-12, its named starting point for most agent workloads. It is strong on Terminal-Bench 4.0 (57.6% at about $2.9). Reasonable for command-line work a person is watching, and as a first pass where tests reliably catch a failure and the failures are rerun at high (section 5) |
| Opus 5.5 at max | About 2.5 times xhigh's cost for 2 points on FrontierCode 2.0, and below xhigh on Terminal-Bench 4.0 | None |
| Fast mode | About double the price | When speed matters more than cost |

## 11. Other Anthropic guidance worth keeping

- Smaller models suit precisely specified or mechanical edits and questions about code already in view. Larger ones suit subtle bugs, unfamiliar areas, architecture and ambiguous work.
- Effort sets how much work happens in a turn: how long the model thinks, how much it reads and how much it verifies. Low effort makes the model more likely to ask for context than to work things out.
- Raise effort where verification or edge cases matter. Max can overthink ordinary tasks and shows diminishing returns.
- When moving to a new model, start from its default effort instead of carrying over the old level.
- **The advisor.** A cheaper model runs the task and consults a stronger one at key moments, such as before committing to an approach and before declaring the work done. In April 2026, on older models, Anthropic reported Sonnet with an Opus advisor scoring 2.7 points higher on a multilingual coding benchmark at 11.9 percent lower cost per task. For the current models, the cost guide read on 2026-11-12 has figures (section 5). An advisor helped only where the cheaper model consulted it. Opus 5.5 at high with a Fable 5.1 advisor gained 1.7 points for about 2.1 times the cost, and Sonnet 5.5 at high and Haiku 5.5 did not consult their Opus 5.5 advisor at all. See `claude-code-setup.md` for how it behaves in Claude Code.
- At the Fable 5.2 release Anthropic described two roles for Fable in a team of models: an advisor that smaller models consult on harder problems, and an orchestrator that hands simpler tasks to smaller models. On the defect-search benchmark, Fable 5.2 as the orchestrator scored about the same as Opus 5.5 in that role and cost 19 percent more (section 5).
- Tune one model before adding a second. Anthropic's cost guide says to sweep effort on the current model first and to "build a pairing only if it beats the single model's whole curve of score against spend".
- Agents earn their tokens in four cases: parallel work, keeping noisy output out of the main session, unbiased review, and review limited to read-only tools. On the same or a smaller model they give parallelism or fresh eyes, not a better answer.
- Agent teams use about seven times the tokens of a single session when teammates run in plan mode. Anthropic suggests Sonnet for teammates and small teams.

## 12. Open questions

- How much faster Fable draws the shared weekly limit than Opus. This is not published. Anthropic says only that Fable models use plan limits "faster than other Claude models". Until it is known, Fable work cannot be priced in plan allowance, only in dollars per task. This is one reason included plans default to Opus 5.5 at high.
- How the weekly limit weighs Opus, Sonnet and Haiku tokens against each other.
- Sonnet 5.5's knowledge-work cost by effort, which would settle high against medium for research. Partly answered on 2026-11-12: DeepResearch Bench II gives a cost for high ($1.13 per task). Medium was not run.
- Haiku 5.5's cost by effort from Anthropic's own charts. Partly answered on 2026-11-12: the cost guide has figures for medium, and none for the other levels.
- Whether Anthropic's figures hold on the user's own work. This is the one that matters most.

Added at the 2026-11-12 review, from the cost guide in section 5.

- Fable 5.2 at medium against Opus 5.5 at high as the building default for people who pay per token. Four benchmarks compare the two models and do not agree. A figure for Fable 5.2 at medium on the SWE-bench Pro subset, a second run on the internal agentic-coding benchmark, or a measurement on real work would help settle it.
- Whether Fable 5.2 at low should replace medium on the Fable profile. On two benchmarks low scored as well as medium for less. On two others medium scored 1.1 and 3.4 points higher.
- Whether to adopt Anthropic's rerun approach as a rule: start work that tests can check one effort level lower, and rerun only the failures at high. The saving is published for one benchmark and is a calculation, not a run. It depends on tests that reliably show a failure.
- Whether Opus 5.5 at high is worth its extra cost over medium for building, given that the published gain is about 2 points. The pick is unchanged because medium scored lower on every benchmark, but Anthropic's advice is to start at medium.
- Whether Fable 5.2 is the right pick for high-stakes research reports. On the one published research benchmark with costs it scored no higher than Opus 5.5 or Sonnet 5.5.

Closed at the 2026-11-09 review. The details and sources are in `plans-and-costs.md`, section 3.

- How large the weekly Fable allowance is. Answer: up to 50 percent of the weekly limit, on plans and seats that include Fable (published by Anthropic, re-verified).
- Whether Fable work also counts against the general limit. Answer: yes. Fable draws from the same weekly limit as the other models. It is not a separate pool (published by Anthropic, re-verified).
- What a Fable limit reset clears. Answer: the usage spent on Fable models against the weekly limit, and the whole five-hour window where the account has one. Usage on other models stays (published by Anthropic, re-verified 2026-11-09).

## 13. Sources

- Anthropic, Introducing Claude Fable 5.2 and Claude Mythos 5.2 (2026-11-09): https://www.anthropic.com/claude-fable-and-mythos-5-2
- Anthropic, Claude Fable product page: https://www.anthropic.com/claude/fable (still showed Fable 5.1 to an automated fetch on 2026-11-09)
- Anthropic, Introducing Claude Sonnet 5.5 (2026-09-28): https://www.anthropic.com/news/claude-sonnet-5-5
- Anthropic, Introducing Claude Haiku 5.5 (2026-10-07): https://www.anthropic.com/claude-haiku-5-5
- Anthropic, Optimizing for cost and intelligence: https://platform.claude.com/docs/en/about-claude/models/optimizing-for-cost-and-intelligence (read 2026-11-12)
- Anthropic, models overview: https://platform.claude.com/docs/en/about-claude/models/overview (read 2026-11-12)
- Anthropic, pricing: https://platform.claude.com/docs/en/about-claude/pricing (read 2026-11-09 and again 2026-11-12)
- Anthropic help center, Claude Fable models on your plan: https://support.claude.com/en/articles/15424964 (read 2026-11-09, re-verified 2026-11-09, read again 2026-11-12)
- Anthropic help center, Claude Fable 5.2 launch offers: https://support.claude.com/en/articles/17506494 (read 2026-11-09, re-verified 2026-11-09, read again 2026-11-12)
- Anthropic help center, Use Claude Code with your Pro, Max, or Ultra plan: https://support.claude.com/en/articles/11145838 (read 2026-11-09, first from a summary, then in full, and read again 2026-11-12)
- Anthropic help center, Manage usage credits for paid Claude plans: https://support.claude.com/en/articles/12429409 (read 2026-11-09 and again 2026-11-12)
- Anthropic, plan pricing page: https://claude.com/pricing (read 2026-11-09, first from a summary, then in full)
- Anthropic, Choosing a Claude model and effort level in Claude Code (2026-07-07): https://claude.com/blog/claude-model-and-effort-level-in-claude-code
- Anthropic, The advisor strategy (2026-04-09): https://claude.com/blog/the-advisor-strategy
- Claude Code changelog on GitHub: https://raw.githubusercontent.com/anthropics/claude-code/main/CHANGELOG.md (read 2026-11-12, when the newest version listed was 2.1.323)
- Claude Code documentation, model configuration: https://code.claude.com/docs/en/model-config (read 2026-11-09, re-verified 2026-11-09, read again 2026-11-12. It covers Fable 5.2)
- Claude Code documentation, subagents: https://code.claude.com/docs/en/sub-agents (read 2026-11-09 and again 2026-11-12)
- Claude Code documentation, environment variables: https://code.claude.com/docs/en/env-vars (read 2026-11-12)
- Claude Code documentation, the advisor: https://code.claude.com/docs/en/advisor (read 2026-11-09, checked again 2026-11-12)
- Claude Code documentation, prompt caching: https://code.claude.com/docs/en/prompt-caching (read 2026-11-09, checked again 2026-11-12)
- Anthropic, Claude Platform release notes: https://platform.claude.com/docs/en/release-notes/overview (read 2026-11-09)
- Claude Code documentation, costs: https://code.claude.com/docs/en/costs (read 2026-11-09)
- Third party, Kingy AI, Fable 5.2 specifications and system-card cost figures: https://kingy.ai/blog/claude-fable-5-2/ (read 2026-11-09)
- Third party, DataCamp, Haiku 5.5 table: https://www.datacamp.com/blog/claude-haiku-5-5
- Third party, Beam, Haiku 5.5 effort figures from Artificial Analysis: https://beam.ai/agentic-insights/claude-haiku-5-5-subagents
- Third party, AI Catchup, Haiku 5.5 CursorBench figures: https://aicatchup.com/news/claude-haiku-5-5
- Third party, Computing for Geeks, eight-task Haiku 5.5 test: https://computingforgeeks.com/claude-haiku-5-5-released-features-benchmarks/
