# NeurIPS Venue Module

**Conference on Neural Information Processing Systems**

NeurIPS is a top venue for machine learning, computational neuroscience, and AI. It values theoretical rigor, empirical thoroughness, and genuine algorithmic/conceptual novelty.

---

## Core Evaluation Criteria

### 1. Novelty
- Is the core idea genuinely new, or a recombination of known techniques?
- Does it introduce a new perspective, formulation, or paradigm?
- "Novel application of existing method to new dataset" is NOT sufficient

### 2. Significance
- Does the result advance understanding or capability in a meaningful way?
- Would the community's research direction change if this were true?
- Impact on both theory and practice considered

### 3. Clarity
- Is the paper well-written and easy to follow?
- Are the claims precisely stated?
- Are the limitations honestly discussed?

### 4. Correctness
- Are the theoretical claims proven rigorously?
- Is the experimental methodology sound?
- Are the baselines appropriate and fairly compared?

### 5. Reproducibility
- Is there enough detail to reproduce the results?
- Are hyperparameters, compute requirements, and random seeds reported?
- Code/data availability strongly encouraged

---

## What NeurIPS Reviewers Look For

### Strong Accept Signals
- A clean theoretical result that resolves an open question
- A new algorithm with both theoretical grounding AND strong empirical results
- A surprising empirical finding that challenges conventional wisdom
- A new benchmark/dataset that enables research previously impossible

### Common Acceptance Patterns
- **Theory + Experiments:** Prove a bound, then show it's tight empirically
- **New Paradigm + Ablations:** Propose a fundamentally different approach, ablate every component
- **Surprising Discovery:** "We found that X, which everyone assumed, is actually wrong because Y"
- **Scaling Law / Empirical Law:** Discover a systematic relationship that holds across scales

### Red Flags for Reviewers
- "We achieve SOTA on benchmark X" with no insight into WHY
- Insufficient baselines or unfair comparisons (different compute, data, tuning)
- Claims beyond what the experiments support
- No ablation study — unclear which components matter
- Missing error bars or statistical significance tests

---

## Evaluation Standards

### Theoretical Papers
- Clear problem statement and notation
- Complete proofs (or proof sketches with full proofs in appendix)
- Lower bounds or impossibility results to show tightness
- Simple illustrative examples

### Empirical Papers
- Multiple datasets (at least 3, across different characteristics)
- Strong baselines (including recent ones, not just classic methods)
- Ablation studies for each proposed component
- Compute budget and wall-clock time reported
- Error bars across multiple runs (≥3, ideally 5)
- Statistical significance tests where appropriate

### Benchmark/Dataset Papers
- Clear gap analysis: what can't existing benchmarks measure?
- Baseline results from multiple representative methods
- Datasheet or dataset card
- License and ethical considerations
- Long-term maintenance plan

---

## Paper Structure (Typical)

```
1. INTRODUCTION (~1.5 pages)
   - Problem statement and motivation
   - Key insight / contribution summary
   - Brief description of results

2. RELATED WORK (~1 page)
   - Position relative to closest work
   - Clear differentiation

3. PROBLEM FORMULATION (~0.5-1 page)
   - Formal setup, notation, assumptions

4. METHOD (~2-3 pages)
   - Algorithm/model description
   - Theoretical analysis (if applicable)

5. EXPERIMENTS (~3-4 pages)
   - Setup: datasets, baselines, metrics, compute
   - Main results table
   - Ablation studies
   - Analysis: what works, what doesn't, why

6. DISCUSSION & CONCLUSION (~1 page)
   - Limitations
   - Broader impact statement
   - Future directions
```

---

## Common Rejection Reasons

1. **Incremental:** "This is a straightforward extension of [X] with minor modifications"
2. **Overclaimed:** Results don't support the breadth of claims made
3. **Weak baselines:** Missing obvious comparisons or using outdated baselines
4. **No insight:** Achieves good numbers but doesn't explain why or provide understanding
5. **Poor reproducibility:** Insufficient experimental details
6. **Scope mismatch:** Better suited for a domain-specific venue
7. **Clarity:** Paper is hard to follow; key ideas buried in notation

---

## Taste Calibration for NeurIPS

When applying the 5 taste tests for NeurIPS:
- **Fundamental vs Surface:** Does this change how we think about learning/optimization/representation, or just add a component?
- **Elegance:** Can the key insight be stated as a clean mathematical proposition or algorithmic principle?
- **Generative Power:** Will this spawn a new line of research, or is it a point solution?
- **Pairwise:** Compare against recent oral/spotlight papers, not just any accepted paper
- **Senior Reviewer:** Would a senior area chair find this theoretically or empirically surprising?
