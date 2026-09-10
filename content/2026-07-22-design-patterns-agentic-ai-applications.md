Title: Design Patterns for Agentic AI Applications
Date: 2026-07-22
Category: AI Infrastructure
Tags: design patterns, agentic AI, AI architecture, software design, agent patterns
Slug: design-patterns-agentic-ai-applications
Status: Published

Every team building an AI agent seems to rediscover the same handful of structural problems — how to keep a long task from losing coherence, how to let a model check its own work, how to parallelize independent sub-tasks — and, without a shared vocabulary, tends to solve each one from scratch, in a slightly different and rarely reusable way. Traditional software went through this same phase before design patterns like MVC or observer gave developers a shared language for recurring structural problems. Agentic AI is now accumulating its own equivalent set.

## What It Is
**Design pattern (in this context)** — a named, reusable structural solution to a recurring problem in building agent systems, not a specific library or framework, but a shape a solution tends to take regardless of the underlying tools. Naming these patterns matters less for novelty and more for giving teams a shorthand to discuss trade-offs without re-deriving them from scratch each time.
**Pattern vs. implementation** — a pattern describes a structure (a reviewer step that checks a generator's output before it's used); an implementation is the specific code, prompts, and models that realize it for a given system. The same pattern can be implemented very differently across projects while remaining recognizably the same pattern.

## Why It Exists
As more teams built agentic systems in parallel, certain problems kept recurring regardless of domain — how do you keep a model from confidently committing to a bad plan; how do you let independent sub-tasks run without one blocking the others; how do you catch an error before it propagates to a final answer — and the solutions that worked kept converging on similar shapes even when built independently. Naming these patterns exists to shortcut that convergence: instead of every team rediscovering "have a separate agent check the first agent's work" through trial and error, it becomes a known, discussable pattern with known trade-offs.

> A pattern isn't a clever new idea — it's the same idea enough teams kept arriving at independently that it earned a name.

## Common Patterns
- **Reflection / self-critique** — the agent (or a separate pass) reviews its own output against the original goal before finalizing it, catching errors a single generation pass would have missed. Trade-off: doubles the cost of the step it's applied to, and a flawed self-review can rubber-stamp its own mistake.
- **Planner-executor** — a planning step produces a sequence of sub-tasks, and a separate executor carries them out one at a time, keeping the "what should happen" and "make it happen" concerns distinct rather than entangled in one continuous pass.
- **Orchestrator-worker** — a coordinating agent decomposes a task and dispatches sub-tasks to specialized worker agents (or worker instances of the same agent), then assembles their results — the same pattern underlying most multi-agent systems.
- **Router** — an early step classifies the incoming request and directs it to the most appropriate specialized handler (a different prompt, tool set, or even model) rather than using one generalized handler for every request type.
- **Human-in-the-loop checkpoint** — a defined point where the agent pauses for human approval or correction before proceeding, typically placed at the highest-stakes or least-certain step of a process rather than uniformly throughout.
- **Retrieval-augmented step** — any point in an agent's process where it pulls relevant external information into context before acting, rather than relying solely on what's already in the conversation.
- **Parallel fan-out / fan-in** — independent sub-tasks are dispatched concurrently (fan-out) and their results combined once all complete (fan-in), reducing wall-clock time for tasks with genuinely independent parts.

**Worked example**: consider a system generating a quarterly business summary from raw sales data. A naive single-pass design asks one agent call to read the data and write the whole summary — fast, but prone to arithmetic slips and unverified claims making it into the final text. Applying patterns: a **fan-out** step processes each product category's data in parallel rather than sequentially, cutting total time; each category result goes through a **reflection** step checking that stated totals actually match the source data; a **planner-executor** split separates "decide what sections the summary needs" from "write each section," so structural decisions aren't made mid-sentence while also generating prose; and a **human-in-the-loop checkpoint** holds the final summary for a manager's review before it's sent externally, since this document has real reputational stakes. None of these patterns is exotic individually — the value is in recognizing which known shape fits which part of the problem, rather than inventing a bespoke structure for each.

## Comparison to the Status Quo
Before these patterns had names, teams often built agent systems as one long, monolithic prompt or loop trying to handle planning, execution, and review all within a single pass — workable for simple tasks, and a common source of confused, hard-to-debug failures on complex ones, because there was no structural separation between "deciding what to do," "doing it," and "checking it was done right." Naming and adopting patterns pushes teams toward that separation deliberately, the same way MVC pushed web development away from mixing data logic, business logic, and presentation in a single script.

## Advantages
- **Shared vocabulary speeds design discussions** — "let's add a reflection step here" communicates a specific, well-understood structure faster than describing the mechanism from scratch each time.
- **Known trade-offs, not rediscovered ones** — a team adopting the orchestrator-worker pattern can start from its known failure modes (orchestrator bottleneck, worker miscommunication) rather than discovering them the hard way in production.
- **Composability** — patterns combine; a real system often layers several (router plus planner-executor plus reflection), and having names for each makes discussing that composition tractable.

## Challenges and Limitations
- **Patterns aren't universally correct** — applying reflection or human-in-the-loop checkpoints to every step regardless of stakes adds cost and latency without proportional benefit; matching pattern to actual risk and complexity is a judgment call, not a checklist to apply uniformly.
- **The field's pattern vocabulary is still young and unsettled** — unlike decades-old software design patterns, these are still being named, debated, and revised, and what's called by one name in one team's documentation might mean something subtly different elsewhere.
- **A pattern can mask a bad underlying design** — wrapping a poorly scoped task in a planner-executor structure doesn't fix an unclear goal or bad tool definitions; patterns organize a design, they don't validate that the design's fundamentals are sound.

> Knowing the name of a pattern is not the same as knowing when it's the wrong one to reach for.

## Future Potential
As more agentic systems reach production and teams compare notes across companies, expect this pattern vocabulary to solidify further — likely converging, the way earlier software patterns did, on a smaller canonical set with well-understood trade-offs, taught as a standard part of how agentic systems are designed rather than something each team reconstructs independently. The open work is less about discovering fundamentally new patterns and more about building the shared, evidence-based sense of when each one actually pays for its complexity.

---
*Worth forwarding to a team about to rebuild, from scratch, a review step someone else already has a name for.*