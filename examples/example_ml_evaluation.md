# Example: ML Idea Evaluation — Adaptive Loss Weighting

This example demonstrates Scientific Taste evaluation on an ML idea, showing how the same 5 tests apply outside HCI.

---

## The Idea

**AdaLossWeight:** A meta-learning approach that automatically adjusts per-task loss weights in multi-task learning by treating weight selection as a bandit problem. Uses Thompson Sampling to explore weight configurations during training, converging to optimal weights without manual tuning.

---

## Scientific Taste Evaluation

### One-Sentence Pitch
"Treat multi-task loss weighting as a bandit problem where each arm is a weight configuration, and let Thompson Sampling find the balance during training."

### 5 Taste Tests

| Test | Score | Rationale |
|------|-------|-----------|
| Fundamental vs Surface | ★★☆ | Loss weighting is a real pain point in multi-task learning, but it's a component-level problem. The fundamental issue — WHY tasks interfere with each other — remains unaddressed. This improves the symptom (bad weights) without understanding the disease (task interference). |
| One-Sentence Elegance | ★★★ | Clean formulation. "Loss weighting as a bandit" is an unexpected but natural connection. The insight is that weighting is an exploration-exploitation problem, not a hyperparameter search. |
| Generative Power | ★★☆ | Other researchers could apply the bandit-for-hyperparameters framing to other settings (learning rates, architecture choices), but it's unclear if this is deep enough to become a paradigm. |
| Pairwise Comparison | ★★☆ | Compared to GradNorm (Chen et al., ICML 2018): GradNorm discovered that gradient magnitudes should be balanced, which is a more fundamental insight. AdaLossWeight is a more principled optimization procedure but doesn't deepen understanding of WHY weights matter. |
| Senior Reviewer Test | ★★☆ | A senior reviewer would say: "Nice formulation, solid work, but is this surprising? We already know loss weighting matters and that adaptive methods help. The bandit framing is clean but the insight isn't deep." |

### Verdict: REDESIGN

**Strengths:**
- Clean, elegant formulation (Test 2 is strong)
- Practical value — automatic loss weighting is genuinely useful
- Well-defined scope

**Weaknesses:**
- Doesn't address the fundamental question of task interference (Test 1)
- Feels incremental relative to GradNorm — better optimization, same level of understanding
- The bandit framing, while clean, might be seen as "obvious in hindsight" by reviewers

**Redesign Suggestions:**
1. **Go deeper:** Instead of just finding good weights, use the bandit's exploration to CHARACTERIZE task interference. Which tasks conflict? When during training? Why? If AdaLossWeight discovers that interference patterns change during training (not just magnitudes), that's a fundamental insight.
2. **Generalize the framing:** "Online optimization of training dynamics" — loss weighting is one instance, but the framework should handle curriculum, architecture selection, data mixing. This raises generative power.
3. **Surprising finding:** Run the bandit. What do the learned weight trajectories look like? If they reveal unexpected structure (e.g., "tasks that seem related actually compete early in training but cooperate late"), that finding IS the contribution.

---

## After Redesign

If the author follows suggestion #1 and discovers that task interference has distinct phases (competitive early, cooperative late), the evaluation changes:

| Test | Before | After |
|------|--------|-------|
| Fundamental vs Surface | ★★☆ | ★★★ — Reveals structure in task interference |
| Elegance | ★★★ | ★★★ — "Task interference isn't static — it has phases" |
| Generative Power | ★★☆ | ★★★ — Phase-aware multi-task training as a new paradigm |
| Pairwise | ★★☆ | ★★★ — Goes beyond GradNorm's static view |
| Senior Reviewer | ★★☆ | ★★★ — "I didn't know that!" |

**New Verdict: PROCEED → BEST PAPER CANDIDATE**

---

## Key Takeaway

The original idea was technically sound and well-formulated, but it optimized without understanding. The taste filter identified the gap: elegant mechanism (★★★) but insufficient depth (★★☆ on fundamentals and pairwise). The redesign didn't change the method — it changed the **question** from "how to weight tasks" to "what can weighting reveal about task dynamics."

**The lesson:** In ML, the difference between a solid accept and a best paper is often not the method but the insight the method reveals.
