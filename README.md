# Scientific Taste Agent

An AI agent skill that evaluates research ideas like a senior reviewer — not by checklist scoring, but by scientific taste.

> "The difference between a forgettable paper and a best paper is not following more rules — it's having genuine intellectual taste."

## What It Does

- **Evaluate ideas** with 7-dimension taste evaluation (not just novelty — novelty alone is anti-correlated with impact)
- **Generate ideas** via dual-path pipeline (Problem-First + Insight-First)
- **Kill weak ideas early** before you waste months on them
- **Audit novelty** against real literature (95% of LLM "novel" ideas already exist)
- **Compare ideas** head-to-head with position-swap debiasing
- **Venue-specific checks** for UIST, CHI, NeurIPS, ICML (pluggable)

## Based On

Integrates methodologies from 16+ papers on automated research ideation:

| Paper | Key Contribution |
|-------|-----------------|
| [AI Can Learn Scientific Taste](https://arxiv.org/abs/2603.14473) | RLCF pairwise training — fundamental > surface, paradigm-shifting > incremental |
| [HindSight](https://arxiv.org/abs/2603.15164) (2026) | **Novelty is anti-correlated with real impact** — the most important finding |
| [Can LLMs Generate Novel Research Ideas?](https://arxiv.org/abs/2409.04109) (Si et al., ICLR 2025) | 95% of LLM ideas are duplicates; LLM self-eval is barely above chance |
| [SciJudgeBench](https://arxiv.org/abs/2603.14473) (2026) | Position-swap consistency debiasing for pairwise comparison |
| [ResearchAgent](https://arxiv.org/abs/2404.07738) (NAACL 2025) | Multi-agent review with human-aligned criteria |
| [SciMON](https://arxiv.org/abs/2305.14259) (ACL 2024) | Retrieve-compare-update loop for novelty verification |
| [SciPIP](https://arxiv.org/abs/2410.23166) (2024) | Dual-path generation balancing feasibility and novelty |
| [Chain of Ideas](https://arxiv.org/abs/2410.13185) (EMNLP 2025) | Trajectory alignment — does the idea fit where the field is heading? |
| [Deep Ideation](https://arxiv.org/abs/2511.02238) (2024) | Concept networks + explore-expand-evolve for insight discovery |
| [IdeaSynth](https://arxiv.org/abs/2410.04025) (2024) | Faceted evaluation (problem/method/eval/contribution) |
| [Nova](https://arxiv.org/abs/2410.14255) (2024) | 3.4x more unique ideas through iterative planning |
| [AI Scientist v2](https://arxiv.org/abs/2504.08066) (Sakana AI, 2025) | Agentic tree search for automated research |
| + 5 more | See SKILL.md Part 8 for complete list |

## Quick Start

### Install for Claude Code

```bash
# Clone the repo
git clone https://github.com/Carolzhangzz/scientific-taste-skills.git

# Copy skills to your Claude Code skills directory
cp -r scientific-taste-skills/skills/* ~/.claude/skills/
```

### Usage

```
/scientific-taste evaluate "An AI system that uses intermediate representations
to give users control over generative model outputs"

/scientific-taste generate "game design" "designers can't preview
how players will emotionally respond to their designs"

/scientific-taste compare "Idea A: bandit-based loss weighting"
vs "Idea B: gradient-magnitude normalization"

/scientific-taste audit "using LLMs for automated code review"
```

Add `--venue` for venue-specific checks:

```
/scientific-taste evaluate "..." --venue uist
/scientific-taste evaluate "..." --venue neurips
```

## The 7-Dimension Evaluation

| Dimension | Source | What It Catches |
|-----------|--------|-----------------|
| **Fundamental vs Surface** | RLCF | Is this a root cause or a symptom? |
| **One-Sentence Elegance** | RLCF | Is there a clean core insight? |
| **Generative Power** | RLCF + Citation analysis | Will others build on this? |
| **Literature-Grounded Novelty** | SciMON + Si et al. | Does this actually not exist yet? |
| **Feasibility-Impact Balance** | SciPIP + Si et al. | Is it both doable AND worthwhile? |
| **Trajectory Alignment** | Chain of Ideas | Does this fit where the field is going? |
| **Pairwise Comparison** | SciJudgeBench | How does it stack up against the best? |

### Why 7, Not 5?

v1.0 had 5 tests based on RLCF alone. v2.0 adds:
- **Literature-Grounded Novelty** — because 95% of LLM "novel" ideas already exist (Si et al.)
- **Feasibility-Impact Balance** — because LLM ideas are rated more novel but less feasible (Si et al.)
- **Trajectory Alignment** — because solving yesterday's problem wastes time even if the solution is elegant (Chain of Ideas)

## Key Insight: Novelty ≠ Impact

The single most important finding driving this tool:

> **HindSight (2026) showed that LLM-judged novelty is NEGATIVELY CORRELATED with real-world research impact.**

Most tools maximize novelty. This tool balances novelty with fundamentality, feasibility, groundedness, and trajectory alignment. Maximizing any single dimension produces bad ideas.

## Verdict System

| Verdict | Criteria | Action |
|---------|----------|--------|
| **KILL** | Any dimension ★☆☆ or kill signal | Stop. Find a better problem. |
| **REDESIGN** | Average ★★☆, no ★★★ | Core is there, needs sharpening. |
| **PROCEED** | At least three ★★★, no ★☆☆ | Worth serious investment. |
| **BEST PAPER CANDIDATE** | All ★★★ | Rare. Protect the core insight. |

## Dual-Path Idea Generation

| Path | Start From | Strength | Risk |
|------|-----------|----------|------|
| **Problem-First** | Who is BLOCKED? | Grounded, feasible | Can be incremental |
| **Insight-First** | Surprising connection | Elegant, exciting | Can be infeasible |
| **Combined** | Best of both | Grounded AND elegant | Requires more effort |

## Multi-Agent Review

Every evaluation simulates 3 reviewer perspectives:
- **Domain Expert** — Is this actually novel in the literature?
- **Methodology Critic** — Is the evaluation appropriate?
- **Visionary** — Is this intellectually exciting?

An idea must survive all three.

## Venue Modules

| Module | Coverage |
|--------|----------|
| `uist.md` | 7 criteria, 15 design patterns, paper structure |
| `chi.md` | Contribution types, study designs, mixed methods |
| `neurips.md` | Theory/empirical standards, reproducibility |
| `icml.md` | Theoretical grounding, algorithmic criteria |
| `_template.md` | Template for any custom venue |

## Examples

- [`example_uist_evaluation.md`](examples/example_uist_evaluation.md) — A creative but shallow idea gets killed
- [`example_ml_evaluation.md`](examples/example_ml_evaluation.md) — An ML idea gets redesigned from "solid" to "best paper candidate"

## Philosophy

Most idea evaluation tools use checklists or maximize novelty. Both approaches fail:
- **Checklists** produce papers that check all boxes but excite no one
- **Novelty maximization** produces ideas that sound new but have zero impact (HindSight, 2026)

Scientific Taste works differently. It asks: **Would this idea create lasting structural impact on the field?** This requires balancing multiple dimensions that are often in tension — novel but grounded, exciting but feasible, timely but not trendy.

The most valuable output is often the **kill decision** — telling you NOT to pursue an idea before you invest months.

## Contributing

Contributions welcome:
- New venue modules (use `_template.md`)
- Calibration examples from different fields
- Improvements to failure modes
- Additional methodology integrations

## License

MIT — see [LICENSE.md](LICENSE.md)

## Citation

```bibtex
@software{scientific_taste_skills,
  title={Scientific Taste Agent},
  author={Zhang, Qinshi},
  year={2026},
  url={https://github.com/Carolzhangzz/scientific-taste-skills}
}
```
