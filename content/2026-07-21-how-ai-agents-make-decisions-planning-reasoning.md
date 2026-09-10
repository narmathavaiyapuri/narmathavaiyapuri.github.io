Title: How AI Agents Make Decisions: Planning and Reasoning Explained
Date: 2026-07-21
Category: AI Infrastructure
Tags: planning, reasoning, AI agents, decision-making, ReAct, chain of thought
Slug: how-ai-agents-make-decisions-planning-reasoning
Status: Published

Ask an agent to book a work trip and it has to decide, implicitly or explicitly, dozens of things a human traveler would decide too: which flight constraints matter most, whether to check hotel availability before or after locking in flights, what to do if the preferred option is unavailable. None of that is answered by the model simply being capable — capability says the model can evaluate options, not that it will sequence and choose among them sensibly. How an agent actually gets from "here's a goal" to "here's the sequence of actions I'll take" is the problem planning and reasoning are meant to solve, and it's a less settled problem than it might appear.

## What It Is
**Planning** — the process by which an agent decides on a sequence of steps to reach a goal, either committing to a full sequence upfront or deciding one step at a time as it goes. Planning answers "what should happen, and in what order."
**Reasoning** — the deliberation an agent does at each decision point to choose among options — which tool to use, whether a result is good enough, whether to proceed or backtrack. Reasoning answers "given what I know right now, what's the right next move."

Planning and reasoning are related but distinct: a plan can be well-structured and still executed with poor reasoning at each step (the right sequence, wrong individual choices), and good step-by-step reasoning can still add up to a bad outcome if there was never a coherent plan tying the steps together.

## Why It Exists
A single model call, asked to just "do the task," tends to either attempt too much in one pass (producing a shallow or incomplete result) or get lost partway through a complex request with no mechanism to check its own progress. Explicit planning and reasoning exist to give the model a structure to work within — breaking a large goal into tractable pieces, and giving it a defined moment, at each step, to evaluate rather than just generate. This mirrors why humans plan complex tasks at all: not because improvisation never works, but because an explicit plan catches problems (a missing prerequisite, a wrong assumption) before they compound.

> A model can reason well at every individual step and still walk confidently toward the wrong goal if nothing above it is checking the plan.

## How It Works
- **Upfront (deliberative) planning** — the agent drafts a full sequence of steps before executing any of them, useful when the task's structure is knowable in advance and worth inspecting or approving before committing resources to it. Weakness: brittle if an early assumption turns out wrong, since the whole plan may need to be redone rather than adjusted.
- **Reactive (interleaved) planning** — often implemented as a "ReAct"-style loop: reason about the next single step, act, observe the result, reason again. This adapts naturally to surprises but is harder to inspect as a coherent whole, since the "plan" only exists implicitly across the sequence of individual decisions.
- **Hierarchical planning** — combining both: a high-level plan sets out major phases, while each phase is handled reactively, giving some of the auditability of upfront planning with some of the adaptiveness of reactive planning.
- **Chain-of-thought reasoning** — having the model articulate intermediate reasoning steps before committing to an action, which tends to produce more consistent, higher-quality decisions than asking directly for an action, at the cost of extra tokens and latency per decision.
- **Self-critique and revision** — a step where the agent (or a separate reviewing pass) evaluates whether its current plan or last action is actually sound before proceeding, catching some errors before they propagate further.

**Worked example**: consider an agent tasked with planning a conference trip within a $1,500 budget. An upfront planner might draft: (1) find flights under $500, (2) find a hotel under $150/night for 4 nights, (3) reserve $200 for meals and transit, and only then start executing — useful because a human can review that allocation before anything is booked, but if flights actually cost $650 minimum, the whole plan needs revisiting rather than a small adjustment. A reactive planner instead searches flights first, discovers the $650 minimum, and reasons in the moment — "flights are $150 over what I planned, so I need a cheaper hotel option to stay within budget" — adjusting the remaining steps based on what it just learned, without needing to restart. Neither approach is strictly better: the upfront version is easier to sanity-check before money is spent; the reactive version handles the unexpected flight cost more gracefully without a full restart.

## Comparison to the Status Quo
Before explicit planning patterns were common practice, many agent implementations simply asked a model to "figure out the task" in an unstructured loop, trusting the model's general reasoning to handle sequencing implicitly. This works for short, simple tasks and degrades on longer ones, where without an explicit plan to check progress against, an agent can lose track of the original goal, repeat completed steps, or declare success prematurely. Structured planning and reasoning patterns exist specifically to make that implicit process explicit and inspectable.

## Advantages
- **Better handling of complex, multi-step goals** — explicit planning breaks large tasks into tractable pieces rather than relying on the model to hold the whole task's structure in mind implicitly across a long, unstructured process.
- **Improved auditability** — an explicit plan or reasoning trace gives a human (or a debugging process) something concrete to inspect when a result is wrong, rather than an opaque final answer to guess about.
- **Better recovery from partial failure** — a reactive or hierarchical approach can adjust to an unexpected result mid-task rather than needing the entire process restarted.

## Challenges and Limitations
- **Reasoning traces aren't guaranteed to reflect the real decision process** — a model's stated reasoning can look coherent and plausible while not actually being why it chose a given action, which limits how much a trace should be trusted as ground truth for debugging.
- **Planning quality varies with task ambiguity** — a plan is only as good as the model's understanding of the goal and constraints, and an ambiguous or underspecified request can produce a confidently wrong plan just as easily as a confidently wrong single answer.
- **Latency and cost scale with deliberation** — chain-of-thought reasoning, self-critique passes, and multi-step planning all add tokens and time per decision, and not every task's stakes justify that overhead.
- **Overcommitment to a flawed early plan** — upfront planning, done without a mechanism to revisit the plan when new information contradicts it, can lead an agent to execute a bad plan faithfully rather than catching the problem early.

> The point of a visible plan isn't that the agent will follow it perfectly — it's that you can tell, before it's too late, that the plan was wrong.

## Future Potential
The frontier here isn't planning or reasoning in isolation, but making the two interact better — plans that can be revised cheaply when reasoning at a later step contradicts an earlier assumption, rather than requiring a full restart, and reasoning traces that are verifiable enough to actually be trusted as a debugging signal rather than just a plausible-sounding narrative. Progress on that interaction is likely to matter more for real-world reliability than further gains in either capability alone.

---
*Share this with anyone debugging an agent that took a confident, wrong turn on step 4 of a 10-step task.*