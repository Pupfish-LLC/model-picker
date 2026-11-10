# Evidence behind the picks

Last reviewed 2026-11-09.

## Contents

1. How to read this file
2. FrontierCode 2.0: score against cost per task
3. Terminal-Bench 4.0: score against cost per attempt
4. Other cost findings from the Fable 5.2 release
5. Fable 5.2 release table
6. Sonnet 5.5 release table
7. Haiku 5.5
8. What each pick rests on
9. Choices that were dropped, and why
10. Other Anthropic guidance worth keeping
11. Open questions
12. Sources

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
- Opus 5.5 at high is a good step on both charts (about $0.15 a point here and $0.16 on FrontierCode 2.0). That is why it is the default without Fable.
- Opus 5.5's effort curve differs by task. On FrontierCode 2.0 it gains most from high to xhigh. Here it gains most from low to medium and flattens after high. Any effort choice made from one chart is softer than it looks.

## 4. Other cost findings from the Fable 5.2 release

All published by Anthropic in the release text. They support the pattern that Fable 5.2 at low or medium effort often matches Opus 5.5's best.

- Agentic search (WANDR): Fable 5.2 at medium matches Opus 5.5's top score for about 40 percent of the cost per attempt.
- Humanity's Last Exam: Fable 5.2 at low matches Opus 5.5's top score for less than a tenth of the cost per task.
- Chart reading (Chartography): Fable 5.2 at medium scores 66.4%, ahead of Opus 5.5 at max (64.4%), for less than a tenth of the cost per task.
- Fable 5.2 at medium uses fewer tokens than Fable 5.1.

## 5. Fable 5.2 release table

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

## 6. Sonnet 5.5 release table

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

## 7. Haiku 5.5

Released 2026-10-07. Anthropic published a table and cost charts, but the charts carry no labeled values, so there is no per-effort cost table here.

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

## 8. What each pick rests on

| Pick | Evidence | Strength |
| --- | --- | --- |
| Fable 5.2, xhigh for highest stakes | Top FrontierCode 2.0 score (49.1%), 3.6 points above Opus 5.5's best for about 11 percent more cost per task. Leads most rows of the release table | Strong. Published |
| Fable 5.2, medium as the default | About level with or slightly above Opus 5.5 at high for about the same cost on FrontierCode 2.0. Matches Opus's top score on search and beats it on chart reading at medium. Low to medium is the cheapest step on the chart | Moderate. Rests partly on a chart reading and a gap within noise. Anthropic itself advises starting on Opus 5.5. The comparison is in dollars per task. On a plan that includes Fable, Fable draws the shared weekly limit faster than Opus by an amount Anthropic has not published, so what this pick costs in plan allowance is not known |
| Fable 5.2, high as the step up | About level with Opus 5.5 at max for about half the cost per task | Strong. Published |
| Opus 5.5, high as the default without Fable, and for review and coordination | A good step on both cost charts (about $0.15 to $0.16 a point). On a plan that includes Fable, Opus draws the shared weekly limit more slowly than Fable (published by Anthropic, without a figure) | Moderate. Chart readings on two benchmarks that agree |
| Opus 5.5, xhigh for audits | +8.9 points over high on FrontierCode 2.0 at about $0.31 a point | A judgment call. Terminal-Bench 4.0 shows little gain from the same step |
| Sonnet 5.5, medium for scoped work | Cheapest point on Terminal-Bench 4.0's best value line. Half Opus's price on every line. Anthropic describes medium as good for scoped engineering work | Moderate |
| Sonnet 5.5, high for research | Nearly level with Opus 5.5 on both knowledge-work Elo scores at half the price. Effort buys more reading and checking, which is what research needs | Moderate. The cost of each effort level on knowledge work has not been read from a chart |
| Haiku 5.5, medium for narrow volume work | Anthropic's stated purpose for the model. Medium is its default | Moderate |
| Haiku 5.5, low for lookup | Cheapest option. Solved simple tasks at low in a small third-party test | Weak. Use only where a miss is cheap and easy to see. If it misses, go to medium, then to Sonnet 5.5 at medium |

## 9. Choices that were dropped, and why

| Dropped | Why | Exception |
| --- | --- | --- |
| Fable 5.1, every effort | Below Fable 5.2 at every cost on FrontierCode 2.0 and on every row of the release table, at a higher price per token | None |
| Any model at max, as a default | No better than xhigh, often worse, for 1.5 to 3 times the cost | Sonnet 5.5 at max has Terminal-Bench 4.0's top score (70.6%, against 61.5% at xhigh). On FrontierCode 1.1 its max fell below its xhigh. Consider it only for long command-line work that changes no repository, and test first. Anthropic also suggests max for very hard problems such as finding security flaws, with the advice to test before adopting it widely |
| Fable 5.2 at low | Medium costs about $0.38 more per task for 3.4 points | Short reasoning and lookup questions, where Anthropic shows low matching Opus's best |
| Sonnet 5.5 at low | Medium costs a few cents more for about 9 more points | None |
| Sonnet 5.5 at xhigh | Opus 5.5 at high is cheaper and scores higher on Terminal-Bench 4.0 | None |
| Opus 5.5 at low | Loses about 19 points to medium on Terminal-Bench 4.0 for $1.6 | None |
| Opus 5.5 at medium, as a pick | High is a cheap step up on both charts. Sonnet 5.5 at medium is cheaper for scoped work | It is Anthropic's default and is strong on Terminal-Bench 4.0 (57.6% at about $2.9). Reasonable for command-line work a person is watching |
| Opus 5.5 at max | About 2.5 times xhigh's cost for 2 points on FrontierCode 2.0, and below xhigh on Terminal-Bench 4.0 | None |
| Fast mode | About double the price | When speed matters more than cost |

## 10. Other Anthropic guidance worth keeping

- Smaller models suit precisely specified or mechanical edits and questions about code already in view. Larger ones suit subtle bugs, unfamiliar areas, architecture and ambiguous work.
- Effort sets how much work happens in a turn: how long the model thinks, how much it reads and how much it verifies. Low effort makes the model more likely to ask for context than to work things out.
- Raise effort where verification or edge cases matter. Max can overthink ordinary tasks and shows diminishing returns.
- When moving to a new model, start from its default effort instead of carrying over the old level.
- **The advisor.** A cheaper model runs the task and consults a stronger one at key moments, such as before committing to an approach and before declaring the work done. In April 2026, on older models, Anthropic reported Sonnet with an Opus advisor scoring 2.7 points higher on a multilingual coding benchmark at 11.9 percent lower cost per task. There are no published figures yet for the current models. See `claude-code-setup.md` for how it behaves in Claude Code.
- At the Fable 5.2 release Anthropic described two roles for Fable in a team of models: an advisor that smaller models consult on harder problems, and an orchestrator that hands simpler tasks to smaller models.
- Agents earn their tokens in four cases: parallel work, keeping noisy output out of the main session, unbiased review, and review limited to read-only tools. On the same or a smaller model they give parallelism or fresh eyes, not a better answer.
- Agent teams use about seven times the tokens of a single session when teammates run in plan mode. Anthropic suggests Sonnet for teammates and small teams.

## 11. Open questions

- How much faster Fable draws the shared weekly limit than Opus. This is not published. Anthropic says only that Fable models use plan limits "faster than other Claude models". Until it is known, the Fable default cannot be priced in plan allowance, only in dollars per task.
- How the weekly limit weighs Opus, Sonnet and Haiku tokens against each other.
- Sonnet 5.5's knowledge-work cost by effort, which would settle high against medium for research.
- Haiku 5.5's cost by effort from Anthropic's own charts.
- Whether these vendor figures hold on the user's own work. This is the one that matters most.

Closed at the 2026-11-09 review. The details and sources are in `plans-and-costs.md`, section 3.

- How large the weekly Fable allowance is. Answer: up to 50 percent of the weekly limit, on plans and seats that include Fable (published by Anthropic, re-verified).
- Whether Fable work also counts against the general limit. Answer: yes. Fable draws from the same weekly limit as the other models. It is not a separate pool (published by Anthropic, re-verified).
- What a Fable limit reset clears. Answer: the usage spent on Fable models against the weekly limit, and the whole five-hour window where the account has one. Usage on other models stays (published by Anthropic, re-verified 2026-11-09).

## 12. Sources

- Anthropic, Introducing Claude Fable 5.2 and Claude Mythos 5.2 (2026-11-09): https://www.anthropic.com/claude-fable-and-mythos-5-2
- Anthropic, Claude Fable product page: https://www.anthropic.com/claude/fable (still showed Fable 5.1 to an automated fetch on 2026-11-09)
- Anthropic, Introducing Claude Sonnet 5.5 (2026-09-28): https://www.anthropic.com/news/claude-sonnet-5-5
- Anthropic, Introducing Claude Haiku 5.5 (2026-10-07): https://www.anthropic.com/claude-haiku-5-5
- Anthropic, pricing: https://platform.claude.com/docs/en/about-claude/pricing (read 2026-11-09)
- Anthropic help center, Claude Fable models on your plan: https://support.claude.com/en/articles/15424964 (read 2026-11-09, re-verified 2026-11-09)
- Anthropic help center, Claude Fable 5.2 launch offers: https://support.claude.com/en/articles/17506494 (read 2026-11-09, re-verified 2026-11-09)
- Anthropic help center, Use Claude Code with your Pro, Max, or Ultra plan: https://support.claude.com/en/articles/11145838 (read 2026-11-09, first from a summary, then in full)
- Anthropic help center, Manage usage credits for paid Claude plans: https://support.claude.com/en/articles/12429409 (read 2026-11-09)
- Anthropic, plan pricing page: https://claude.com/pricing (read 2026-11-09, first from a summary, then in full)
- Anthropic, Choosing a Claude model and effort level in Claude Code (2026-07-07): https://claude.com/blog/claude-model-and-effort-level-in-claude-code
- Anthropic, The advisor strategy (2026-04-09): https://claude.com/blog/the-advisor-strategy
- Claude Code documentation, model configuration: https://code.claude.com/docs/en/model-config (read 2026-11-09, re-verified 2026-11-09. It now covers Fable 5.2)
- Claude Code documentation, subagents: https://code.claude.com/docs/en/sub-agents (read 2026-11-09)
- Claude Code documentation, the advisor: https://code.claude.com/docs/en/advisor (read 2026-11-09)
- Claude Code documentation, prompt caching: https://code.claude.com/docs/en/prompt-caching (read 2026-11-09)
- Anthropic, Claude Platform release notes: https://platform.claude.com/docs/en/release-notes/overview (read 2026-11-09)
- Claude Code documentation, costs: https://code.claude.com/docs/en/costs (read 2026-11-09)
- Third party, Kingy AI, Fable 5.2 specifications and system-card cost figures: https://kingy.ai/blog/claude-fable-5-2/ (read 2026-11-09)
- Third party, DataCamp, Haiku 5.5 table: https://www.datacamp.com/blog/claude-haiku-5-5
- Third party, Beam, Haiku 5.5 effort figures from Artificial Analysis: https://beam.ai/agentic-insights/claude-haiku-5-5-subagents
- Third party, AI Catchup, Haiku 5.5 CursorBench figures: https://aicatchup.com/news/claude-haiku-5-5
- Third party, Computing for Geeks, eight-task Haiku 5.5 test: https://computingforgeeks.com/claude-haiku-5-5-released-features-benchmarks/
