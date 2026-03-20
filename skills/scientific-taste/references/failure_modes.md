# 12 Common Failure Modes in Research Idea Generation

These failure modes are derived from evaluating 100+ research idea proposals across HCI, ML, and systems venues, combined with findings from 16+ papers on automated research ideation.

---

## Failure 1: Technology-First Combination

**Pattern:** "Let's combine [hot technology A] + [hot technology B] + [domain C]!"

**Why it fails:** Starting from technologies instead of problems produces ideas with no grounding in real human or scientific need. The resulting "contribution" is just an existence proof that two things can be combined.

**Example:**
- Bad: "Combine world models + emotion recognition + games"
- Good: "Game designers can't preview how players will feel — they iterate blindly for months"

**Fix:** Always start from a stakeholder who is BLOCKED. The technology should be the solution, not the starting point. Use the Problem-First generation path.

---

## Failure 2: "Better X" Instead of "New X"

**Pattern:** "Our system achieves higher accuracy/speed/quality than the baseline"

**Why it fails:** Incremental improvements to existing approaches are easily superseded. They don't change how the field thinks about the problem.

**Example:**
- Bad: "A better emotion recognition system" (ML improvement)
- Good: "A new way to author emotion trajectories in interactive media" (new paradigm)

**Fix:** Remove the words "better/faster/easier/more accurate" from your pitch. Replace with "didn't exist before" or "now possible."

---

## Failure 3: Scope Creep

**Pattern:** "Our system handles X, Y, Z, and also W simultaneously"

**Why it fails:** Breadth kills depth. Reviewers respect systems that do ONE thing remarkably well over systems that do many things adequately.

**Fix:** Pick the ONE modality/domain/task where your contribution is strongest. Nail it. Mention others as future work.

---

## Failure 4: Missing Empirical Grounding

**Pattern:** "We designed these features based on our understanding of user needs"

**Why it fails:** Without formative evidence (interviews, observations, corpus analysis), design decisions appear arbitrary. Reviewers will ask "where did this come from?"

**Fix:** Ground every major design decision in empirical evidence — formative studies, corpus analysis, existing literature, or domain expert consultation.

---

## Failure 5: Evaluating the Method, Not the Contribution

**Pattern:** "Our system achieves 94% accuracy on the benchmark"

**Why it fails:** If your contribution is a new interaction paradigm, measuring model accuracy misses the point. If your contribution is a new framework, measuring one instantiation's performance misses the generality.

**Fix:** Match your evaluation to your claimed contribution. What does the paper promise? Evaluate that promise directly.

---

## Failure 6: No Result Story

**Pattern:** The paper works, the evaluation is solid, but there's no compelling moment

**Why it fails:** Every memorable paper has a moment — a demo, a figure, a result — that captures the contribution in 30 seconds.

**Example:**
- HCI: "Draw a sketch on a textbook page → it becomes a working physics simulation" (Augmented Physics)
- ML: "A single model trained on text predicts protein structure" (AlphaFold)

**Fix:** Before building anything, describe the one figure/demo/result that captures your contribution.

---

## Failure 7: Ignoring Related Work

**Pattern:** "We believe our approach is the first to..."

**Why it fails:** If you don't know the 5 closest papers intimately, you can't articulate what's genuinely new. Reviewers who work in the area WILL know those papers.

**Data:** Si et al. (ICLR 2025) found that 95% of LLM-generated "novel" ideas already existed in the literature. This failure mode is MUCH more common than people think.

**Fix:** Run the Literature-Grounded Novelty Audit (Dimension 4). For each of the 5 closest papers, write: "X did Y. We do Z. The essential difference is W."

---

## Failure 8: Surface-Level Problem

**Pattern:** "Users find it hard to [minor inconvenience]"

**Why it fails:** If the problem could be solved by better UX design, a new feature, or existing tools, it doesn't need a research paper.

**Fix:** Ask: "Would a senior researcher find this problem intellectually interesting?" If the response would be "just ship a better product," the problem is too shallow.

---

## Failure 9: No Generative Power

**Pattern:** The system works, the demo is cool, the evaluation is solid — but nobody will ever build on it

**Why it fails:** The "dead-end paper." Gets accepted, gets some citations as "related work," forgotten. High-impact ideas introduce new abstractions that others apply to their own domains.

**Fix:** Ask: "Will anyone cite this paper to BUILD on it, or only to RELATE to it?"

---

## Failure 10: Variant, Not Vision

**Pattern:** "We applied [method X] to [new domain Y]"

**Why it fails:** Variants get accepted but never become best papers. The RLCF findings show that trained models consistently prefer paradigm-shifting solutions over incremental variants.

**Fix:** If your idea is "X but for Y," ask: what would a genuinely new approach to Y look like?

---

## Failure 11: Novelty Illusion
*(NEW — from HindSight, 2026 + Si et al., ICLR 2025)*

**Pattern:** "This feels novel to me, and ChatGPT also says it's novel"

**Why it fails:** HindSight showed that LLM-judged novelty is NEGATIVELY CORRELATED with real-world impact. LLMs mistake unfamiliarity for novelty. And 95% of LLM-generated "novel" ideas already exist in the literature.

**Example:**
- You ask GPT: "Is this idea novel?" GPT says yes. You feel validated.
- A reviewer searches Semantic Scholar and finds three papers that already did this.
- Your paper gets desk-rejected.

**Fix:** NEVER rely on LLM self-assessment for novelty. Always use retrieval-based verification: search Semantic Scholar, Google Scholar, arXiv, and connected papers. The Novelty Audit (Dimension 4) makes this systematic.

---

## Failure 12: Trajectory Misalignment
*(NEW — from Chain of Ideas, EMNLP 2025)*

**Pattern:** Solving a problem the field has already moved past, or that will become irrelevant soon

**Why it fails:** Even a well-executed paper on a dead problem won't generate impact. Fields evolve, and the "hot" problems of 2 years ago may be fully solved or abandoned today.

**Example:**
- Publishing a better GAN architecture in 2025 (the field moved to diffusion models in 2022)
- Publishing a new pre-training method when the field is focused on post-training alignment

**Fix:** Map the field's trajectory using Chain of Ideas methodology:
1. What were the key papers in this area each year for the last 3 years?
2. What trend do they reveal?
3. Does your idea extend this trend, redirect it, or ignore it?
4. If it ignores the trend, do you have a compelling reason why the trend is wrong?
