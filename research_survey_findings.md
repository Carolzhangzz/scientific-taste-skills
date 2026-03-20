# Survey: Automated Research Idea Generation & Evaluation (2024-2026)

## 1. The AI Scientist (v1 & v2)

**v1: "The AI Scientist: Towards Fully Automated Open-Ended Scientific Discovery"**
- **Authors:** Chris Lu, Cong Lu, Robert Tjarko Lange, Jakob Foerster, Jeff Clune, David Ha
- **Year/Venue:** 2024, arXiv (Sakana AI + Oxford + UBC)
- **Key Methodology:**
  - End-to-end pipeline: Idea Generation -> Code Implementation -> Experiment Execution -> Visualization -> Paper Writing -> Automated Review
  - Automated reviewer achieves near-human accuracy for paper scoring
  - Iterative open-ended development, mimicking the human scientific community
  - Cost: ~$15 per paper; tested on diffusion models, transformers, grokking
- **What works well:** Full-loop automation with self-review; open-ended iteration
- **Relevance to "scientific taste":** Their automated reviewer is an early attempt at codifying evaluation taste, but it's trained on conference acceptance thresholds rather than deeper quality signals

**v2: "The AI Scientist-v2: Workshop-Level Automated Scientific Discovery via Agentic Tree Search"**
- **Authors:** Yutaro Yamada, Robert Tjarko Lange, Cong Lu, Shengran Hu, Chris Lu, Jakob Foerster, Jeff Clune, David Ha
- **Year/Venue:** 2025, ICLR Workshop (first AI-generated peer-reviewed accepted paper)
- **Key Methodology:**
  - Progressive agentic tree-search managed by a dedicated experiment manager agent
  - Eliminates reliance on human-authored code templates
  - Vision-Language Model feedback for iterative figure refinement
  - Generalizes across diverse ML domains
- **What works well:** Tree search allows exploring multiple research directions simultaneously; no templates needed
- **Relevance to "scientific taste":** Tree search implicitly encodes taste through branch selection/pruning decisions

---

## 2. "Can LLMs Generate Novel Research Ideas?" (Si et al.)

- **Title:** "Can LLMs Generate Novel Research Ideas? A Large-Scale Human Study with 100+ NLP Researchers"
- **Authors:** Chenglei Si, Diyi Yang, Tatsunori Hashimoto
- **Year/Venue:** 2024, arXiv:2409.04109; accepted ICLR 2025
- **Key Methodology:**
  - **Paper Retrieval:** Semantic Scholar API with KeywordQuery(), PaperQuery(), GetReferences(); up to 120 papers per topic, reranked by relevance, empirical rigor, inspirational value
  - **Seed Idea Generation:** 4,000 candidate ideas per topic via RAG; top k=10 papers included as context
  - **Deduplication & Ranking:** Cosine similarity threshold 0.8 removes duplicates (~5% survive); Swiss-system tournament (5 rounds of pairwise comparison)
  - **Evaluation Dimensions:** Novelty, Excitement, Feasibility, Expected Effectiveness, Overall Score (1-10 scale)
  - Standardized proposal template: title, problem statement, motivation, proposed method, step-by-step experiment plan, test cases, fallback plan
- **Key Findings:**
  - LLM ideas judged MORE NOVEL than human expert ideas (p < 0.05) but slightly weaker on feasibility
  - Only 5% of 4,000 generated ideas are unique (massive diversity problem)
  - LLM self-evaluation accuracy: 53.3% vs human inter-reviewer consistency: 56.1%
  - Key failure modes: vague implementation details, dataset misuse, missing baselines, unrealistic assumptions, weak motivation
- **Relevance to "scientific taste":** Demonstrates that novelty alone is insufficient -- feasibility, grounding, and implementability matter. LLMs cannot reliably self-evaluate, suggesting taste must come from external signals

---

## 3. ResearchAgent

- **Title:** "ResearchAgent: Iterative Research Idea Generation over Scientific Literature with Large Language Models"
- **Authors:** Jinheon Baek, Sujay Kumar Jauhar, Silviu Cucerzan, Sung Ju Hwang
- **Year/Venue:** 2024 (arXiv April 2024), NAACL 2025
- **Key Methodology:**
  - Starts from a core scientific paper
  - **Academic graph augmentation:** Connects information over citation/co-authorship graphs + knowledge store of shared underlying concepts mined across papers
  - **Entity-based knowledge store:** Extracts shared concepts across papers for cross-pollination
  - **Multiple ReviewingAgents:** LLM-based reviewers provide iterative feedback; instantiated with human-preference-aligned LLMs; evaluation criteria elicited from actual human judgments
  - Iterative revision loop: generate -> review -> revise -> review again
- **What works well:** Multi-agent review with human-aligned criteria; knowledge graph grounding
- **Relevance to "scientific taste":** ReviewingAgents' criteria are elicited from human judgments -- a direct attempt to learn taste from expert preferences

---

## 4. SciMON

- **Title:** "SciMON: Scientific Inspiration Machines Optimized for Novelty"
- **Authors:** Qingyun Wang, Doug Downey, Heng Ji, Tom Hope
- **Year/Venue:** ACL 2024, Bangkok
- **Key Methodology:**
  - **Inspiration retrieval** via three mechanisms:
    1. Semantic neighbors (SentenceBERT cosine similarity on training pairs)
    2. Knowledge graph neighbors (task-method-material relations from corpus)
    3. Citation neighbors (cited paper titles matched by similarity)
  - **Iterative novelty boosting loop:**
    1. LLM generates idea from context + inspirations
    2. Generated idea queries reference corpus (SentenceBERT, top-20 similar)
    3. Compare similarity scores against threshold (0.6)
    4. If above threshold: provide negative examples + instructions to differentiate
    5. Repeat until all retrieved ideas fall below threshold
  - **In-context contrastive loss:** InfoNCE loss encouraging distinctiveness from input
  - **Information extraction pipeline:** PL-Marker for entities, SciCo for coreference
- **Key Findings:**
  - 55.6% of ideas gained novelty through iterative boosting
  - But ideas remain "incremental and with insufficient detail"
  - Ground truth papers rated significantly higher (85% of comparisons) than generated ideas in technical depth
  - Models frequently copy from context or suggest generic combinations
- **Relevance to "scientific taste":** The novelty-via-negative-examples approach is a key technique -- taste can be partially operationalized as "distance from existing work." But novelty != quality

---

## 5. AI Can Learn Scientific Taste

- **Title:** "AI Can Learn Scientific Taste"
- **Authors:** Jingqi Tong, Mingzhe Li, Hangcheng Li, et al. (Fudan University, OpenMOSS, Tsinghua)
- **Year/Venue:** March 2026, arXiv:2603.14473
- **Key Methodology:**
  - **Defines "scientific taste"** as: capacity to judge and propose research ideas with high potential impact
  - Three formal components:
    1. **Potential Impact:** Cumulative expected citations over time
    2. **Judgement Capability:** Accuracy in pairwise comparison of papers' expected impact
    3. **Ideation Capability:** Expected impact of proposed ideas
  - **SciJudgeBench:** 700K field- and time-matched citation-based paper abstract pairs from 2.1M arXiv papers
    - Pairs matched by field + publication time to isolate quality signals
    - Criteria: absolute citation difference >= 8, relative difference >= 30%
  - **Scientific Judge model:** Generative reward model trained via GRPO (Group Relative Policy Optimization)
    - Generates reasoning traces before predicting which paper has higher citations
    - Binary correctness rewards (1 correct, 0 incorrect)
  - **Position-swap consistency:** Each pair evaluated twice with swapped order; correct only if consistent
  - **Scientific Thinker:** Extends judge to ideation; 81.5% win rate against base policy
- **Key Results:**
  - Scientific Judge outperforms GPT-5.2 and Gemini 3 Pro (80.6% accuracy on Qwen3-30B)
  - Generalizes across time (future papers), fields, and metrics (peer review scores)
- **Relevance to "scientific taste":** THIS IS THE MOST DIRECTLY RELEVANT PAPER. Citation-based ground truth for taste; GRPO training; reasoning traces before judgment; position-swap debiasing

---

## 6. HindSight

- **Title:** "HindSight: Evaluating LLM-Generated Research Ideas via Future Impact"
- **Authors:** (arXiv:2603.15164, March 2026)
- **Key Methodology:**
  - Time-split evaluation framework: restrict idea generation to pre-cutoff literature, evaluate against papers published in subsequent 30 months
  - Match generated ideas against real future publications; score by citation impact and venue acceptance
  - Tests across 10 AI/ML research topics
- **Critical Finding:** HindSight scores are NEGATIVELY CORRELATED with LLM-judged novelty
  - LLMs systematically overvalue novel-sounding ideas that never materialize in real research
  - RAG-augmented system produces 2.5x higher-scoring ideas, but LLM-as-Judge sees no difference
- **Relevance to "scientific taste":** Demonstrates that LLM novelty judgments are anti-correlated with real impact -- true taste must incorporate feasibility/groundedness, not just novelty signals

---

## 7. IdeaSynth

- **Title:** "IdeaSynth: Iterative Research Idea Development Through Evolving and Composing Idea Facets with Literature-Grounded Feedback"
- **Authors:** Kevin Pu, K.J. Kevin Feng, Tovi Grossman, Tom Hope, Bhavana Dalvi Mishra, Matt Latzke, Jonathan Bragg, Joseph Chee Chang, Pao Siangliulue
- **Year/Venue:** October 2024, arXiv:2410.04025 (U Toronto, U Washington, Allen AI)
- **Key Methodology:**
  - **Canvas-based interface** with node graph for idea exploration
  - **Four idea facets:** Problem/RQ, Proposed Design/Solution, Evaluation Methods, Contribution/Impact
  - **Literature-grounded RAG:** PDFs processed via GROBID + GPT-3.5-turbo for facet-specific summarization
  - **Three feedback types:** Iteration (clarifying questions), Alternatives (variations), Expansions (cross-facet connections)
  - Human-in-the-loop: researchers maintain agency while AI provides structured suggestions
- **Study Results:**
  - Significantly greater exploration of alternatives (5.40 vs 3.65, p<0.01)
  - Better idea expansion with details (6.05 vs 4.45)
  - Lab study N=20, field deployment N=7
- **Relevance to "scientific taste":** Faceted decomposition of ideas is a key insight -- taste evaluation could operate on individual facets rather than holistic judgments

---

## 8. Deep Ideation

- **Title:** "Deep Ideation: Designing LLM Agents to Generate Novel Research Ideas on Scientific Concept Network"
- **Year/Venue:** November 2024, arXiv:2511.02238
- **Key Methodology:**
  - **Scientific concept network** based on keyword co-occurrence in literature
  - **Explore-Expand-Evolve workflow** with an Idea Stack to track progress
  - **Critic engine** trained on real-world reviewer feedback for continuous novelty/feasibility scoring
  - LLM queries the concept network iteratively during ideation
- **Key Results:** 10.67% quality improvement over baselines; ideas surpass top conference acceptance levels
- **Relevance to "scientific taste":** Critic engine trained on reviewer feedback is another approach to learning taste; concept network provides structural grounding

---

## 9. Nova

- **Title:** "Nova: An Iterative Planning and Search Approach to Enhance Novelty and Diversity of LLM Generated Ideas"
- **Year/Venue:** October 2024, arXiv:2410.14255
- **Key Methodology:**
  - Iterative planning framework specifically targeting the diversity problem in LLM ideation
  - Search-based approach to explore wider idea space
- **Key Results:**
  - 2.5x more high-quality ideas than SOTA methods
  - 3.4x more unique novel ideas than approaches without iterative planning
- **Relevance to "scientific taste":** Addresses the critical diversity failure mode; taste should reward diversity, not just individual idea quality

---

## 10. Chain of Ideas (CoI)

- **Title:** "Chain of Ideas: Revolutionizing Research Via Novel Idea Development with LLM Agents"
- **Year/Venue:** October 2024, arXiv:2410.13185; EMNLP 2025 Findings
- **Key Methodology:**
  - Organizes literature into **chain structures** reflecting progressive development in a domain
  - Three stages: CoI Construction -> Idea Generation -> Experiment Design
  - For each chain, LLM predicts future research directions via step-by-step consolidation + iterative novelty checks
  - Addresses the problem that dumping all literature on an LLM leads to incoherent ideas
- **Relevance to "scientific taste":** Chain structure captures research trajectory/momentum -- taste could incorporate "where is the field heading" signals

---

## 11. SciPIP

- **Title:** "SciPIP: An LLM-based Scientific Paper Idea Proposer"
- **Year/Venue:** October 2024, arXiv:2410.23166
- **Key Methodology:**
  - **Multi-dimensional literature retrieval:** semantics, entity co-occurrence, and citation co-occurrence
  - **Dual-path idea generation:**
    1. Path 1: Infer solutions from retrieved literature (feasibility-oriented)
    2. Path 2: Generate original ideas through model brainstorming (novelty-oriented)
    3. Combine both paths for balance between feasibility and originality
  - Dataset: 78,571 papers from prominent AI conferences
- **Relevance to "scientific taste":** Dual-path balancing novelty vs. feasibility is a key design pattern for taste -- taste requires BOTH

---

## 12. MLR-Copilot

- **Title:** "MLR-Copilot: Autonomous Machine Learning Research based on Large Language Models Agents"
- **Year/Venue:** August 2024, arXiv:2408.14033
- **Key Methodology:**
  - Three phases: Idea Generation (IdeaAgent with RL-tuned LLM) -> Experiment Implementation (ExperimentAgent) -> Execution
  - IdeaAgent uses RL-tuned LLM for idea quality
  - ExperimentAgent retrieves prototype code + candidate models/data from HuggingFace
- **Relevance to "scientific taste":** RL-tuning the IdeaAgent is an attempt to learn quality signals -- taste via reinforcement learning

---

## 13. AI-Researcher

- **Title:** "AI-Researcher: Autonomous Scientific Innovation"
- **Authors:** Jiabin Tang, Lianghao Xia, et al.
- **Year/Venue:** May 2025, NeurIPS 2025 Spotlight
- **Key Methodology:**
  - Multi-agent architecture with structured knowledge exchange
  - **Resource Analyst agents:** Decompose research concepts with bidirectional mappings between math formulations and code
  - **Iterative refinement:** Specialized agents collaborate through structured feedback cycles
  - **Scientist-Bench:** Benchmark with SOTA papers across AI domains; guided innovation + open-ended exploration tasks
- **Relevance to "scientific taste":** Bidirectional math-code mapping ensures ideas are grounded in implementability -- a key taste signal

---

## 14. ResearchBench

- **Title:** "ResearchBench: Benchmarking LLMs in Scientific Discovery via Inspiration-Based Task Decomposition"
- **Year/Venue:** March 2025, arXiv:2503.21248
- **Key Methodology:**
  - Decomposes scientific discovery into three sub-tasks: **Inspiration Retrieval, Hypothesis Composition, Hypothesis Ranking**
  - Automated extraction of research questions, background surveys, inspirations, and hypotheses from papers across 12 disciplines
  - Focus on 2024 papers to prevent data contamination
- **Key Finding:** LLMs perform well at retrieving inspirations (novel knowledge associations) -- "research hypothesis mines"
- **Relevance to "scientific taste":** Task decomposition into retrieval/composition/ranking enables modular evaluation of taste components

---

## 15. Novelty Assessment Methods

**SchNovel Benchmark:** 15,000 paper pairs across 6 fields with 2-10 year publication gaps for evaluating LLM novelty assessment

**RAG-Novelty:** Retrieval-augmented novelty assessment mirroring human peer review; outperforms baselines by grounding assessment in retrieved context

**GraphMind:** Interactive novelty assessment system

**Key finding across studies:** LLMs significantly overlook novelty when evaluating paper weaknesses; semantic entropy proposed as a reference-free metric for novelty and diversity

---

## 16. Survey Papers

- **"From Automation to Autonomy: A Survey on Large Language Models in Scientific Discovery"** -- EMNLP 2025; three autonomy levels: LLM as Tool, Analyst, Scientist
- **"Agentic AI for Scientific Discovery: A Survey"** -- ICLR 2025; published as conference paper
- **"From AI for Science to Agentic Science"** -- arXiv:2508.14111; domain-oriented review across life sciences, chemistry, materials, physics
- **"A Survey of AI Scientists"** -- arXiv:2510.23045; unified framework: Literature Review -> Idea Generation -> Experimental Preparation -> Execution -> Writing -> Paper Generation
- **Evolution timeline:** Foundational Modules (2022-2023) -> Closed-Loop Integration (2024) -> Scalability & Collaboration (2025+)

---

## Synthesis: Techniques for General "Scientific Taste" Evaluation

### Proven Approaches:
1. **Citation-based ground truth** (SciJudgeBench): Pairwise comparison of papers matched by field+time, using citations as impact proxy
2. **GRPO training with reasoning traces** (Scientific Judge): Model generates reasoning before judging; trained with binary rewards
3. **Position-swap consistency** (Scientific Judge, HindSight): Evaluate each pair twice with swapped order to debias
4. **Time-split evaluation** (HindSight): Generate ideas with pre-cutoff knowledge, evaluate against real future publications
5. **Iterative novelty boosting** (SciMON): Retrieve-compare-update loop with similarity thresholds
6. **Multi-agent review** (ResearchAgent): Multiple reviewing agents with human-preference-aligned criteria
7. **Faceted decomposition** (IdeaSynth, ResearchBench): Evaluate problem, method, evaluation, contribution separately
8. **Dual-path generation** (SciPIP): Balance feasibility-first and novelty-first paths

### Critical Insights for Taste Evaluation:
- **Novelty is anti-correlated with real impact** (HindSight) -- taste must NOT be just novelty
- **LLMs cannot self-evaluate reliably** (Si et al.) -- external signals needed
- **Diversity is a massive problem** -- only 5% of generated ideas are unique
- **Feasibility and grounding matter more than novelty** for real-world impact
- **Reviewer feedback training** (Deep Ideation critic engine) improves quality assessment
- **RL/GRPO on preference data** is the most promising training approach for taste models
- **Structural signals** (concept networks, citation graphs, chain-of-ideas trajectories) provide taste context that raw text cannot
