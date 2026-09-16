---
name: grilling
description: Interview the user relentlessly about a plan, decision, or idea until every branch of the design tree is resolved — rounds of pointed questions with real tradeoffs, facts looked up by the agent, decisions made by the user. Use when the user wants to stress-test or sharpen their thinking, or uses any 'grill' trigger phrases. The interview primitive behind grill-me, grill-with-docs, triage, wayfinder and improve-codebase-architecture.
---

Interview the user relentlessly until you reach a shared understanding. Map this as a **design tree**: every decision branches into the decisions that hang off it.

Work the tree in **rounds**. The **frontier** is every decision whose prerequisites are already settled: the questions you can ask _now_ without guessing at answers you haven't heard yet. Ask the whole frontier in one round, then wait for the user's answers before the next round.

**Use the `AskUserQuestion` tool (Claude Code's `ask`), not prose.** Put the entire frontier in ONE call: one question per decision, each with 2–5 concrete options, tradeoffs in the option descriptions, and the option carrying your recommendation first, labelled `(Recommended)`. The UI adds a free-text "Other", so open questions still work. Keep chat text to a one-line recap of what just settled — never dump the questions into the message.

Each round the user's answers reshape the tree: settled decisions push the frontier outward and unblock questions that depended on them. Recompute the frontier and ask the next round. A question whose answer depends on another question still open in this round belongs to a _later_ round, not this one.

**Every question earns its place.** It must be a **real fork** — 2+ viable options, actual tradeoffs, and an answer that changes what gets built; drop anything else. Ask in the user's **own words**, reflecting back what they've told you rather than re-asking settled ground. Aim at the **implicit**: the assumed constraint, the unweighed tradeoff, the contradiction between two earlier answers. When a contradiction appears, stop and put it to the user — that's where the real decision usually hides. If a question can only be answered by seeing or feeling something (how a UI should look, how a flow should feel), say so and route to a prototype instead of guessing.

**Facts are your job, never the user's.** When a frontier question needs a fact from the environment (filesystem, tools, etc.), dispatch a sub-agent to find it; don't ask the user for anything you could look up yourself. Don't block on it: a running exploration is an unsettled prerequisite, so only the questions downstream of it wait for the sub-agent to report; ask the rest of the frontier now. The _decisions_ are the user's: put each to them and wait.

**Converge, don't drone.** A terse answer earns one sharp follow-up to pin the tradeoff; a thorough answer earns a move on. When the next round would only restate settled ground or manufacture questions to keep the interview going, the frontier is empty — stop. Never answer your own questions, and never start building.

The session is done when the frontier is empty: every branch of the design tree visited, nothing left silently assumed. Name what is **not** decided — edge cases and open risks — so "settled" is honest. Present the settled decisions as a shared-understanding summary and confirm it via one final `AskUserQuestion` (e.g. "确认" / "有调整") before acting on anything.
