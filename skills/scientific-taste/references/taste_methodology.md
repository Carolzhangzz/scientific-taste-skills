# Scientific Taste Methodology — Deep Reference

Detailed reference for the theoretical foundations behind the 7-dimension evaluation, integrating findings from 16+ papers on automated research ideation and evaluation.

---

## Foundation 1: RLCF — Reinforcement Learning from Citation Feedback
*(Source: "AI Can Learn Scientific Taste", arXiv:2603.14473, 2026)*

### What It Is
Trains language models to evaluate scientific ideas using citation-based pairwise comparison. Uses SciJudgeBench (700K field- and time-matched paper pairs from 2.1M arXiv papers).

### Core Findings
Models trained on citation signals learn preferences that align with experienced researcher "taste":
1. **Fundamental > Surface** — Root causes over symptoms
2. **Paradigm-shifting > Incremental** — New directions over improvements
3. **Broadly applicable > Narrow** — Cross-domain over single-domain

### Why Pairwise, Not Absolute Scoring
- Higher inter-rater agreement
- More robust training signals
- Better generalization across fields
- Position-swap consistency eliminates positional bias

### Technical Detail: GRPO Training
Uses Group Relative Policy Optimization with binary correctness rewards. Models generate reasoning traces BEFORE making judgments, which improves accuracy significantly over direct classification.

---

## Foundation 2: The Novelty Trap
*(Source: HindSight, 2026)*

### The Shocking Finding
LLM-judged "novelty" is **negatively correlated** with real-world research impact. RAG-augmented ideas score 2.5x higher on real impact, but LLM-as-Judge sees no difference.

### Why This Happens
- LLMs mistake **unfamiliarity** for **novelty** — they rate obscure ideas as more novel
- Truly impactful ideas are often **surprisingly connected** to existing work, not isolated
- The most-cited papers often feel "obvious in retrospect" — they combine known elements in a way that creates new insight

### Implication for Taste
Taste is NOT novelty maximization. A "novel" idea that nobody builds on is worse than a "connected" idea that becomes foundational. The evaluation must balance novelty with groundedness, feasibility, and trajectory alignment.

---

## Foundation 3: The 95% Duplication Problem
*(Source: Si, Yang, Hashimoto, ICLR 2025)*

### The Study
100+ NLP researchers evaluated LLM-generated research ideas in a controlled study. Key findings:
- Only **5% of 4,000 LLM-generated ideas** were unique — 95% duplicated each other
- LLM ideas were rated **more novel** but **less feasible** than human expert ideas
- LLM self-evaluation accuracy was **53.3%** — barely above chance

### Implication for Taste
1. **Literature-grounded novelty checking is essential** — LLMs cannot self-assess novelty
2. **Feasibility must be evaluated alongside novelty** — the ideas LLMs generate well (novel-sounding but infeasible) are exactly the wrong type
3. **Diversity requires explicit intervention** — without it, LLMs converge to the same ideas

---

## Foundation 4: Retrieve-Compare-Update Loop
*(Source: SciMON, Wang et al., ACL 2024)*

### The Method
Iteratively boost novelty through:
1. **Retrieve** — Find closest existing papers to the current idea
2. **Compare** — Identify overlap and differences
3. **Update** — Modify the idea to increase differentiation from retrieved papers
4. Repeat until the idea passes a similarity threshold

### Results
55.6% of ideas gain meaningful novelty through this loop. BUT the study also found that novelty boosting alone produces ideas that are more novel but not more impactful — confirming the HindSight finding.

### Implication for Taste
The retrieve-compare-update loop is valuable for novelty VERIFICATION (Dimension 4), but should not be used to blindly maximize novelty. The loop should stop when the idea is clearly differentiated, not when it's maximally different.

---

## Foundation 5: Multi-Agent Review
*(Source: ResearchAgent, Baek et al., NAACL 2025)*

### The Architecture
Multiple ReviewingAgents, each with criteria learned from human reviewer judgments. The agents provide:
- Academic knowledge graph augmentation
- Cross-disciplinary perspective
- Structured feedback on specific criteria

### Why Multiple Agents
Single-agent evaluation has systematic blind spots. Multiple agents with different "expertise" catch different failure modes:
- Domain Expert catches novelty failures
- Methodology Critic catches evaluation design failures
- Visionary catches taste failures

---

## Foundation 6: Dual-Path Generation
*(Source: SciPIP, 2024)*

### The Problem
Most idea generation pipelines use a single path: problem → solution. But many breakthrough papers start from an insight or surprising connection, THEN find the problem it solves.

### The Solution
Generate ideas from two paths simultaneously:
- **Feasibility-First Path:** Start from a real problem, design the minimum viable solution
- **Novelty-First Path:** Start from a surprising connection, find the problem it addresses
Then compare and combine the best elements of both.

### Why It Works
Feasibility-first ideas tend to be incremental but executable. Novelty-first ideas tend to be exciting but vague. The best research ideas combine both: a real problem + a surprising insight about how to solve it.

---

## Foundation 7: Trajectory Alignment
*(Source: Chain of Ideas, EMNLP 2025)*

### The Method
Organizes literature into progressive chains that capture a field's trajectory. Rather than treating papers as independent data points, it models how ideas EVOLVE over time:
- What was the prevailing approach 5 years ago?
- What changed?
- Where is the field heading?
- What's the natural "next step" that nobody has taken yet?

### Why It Matters
An idea can be novel, fundamental, and elegant — but if it solves a problem the field has already moved past, nobody will care. Trajectory alignment ensures the idea is timely.

### Caution
Trajectory alignment should NOT mean "follow the trend." The best papers often REDIRECT a field's trajectory. But they do so by understanding the trajectory deeply, not by ignoring it.

---

## Foundation 8: Concept Networks for Insight Discovery
*(Source: Deep Ideation, 2024)*

### The Method
Build a network of scientific concepts and their relationships. Then use explore-expand-evolve:
1. **Explore** — Traverse the network looking for unexpected connections
2. **Expand** — For each connection, ask "what would be true if this were exploitable?"
3. **Evolve** — Combine and refine through a critic engine trained on real reviewer feedback

### Results
10.67% quality improvement over baselines, with ideas that are both more novel and more grounded.

### Implication for Taste
Used in the Insight-First generation path (Path B). The concept network provides structured serendipity — finding connections that are surprising but principled, not random combinations.

---

## How the 7 Dimensions Map to Research Foundations

| Dimension | Primary Source | Secondary Sources |
|-----------|---------------|-------------------|
| Fundamental vs Surface | RLCF (arXiv:2603.14473) | — |
| One-Sentence Elegance | RLCF | IdeaSynth (faceted decomposition) |
| Generative Power | RLCF (citation breadth) | ResearchBench (inspiration retrieval) |
| Literature-Grounded Novelty | SciMON (retrieve-compare-update) | Si et al. (95% duplication), HindSight (novelty ≠ impact) |
| Feasibility-Impact Balance | SciPIP (dual-path) | Si et al. (feasibility gap) |
| Trajectory Alignment | Chain of Ideas | Nova (iterative planning) |
| Pairwise Comparison | SciJudgeBench (position-swap) | RLCF |

---

## The Citation Signal — What It Actually Measures

### What Citations Capture
- **Breadth of citing fields** → Generative power (cross-domain impact)
- **Citation velocity** → Addressed a real bottleneck (others immediately build on it)
- **Citation context** → "Building on" vs "related to" distinguishes structural contributions from incremental ones

### What Citations Miss
- Timing effects (earlier papers get more citations)
- Prestige bias (famous labs get more citations)
- Negative citations (citing to disagree)
- Application papers (impactful in practice but low-cited in academia)

SciJudgeBench controls for timing and field by using **field- and time-matched pairs**. But prestige bias and application impact remain limitations.

---

## The Kill Decision

The most valuable output of the taste filter is the **kill decision**. Researchers waste enormous time on ideas that are:
- Technically feasible
- Clearly publishable somewhere
- But fundamentally unexciting

The taste filter catches these. The HindSight finding makes this even more important: an idea that FEELS novel (and would be rated as novel by an LLM) may have zero real-world impact. The 7-dimension evaluation catches ideas that pass the novelty test but fail on fundamentality, generative power, trajectory alignment, or feasibility.

**Kill early, kill often, find a better problem.**
