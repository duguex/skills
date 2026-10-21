---
name: grilling
description: Interview the user relentlessly about a plan, decision, or idea until every branch of the design tree is resolved — rounds of pointed questions with real tradeoffs, facts looked up by the agent, decisions made by the user. Use when the user wants to stress-test or sharpen their thinking, or uses any 'grill' trigger phrases. The interview primitive behind grill-me, grill-with-docs, triage, wayfinder and improve-codebase-architecture.
---

Interview the user relentlessly until you reach a shared understanding. Map this as a **design tree**: every decision branches into the decisions that hang off it.

Work the tree in **rounds**. The **frontier** is every decision whose prerequisites are already settled: the questions you can ask _now_ without guessing at answers you haven't heard yet. Ask the whole frontier in one round, then wait for the user's answers before the next round.

**Use the `AskUserQuestion` tool, not prose.** Put every decision to the user through the picker — never dump the questions into the message. **The tool caps each call at 4 questions and each question at 4 options**, so "the whole frontier" means all of it that fits the cap; a frontier larger than 4 splits across multiple calls. **Split by dependency, not by numbering**: a question that depends on an answer you have not heard yet belongs to a _later_ round, not to a second batch — by the rule above it is not in this round's frontier at all. Do not force it into another call: ask only the independent head, wait, recompute the frontier, and let newly unblocked questions into the next round. Only when the tail questions are genuinely independent of the head may they go in further calls of the same round.

- Each question gets 2–4 concrete, mutually exclusive options with real tradeoffs in the option `description` — the description says what choosing actually commits to, never restates the label.
- **Never drop the recommendation.** The option carrying your recommendation is labelled `(Recommended)` and its `description` says _why_ — the most valuable part of the template, it must survive the picker.
- The UI adds a free-text "Other", so open questions still work. When the options genuinely cannot be enumerated in advance — exploratory questions like "what problem are you actually trying to solve" — the picker would narrow the answer space on the user's behalf; ask those in prose.
- Keep chat text to a one-line recap of what just settled.

Each round the user's answers reshape the tree: settled decisions push the frontier outward and unblock questions that depended on them. Recompute the frontier and ask the next round. A question whose answer depends on another question still open in this round belongs to a _later_ round, not this one.

**Every question earns its place.** It must be a **real fork** — 2+ viable options, actual tradeoffs, and an answer that changes what gets built; drop anything else. Ask in the user's **own words**, reflecting back what they've told you rather than re-asking settled ground. Aim at the **implicit**: the assumed constraint, the unweighed tradeoff, the contradiction between two earlier answers. When a contradiction appears, stop and put it to the user — that's where the real decision usually hides. If a question can only be answered by seeing or feeling something (how a UI should look, how a flow should feel), say so and route to a prototype instead of guessing.

**Facts are your job, never the user's.** When a frontier question needs a fact from the environment (filesystem, tools, etc.), dispatch a sub-agent to find it; don't ask the user for anything you could look up yourself. Don't block on it: a running exploration is an unsettled prerequisite, so only the questions downstream of it wait for the sub-agent to report; ask the rest of the frontier now. The _decisions_ are the user's: put each to them and wait.

**Converge, don't drone.** A terse answer earns one sharp follow-up to pin the tradeoff; a thorough answer earns a move on. When the next round would only restate settled ground or manufacture questions to keep the interview going, the frontier is empty — stop. Never answer your own questions, and never start building.

## When the picker returns nothing

`AskUserQuestion` may come back with **no answer** — the user neither picked an option nor typed anything. That is a failure of the mechanism, not an answer from the user.

**After the same question returns nothing twice in a row, do not try a third time.** Fall back to asking it in prose, offering three ways to reply so the user can pick the channel: answer by number, answer in free text, or discuss it first and decide after.

**Never settle a question yourself because the picker came back empty.** That writes a decision the user never made into whatever you produce next, which is the single worst failure mode here. Stop and say where you are stuck instead.

The session is done when the frontier is empty: every branch of the design tree visited, nothing left silently assumed. Name what is **not** decided — edge cases and open risks — so "settled" is honest. Present the settled decisions as a shared-understanding summary and confirm it via one final `AskUserQuestion` (e.g. "确认" / "有调整") before acting on anything.
