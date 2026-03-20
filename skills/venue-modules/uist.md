# UIST Venue Module

**ACM Symposium on User Interface Software and Technology**

UIST is the premier venue for novel interactive systems, interaction techniques, and enabling technologies. It values working systems with compelling demos over studies or frameworks alone.

---

## 7 Criteria Every UIST Paper Must Meet

### 1. "Impossible Before" — Not "Better", But "Didn't Exist"

Every strong UIST paper identifies something **structurally impossible** with prior tools:
- Augmented Physics: static textbook diagram → interactive simulation (not "better simulation")
- Generative Agents: 25 agents autonomously forming social relationships (not "smarter NPCs")
- Sketch-n-Sketch: recursive programs built entirely via GUI (not "better code editor")

**Test:** Remove "better/faster/easier" from your pitch. Replace with "didn't exist before." If it still makes sense, it passes.

### 2. AI is a Means, Not the Contribution

UIST AI papers use off-the-shelf models (GPT-4, SAM, Stable Diffusion). The contribution is ALWAYS the interaction design around the AI:
- VRCopilot: wireframes as intermediate representation for AI 3D generation
- Block & Detail: semantic stroke hierarchy for stable sketch-to-image
- Policy Maps: 2D projected behavioral maps for LLM policy authoring

**Test:** Could you describe the contribution WITHOUT naming any specific AI model? If yes, it passes.

### 3. Formative Study → Design Goals → System

The canonical structure:
- WorldSmith: 4 world-builders → D1-D4 → system features
- Augmented Physics: 7 physics teachers → 4 augmentation strategies → system
- MapStory: 200 YouTube videos + 3 animators → animation primitive taxonomy → system

Design goals must emerge from the formative study, not be reverse-engineered from a pre-existing system.

### 4. Multi-Method Evaluation

Combine 2-3 evaluation methods:
- Technical evaluation (pipeline accuracy, latency, benchmarks)
- User study (N=12-24, within/between subjects)
- Expert validation (N=3-5, structured interviews)

**Measures are about INTERACTION quality** (agency, control, creativity, workload), not model quality (accuracy, F1).

### 5. 30-Second "Whoa" Demo

Every UIST paper implies a compelling demo moment:
- Augmented Physics: textbook diagram comes alive as interactive simulation
- RealityCanvas: stomp foot → hand-drawn water splash appears in real time
- Block & Detail: add detail strokes within a block → only that region changes

**Test:** Can you describe the exact 5-second sequence that would make someone say "whoa"?

### 6. Interaction Vocabulary from Corpus/Practice Analysis

Features are DERIVED from studying real practice, not invented:
- RealityTalk: 177 augmented presentation videos → 4D design space
- MapStory: 200 YouTube map animations → animation primitive taxonomy
- Block & Detail: studied illustrator drawing process → blocking-then-detailing workflow

### 7. Natural Modality for Intent Expression

The user expresses intent through the modality most natural for the domain:
- Spatial intent → sketch/draw
- Behavioral intent → speech
- Stylistic intent → reference example
- Structural intent → direct manipulation

The system adapts to the user's language. The user never adapts to the system's language.

---

## 15 Design Patterns

### Human-AI Co-Creation

| # | Pattern | Template | Example Papers |
|---|---------|----------|----------------|
| 1 | Intermediate Representation as Agency Bridge | User creates low-fi rep → AI converts to high-fi → User edits low-fi to iterate | VRCopilot, Block & Detail, Policy Maps |
| 2 | Auto-Generate then Refine | AI first draft → User refines with multi-granularity controls | SGToolkit, EchoLadder, GenTune |
| 3 | Dual-Agent Architecture | Agent 1 decomposes → Agent 2 grounds with facts → User edits units | MapStory |
| 4 | Dialogue-Based Decomposition | System asks structured Qs → User responds naturally → Structured artifact | StepWrite |

### Augmentation

| # | Pattern | Template | Example Papers |
|---|---------|----------|----------------|
| 5 | Augment-in-Place | Take existing artifact → Overlay interactive behavior → Preserve context | Augmented Physics, RealitySketch, NoteIt |
| 6 | Scaffolded Critique | Expert knowledge → Independent toggleable layers → Diagnostic feedback | ArtKrit |

### Sketching & Physical Interaction

| # | Pattern | Template | Example Papers |
|---|---------|----------|----------------|
| 7 | Sketch-then-Speak | Spatial authoring (draw) + Behavioral authoring (speak) → Interactive artifact | DrawTalking, RealityTalk |
| 8 | Trigger-Bound Interaction | Separate content from activation → Connect through sensing | RealityCanvas, RealityTalk |
| 9 | Bidirectional Reality Binding | Virtual affects physical AND physical affects virtual | Sketched Reality |
| 10 | Output-Directed Programming | Manipulate output → System infers source code changes | Sketch-n-Sketch |

### Sensing & Hardware

| # | Pattern | Template | Example Papers |
|---|---------|----------|----------------|
| 11 | Repurposed Sensing | Hardware for X → Discover it senses Y via novel physical principle | EclipseTouch, MARS |
| 12 | Minimal Multimodal Fusion | Fewest complementary sensors + Sophisticated ML → Rich state | Wrist2Finger |

### Transformation & Style

| # | Pattern | Template | Example Papers |
|---|---------|----------|----------------|
| 13 | Motion/Style Transfer by Example | Existing artifact as specification → Transfer to new medium | Wakey-Wakey, CineVision |
| 14 | Video-to-X Transformation | Analyze video → Extract structure → Produce interactive artifact | Vid2Coach, NoteIt, MapStory |
| 15 | Hierarchical Style Presets | Parameter tiers + Expert style bundles → User customization | CineVision, GenTune |

---

## UIST Paper Structure

```
1. INTRODUCTION (~2 pages)
   - Compelling scenario or vision question
   - Specific breakdown in current practice
   - What is now possible that wasn't before
   - Contributions (typically 3: system, design knowledge, evaluation)

2. RELATED WORK (~2 pages)
   - Bridge 3-4 research threads
   - For each: what it contributes, what gap remains

3. FORMATIVE STUDY (~1.5-2 pages)
   - Participants, method, findings
   - Design goals (DG1, DG2, ...) derived from findings

4. SYSTEM (~3-4 pages)
   - Overview figure, user workflow walkthrough
   - Each feature mapped to a design goal
   - Technical implementation, annotated UI screenshots

5. EVALUATION (~3-4 pages)
   - Technical evaluation + User study (N=12-24) + Expert validation (N=3-5)

6. DISCUSSION (~1.5-2 pages)
   - Design implications, limitations, future work

7. CONCLUSION (~0.5 page)
```

---

## Evaluation Measures

| Category | Measures |
|----------|----------|
| Interaction Quality | NASA-TLX, SUS, Creativity Support Index, perceived agency/control |
| Process | Time to first result, iteration count, edit granularity |
| Output Quality | Blind expert eval (Likert), pairwise preference vs baseline |
| Technical | Pipeline success rate, end-to-end latency, component accuracy |

---

## UIST vs CHI Decision Guide

| Your contribution is... | Submit to |
|--------------------------|-----------|
| Novel interaction technique or system | UIST |
| Toolkit enabling new interactive artifacts | UIST |
| Empirical study of user behavior | CHI |
| Design space with no working system | CHI |
| AI model with a GUI wrapper | Neither (ML venue) |
| Fabrication technique for interactive devices | UIST |
| Working system + user study showing new workflow | UIST |
| Theory or framework without implementation | CHI |

**Litmus test:** Does it have a compelling 30-second demo video? If not, it's probably CHI.
