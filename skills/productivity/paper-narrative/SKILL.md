---
name: paper-narrative
description: Revise a scientific manuscript as narrative — the abstract, introduction and conclusions as narrative, the results, figures and discussion as evidence — without touching the science, by calibrating against the target field's own papers.
disable-model-invocation: true
---

Revise how a manuscript **tells** its story, leaving what it **claims** untouched. The science is the user's: numbers, formulas, conclusions, and scope stay exactly as written. What changes is the arrangement, the resolution, and the framing.

Run the passes in order. Each pass ends on a criterion you can check.

Passes 1–4 work the **narrative layer** (abstract, introduction, conclusions): the sections that state the claim, motivate it, and close on it. Pass 5 works the **evidence layer** (results, figures, discussion): the sections that carry the proof. The two layers fail differently, so they are diagnosed differently — do not stretch a narrative rule over an evidence section. "The abstract leaks the step size" and "Results repeats its figure captions" are both narrative problems, but the second is not a leak.

## Pass 1 — Resolution

Scientific writing carries several **resolutions**, and each one belongs to a layer: the abstract states the claim and the order of magnitude, the body carries the numbers, Methods carries the implementation. A detail sitting above its layer is a **leak** — the seed count in the abstract, the finite-difference step in the opening sentence. A leak costs more than words: it interrupts the reader's descent from claim to evidence, and it signals that the author has not decided what matters.

Sweep the abstract, introduction, and conclusions for leaks. Treat the trigger as a **class**, not an instance: when the user names one leak, find its siblings before editing — a step size in one sentence predicts an epoch count three sentences later. Collect every candidate, present them together, and let the user rule on which layers each belongs to.

A removed detail is **relocated**, not deleted: name where it goes (Methods, a specific section, a table). Deleting a number without a destination loses information the paper needs.

*Done when:* every detail in a high-level section either belongs to that section's resolution or has a named destination below it.

## Pass 2 — Skeleton

A field writes its abstracts to a shared **skeleton**, and readers — especially reviewers — recognize deviations from it before they can say what is wrong. Recover the skeleton from the field itself, never from memory or from a template you brought with you: a skeleton inferred from 8 ML-Hamiltonian papers does not transfer to a condensed-matter theory paper, and imposing it would be the same error as the leak, one level up.

Collect 5–10 recent papers of the target type and venue. Local assets first — the user's own repositories often hold the field's PDFs already (`repos/*/`, a `calc_paper`-style library) — and the open web only for what is missing. Read what each one opens with and what it closes on, then name the recurring slots.

Lay your draft against the skeleton slot by slot. The gap is the finding: a draft missing its "pain point" slot does not read as incomplete, it reads as unmotivated — the reader meets the solution before learning what needs solving.

[`references/skeletons.md`](references/skeletons.md) holds a skeleton already recovered this way, with the recovery procedure and one worked field as evidence of what the method yields. Read it to see the shape of the output; recover the target field's skeleton fresh regardless — a recorded skeleton is a hypothesis to test, not a template to apply.

*Done when:* you can name each slot of the field's skeleton and point to the sentence in the draft that fills it, or record the slot as missing.

## Pass 3 — Contest

The skeleton's pain-point slot is where a paper stakes its claim, and it is read twice: once for how the draft motivates itself, and once for what the field has left undone. Collect the pain points of every sampled paper and ask what they have in common. A pain point repeated across the field is an **assumption** — load-bearing, invisible, and shared. A gap no paper claims is the draft's slot.

This pass is where writing and positioning merge: the sentence you add to the introduction is the same sentence that tells you whether the paper has a contribution at all. When the sampled pain points all point somewhere other than where your draft points — at cost, at scale, at coverage, rather than at the axis you measured — say so, because it is the strongest evidence the draft has something to say.

*Done when:* you can state the field's shared assumption in one sentence, and the draft has a sentence that names it and a sentence that answers it.

## Pass 4 — Frame

The framing decides what is the subject and what is the demonstration. A method paper is about the method; a host material is where it was shown. Getting this backwards makes a general result read as a case study, and a case study read as overclaiming. Settle with the user which one the draft is: it changes the title, the opening sentence, and every sentence that names the host.

Set the claim once, then **echo** it at rising resolution — the abstract asserts it, the introduction grounds it in the field's state, the conclusions close on the measurement. The echo is not repetition: each version answers a different question the reader is holding at that point in the paper.

*Done when:* the subject and the demonstration are distinguishable in every high-level section, and the central claim appears in the abstract, introduction, and conclusions at three different resolutions.

## Pass 5 — Evidence

The narrative layer decides what is claimed; the evidence layer has to deliver it readably. A results section can be scientifically complete and still fail its reader — by making them assemble the finding from a figure, by hiding the point in a neutral heading, by restating in prose what the caption already said. Three tests, run over the sections that carry proof:

**Headings carry the finding.** A results heading is a sentence a reader can read alone and learn something ("Supervising slopes cuts the error to 9.5% at no static cost"), not a label ("Slope results"). Scan every heading in the results and discussion sections; each one should survive being read out of context.

**Captions stand alone.** A reader who jumps to a figure first should get its finding without the surrounding prose, and a reader who reads the prose should gain something the caption did not already give. Check both directions: a caption that only names the axes fails the first, prose that repeats the caption's sentences fails the second.

**Discussion rises.** The discussion earns its place by answering a question the results cannot: what the finding means, where its boundary is, what it does not license. Re-reading the results in different words, or restating the numbers, is a failure — the numbers already have a home. Each discussion paragraph should be traceable to a question the introduction left open, or to a limitation the results exposed.

*Done when:* every heading states a finding, every caption is self-sufficient and non-duplicative of its body text, and every discussion paragraph answers a question that the results section cannot answer on its own.

## Constraints

**Revise the telling, not the claims.** Numbers, formulas, derived conclusions, and scope statements stay as written. When a sentence needs a number changed, that is a scientific decision — surface it and stop.

**Compile and look.** After editing, build the manuscript and confirm it resolves (no undefined references, no missing citations), then render the changed pages and read them as the reader will. A diff that looks right in the source can break across a page or collide with a float.

## Reporting

Close with the changes grouped by exactly what moved: what was relocated and where, which skeleton slots were missing and how they were filled, how the framing was settled, which headings and captions were rewritten under Pass 5, and which details were left alone because they belong to the science.
