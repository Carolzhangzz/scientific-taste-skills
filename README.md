# Scientific Taste Agent

An AI agent skill that evaluates research ideas like a senior reviewer — not by checklist scoring, but by scientific taste.

> "The difference between a forgettable paper and a best paper is not following more rules — it's having genuine intellectual taste."

## What It Does

- **Evaluate ideas** with 5 taste tests (Fundamental vs Surface, Elegance, Generative Power, Pairwise Comparison, Senior Reviewer Test)
- **Generate ideas** from problems, not from technology combinations
- **Kill weak ideas early** before you waste months on them
- **Compare ideas** head-to-head using pairwise comparison
- **Venue-specific checks** for UIST, CHI, NeurIPS, ICML (pluggable)

## Based On

- [AI Can Learn Scientific Taste](https://arxiv.org/abs/2603.14473) — RLCF methodology showing that models trained on citation-based pairwise comparison learn to prefer: fundamental > surface, paradigm-shifting > incremental, broadly applicable > narrow
- 40+ UIST papers (2019-2025) for the HCI venue module
- Empirically derived design patterns and failure modes

## Quick Start

### Install for Claude Code

```bash
# Clone the repo
git clone https://github.com/qinshi-zhang/scientific-taste-agent.git

# Copy skills to your Claude Code skills directory
cp -r scientific-taste-agent/skills/* ~/.claude/skills/
```

### Usage

Once installed, use these commands in Claude Code:

```
/scientific-taste evaluate "An AI system that uses intermediate representations
to give users control over generative model outputs"

/scientific-taste generate "game design" "designers can't preview
how players will emotionally respond to their designs"

/scientific-taste compare "Idea A: bandit-based loss weighting"
vs "Idea B: gradient-magnitude normalization"
```

Add `--venue` for venue-specific checks:

```
/scientific-taste evaluate "..." --venue uist
/scientific-taste evaluate "..." --venue neurips
/scientific-taste evaluate "..." --venue chi
/scientific-taste evaluate "..." --venue icml
```

## The 5 Taste Tests

| Test | What It Measures | Kill Signal |
|------|-----------------|-------------|
| **Fundamental vs Surface** | Problem depth — root cause or symptom? | Could be solved by better engineering, no new insight needed |
| **One-Sentence Elegance** | Conceptual clarity — clean insight or just descriptive? | Can't write the sentence → no core insight |
| **Generative Power** | Abstraction quality — will others build on this? | Nobody would cite it to build on |
| **Pairwise Comparison** | Relative positioning — vs known best papers | Feels like "a variant of X" for every comparator |
| **Senior Reviewer Test** | Holistic taste — exciting or just "fine"? | Can't identify what would make a reviewer excited |

## Verdict System

| Verdict | Criteria | Action |
|---------|----------|--------|
| **KILL** | Any test ★☆☆ or triggers kill signal | Stop. Find a better problem. |
| **REDESIGN** | Average ★★☆ but no ★★★ | Core is there, needs sharpening. |
| **PROCEED** | At least two ★★★, no ★☆☆ | Worth serious investment. |
| **BEST PAPER CANDIDATE** | All ★★★ | Rare. Protect the core insight. |

## Venue Modules

| Module | File | Coverage |
|--------|------|----------|
| UIST | `venue-modules/uist.md` | 7 criteria, 15 design patterns, paper structure |
| CHI | `venue-modules/chi.md` | Contribution types, study designs, evaluation |
| NeurIPS | `venue-modules/neurips.md` | Theory/empirical standards, reproducibility |
| ICML | `venue-modules/icml.md` | Theoretical grounding, algorithmic criteria |
| Custom | `venue-modules/_template.md` | Template for any venue |

## Examples

See the `examples/` directory:
- [`example_uist_evaluation.md`](examples/example_uist_evaluation.md) — A creative but shallow idea gets killed (OsmoCut)
- [`example_ml_evaluation.md`](examples/example_ml_evaluation.md) — An ML idea gets redesigned from "solid" to "best paper candidate"

## Project Structure

```
scientific-taste-agent/
├── README.md
├── LICENSE.md
├── .gitignore
├── skills/
│   ├── scientific-taste/           # Core skill
│   │   ├── SKILL.md                # Main: 5 taste tests + pipeline
│   │   └── references/
│   │       ├── taste_methodology.md   # RLCF methodology details
│   │       └── failure_modes.md       # 10 common failure modes
│   └── venue-modules/              # Pluggable venue criteria
│       ├── uist.md
│       ├── chi.md
│       ├── neurips.md
│       ├── icml.md
│       └── _template.md
└── examples/
    ├── example_uist_evaluation.md
    └── example_ml_evaluation.md
```

## Philosophy

Most idea evaluation tools use checklists: "Does your paper have X? Y? Z?" This produces papers that check all boxes but excite no one.

Scientific Taste works differently. It asks: **Would this idea make the field structurally better?** The 5 tests operationalize the trained intuition that senior researchers develop over decades of reading and reviewing papers.

The most valuable output is often the **kill decision** — telling you NOT to pursue an idea before you invest months. Researchers routinely waste 6-12 months on ideas that are technically feasible and clearly publishable but fundamentally unexciting. The taste filter catches these.

## Contributing

Contributions welcome, especially:
- New venue modules (submit as PR with the `_template.md` structure)
- Calibration examples from different fields
- Improvements to the failure modes catalog

## License

MIT — see [LICENSE.md](LICENSE.md)

## Citation

If you use this in your research workflow:

```bibtex
@software{scientific_taste_agent,
  title={Scientific Taste Agent},
  author={Zhang, Qinshi},
  year={2026},
  url={https://github.com/qinshi-zhang/scientific-taste-agent}
}
```

The underlying methodology:

```bibtex
@article{scientific_taste_2025,
  title={AI Can Learn Scientific Taste},
  author={...},
  journal={arXiv preprint arXiv:2603.14473},
  year={2025}
}
```
