---
name: scientific-taste
description: >
  Evaluate and generate research ideas using Scientific Taste —
  distinguishing paradigm-shifting ideas from incremental variants.
  Integrates methodologies from 16+ papers on automated research ideation.
  Works for any venue and any discipline.
license: MIT
metadata:
  skill-author: Qinshi Zhang
  version: 2.0.0
---

# Scientific Taste Agent

Evaluate and generate research ideas using Scientific Taste — not checklist scoring, but the trained intuition that separates paradigm-shifting ideas from incremental variants.

**v2.0: Now integrates methodologies from 16+ papers on automated research ideation and evaluation, including RLCF pairwise training, literature-grounded novelty verification, faceted evaluation, dual-path generation, trajectory alignment, and the critical finding that novelty alone is anti-correlated with real-world impact.**

## When to Use This Skill

- Evaluating whether a research idea is worth pursuing
- Generating ideas from real problems (not technology combinations)
- Comparing two ideas head-to-head
- Stress-testing a paper concept before committing months of work
- Checking venue fit (UIST, CHI, NeurIPS, ICML, or custom)

## Commands

- `/scientific-taste evaluate [idea description]` — Run 7-dimension evaluation on an idea
- `/scientific-taste generate [domain] [problem]` — Generate ideas from a problem using dual-path pipeline
- `/scientific-taste compare [idea A] vs [idea B]` — Pairwise comparison with position-swap debiasing
- `/scientific-taste audit [idea]` — Literature-grounded novelty audit (are you actually novel?)
- Add `--venue uist|chi|neurips|icml` to any command for venue-specific checks

## How It Works

When invoked, this agent will:
1. Understand the research context (domain, resources, constraints)
2. Run literature-grounded novelty audit (avoid reinventing existing work)
3. Apply the 7-Dimension Taste Evaluation
4. Check trajectory alignment (does this idea fit where the field is going?)
5. Optionally load venue-specific criteria from `venue-modules/`
6. Produce a structured evaluation with kill/proceed recommendation

---

## PART 1: The Novelty Trap — Why Taste ≠ Novelty

> **Critical finding from HindSight (2026): LLM-judged "novelty" is NEGATIVELY CORRELATED with real-world research impact.**

Most researchers (and AI tools) equate good ideas with novel ideas. This is wrong. The HindSight study showed that RAG-augmented ideas score 2.5x higher on real impact, but LLM-as-Judge sees no difference — because LLMs mistake unfamiliarity for novelty.

Additionally, Si et al. (ICLR 2025) found that 95% of LLM-generated "novel" ideas are duplicates of existing work, and LLM self-evaluation accuracy is barely above chance (53.3%).

**Scientific Taste is NOT novelty maximization. It is the ability to judge whether an idea will create lasting structural impact — which requires balancing:**

| Dimension | Why It Matters | Anti-Pattern |
|-----------|---------------|-------------|
| Novelty | Must be genuinely new | But novelty alone → obscure dead-end |
| Feasibility | Must be executable | But feasibility alone → incremental |
| Groundedness | Must connect to real problems | But groundedness alone → engineering |
| Trajectory Alignment | Must fit where the field is heading | But alignment alone → bandwagon |
| Generative Power | Must enable follow-up work | But generative power alone → vaporware |

The taste filter balances all five. Maximizing any single dimension produces bad ideas.

---

## PART 2: 7-Dimension Taste Evaluation

### Dimension 1: Fundamental vs Surface
*(From RLCF / Scientific Taste, arXiv:2603.14473)*

> Does this idea attack a **fundamental bottleneck** or a **surface-level limitation**?

- **Surface:** "Add uncertainty handling to this pipeline" → incremental, forgettable
- **Fundamental:** "The entire static-training paradigm is wrong; we need online adaptation" → paradigm shift

**Ask:** If you removed this idea from the world, would the field be **structurally stuck**, or would someone else easily patch the gap?

**Scoring:**
- ★★★ Addresses a root cause that blocks an entire class of solutions
- ★★☆ Addresses a real limitation but at a component level
- ★☆☆ Improves an existing approach without changing the paradigm
- Kill signal: Could be solved by better engineering without new research insight

### Dimension 2: One-Sentence Elegance
*(From RLCF — high-impact papers have clean core insights)*

> Can you explain the core insight in ONE sentence that makes a researcher say "oh, that's clever"?

- **Bad:** "We combine sketch input with diffusion models for topology optimization"
- **Good:** "What if the UI controls for an editing task didn't exist until you needed them, then dissolved after?"

**Scoring:**
- ★★★ Reveals an unexpected insight that reframes the problem
- ★★☆ Understandable but doesn't surprise
- ★☆☆ Just describes what the system does
- Kill signal: Can't write the sentence at all → no core insight

### Dimension 3: Generative Power
*(From RLCF — citation breadth predicts structural impact)*

> Would this idea **spawn follow-up papers** from other researchers?

- **Low:** A system for one domain, one task, one user group
- **High:** A new design pattern, representation, or paradigm others apply to THEIR domains

**Scoring:**
- ★★★ Introduces a new abstraction/representation others will build on
- ★★☆ Applicable to 2-3 adjacent domains
- ★☆☆ Works for one specific use case
- Kill signal: Nobody would cite this to BUILD on it

### Dimension 4: Literature-Grounded Novelty Audit
*(From SciMON, ACL 2024 + Si et al., ICLR 2025)*

> Is this idea ACTUALLY novel, or does it already exist under a different name?

This is NOT a subjective judgment. This is a systematic check:

1. **Retrieve:** Search for the 5 closest existing papers using the idea's core claim
2. **Compare:** For each retrieved paper, explicitly state: "Paper X does Y. Our idea does Z. The essential difference is W."
3. **Verify:** If you cannot articulate a clear essential difference for ANY of the 5 papers, the idea is not novel — it's a rediscovery
4. **Iterate:** If novelty is borderline, use SciMON's retrieve-compare-update loop: modify the idea to explicitly differentiate from the closest match, then re-retrieve

**Scoring:**
- ★★★ No close match in literature; clear blue ocean
- ★★☆ Related work exists but the essential difference is articulable and significant
- ★☆☆ Very close match found; difference is marginal or cosmetic
- Kill signal: The idea already exists and you didn't know about it

**Warning:** LLMs are terrible at this test when relying on parametric knowledge alone. Always use retrieval (Semantic Scholar, Google Scholar, arXiv search) to ground the novelty check.

### Dimension 5: Feasibility-Impact Balance
*(From SciPIP, 2024 + Si et al., ICLR 2025)*

> Is this idea both achievable AND impactful? Not one or the other — BOTH.

Si et al. found that LLM ideas are rated more novel but less feasible than human expert ideas. SciPIP addresses this with dual-path generation (see Part 3).

**Evaluate on two axes:**

| | Low Feasibility | High Feasibility |
|---|---|---|
| **High Impact** | Moonshot — exciting but risky | Sweet spot — pursue this |
| **Low Impact** | Worst case — hard AND boring | Engineering — not research |

**Scoring:**
- ★★★ High impact AND clearly feasible within 6-12 months
- ★★☆ High impact but feasibility uncertain, OR feasible but moderate impact
- ★☆☆ Either clearly infeasible or clearly low-impact
- Kill signal: Falls in "Low Feasibility + Low Impact" quadrant

### Dimension 6: Trajectory Alignment
*(From Chain of Ideas, EMNLP 2025)*

> Does this idea align with where the field is heading, or does it solve yesterday's problem?

Chain of Ideas organizes literature into progressive chains that capture a field's trajectory. An idea with taste doesn't just solve a current problem — it anticipates the field's next move.

**Check:**
1. What are the 3 most important trends in this field over the last 2 years?
2. Does this idea ride one of these trends, or does it address something the field has moved past?
3. Would this idea have been equally relevant 3 years ago? If yes, why hasn't someone done it? (Either they have and you missed it, or there's a good reason it's hard/uninteresting)
4. Will this idea still be relevant in 3 years? Or will the field's trajectory make it obsolete?

**Scoring:**
- ★★★ Anticipates the field's next move; opens a new trajectory
- ★★☆ Aligns with current trends; timely and relevant
- ★☆☆ Solves a problem the field has moved past, or is orthogonal to current momentum
- Kill signal: The "why now" question has no good answer

### Dimension 7: Pairwise Comparison with Position-Swap Debiasing
*(From SciJudgeBench, 2026 — 700K paper pairs, position-swap consistency)*

> Compare your idea against the closest best paper — TWICE, swapping order.

This is the most diagnostic test. SciJudgeBench showed that position-swap consistency (evaluating A vs B, then B vs A) eliminates positional bias and produces more reliable judgments.

**Procedure:**
1. Pick the 3 closest high-impact papers in the target venue
2. For each, compare in BOTH directions:
   - "Is my idea more fundamental / broadly applicable / paradigm-shifting than Paper X?"
   - "Is Paper X more fundamental / broadly applicable / paradigm-shifting than my idea?"
3. If the answers are inconsistent (you favor your idea in both orderings), you have positional bias — re-evaluate more carefully
4. The comparison must be on STRUCTURAL merit, not surface differences

**Scoring:**
- ★★★ Consistently comparable or exceeds best papers in both orderings
- ★★☆ Competitive but doesn't clearly surpass
- ★☆☆ Feels like "a variant of X" in both orderings
- Kill signal: Inconsistent answers suggest self-deception about the idea's quality

### Taste Verdict

After running all 7 dimensions, classify the idea:

| Verdict | Criteria | Action |
|---------|----------|--------|
| **KILL** | Any dimension scores ★☆☆ or triggers a kill signal | Stop. Redesign from the problem level. |
| **REDESIGN** | Average ★★☆ but no ★★★ on any dimension | The core is there but needs sharpening. Identify the weakest dimension. |
| **PROCEED** | At least three ★★★ and no ★☆☆ | Worth investing serious time. Move to venue check and stress test. |
| **BEST PAPER CANDIDATE** | All ★★★ | Rare. Protect the core insight and don't dilute it. |

---

## PART 3: Idea Generation Pipeline

### Overview: Dual-Path Generation
*(From SciPIP, 2024)*

Generate ideas from TWO paths simultaneously, then select the best:

- **Path A: Problem-First** — Start from a real breakdown, find the minimum viable contribution
- **Path B: Insight-First** — Start from a surprising finding or connection, find the problem it solves

Most research idea tools only use Path A. But some of the best papers start from a surprising insight (e.g., "attention is all you need" didn't start from a user complaint about RNNs). SciPIP showed that balancing both paths produces higher-quality ideas.

### Path A: Problem-First (6 Phases)

#### Phase 1: Problem Discovery
1. **Identify stakeholder** — Who is BLOCKED by what? (Not "who could benefit from" — who is BLOCKED?)
2. **Study current practice** — What do they do now? What tools? Where does it break?
3. **Find the breakdown** — Not "could be better" but "literally cannot do X"
4. **Verify with evidence** — Papers, surveys, industry reports, domain expert interviews

#### Phase 2: Root Cause Analysis
5. **Technical barrier** — What specific capability was missing? (Sensing? Modeling? Representation? Interaction paradigm? Theory?)
6. **Disciplinary blind spot** — Which communities work on this? What does each miss?
7. **"Why now" enablers** — What changed in the last 1-2 years? (New models, hardware, datasets, frameworks?)
8. **The structural gap** — What's the mismatch between how humans think about X and how tools/methods represent X?

#### Phase 3: Solution Design
9. **Adjacent field analogy** — Has another field solved a structurally similar problem?
10. **Minimum viable contribution** — What's the smallest novel contribution that solves the breakdown?
11. **Core abstraction** — What new representation, framework, or paradigm bridges the gap?
12. **Result story** — Can you describe the one figure/demo/result that captures the contribution?

#### Phase 4: Literature-Grounded Novelty Audit
13. Run the novelty audit (Dimension 4). Retrieve 5 closest papers. Explicitly differentiate.
14. If too close to existing work, use the **retrieve-compare-update loop**: modify idea → re-retrieve → re-compare until the essential difference is clear and significant.

#### Phase 5: Scientific Taste Filter
15. Run all 7 dimensions (Part 2). If verdict is KILL or REDESIGN, iterate.

#### Phase 6: Stress Test
16. **Related work attack** — For each of the 5 closest papers, articulate the essential difference in one sentence.
17. **Reviewer's kill shot** — What's the strongest argument against this paper? Can you survive it?
18. **Feasibility check** — Can you produce a convincing result within the timeline?
19. **Trajectory check** — Will this idea still matter in 3 years?

### Path B: Insight-First (4 Phases)

#### Phase 1: Insight Discovery
*(From Deep Ideation, 2024 — scientific concept network + explore-expand-evolve)*

1. **Concept network** — Map the key concepts in your domain and their relationships
2. **Explore** — Look for unexpected connections between distant concepts
3. **Expand** — For each surprising connection, ask: "What would be true if this connection were exploitable?"
4. **Evolve** — Combine and refine the most promising connections

#### Phase 2: Problem Grounding
5. **Find the problem this insight solves** — A surprising insight without a problem is a curiosity, not research
6. **Verify the problem is real** — Evidence that people are actually blocked
7. **Check it's not already solved** — Run the novelty audit

#### Phase 3: Scientific Taste Filter
8. Run all 7 dimensions. Insight-first ideas often score high on Elegance but low on Feasibility or Groundedness — watch for this pattern.

#### Phase 4: Stress Test
9. Same as Path A, Phase 6.

### Selecting Between Paths

After generating ideas from both paths, compare them using the `/scientific-taste compare` command. The best ideas often combine: a fundamental problem (Path A) with an elegant insight (Path B).

---

## PART 4: Multi-Agent Review Protocol
*(From ResearchAgent, NAACL 2025 — multiple ReviewingAgents with human-aligned criteria)*

When evaluating an idea, simulate THREE reviewer perspectives:

### Reviewer 1: The Domain Expert
- "What does the literature actually say about this problem?"
- "Are the closest related papers properly differentiated?"
- "Is the claimed contribution genuinely new to this subfield?"

### Reviewer 2: The Methodology Critic
- "Is the proposed evaluation appropriate for the claimed contribution?"
- "Are there confounds or alternative explanations?"
- "Would the results be convincing to a skeptic?"

### Reviewer 3: The Visionary
- "Is this intellectually exciting?"
- "Would I discuss this at dinner?"
- "Does this change how I think about the field?"

**The idea must survive all three.** Domain Expert catches novelty failures. Methodology Critic catches feasibility failures. Visionary catches taste failures.

An idea that survives Reviewers 1 and 2 but fails Reviewer 3 is "publishable but forgettable" — the most dangerous outcome because it wastes time on work that won't matter.

---

## PART 5: Common Failure Modes

Reference `references/failure_modes.md` for detailed descriptions. Summary:

| # | Failure Mode | One-Line Test |
|---|-------------|---------------|
| 1 | Technology-First Combination | Did you start from a technology or from a problem? |
| 2 | "Better X" Instead of "New X" | Remove "better/faster/easier" — does the pitch still work? |
| 3 | Scope Creep | Can you nail ONE thing deeply? |
| 4 | Missing Empirical Grounding | Where did your design decisions come from? |
| 5 | Evaluating the Method, Not the Contribution | Are you measuring the right thing? |
| 6 | No Result Story | Can you describe the one compelling figure/demo? |
| 7 | Ignoring Related Work | Do you know the 5 closest papers intimately? |
| 8 | Surface-Level Problem | Would a senior researcher find this problem interesting? |
| 9 | No Generative Power | Will anyone build on this? |
| 10 | Variant, Not Vision | Is this "X but for Y" or a genuinely new direction? |
| 11 | Novelty Illusion | Does it ACTUALLY not exist, or did you just not search hard enough? |
| 12 | Trajectory Misalignment | Is this solving yesterday's problem? |

---

## PART 6: Output Format

### For `/scientific-taste evaluate`

```
## Scientific Taste Evaluation: [Idea Title]

### One-Sentence Pitch
[The core insight in one sentence]

### 7-Dimension Evaluation

| Dimension | Score | Rationale |
|-----------|-------|-----------|
| Fundamental vs Surface | ★★★/★★☆/★☆☆ | ... |
| One-Sentence Elegance | ★★★/★★☆/★☆☆ | ... |
| Generative Power | ★★★/★★☆/★☆☆ | ... |
| Literature-Grounded Novelty | ★★★/★★☆/★☆☆ | ... |
| Feasibility-Impact Balance | ★★★/★★☆/★☆☆ | ... |
| Trajectory Alignment | ★★★/★★☆/★☆☆ | ... |
| Pairwise Comparison | ★★★/★★☆/★☆☆ | ... |

### Closest Papers (Novelty Audit)
1. [Paper] — Essential difference: ...
2. [Paper] — Essential difference: ...
3. [Paper] — Essential difference: ...

### Multi-Agent Review
- Domain Expert: ...
- Methodology Critic: ...
- Visionary: ...

### Verdict: [KILL / REDESIGN / PROCEED / BEST PAPER CANDIDATE]

### Key Strengths
- ...

### Fatal Weaknesses (if any)
- ...

### Redesign Suggestions (if REDESIGN)
- ...
```

### For `/scientific-taste generate`

```
## Idea Proposal: [Title]

### Generation Path: [Problem-First / Insight-First / Combined]

### Problem
[Who is blocked? What's the breakdown?]

### Root Cause / Core Insight
[The structural gap or surprising connection]

### One-Sentence Pitch
[The elegant formulation]

### Solution
[Minimum viable contribution + core abstraction]

### Result Story
[The compelling figure/demo/experiment]

### Novelty Audit
[5 closest papers + essential differences]

### 7-Dimension Scores
[Full evaluation table]

### Trajectory Alignment
[How this fits the field's direction]

### Venue Fit
[If --venue specified]

### Stress Test
[Related work attack, kill shot, feasibility, trajectory]
```

### For `/scientific-taste compare`

```
## Head-to-Head Comparison (Position-Swap Debiased)

### Ordering 1: A vs B
| Dimension | Idea A | Idea B |
|-----------|--------|--------|
| Fundamental vs Surface | ... | ... |
| Elegance | ... | ... |
| Generative Power | ... | ... |
| Novelty | ... | ... |
| Feasibility-Impact | ... | ... |
| Trajectory | ... | ... |
| Pairwise (vs best papers) | ... | ... |

### Ordering 2: B vs A (consistency check)
[Same table, evaluated with B presented first]

### Consistency Analysis
[Were the judgments consistent across orderings? Flag any reversals.]

### Verdict
[Which idea to pursue and why, accounting for any positional bias detected]
```

### For `/scientific-taste audit`

```
## Literature-Grounded Novelty Audit: [Idea]

### Core Claim
[What this idea claims to contribute]

### Retrieved Closest Papers
1. [Paper, Year, Venue] — Similarity: [high/medium/low]
   What they did: ...
   Essential difference: ...

2-5. [Same format]

### Novelty Verdict
[NOVEL / BORDERLINE / ALREADY EXISTS]

### If Borderline — Differentiation Suggestions
[How to modify the idea to create clear separation]
```

---

## PART 7: Venue Module System

This skill supports pluggable venue modules. When `--venue [name]` is specified:

1. Load `venue-modules/[name].md`
2. After the taste filter passes, check venue-specific criteria
3. Include venue-specific evaluation in the output

Available modules: `uist`, `chi`, `neurips`, `icml`
Custom: Copy `venue-modules/_template.md` and fill in your venue's criteria.

If no venue is specified, the skill runs only the universal 7-dimension evaluation — which is sufficient for evaluating any research idea in any field.

---

## PART 8: Methodology Sources

This skill integrates techniques from the following papers:

| Paper | Year | Key Technique Used |
|-------|------|--------------------|
| AI Can Learn Scientific Taste (arXiv:2603.14473) | 2026 | RLCF pairwise training, 5 core taste dimensions |
| HindSight | 2026 | Novelty ≠ Impact finding, time-split validation |
| SciJudgeBench | 2026 | Position-swap consistency debiasing, reasoning traces |
| Can LLMs Generate Novel Research Ideas? (Si et al.) | 2025 | 95% duplication finding, feasibility gap |
| ResearchAgent (Baek et al.) | 2025 | Multi-agent review with human-aligned criteria |
| AI Scientist v2 (Sakana AI) | 2025 | Agentic tree search for research exploration |
| Chain of Ideas | 2025 | Progressive literature chains, trajectory prediction |
| Deep Ideation | 2024 | Scientific concept network, explore-expand-evolve |
| SciMON (Wang et al.) | 2024 | Retrieve-compare-update novelty loop |
| SciPIP | 2024 | Dual-path feasibility/novelty generation |
| IdeaSynth (Pu et al.) | 2024 | Faceted decomposition (problem/method/eval/contribution) |
| Nova | 2024 | Iterative planning for idea diversity (3.4x improvement) |
| ResearchBench | 2025 | Inspiration retrieval → hypothesis composition → ranking |
| MLR-Copilot | 2024 | RL-tuned quality-aware generation |
| IdeaBench | 2025 | GPT-4o ranking with Insight Score |
| AI-Researcher (Tang et al.) | 2025 | Bidirectional math-code mapping for implementability |
