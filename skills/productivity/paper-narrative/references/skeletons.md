# Recovered skeletons

Skeletons are field artifacts, not universal templates. These are recorded as **evidence of the method** — what the recovery yields — and as a starting hypothesis to test against a new field's samples, never to apply untested.

## ML-for-science (Hamiltonian / interatomic-potential papers)

Recovered from DeepH (Li 2022), DeepH-E3 (Gong 2023), HamGNN (Zhong 2023), Deep DFPT (Li 2024), Zhong EPC (2024), Universal KS Hamiltonian (Zhong 2024), Xia 2025, NextHAM (Yin 2026), MACE-H (Qian 2026).

| Slot | What fills it |
|---|---|
| Field value | Why the direction is worth doing — often an accuracy–efficiency dilemma |
| Pain point | What blocks the field now: DFT cost, poor scaling, insufficient generalization, training-data expense |
| Solution | What this paper proposes |
| Result | Numbers, preferably with a scale claim |
| Outlook | What the result opens up |

Observed in this sample:

- Every pain point pointed at **cost, scale, coverage, or data** — never at the *accuracy axis* of the learned quantity.
- Every value claim landed on **replacing DFT** — "DFT-level fidelity at a fraction of the cost".
- The result slot is where the invariance holds: a paper claiming sub-meV accuracy and one claiming 10⁴-atom scale both fill it.

The gap this recovery exposed: if every paper optimizes static accuracy and none audits whether the derivative follows, then "static fidelity does not imply response fidelity" is a slot no one occupies. The pain-point pass and the positioning pass are the same pass.

## Recovery procedure

1. Gather 5–10 papers: same subfield, same venue tier, recent.
2. Source order — local library first (`repos/`, a paper corpus, the group's own PDFs), open web for gaps.
3. Extract for each: the opening claim, the stated obstacle, the proposed object, the headline number, the closing promise.
4. Cluster the extractions into slots; name each slot by the question it answers, not by its position.
5. Note the invariant slots (these define the skeleton) and the variable ones (these carry the paper's identity).
6. Collect the pain-point slot across all samples — the shared content is the field's assumption, the absent content is your draft's opportunity.
