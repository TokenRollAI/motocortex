# Usability Evidence and Evaluation

Interaction decisions are claims about how people will behave. This reference helps choose evidence proportionate to the decision, and keeps predictions distinct from observations.

## Sources of evidence

Start with what already exists before generating new data. Product analytics show paths, drop-off, and feature use, but not why; traffic to a feature can include people who arrived by mistake, so confirm surprising numbers with observation. Support tickets, community questions, and failed or zero-result searches reveal user vocabulary and the places people get stuck. Session recordings and logs show sequences of actions around errors. Platform guidelines and neighboring products show conventions users have already learned.

When the product can reach users, choose a method by the question:

- Task analysis or contextual inquiry, watching people do their real work in their setting, reveals goals, workarounds, and the mental model a design must fit. Use it before designing a new workflow.
- Moderated usability testing with realistic tasks shows whether people can complete them and where they struggle. Use it on prototypes or builds before committing.
- Unmoderated tests, surveys, and analytics at scale estimate how often something happens. Use them to size a problem or compare alternatives quantitatively.
- Card sorting and tree testing check whether an information architecture matches how people group and look for things.

## Sample sizes and their limits

Small qualitative tests with around five comparable users tend to uncover most of the frequent, serious problems, which makes several small rounds with fixes in between more valuable than one large study. That figure is an average, not a guarantee: individual groups of five can find far fewer problems, distinct user groups each need their own participants, and quantitative comparisons need substantially larger samples, commonly twenty or more per condition. State the sample and its limits when reporting a result.

## Heuristic evaluation

A heuristic review checks a design against established principles such as visibility of system status, match with the real world, user control, consistency, error prevention, recognition over recall, flexibility, minimalist design, error recovery, and help. It is fast and cheap, and it is a prediction. Different evaluators reviewing the same interface with the same method routinely report substantially different problems, and a guideline violation does not always harm users. Improve reliability by having several evaluators review independently and merge their findings, and do not present a heuristic review as a substitute for watching users.

## Severity

Rate each problem on three factors: frequency, meaning how many people encounter it; impact, meaning how hard it is to overcome; and persistence, meaning whether people keep hitting it after they know about it. A common scale runs from 0 to 4: 0 not a usability problem, 1 cosmetic, 2 minor, 3 major and worth high priority, and 4 catastrophic and required to fix before release. Single-rater severity judgments are unreliable; average independent ratings when several reviewers are available, and let observed behavior override predicted severity.

## Metrics

Usability is the extent to which specified users can achieve specified goals with effectiveness, efficiency, and satisfaction in a specified context of use. Measure the dimension the decision depends on:

- Effectiveness: task success rate, error rate, and the rate of recovery from errors.
- Efficiency: time on task, number of steps, and backtracking.
- Satisfaction: a single ease question after each task, such as a seven-point rating of how difficult or easy it was, and a standardized questionnaire such as the System Usability Scale after a session. SUS scores are not percentages; the commonly cited average is about 68.
- Behavioral signals in production: abandonment, undo usage, repeated attempts, support contacts, and zero-result searches.

Compare metrics against a baseline or an alternative measured the same way; a single number without comparison says little.

## Reporting

Tie every finding to a user, a task, and the evidence behind it. Mark each as observed, measured, or predicted. Give the severity, the likely cause, and a fix that follows existing conventions, and say what evidence would change the conclusion.
