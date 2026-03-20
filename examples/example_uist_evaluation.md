# Example: UIST Idea Evaluation — OsmoCut

This example demonstrates the Scientific Taste evaluation on a real idea that was ultimately **killed** — showing how the taste filter saves months of wasted effort.

---

## The Idea

**OsmoCut:** An AI-assisted video editing tool that uses osmotic pressure as a metaphor for clip arrangement. Clips are treated as "molecules" with concentration gradients — the system automatically arranges clips to maintain narrative "equilibrium" while the user adjusts "pressure points" to create tension and release.

---

## Scientific Taste Evaluation

### One-Sentence Pitch
"What if video clips self-organized based on narrative tension gradients, like molecules in osmotic pressure?"

### 5 Taste Tests

| Test | Score | Rationale |
|------|-------|-----------|
| Fundamental vs Surface | ★☆☆ | The metaphor is creative but the underlying problem (clip arrangement) is well-served by existing timeline-based tools. Professional editors are not "blocked" — they have workflows that work. This addresses a surface-level UX preference, not a structural impossibility. |
| One-Sentence Elegance | ★★☆ | The osmotic pressure metaphor is intriguing, but it's an analogy, not an insight. The sentence describes a mechanism, not a revelation about how editing works. |
| Generative Power | ★☆☆ | Physics metaphors for UI layout is not a new abstraction others would build on. This is a one-off design choice, not a generalizable paradigm. |
| Pairwise Comparison | ★☆☆ | Compared to Block & Detail (which introduced intermediate representations for AI generation control): OsmoCut addresses a less fundamental problem, is less broadly applicable, and introduces no reusable abstraction. |
| Senior Reviewer Test | ★☆☆ | A senior reviewer would likely say: "Cute metaphor, but why do editors need this? What can they do now that they couldn't before?" The idea is novel in execution but not intellectually exciting. |

### Verdict: KILL

**Fatal Weaknesses:**
1. No evidence that professional editors are structurally blocked by current tools
2. The osmotic pressure metaphor is decorative, not structural — you could replace it with any physics simulation and the "contribution" would be the same
3. Zero generative power — no one will build "osmotic X" for other creative tools

**What Would Make This a PROCEED:**
Start from the real problem. Interview editors. Find what they CANNOT do. If the answer is "maintain narrative coherence while non-linearly rearranging large clip collections" — then the contribution is a new representation for narrative structure, not a physics metaphor. The metaphor might still be the implementation, but the taste comes from the problem.

---

## Key Takeaway

This idea has a clever surface (the osmotic metaphor) but no depth. The taste filter caught it at Test 1 (Surface-Level Problem) and confirmed the kill at Tests 3-5. Total time saved: ~4-6 months of development and evaluation that would have produced a borderline-reject paper.

**The lesson:** Start from the problem, not the metaphor. Creative mechanisms are the easiest part of research; finding the right problem is the hardest.
