# Tips for Building AI

Practical, opinionated advice for teams building AI products that need to work
in the real world.

AI products are products under uncertainty. The useful work is rarely just
choosing a model: it is deciding what the product should do, what evidence is
good enough, how people stay in control, and how the team responds when the
system is wrong.

This guide is for engineers, designers, product people, and technical leaders.
Read it from top to bottom, choose the section closest to your current problem,
or follow one of the [role-based reading paths](#reading-paths).

## How to use this guide

- Pick one tip that changes a decision you are making this week.
- Discuss the “Try this” prompt with the people who own the surrounding
  workflow.
- Record what you decided and the evidence that would change your mind.
- Revisit the decision when users, data, models, or risks change.

This is a field guide, not a compliance checklist. For a structured launch
assessment, use the
[Production AI Checklist](https://github.com/attractorhq/production-ai-checklist).

## Contents

1. [Choose work worth doing](#1-choose-work-worth-doing)
2. [Work with uncertainty](#2-work-with-uncertainty)
3. [Know your data and context](#3-know-your-data-and-context)
4. [Evaluate what can fail](#4-evaluate-what-can-fail)
5. [Design for people](#5-design-for-people)
6. [Own the production system](#6-own-the-production-system)

## 1. Choose work worth doing

### 1. Start with a user decision

**Advice:** Define the decision or action the product should improve before
defining the AI output.

**Why it matters:** A fluent answer is not useful by itself. A clear downstream
decision makes value and failure measurable.

**Try this:** Complete: “After seeing this output, the user can [action] with
less [cost or delay].”

**Watch out:** “Use AI to improve the experience” is not a testable outcome.

### 2. Name the current baseline

**Advice:** Compare the idea with the workflow people use today, including its
cost, delay, and error rate.

**Why it matters:** A prototype can look impressive while making the full
workflow slower or less reliable.

**Try this:** Observe five real examples of the current workflow and record
time, handoffs, and failure recovery.

**Watch out:** Do not compare a polished demo with an imaginary zero-cost
baseline.

### 3. Prefer a narrow useful workflow

**Advice:** Start with one bounded task, audience, and consequence.

**Why it matters:** Narrow scope gives the team a realistic chance to collect
evidence and design safe fallbacks.

**Try this:** State who the first release is for, which inputs it accepts, and
which actions remain out of scope.

**Watch out:** “Anyone can ask anything” is a discovery interface, not a
production boundary.

### 4. Write down non-goals

**Advice:** Make explicit what the system must not decide, generate, reveal, or
automate.

**Why it matters:** Non-goals prevent quiet scope expansion as the demo gains
attention.

**Try this:** Add three non-goals to the product brief and turn each into an
acceptance or abuse test.

**Watch out:** A disclaimer does not enforce a boundary.

## 2. Work with uncertainty

### 5. Treat every output as uncertain

**Advice:** Design as if plausible-looking outputs can be incomplete, stale, or
wrong.

**Why it matters:** Model confidence and writing quality do not reliably
describe correctness.

**Try this:** List the consequences of a wrong output and match each consequence
with prevention, detection, or recovery.

**Watch out:** Do not use confident wording as evidence of confidence.

### 6. Design a useful abstention

**Advice:** Give the system a clear way to say that it cannot answer safely.

**Why it matters:** Refusal is only useful when it helps the user make progress.

**Try this:** Define when to abstain, what explanation to show, and where the
user can go next.

**Watch out:** A generic “Something went wrong” message hides both risk and
recovery.

### 7. Keep a human override

**Advice:** Make consequential actions reviewable, reversible, or interruptible.

**Why it matters:** Human control must exist in the workflow, not only in a
policy document.

**Try this:** Rehearse how an operator stops one action, one user session, and
the entire feature.

**Watch out:** Approval fatigue can turn a nominal review step into automatic
acceptance.

### 8. Separate the demo promise from the product promise

**Advice:** Describe what has been demonstrated separately from what is
reliable at production scale.

**Why it matters:** A few successful examples do not establish coverage,
stability, or safe operation.

**Try this:** Maintain two lists: observed capabilities and unverified
assumptions.

**Watch out:** Do not let a compelling edge case become the default roadmap.

## 3. Know your data and context

### 9. Trace where context came from

**Advice:** Preserve the source, version, access decision, and retrieval path for
information used in an output.

**Why it matters:** Provenance makes answers explainable, incidents
investigable, and corrections possible.

**Try this:** Pick one answer and trace every important claim back to the
specific source available at generation time.

**Watch out:** A URL alone does not prove which version or passage was used.

### 10. Test with realistic data

**Advice:** Include the ambiguity, missingness, language, noise, and long-tail
cases found in the real workflow.

**Why it matters:** Clean examples reward the demo while hiding production
failure modes.

**Try this:** Ask domain experts for the ten examples that make current tools
struggle.

**Watch out:** Remove or protect personal and confidential data before building
shared fixtures.

### 11. Minimize what the system can see

**Advice:** Send and retain only the data required for the task.

**Why it matters:** Every extra field expands privacy, security, and operational
risk.

**Try this:** Review one end-to-end trace and justify every captured input,
metadata field, and log entry.

**Watch out:** “We may need it later” is not a retention purpose.

### 12. Plan for stale and hostile context

**Advice:** Treat retrieved documents, tool output, and user-provided content as
untrusted and time-sensitive.

**Why it matters:** Context can be outdated, incorrectly permissioned, or
written to manipulate the system.

**Try this:** Test an expired policy, a revoked document, and an instruction
hidden inside retrieved content.

**Watch out:** Retrieval relevance does not imply authority or safety.

## 4. Evaluate what can fail

### 13. Build an evaluation set before tuning

**Advice:** Capture representative cases and expected behavior before changing
models, prompts, or retrieval.

**Why it matters:** Without a stable reference set, improvement becomes a memory
of whichever examples were tried last.

**Try this:** Start with 20 reviewed cases covering common, difficult, and
should-not-answer behavior.

**Watch out:** Avoid writing every expected answer in the exact style of the
current implementation.

### 14. Measure important slices separately

**Advice:** Break aggregate results down by consequence, user group, language,
content type, and known failure mode.

**Why it matters:** A strong average can hide a severe regression for a small
but important slice.

**Try this:** Define the three slices that would block a release even if the
overall score improved.

**Watch out:** Add slices for a reason; dozens of unused dashboards do not
improve decisions.

### 15. Keep the evidence with the change

**Advice:** Store evaluation inputs, outputs, configuration, thresholds, and
results so a release decision can be reproduced.

**Why it matters:** AI behavior changes through more than source code.

**Try this:** From a release record, reconstruct which model, prompt, context,
and evaluation result were approved.

**Watch out:** A screenshot of a dashboard is not enough for investigation.

### 16. Turn failures into durable tests

**Advice:** Add reviewed production failures and near misses to the evaluation
set.

**Why it matters:** Incidents are expensive evidence. Reusing them prevents the
same class of failure from returning unnoticed.

**Try this:** Make “evaluation case added” part of the incident follow-up when
the failure is reproducible.

**Watch out:** Redact sensitive details without removing the feature that caused
the failure.

## 5. Design for people

### 17. Show evidence, not artificial confidence

**Advice:** Help users inspect relevant sources, assumptions, and limitations.

**Why it matters:** A percentage or authoritative tone can imply certainty the
system has not earned.

**Try this:** Test whether a user can verify the most consequential claim in
under a minute.

**Watch out:** Citations are useful only when they support the claim and the
user may access them.

### 18. Make correction easy

**Advice:** Let users edit, reject, retry, or report an output without restarting
their work.

**Why it matters:** Recovery quality often matters more than first-answer
perfection.

**Try this:** Observe someone recover from a deliberately wrong answer and count
the steps.

**Watch out:** A free-text feedback box alone does not repair the current task.

### 19. Preserve meaningful user control

**Advice:** Make it clear when AI is involved and which actions remain the
user's responsibility.

**Why it matters:** People cannot calibrate trust or consent to automation they
cannot see.

**Try this:** Ask a new user to explain what the system did, what it did not do,
and what happens next.

**Watch out:** Do not hide consequential automation behind friendly
anthropomorphic language.

### 20. Test the degraded experience

**Advice:** Design the interface for slow, unavailable, refused, partial, and
low-quality outcomes.

**Why it matters:** Production users encounter states that never appear in the
happy-path prototype.

**Try this:** Run a usability session with the provider unavailable and one data
source delayed.

**Watch out:** Endless loading is not a fallback.

## 6. Own the production system

### 21. Threat-model the whole model path

**Advice:** Include prompts, retrieval, tools, permissions, outputs, logs, and
human handoffs in security review.

**Why it matters:** Most serious failures happen at system boundaries rather
than inside the model alone.

**Try this:** Draw the path from user input to external action and mark every
trust boundary.

**Watch out:** Content filtering cannot compensate for excessive tool
permissions.

### 22. Bound latency and cost

**Advice:** Set budgets per request, user, and workflow, then define what happens
when a budget is reached.

**Why it matters:** Retries, long context, and agent loops can turn small errors
into operational incidents.

**Try this:** Test the maximum-length input, the slowest dependency, and a tool
that repeatedly fails.

**Watch out:** Average cost and latency hide the cases that hurt users and
budgets most.

### 23. Instrument the decision path

**Advice:** Capture enough structured telemetry to connect user impact with
retrieval, generation, tools, policy decisions, and fallbacks.

**Why it matters:** Token counts and uptime cannot explain why the product
failed.

**Try this:** Starting from one user report, locate the trace and identify the
failed component without reading sensitive content.

**Watch out:** Observability should not become an uncontrolled copy of user
data.

### 24. Assign an owner and rehearse failure

**Advice:** Give the feature an operational owner, escalation path, and tested
runbook before launch.

**Why it matters:** AI incidents cross product, engineering, security, legal,
and communications boundaries.

**Try this:** Run a 45-minute tabletop exercise using
[AI Failure Drills](https://github.com/attractorhq/ai-failure-drills).

**Watch out:** A runbook nobody has used is still a hypothesis.

## Reading paths

### Engineering

Start with tips 9–16 and 21–24. Then read tips 5–8 with the product and design
people who own fallbacks and user control.

### Product and design

Start with tips 1–8 and 17–20. Then use tips 13–16 to turn intended product
behavior into release evidence.

### Technical and product leadership

Start with tips 1–4, 14–16, and 21–24. Ask who owns each unresolved trade-off
and what evidence will support the next investment or launch decision.

## Go deeper

The [resources page](resources.md) contains a short selection of primary,
vendor-neutral references. It is intentionally curated rather than exhaustive.

## Contributing

Real examples, disagreements, and focused improvements are welcome. Use
[Discussions](https://github.com/attractorhq/tips-for-building-ai/discussions)
for questions, or read [CONTRIBUTING.md](CONTRIBUTING.md) before suggesting a
change.

Attractor maintains this guide for the community. It is licensed under
[Apache-2.0](LICENSE).
