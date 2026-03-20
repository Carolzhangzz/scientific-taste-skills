# ICML Venue Module

**International Conference on Machine Learning**

ICML is a top venue for machine learning research with particular emphasis on theoretical grounding, algorithmic innovation, and principled methodology. Compared to NeurIPS, ICML places relatively more weight on theoretical depth and mathematical rigor.

---

## Core Evaluation Criteria

### 1. Novelty
- New algorithm, theory, or formulation — not just a new architecture or hyperparameter
- Clear articulation of what is new vs. what is borrowed from prior work

### 2. Significance
- Does this advance the field's understanding or capability in a lasting way?
- Theoretical: does it resolve an open problem or tighten known bounds?
- Empirical: does it reveal a new phenomenon or enable a new capability?

### 3. Theoretical Grounding
- Are claims supported by formal analysis?
- Are assumptions clearly stated and reasonable?
- ICML particularly values papers that provide theoretical understanding of empirical phenomena

### 4. Clarity and Presentation
- Precise notation and clear problem formulation
- Well-structured proofs (or proof sketches with full proofs in appendix)
- Experimental details sufficient for reproduction

### 5. Experimental Rigor
- Appropriate baselines and fair comparisons
- Ablation studies
- Analysis beyond aggregate metrics — understanding failure cases

---

## What ICML Reviewers Value

### Strongest Contributions
- A new algorithm with provable guarantees that also works well in practice
- Theoretical understanding of why a popular method works (or doesn't)
- A new problem formulation that elegantly captures a practical challenge
- Connections between previously separate areas of ML theory

### Common Acceptance Patterns
- **Algorithm + Theory + Experiments:** Propose method, prove convergence/bounds, verify empirically
- **Theoretical Analysis of Practice:** "Everyone uses X. Here's why it works, and here's when it breaks."
- **New Problem Formulation:** "The real challenge isn't X — it's Y. Here's the right way to formalize Y."
- **Unifying Framework:** "Methods A, B, and C are all special cases of this general principle"

### Red Flags
- Pure engineering / "bag of tricks" without insight into why
- Theoretical results with unrealistic assumptions and no empirical validation
- SOTA claims without understanding the source of improvement
- Over-reliance on one benchmark or dataset
- Missing comparison with theoretically motivated baselines

---

## Evaluation Standards

### Theory Papers
- Complete, correct proofs
- Lower bounds or matching bounds to show tightness
- Simple examples illustrating the theory
- Discussion of assumption necessity
- Experimental validation of theoretical predictions

### Algorithm Papers
- Clear pseudocode
- Complexity analysis (time, space, communication)
- Convergence guarantees where applicable
- Comparison with both heuristic SOTA and theoretically motivated methods
- Sensitivity analysis for hyperparameters

### Empirical Papers (less common at ICML but acceptable)
- Must include substantial analysis/insight, not just numbers
- Controlled experiments isolating specific factors
- Scaling behavior and computational cost analysis
- Reproducibility: code, data, exact hyperparameters

---

## Paper Structure (Typical)

```
1. INTRODUCTION (~1.5 pages)
   - Problem motivation
   - Informal statement of results
   - Contribution list

2. PRELIMINARIES (~1 page)
   - Notation, definitions, problem setup
   - Key assumptions

3. RELATED WORK (~1 page)
   - Positioning relative to theory and practice

4. MAIN RESULTS (~3-4 pages)
   - Formal statements (theorems, propositions)
   - Proof sketches for key results
   - Algorithm description (if applicable)

5. EXPERIMENTS (~2-3 pages)
   - Synthetic experiments validating theory
   - Real-world experiments showing practical relevance
   - Ablations and analysis

6. DISCUSSION (~0.5-1 page)
   - Limitations, open questions, broader impact
```

---

## Common Rejection Reasons

1. **Incremental theory:** Minor extension of known results to a slightly different setting
2. **Gap between theory and practice:** Theoretical guarantees require assumptions that don't hold in practice, and no empirical validation bridges the gap
3. **Engineering paper:** Good results but no understanding of why
4. **Scope:** Better suited for an applications venue or workshop
5. **Correctness issues:** Proof errors or flawed experimental methodology
6. **Novelty:** Core technique already exists in a different community/paper

---

## Taste Calibration for ICML

When applying the 5 taste tests for ICML:
- **Fundamental vs Surface:** Does this address a fundamental limitation of current learning theory/algorithms, or just improve performance on a benchmark?
- **Elegance:** Is the key result a clean theorem, a simple algorithm, or a unifying insight?
- **Generative Power:** Will this open new lines of theoretical inquiry or enable new algorithmic families?
- **Pairwise:** Compare against ICML Best Papers and Test of Time Award winners
- **Senior Reviewer:** Would a senior AC find the theoretical contribution deep, or is it "straightforward extension"?
