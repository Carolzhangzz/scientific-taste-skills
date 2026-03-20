# Scientific Taste Methodology

Detailed reference for the theoretical foundations behind the 5 taste tests.

## Origin: "AI Can Learn Scientific Taste" (arXiv:2603.14473)

The RLCF (Reinforcement Learning from Citation Feedback) methodology trains language models to evaluate scientific ideas using citation-based pairwise comparison. Key findings:

### Core Discovery
Models trained on citation signals learn to distinguish high-impact from low-impact research — and the learned preferences align with what experienced researchers call "taste":

1. **Fundamental > Surface** — Models prefer ideas that address root causes over those that treat symptoms
2. **Paradigm-shifting > Incremental** — Models prefer ideas that change how a field thinks over those that improve existing approaches
3. **Broadly applicable > Narrow** — Models prefer ideas that generalize across domains over those locked to one use case

### Why Pairwise, Not Absolute Scoring

Absolute quality scores are unreliable — different reviewers calibrate differently, and scores are anchored to venue-specific norms. Pairwise comparison ("Is idea A more impactful than idea B?") produces:
- Higher inter-rater agreement
- More robust training signals
- Better generalization across fields

This is why Taste Test 4 (Pairwise Comparison) is the most diagnostic test in the battery.

### The Citation Signal

High-citation papers are not always better, but citation patterns reveal structural impact:
- **Breadth of citing fields** — Ideas cited across multiple subfields have higher generative power
- **Citation velocity** — Ideas that spawn immediate follow-up work addressed a real bottleneck
- **Citation context** — Ideas cited as "building on" (vs "related to") introduced useful abstractions

### What "Taste" Is NOT

- Not preference for trendy topics (taste is orthogonal to hype)
- Not preference for complex solutions (taste often favors elegance and simplicity)
- Not preference for famous authors (the methodology controls for author reputation)
- Not a checklist (taste is holistic judgment, not item-by-item verification)

## How the 5 Tests Map to RLCF Findings

| Taste Test | RLCF Finding | What It Measures |
|-----------|-------------|-----------------|
| Fundamental vs Surface | Models prefer root-cause ideas | Problem depth |
| One-Sentence Elegance | High-impact papers have clean core insights | Conceptual clarity |
| Generative Power | Citation breadth predicts impact | Abstraction quality |
| Pairwise Comparison | Direct application of RLCF methodology | Relative positioning |
| Senior Reviewer Test | Expert-model agreement is highest on "excitement" | Holistic taste |

## Applying Taste Across Fields

The 5 tests are field-independent because they evaluate the **structure** of an idea, not its content:

- In **HCI**: Does the interaction paradigm address a fundamental gap between user intent and tool capability?
- In **ML**: Does the method address a fundamental limitation of the learning paradigm, or just add a module?
- In **Systems**: Does the architecture address a fundamental mismatch between workload patterns and system abstractions?
- In **Theory**: Does the result reveal structural insight or just extend a technique to a new setting?

The venue-specific criteria (what counts as a "contribution," what evaluation methods are expected) are handled by venue modules. The taste tests evaluate whether the idea is worth pursuing in the first place.

## The Kill Decision

The most valuable output of the taste filter is the **kill decision** — recommending NOT to pursue an idea. Researchers waste enormous time on ideas that are:
- Technically feasible
- Clearly publishable somewhere
- But fundamentally unexciting

The taste filter catches these by asking: "Would the field be structurally stuck without this?" If no, the idea is likely incremental regardless of execution quality. Kill it early and find a better problem.
