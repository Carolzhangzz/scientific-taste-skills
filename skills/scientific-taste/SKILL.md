---
name: scientific-taste
description: >
  Evaluate and generate research ideas using Scientific Taste —
  distinguishing paradigm-shifting ideas from incremental variants.
  Works for any venue (UIST, CHI, NeurIPS, ICML, etc.).
  Based on "AI Can Learn Scientific Taste" (arXiv:2603.14473).
license: MIT
metadata:
  skill-author: Qinshi Zhang
  version: 1.0.0
---

# Scientific Taste Agent

Evaluate and generate research ideas using Scientific Taste — not checklist scoring, but the trained intuition that separates paradigm-shifting ideas from incremental variants.

## When to Use This Skill

- Evaluating whether a research idea is worth pursuing
- Generating ideas from real problems (not technology combinations)
- Comparing two ideas head-to-head
- Stress-testing a paper concept before committing months of work
- Checking venue fit (UIST, CHI, NeurIPS, ICML, or custom)

## Commands

- `/scientific-taste evaluate [idea description]` — Run 5 taste tests on an idea
- `/scientific-taste generate [domain] [problem]` — Generate ideas from a problem
- `/scientific-taste compare [idea A] vs [idea B]` — Pairwise comparison
- Add `--venue uist|chi|neurips|icml` to any command for venue-specific checks

## How It Works

When invoked, this agent will:
1. Understand the research context (domain, resources, constraints)
2. Apply the Scientific Taste Filter (5 tests)
3. Optionally load venue-specific criteria from `venue-modules/`
4. Produce a structured evaluation or idea proposal with kill/proceed recommendation

---

## PART 1: Scientific Taste — 5 Tests

The difference between a forgettable paper and a best paper is NOT following more rules — it's having genuine intellectual taste. These 5 tests are derived from the RLCF methodology in "AI Can Learn Scientific Taste" (arXiv:2603.14473), which found that models trained on citation-based pairwise comparison consistently prefer: fundamental over surface, paradigm-shifting over incremental, broadly applicable over narrow.

### Test 1: Fundamental vs Surface

> Does this idea attack a **fundamental bottleneck** or a **surface-level limitation**?

- **Surface:** "Add uncertainty handling to this pipeline" → incremental, forgettable
- **Fundamental:** "The entire static-training paradigm is wrong; we need online adaptation" → paradigm shift

**Ask:** If you removed this idea from the world, would the field be **structurally stuck**, or would someone else easily patch the gap?

**Scoring:**
- ★★★ Fundamental — Addresses a root cause that blocks an entire class of solutions
- ★★☆ Moderate — Addresses a real limitation but at a component level
- ★☆☆ Surface — Improves an existing approach without changing the paradigm
- Kill signal: If the problem could be solved by better engineering without new research insight

### Test 2: One-Sentence Elegance

> Can you explain the core insight in ONE sentence that makes a researcher say "oh, that's clever"?

- **Bad:** "We combine sketch input with diffusion models for topology optimization"
- **Good:** "What if the UI controls for an editing task didn't exist until you needed them, then dissolved after?"

If the one-sentence pitch requires jargon or multiple clauses, the insight isn't clean enough.

**Scoring:**
- ★★★ Elegant — The sentence reveals an unexpected insight that reframes the problem
- ★★☆ Clear — The sentence is understandable but doesn't surprise
- ★☆☆ Descriptive — The sentence just describes what the system does
- Kill signal: If you can't write the sentence at all, there may be no core insight

### Test 3: Generative Power

> Would this idea **spawn follow-up papers** from other researchers?

- **Low generative power:** A system that works for one domain, one task, one user group
- **High generative power:** A new design pattern, representation, or interaction paradigm that others will apply to THEIR domains

**Compare:** "A video editing tool" (low) vs "ephemeral task-specific UI as an interaction paradigm" (high — others will apply it to audio, code, 3D, etc.)

**Scoring:**
- ★★★ Paradigm — Introduces a new abstraction/representation others will build on
- ★★☆ Extensible — Clearly applicable to 2-3 adjacent domains
- ★☆☆ Narrow — Works for one specific use case
- Kill signal: If nobody would cite this for anything other than "related work"

### Test 4: Pairwise Comparison Against Known Best Papers

> Pick the closest best paper in your target venue. Is your idea **more fundamental**, **more broadly applicable**, or **more paradigm-shifting** than that paper?

This mirrors how Scientific Taste works: not absolute scoring, but relative comparison against known high-impact work.

- If your idea feels like "a variant of X" rather than "a new direction inspired by X," it lacks taste
- For each close comparator, ask: Does our idea address a MORE FUNDAMENTAL problem? Is our solution MORE BROADLY APPLICABLE? Would our paper generate MORE FOLLOW-UP WORK?

**Scoring:**
- ★★★ Comparable or exceeds — Stands alongside best papers in ambition and insight
- ★★☆ Same league — Competitive but doesn't clearly surpass
- ★☆☆ Variant — Feels like "X but for Y" relative to comparators
- Kill signal: If the answer is "no" to all three questions for any single comparator

### Test 5: Senior Reviewer Test

> Imagine a senior reviewer who has reviewed 200+ papers. Would they find this **intellectually exciting** — something they'd discuss at dinner — or just "fine, competent, publishable"?

- "Fine" ideas get borderline scores and die in discussion
- "Exciting" ideas get championed by at least one reviewer

What makes the difference: an unexpected insight, an elegant abstraction, or a demo/result that reframes how people think about a problem.

**Scoring:**
- ★★★ Champion — A reviewer would fight for this in the PC meeting
- ★★☆ Positive — Solid work that reviewers would accept but not champion
- ★☆☆ Borderline — "Competent but not exciting"
- Kill signal: If you can't identify what would make a reviewer excited

### Taste Verdict

After running all 5 tests, classify the idea:

| Verdict | Criteria | Action |
|---------|----------|--------|
| **KILL** | Any test scores ★☆☆ or triggers a kill signal | Stop. Redesign from the problem level. |
| **REDESIGN** | Average ★★☆ but no ★★★ on any test | The core is there but needs sharpening. Identify which test is weakest. |
| **PROCEED** | At least two ★★★ and no ★☆☆ | Worth investing serious time. Move to venue check and stress test. |
| **BEST PAPER CANDIDATE** | All ★★★ | Rare. Protect the core insight and don't dilute it. |

---

## PART 2: Idea Generation Pipeline

### Phase 1: Problem Discovery
1. **Identify stakeholder** — Who is BLOCKED by what? (Not "who could benefit from" — who is BLOCKED?)
2. **Study current practice** — What do they do now? What tools? Where does it break?
3. **Find the breakdown** — Not "could be better" but "literally cannot do X"
4. **Verify with evidence** — Papers, surveys, industry reports, domain expert interviews

### Phase 2: Root Cause Analysis
5. **Technical barrier** — What specific capability was missing? (Sensing? Modeling? Representation? Interaction paradigm? Theory?)
6. **Disciplinary blind spot** — Which communities work on this? What does each miss?
7. **"Why now" enablers** — What changed in the last 1-2 years? (New models, hardware, datasets, frameworks?)
8. **The structural gap** — What's the mismatch between how humans think about X and how tools/methods represent X?

### Phase 3: Solution Design
9. **Adjacent field analogy** — Has another field solved a structurally similar problem?
10. **Minimum viable contribution** — What's the smallest novel contribution that solves the breakdown?
11. **Core abstraction** — What new representation, framework, or paradigm bridges the gap?
12. **Result story** — Can you describe the one figure/demo/result that captures the contribution?

### Phase 4: Scientific Taste Filter
13. Run all 5 taste tests (Part 1). If verdict is KILL or REDESIGN, iterate on the problem or solution.

### Phase 5: Venue-Specific Check
14. Load the appropriate venue module from `venue-modules/`. Verify the idea meets venue-specific criteria.
    - If no venue module exists, use `_template.md` to think through venue fit.

### Phase 6: Stress Test
15. **Related work attack** — Find 3 closest papers. Articulate the essential difference for each.
16. **Reviewer's kill shot** — What's the strongest argument against this paper? Can you survive it?
17. **Feasibility check** — Can you produce a convincing result within the timeline?
18. **Pairwise taste check** — Compare against the 3 closest papers. For each: "Does our idea address a MORE FUNDAMENTAL problem? Is our solution MORE BROADLY APPLICABLE? Would our paper generate MORE FOLLOW-UP WORK?" If "no" to all three for any comparator, redesign.

---

## PART 3: Common Failure Modes

Reference `references/failure_modes.md` for detailed descriptions. Summary:

| # | Failure Mode | One-Line Test |
|---|-------------|---------------|
| 1 | Technology-First Combination | Did you start from a technology or from a problem? |
| 2 | "Better X" Instead of "New X" | Remove "better/faster/easier" — does the pitch still work? |
| 3 | Scope Creep | Can you nail ONE thing deeply? |
| 4 | Missing Empirical Grounding | Where did your design decisions come from? |
| 5 | Evaluating the Method, Not the Contribution | Are you measuring the right thing? |
| 6 | No Result Story | Can you describe the one compelling figure/demo? |
| 7 | Ignoring Related Work | Do you know the 3 closest papers intimately? |
| 8 | Surface-Level Problem | Would a senior researcher find this problem interesting? |
| 9 | No Generative Power | Will anyone build on this? |
| 10 | Variant, Not Vision | Is this "X but for Y" or a genuinely new direction? |

---

## PART 4: Output Format

### For `/scientific-taste evaluate`

```
## Scientific Taste Evaluation: [Idea Title]

### One-Sentence Pitch
[The core insight in one sentence]

### 5 Taste Tests

| Test | Score | Rationale |
|------|-------|-----------|
| Fundamental vs Surface | ★★★/★★☆/★☆☆ | ... |
| One-Sentence Elegance | ★★★/★★☆/★☆☆ | ... |
| Generative Power | ★★★/★★☆/★☆☆ | ... |
| Pairwise Comparison | ★★★/★★☆/★☆☆ | ... |
| Senior Reviewer Test | ★★★/★★☆/★☆☆ | ... |

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

### Problem
[Who is blocked? What's the breakdown?]

### Root Cause
[The structural gap]

### Core Insight
[One sentence]

### Solution
[Minimum viable contribution + core abstraction]

### Result Story
[The compelling figure/demo/experiment]

### Scientific Taste Scores
[5 tests with scores]

### Venue Fit
[If --venue specified]

### Stress Test
[Related work, kill shot, feasibility]
```

### For `/scientific-taste compare`

```
## Head-to-Head Comparison

| Dimension | Idea A | Idea B |
|-----------|--------|--------|
| Fundamental vs Surface | ... | ... |
| Elegance | ... | ... |
| Generative Power | ... | ... |
| Pairwise (vs best papers) | ... | ... |
| Senior Reviewer Excitement | ... | ... |

### Verdict
[Which idea to pursue and why]
```

---

## PART 5: Venue Module System

This skill supports pluggable venue modules. When `--venue [name]` is specified:

1. Load `venue-modules/[name].md`
2. After the taste filter passes, check venue-specific criteria
3. Include venue-specific evaluation in the output

Available modules: `uist`, `chi`, `neurips`, `icml`
Custom: Copy `venue-modules/_template.md` and fill in your venue's criteria.

If no venue is specified, the skill runs only the universal taste tests — which are sufficient for evaluating any research idea in any field.
