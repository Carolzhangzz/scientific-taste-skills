# 10 Common Failure Modes in Research Idea Generation

These failure modes are derived from evaluating 100+ research idea proposals across HCI, ML, and systems venues. They are the most common reasons that technically sound ideas fail the taste filter.

---

## Failure 1: Technology-First Combination

**Pattern:** "Let's combine [hot technology A] + [hot technology B] + [domain C]!"

**Why it fails:** Starting from technologies instead of problems produces ideas with no grounding in real human or scientific need. The resulting "contribution" is just an existence proof that two things can be combined.

**Example:**
- Bad: "Combine world models + emotion recognition + games"
- Good: "Game designers can't preview how players will feel — they iterate blindly for months"

**Fix:** Always start from a stakeholder who is BLOCKED. The technology should be the solution, not the starting point.

---

## Failure 2: "Better X" Instead of "New X"

**Pattern:** "Our system achieves higher accuracy/speed/quality than the baseline"

**Why it fails:** Incremental improvements to existing approaches are easily superseded. They don't change how the field thinks about the problem.

**Example:**
- Bad: "A better emotion recognition system" (ML improvement)
- Good: "A new way to author emotion trajectories in interactive media" (new paradigm)

**Fix:** Remove the words "better/faster/easier/more accurate" from your pitch. Replace with "didn't exist before" or "now possible." If it still makes sense, you have a real contribution.

---

## Failure 3: Scope Creep

**Pattern:** "Our system handles X, Y, Z, and also W simultaneously"

**Why it fails:** Breadth kills depth. Reviewers respect systems that do ONE thing remarkably well over systems that do many things adequately.

**Example:**
- Bad: "Controls emotion in images, video, music, AND narrative"
- Good: "Controls emotion trajectories in game narrative through a single interaction paradigm"

**Fix:** Pick the ONE modality/domain/task where your contribution is strongest. Nail it. Mention others as future work.

---

## Failure 4: Missing Empirical Grounding

**Pattern:** "We designed these features based on our understanding of user needs"

**Why it fails:** Without formative evidence (interviews, observations, corpus analysis), design decisions appear arbitrary. Reviewers will ask "where did this come from?"

**Example:**
- Bad: "We identified three key challenges in collaborative writing" (from intuition)
- Good: "Interviews with 8 professional screenwriters revealed three breakdowns..." (from evidence)

**Fix:** Ground every major design decision in empirical evidence — formative studies, corpus analysis, existing literature, or domain expert consultation.

---

## Failure 5: Evaluating the Method, Not the Contribution

**Pattern:** "Our system achieves 94% accuracy on the benchmark"

**Why it fails:** If your contribution is a new interaction paradigm, measuring model accuracy misses the point. If your contribution is a new framework, measuring one instantiation's performance misses the generality.

**Example:**
- In HCI: Measure perceived control, agency, creativity support, cognitive load — not model accuracy
- In ML: If proposing a new framework, show it enables things that weren't possible before — not just SOTA on one benchmark

**Fix:** Match your evaluation to your claimed contribution. What does the paper promise? Evaluate that promise directly.

---

## Failure 6: No Result Story

**Pattern:** The paper works, the evaluation is solid, but there's no compelling moment

**Why it fails:** Every memorable paper has a moment — a demo, a figure, a result — that captures the contribution in 30 seconds. Without it, the paper lacks identity.

**Example:**
- In HCI: "Draw a sketch on a textbook page → it becomes a working physics simulation" (Augmented Physics)
- In ML: "A single model trained on text predicts protein structure" (AlphaFold's famous figure)

**Fix:** Before building anything, describe the one figure/demo/result that captures your contribution. If you can't, the contribution may not be clear enough.

---

## Failure 7: Ignoring Related Work

**Pattern:** "We believe our approach is the first to..."

**Why it fails:** If you don't know the 3 closest papers intimately, you can't articulate what's genuinely new. Reviewers who work in the area WILL know those papers.

**Example:**
- Bad: "To our knowledge, no prior work addresses emotional trajectory authoring" (someone has, and a reviewer will find it)
- Good: "Ansari et al. (2021) proposed emotion heatmaps for game design, but their approach is post-hoc analysis, not authoring. We enable real-time trajectory design."

**Fix:** For each of the 3 closest papers, write one sentence: "X did Y. We do Z. The essential difference is W."

---

## Failure 8: Surface-Level Problem

**Pattern:** "Users find it hard to [minor inconvenience]"

**Why it fails:** If the problem could be solved by better UX design, a new feature, or existing tools, it doesn't need a research paper. High-impact research addresses problems where the current paradigm is structurally inadequate.

**Example:**
- Surface: "Users find it hard to navigate complex menus"
- Fundamental: "The mismatch between how users think about creative intent and how tools expose parameters means entire classes of designs are unreachable"

**Fix:** Ask: "Would a senior researcher find this problem intellectually interesting?" If the response would be "just ship a better product," the problem is too shallow for research.

---

## Failure 9: No Generative Power

**Pattern:** The system works, the demo is cool, the evaluation is solid — but nobody will ever build on it

**Why it fails:** This is the "dead-end paper" failure. It gets accepted, gets some citations as "related work," and is forgotten. High-impact ideas introduce new abstractions that other researchers apply to their own domains.

**Example:**
- Low generative power: A custom tool for one specific task (e.g., "a tool for annotating bird songs")
- High generative power: A new interaction paradigm (e.g., "intermediate representations as agency bridges" — applicable to any human-AI co-creation task)

**Fix:** Ask: "Will anyone cite this paper to BUILD on it, or only to RELATE to it?" If the latter, the contribution is too narrow. Look for the general principle behind your specific system.

---

## Failure 10: Variant, Not Vision

**Pattern:** "We applied [method X] to [new domain Y]"

**Why it fails:** Variants get accepted but never become best papers or high-impact work. They demonstrate that X works in Y, which is useful but not exciting.

**Example:**
- Variant: "We used diffusion models for audio generation" (X in new domain Y)
- Vision: "We discovered that the way musicians think about sound textures is fundamentally different from how synthesis tools represent them — and here's a new representation that bridges the gap"

**Fix:** The RLCF findings (arXiv:2603.14473) show that trained models consistently prefer paradigm-shifting solutions over incremental variants. If your idea is "X but for Y," ask: what would a genuinely new approach to Y look like? What would someone who had never heard of X propose?
