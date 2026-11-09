# How to read a score against cost chart

Anthropic publishes charts that plot a benchmark score against the cost per task for each model at each effort level. This is the method used to turn those charts into picks. Use it when a new model or a new chart appears, or when the user wants to see the reasoning.

## The method

1. **Read every point.** Record the model, the effort label, the cost and the score. Note which points are unlabeled and how you worked out their labels (the order of the points, a footnote, the caption, a figure in the table).

2. **Draw the best value line.** This is the highest score each dollar can buy, joining the points that nothing else beats. A point below the line is dominated. Some other point, or a mix of two neighboring points, scores more for the same cost.

3. **Price each step.** Divide the extra cost by the extra points for each step up in effort.
   - Under about $0.50 a point: a good buy.
   - Above about $2 a point: rarely worth it.
   - A step that lowers the score: never.

4. **Compare only within one chart.** Each benchmark has its own cost scale. To compare two models that never share a chart, go through a model that both charts show, and treat the result as rough.

5. **Match the benchmark to the work.**

   | Work | Benchmarks to look at |
   | --- | --- |
   | Code changes in a repository | FrontierCode, FrontierSWE |
   | Long command-line sessions | Terminal-Bench |
   | Knowledge work | AA-Briefcase, GDPval, Remote Labor Index |
   | Search | WANDR |
   | Computer use | OSWorld |

6. **Trust charts where they agree.** Where two charts disagree, the choice is a judgment call, and a measurement on real work decides it.

7. **Allow for noise.** A gap of two or three points is within the normal noise of these benchmarks. Do not build a rule on it alone.

8. **Convert to plan terms.** Dollars per task are a stand-in. On a subscription what matters is which weekly limit the work draws on and how full it is.

## Placing a new model

A new model and effort pair earns a place in the lineup only when it is on the best value line and either beats the current pick at the same cost or matches it for less. Whatever it dominates is dropped, with the reason recorded.

Do not place a model from its name, its tier or the vendor's adjectives. Place it from its points on a chart.

## Common mistakes

- Comparing Elo scores across release pages. Elo is relative to the pool of models on each page.
- Comparing scores across benchmark versions. A new version usually changes the tasks and the grading.
- Reading a release table as if every score were at the same effort. Tables usually show each model's highest effort, which is rarely the effort worth paying for.
- Treating price per token as cost per task.
- Treating a chart reading as exact. Log-scale axes make small reading errors large.
