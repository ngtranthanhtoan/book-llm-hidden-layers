# The Hidden Layers

**What Really Happens Between Your Message and AI's Response**

---

## Introduction

You type a message. A few seconds later, an answer appears — sometimes brilliant, sometimes baffling, occasionally wrong with absolute confidence. To most people, what happens in between is a black box.

This book opens that box.

*The Hidden Layers* is not a book about how to build an AI. It is a book about what is actually happening — right now, every time you talk to one. Every hidden instruction the AI reads before you type a word. Every classifier silently screening your message. Every layer of reasoning, self-critique, and compromise the machine works through before a single token of response appears on your screen.

By the time you finish this book, you will have something close to X-ray vision for every AI conversation. You will understand why the AI gives different answers when you rephrase the same question, why it sometimes refuses something harmless, why asking "are you sure?" genuinely changes the response, and why longer prompts often produce better results. More importantly, you will know exactly how to use that understanding to become dramatically more effective at working with AI.

This book is written for curious, intelligent people who are *not* engineers — business professionals, writers, educators, policymakers, journalists, and anyone who wants to move from casual AI user to someone who truly understands the machine they are talking to every day. There is no math, no code, no jargon without an immediate plain-English explanation. Every concept is grounded in analogies from everyday life, concrete examples, and connections to behaviors you have already noticed but never understood.

Welcome backstage at the most advanced technology in the world.

---

## Table of Contents

### Part 1: What You're Actually Talking To

*Setting the foundation — building a correct mental model before we reveal the hidden layers.*

#### Chapter 1: The Billion-Dollar Autocomplete
- [Lesson 1: What an LLM Actually Is](part-01-what-youre-actually-talking-to/chapter-01-the-billion-dollar-autocomplete/lesson-01-what-an-llm-actually-is.md)
- [Lesson 2: Next-Token Prediction and Why It Works](part-01-what-youre-actually-talking-to/chapter-01-the-billion-dollar-autocomplete/lesson-02-next-token-prediction-and-why-it-works.md)
- [Lesson 3: From ELIZA to GPT — A Brief History](part-01-what-youre-actually-talking-to/chapter-01-the-billion-dollar-autocomplete/lesson-03-from-eliza-to-gpt-a-brief-history.md)
- [Lesson 4: The Paradox of Knowing Without Knowing](part-01-what-youre-actually-talking-to/chapter-01-the-billion-dollar-autocomplete/lesson-04-the-paradox-of-knowing-without-knowing.md)
- [Lesson 5: Shaping Generation, Not Querying a Database](part-01-what-youre-actually-talking-to/chapter-01-the-billion-dollar-autocomplete/lesson-05-shaping-generation-not-querying-a-database.md)

#### Chapter 2: How AI Reads — Tokenization
- [Lesson 1: Tokens — The Pieces AI Actually Sees](part-01-what-youre-actually-talking-to/chapter-02-how-ai-reads-tokenization/lesson-01-tokens-the-pieces-ai-actually-sees.md)
- [Lesson 2: The Token Boundary Problem](part-01-what-youre-actually-talking-to/chapter-02-how-ai-reads-tokenization/lesson-02-the-token-boundary-problem.md)
- [Lesson 3: Languages, Scripts, and Unequal Tokenization](part-01-what-youre-actually-talking-to/chapter-02-how-ai-reads-tokenization/lesson-03-languages-scripts-and-unequal-tokenization.md)
- [Lesson 4: The Vocabulary — A Fixed Menu of Pieces](part-01-what-youre-actually-talking-to/chapter-02-how-ai-reads-tokenization/lesson-04-the-vocabulary-a-fixed-menu-of-pieces.md)
- [Lesson 5: Token Limits and Conversation Constraints](part-01-what-youre-actually-talking-to/chapter-02-how-ai-reads-tokenization/lesson-05-token-limits-and-conversation-constraints.md)

#### Chapter 3: Meaning as Geography — Embeddings
- [Lesson 1: From Tokens to Positions in Semantic Space](part-01-what-youre-actually-talking-to/chapter-03-meaning-as-geography-embeddings/lesson-01-from-tokens-to-positions-in-semantic-space.md)
- [Lesson 2: Vector Arithmetic and Word Relationships](part-01-what-youre-actually-talking-to/chapter-03-meaning-as-geography-embeddings/lesson-02-vector-arithmetic-and-word-relationships.md)
- [Lesson 3: The Knowledge Map — How Meaning Is Organized](part-01-what-youre-actually-talking-to/chapter-03-meaning-as-geography-embeddings/lesson-03-the-knowledge-map-how-meaning-is-organized.md)
- [Lesson 4: Strange Neighborhoods in Embedding Space](part-01-what-youre-actually-talking-to/chapter-03-meaning-as-geography-embeddings/lesson-04-strange-neighborhoods-in-embedding-space.md)

#### Chapter 4: Patterns, Not Understanding
- [Lesson 1: Statistical Patterns at Unimaginable Scale](part-01-what-youre-actually-talking-to/chapter-04-patterns-not-understanding/lesson-01-statistical-patterns-at-unimaginable-scale.md)
- [Lesson 2: Competence Versus Comprehension](part-01-what-youre-actually-talking-to/chapter-04-patterns-not-understanding/lesson-02-competence-versus-comprehension.md)
- [Lesson 3: Hallucination — Confident Pattern Completion](part-01-what-youre-actually-talking-to/chapter-04-patterns-not-understanding/lesson-03-hallucination-confident-pattern-completion.md)
- [Lesson 4: When to Trust and When to Verify](part-01-what-youre-actually-talking-to/chapter-04-patterns-not-understanding/lesson-04-when-to-trust-and-when-to-verify.md)

---

### Part 2: The Invisible Infrastructure

*Everything that happens before and around the Transformer — the systems most users don't know exist.*

#### Chapter 5: The Prompt You Never Wrote
- [Lesson 1: System Prompts — The Invisible Instructions](part-02-the-invisible-infrastructure/chapter-05-the-prompt-you-never-wrote/lesson-01-system-prompts-the-invisible-instructions.md)
- [Lesson 2: Hidden Context and What the Model Really Sees](part-02-the-invisible-infrastructure/chapter-05-the-prompt-you-never-wrote/lesson-02-hidden-context-and-what-the-model-really-sees.md)
- [Lesson 3: How Personality and Rules Are Pre-Defined](part-02-the-invisible-infrastructure/chapter-05-the-prompt-you-never-wrote/lesson-03-how-personality-and-rules-are-pre-defined.md)
- [Lesson 4: Temperature, Top-p, and Hidden Settings](part-02-the-invisible-infrastructure/chapter-05-the-prompt-you-never-wrote/lesson-04-temperature-top-p-and-hidden-settings.md)
- [Lesson 5: Same Brain, Different Characters](part-02-the-invisible-infrastructure/chapter-05-the-prompt-you-never-wrote/lesson-05-same-brain-different-characters.md)

#### Chapter 6: The Army of Classifiers
- [Lesson 1: The Classifier Ensemble Explained](part-02-the-invisible-infrastructure/chapter-06-the-army-of-classifiers/lesson-01-the-classifier-ensemble-explained.md)
- [Lesson 2: Input Classifiers — Screening Every Message](part-02-the-invisible-infrastructure/chapter-06-the-army-of-classifiers/lesson-02-input-classifiers-screening-every-message.md)
- [Lesson 3: Intent Classifiers — Understanding Your Task](part-02-the-invisible-infrastructure/chapter-06-the-army-of-classifiers/lesson-03-intent-classifiers-understanding-your-task.md)
- [Lesson 4: Image Classifiers and Multimodal Screening](part-02-the-invisible-infrastructure/chapter-06-the-army-of-classifiers/lesson-04-image-classifiers-and-multimodal-screening.md)
- [Lesson 5: The False Positive Problem](part-02-the-invisible-infrastructure/chapter-06-the-army-of-classifiers/lesson-05-the-false-positive-problem.md)

#### Chapter 7: The Routing Layer
- [Lesson 1: Model Routing — Which Brain Answers](part-02-the-invisible-infrastructure/chapter-07-the-routing-layer/lesson-01-model-routing-which-brain-answers.md)
- [Lesson 2: Complexity Estimation and Its Failures](part-02-the-invisible-infrastructure/chapter-07-the-routing-layer/lesson-02-complexity-estimation-and-its-failures.md)
- [Lesson 3: Load Balancing and Queue Management](part-02-the-invisible-infrastructure/chapter-07-the-routing-layer/lesson-03-load-balancing-and-queue-management.md)
- [Lesson 4: A/B Testing and the Economics of Routing](part-02-the-invisible-infrastructure/chapter-07-the-routing-layer/lesson-04-ab-testing-and-the-economics-of-routing.md)

#### Chapter 8: Memory, Context, and Why AI Forgets
- [Lesson 1: Context Windows — The Hard Memory Limit](part-02-the-invisible-infrastructure/chapter-08-memory-context-and-why-ai-forgets/lesson-01-context-windows-the-hard-memory-limit.md)
- [Lesson 2: What Gets Kept and What Gets Dropped](part-02-the-invisible-infrastructure/chapter-08-memory-context-and-why-ai-forgets/lesson-02-what-gets-kept-and-what-gets-dropped.md)
- [Lesson 3: Persistent Memory Systems](part-02-the-invisible-infrastructure/chapter-08-memory-context-and-why-ai-forgets/lesson-03-persistent-memory-systems.md)
- [Lesson 4: RAG — Retrieval-Augmented Generation](part-02-the-invisible-infrastructure/chapter-08-memory-context-and-why-ai-forgets/lesson-04-rag-retrieval-augmented-generation.md)
- [Lesson 5: Structuring Conversations for Better Memory](part-02-the-invisible-infrastructure/chapter-08-memory-context-and-why-ai-forgets/lesson-05-structuring-conversations-for-better-memory.md)

---

### Part 3: The Attention Engine

*The core mechanism that makes everything work — how the AI focuses.*

#### Chapter 9: Attention — The Breakthrough
- [Lesson 1: The Transformer in Plain English](part-03-the-attention-engine/chapter-09-attention-the-breakthrough/lesson-01-the-transformer-in-plain-english.md)
- [Lesson 2: The Attention Mechanism Explained](part-03-the-attention-engine/chapter-09-attention-the-breakthrough/lesson-02-the-attention-mechanism-explained.md)
- [Lesson 3: Multi-Head Attention — Parallel Perspectives](part-03-the-attention-engine/chapter-09-attention-the-breakthrough/lesson-03-multi-head-attention-parallel-perspectives.md)
- [Lesson 4: Why Attention Changed Everything](part-03-the-attention-engine/chapter-09-attention-the-breakthrough/lesson-04-why-attention-changed-everything.md)

#### Chapter 10: The Attention Patterns
- [Lesson 1: Types of Attention Heads](part-03-the-attention-engine/chapter-10-the-attention-patterns/lesson-01-types-of-attention-heads.md)
- [Lesson 2: How AI Reads Non-Linearly](part-03-the-attention-engine/chapter-10-the-attention-patterns/lesson-02-how-ai-reads-non-linearly.md)
- [Lesson 3: The Attention Map Visualized](part-03-the-attention-engine/chapter-10-the-attention-patterns/lesson-03-the-attention-map-visualized.md)
- [Lesson 4: Why Word Order and Context Matter](part-03-the-attention-engine/chapter-10-the-attention-patterns/lesson-04-why-word-order-and-context-matter.md)

#### Chapter 11: Layer by Layer — The 80-Story Building
- [Lesson 1: Early Layers — Surface Parsing](part-03-the-attention-engine/chapter-11-layer-by-layer-the-80-story-building/lesson-01-early-layers-surface-parsing.md)
- [Lesson 2: Middle Layers — Semantic Assembly](part-03-the-attention-engine/chapter-11-layer-by-layer-the-80-story-building/lesson-02-middle-layers-semantic-assembly.md)
- [Lesson 3: Deep Layers — Reasoning and Planning](part-03-the-attention-engine/chapter-11-layer-by-layer-the-80-story-building/lesson-03-deep-layers-reasoning-and-planning.md)
- [Lesson 4: Final Layers — Output Preparation](part-03-the-attention-engine/chapter-11-layer-by-layer-the-80-story-building/lesson-04-final-layers-output-preparation.md)
- [Lesson 5: The Residual Stream and Information Flow](part-03-the-attention-engine/chapter-11-layer-by-layer-the-80-story-building/lesson-05-the-residual-stream-and-information-flow.md)

---

### Part 4: The Hidden Thinking

*Reasoning, planning, and self-critique — what happens inside the "thinking" process.*

#### Chapter 12: The Thinking You Never See
- [Lesson 1: Chain of Thought — The Hidden Scratchpad](part-04-the-hidden-thinking/chapter-12-the-thinking-you-never-see/lesson-01-chain-of-thought-the-hidden-scratchpad.md)
- [Lesson 2: The Six Phases of Extended Thinking](part-04-the-hidden-thinking/chapter-12-the-thinking-you-never-see/lesson-02-the-six-phases-of-extended-thinking.md)
- [Lesson 3: When Thinking Triggers and When It Doesn't](part-04-the-hidden-thinking/chapter-12-the-thinking-you-never-see/lesson-03-when-thinking-triggers-and-when-it-doesnt.md)
- [Lesson 4: Thinking Time Versus Answer Quality](part-04-the-hidden-thinking/chapter-12-the-thinking-you-never-see/lesson-04-thinking-time-versus-answer-quality.md)

#### Chapter 13: Intent Resolution
- [Lesson 1: The Four Layers of Intent](part-04-the-hidden-thinking/chapter-13-intent-resolution/lesson-01-the-four-layers-of-intent.md)
- [Lesson 2: Reading Intent Signals](part-04-the-hidden-thinking/chapter-13-intent-resolution/lesson-02-reading-intent-signals.md)
- [Lesson 3: Ambiguity Resolution — Picking an Interpretation](part-04-the-hidden-thinking/chapter-13-intent-resolution/lesson-03-ambiguity-resolution-picking-an-interpretation.md)
- [Lesson 4: When Intent Resolution Goes Wrong](part-04-the-hidden-thinking/chapter-13-intent-resolution/lesson-04-when-intent-resolution-goes-wrong.md)

#### Chapter 14: The Internal Debate
- [Lesson 1: Self-Consistency Checking](part-04-the-hidden-thinking/chapter-14-the-internal-debate/lesson-01-self-consistency-checking.md)
- [Lesson 2: Confidence Calibration](part-04-the-hidden-thinking/chapter-14-the-internal-debate/lesson-02-confidence-calibration.md)
- [Lesson 3: The Revision Loop — Draft, Critique, Revise](part-04-the-hidden-thinking/chapter-14-the-internal-debate/lesson-03-the-revision-loop-draft-critique-revise.md)
- [Lesson 4: Why "Are You Sure?" Changes the Answer](part-04-the-hidden-thinking/chapter-14-the-internal-debate/lesson-04-why-are-you-sure-changes-the-answer.md)

#### Chapter 15: The Intent Stack
- [Lesson 1: The Seven Simultaneous Layers](part-04-the-hidden-thinking/chapter-15-the-intent-stack/lesson-01-the-seven-simultaneous-layers.md)
- [Lesson 2: How Layers Conflict and Resolve](part-04-the-hidden-thinking/chapter-15-the-intent-stack/lesson-02-how-layers-conflict-and-resolve.md)
- [Lesson 3: RLHF and Learned Tradeoff Preferences](part-04-the-hidden-thinking/chapter-15-the-intent-stack/lesson-03-rlhf-and-learned-tradeoff-preferences.md)
- [Lesson 4: Steering the Stack with Explicit Priorities](part-04-the-hidden-thinking/chapter-15-the-intent-stack/lesson-04-steering-the-stack-with-explicit-priorities.md)

#### Chapter 16: Task Decomposition
- [Lesson 1: How AI Converts Complex Requests to Subtasks](part-04-the-hidden-thinking/chapter-16-task-decomposition/lesson-01-how-ai-converts-complex-requests-to-subtasks.md)
- [Lesson 2: The Decomposition Hierarchy](part-04-the-hidden-thinking/chapter-16-task-decomposition/lesson-02-the-decomposition-hierarchy.md)
- [Lesson 3: Why Complex Requests Fail](part-04-the-hidden-thinking/chapter-16-task-decomposition/lesson-03-why-complex-requests-fail.md)
- [Lesson 4: Structuring Requests for Complete Responses](part-04-the-hidden-thinking/chapter-16-task-decomposition/lesson-04-structuring-requests-for-complete-responses.md)

#### Chapter 17: Policy Reasoning
- [Lesson 1: The Safety Spectrum](part-04-the-hidden-thinking/chapter-17-policy-reasoning/lesson-01-the-safety-spectrum.md)
- [Lesson 2: The Refusal Decision Tree](part-04-the-hidden-thinking/chapter-17-policy-reasoning/lesson-02-the-refusal-decision-tree.md)
- [Lesson 3: The Over-Refusal Problem](part-04-the-hidden-thinking/chapter-17-policy-reasoning/lesson-03-the-over-refusal-problem.md)
- [Lesson 4: Context as a Key — Unlocking Refused Requests](part-04-the-hidden-thinking/chapter-17-policy-reasoning/lesson-04-context-as-a-key-unlocking-refused-requests.md)

---

### Part 5: The Generation Engine

*How words actually appear — the mechanics of response creation.*

#### Chapter 18: Word by Word
- [Lesson 1: The Autoregressive Loop Explained](part-05-the-generation-engine/chapter-18-word-by-word/lesson-01-the-autoregressive-loop-explained.md)
- [Lesson 2: The Probability Distribution at Each Step](part-05-the-generation-engine/chapter-18-word-by-word/lesson-02-the-probability-distribution-at-each-step.md)
- [Lesson 3: The Commitment Problem](part-05-the-generation-engine/chapter-18-word-by-word/lesson-03-the-commitment-problem.md)
- [Lesson 4: Steering Generation with Opening Words](part-05-the-generation-engine/chapter-18-word-by-word/lesson-04-steering-generation-with-opening-words.md)

#### Chapter 19: The Creativity Dial
- [Lesson 1: Temperature — Predictable Versus Creative](part-05-the-generation-engine/chapter-19-the-creativity-dial/lesson-01-temperature-predictable-versus-creative.md)
- [Lesson 2: Top-p, Top-k, and Sampling Strategies](part-05-the-generation-engine/chapter-19-the-creativity-dial/lesson-02-top-p-top-k-and-sampling-strategies.md)
- [Lesson 3: Beam Search and Best-of-N](part-05-the-generation-engine/chapter-19-the-creativity-dial/lesson-03-beam-search-and-best-of-n.md)
- [Lesson 4: Matching Randomness to Your Task](part-05-the-generation-engine/chapter-19-the-creativity-dial/lesson-04-matching-randomness-to-your-task.md)

#### Chapter 20: When the AI Uses Tools
- [Lesson 1: The Tool Use Decision Process](part-05-the-generation-engine/chapter-20-when-the-ai-uses-tools/lesson-01-the-tool-use-decision-process.md)
- [Lesson 2: The Orchestration Loop](part-05-the-generation-engine/chapter-20-when-the-ai-uses-tools/lesson-02-the-orchestration-loop.md)
- [Lesson 3: Multi-Step Tool Chains](part-05-the-generation-engine/chapter-20-when-the-ai-uses-tools/lesson-03-multi-step-tool-chains.md)
- [Lesson 4: AI Agents — Autonomous Workflows](part-05-the-generation-engine/chapter-20-when-the-ai-uses-tools/lesson-04-ai-agents-autonomous-workflows.md)

---

### Part 6: The Quality Layer

*Post-generation processing — what happens after the AI writes but before you read.*

#### Chapter 21: The Output Filter
- [Lesson 1: Output Safety Classifiers](part-06-the-quality-layer/chapter-21-the-output-filter/lesson-01-output-safety-classifiers.md)
- [Lesson 2: What the Filters Check](part-06-the-quality-layer/chapter-21-the-output-filter/lesson-02-what-the-filters-check.md)
- [Lesson 3: The Reward Model — Scoring Responses](part-06-the-quality-layer/chapter-21-the-output-filter/lesson-03-the-reward-model-scoring-responses.md)
- [Lesson 4: Blocked, Truncated, or Regenerated](part-06-the-quality-layer/chapter-21-the-output-filter/lesson-04-blocked-truncated-or-regenerated.md)

#### Chapter 22: The Feedback Loop
- [Lesson 1: How Your Reactions Become Training Data](part-06-the-quality-layer/chapter-22-the-feedback-loop/lesson-01-how-your-reactions-become-training-data.md)
- [Lesson 2: The RLHF Cycle Explained](part-06-the-quality-layer/chapter-22-the-feedback-loop/lesson-02-the-rlhf-cycle-explained.md)
- [Lesson 3: A/B Testing and Red Teaming](part-06-the-quality-layer/chapter-22-the-feedback-loop/lesson-03-ab-testing-and-red-teaming.md)
- [Lesson 4: The Continuous Improvement Pipeline](part-06-the-quality-layer/chapter-22-the-feedback-loop/lesson-04-the-continuous-improvement-pipeline.md)

---

### Part 7: Mastering the Machine

*Practical application — now that you understand every hidden layer, here's how to use that knowledge.*

#### Chapter 23: The Art of Asking
- [Lesson 1: Prompt Engineering Through Hidden Layers](part-07-mastering-the-machine/chapter-23-the-art-of-asking/lesson-01-prompt-engineering-through-hidden-layers.md)
- [Lesson 2: The Anatomy of an Effective Prompt](part-07-mastering-the-machine/chapter-23-the-art-of-asking/lesson-02-the-anatomy-of-an-effective-prompt.md)
- [Lesson 3: Few-Shot Prompting — Showing What You Want](part-07-mastering-the-machine/chapter-23-the-art-of-asking/lesson-03-few-shot-prompting-showing-what-you-want.md)
- [Lesson 4: The Iterative Approach — Conversation, Not Search](part-07-mastering-the-machine/chapter-23-the-art-of-asking/lesson-04-the-iterative-approach-conversation-not-search.md)

#### Chapter 24: Patterns That Work
- [Lesson 1: Writing, Editing, and Creative Content](part-07-mastering-the-machine/chapter-24-patterns-that-work/lesson-01-writing-editing-and-creative-content.md)
- [Lesson 2: Research, Analysis, and Decision-Making](part-07-mastering-the-machine/chapter-24-patterns-that-work/lesson-02-research-analysis-and-decision-making.md)
- [Lesson 3: Learning, Tutoring, and Code Tasks](part-07-mastering-the-machine/chapter-24-patterns-that-work/lesson-03-learning-tutoring-and-code-tasks.md)
- [Lesson 4: Data Analysis and Summarization](part-07-mastering-the-machine/chapter-24-patterns-that-work/lesson-04-data-analysis-and-summarization.md)
- [Lesson 5: Strategic Thinking and Planning](part-07-mastering-the-machine/chapter-24-patterns-that-work/lesson-05-strategic-thinking-and-planning.md)

#### Chapter 25: The Limits and the Future
- [Lesson 1: What AI Fundamentally Cannot Do](part-07-mastering-the-machine/chapter-25-the-limits-and-the-future/lesson-01-what-ai-fundamentally-cannot-do.md)
- [Lesson 2: Multimodal Models — Seeing and Hearing](part-07-mastering-the-machine/chapter-25-the-limits-and-the-future/lesson-02-multimodal-models-seeing-and-hearing.md)
- [Lesson 3: Agents and Autonomous AI](part-07-mastering-the-machine/chapter-25-the-limits-and-the-future/lesson-03-agents-and-autonomous-ai.md)
- [Lesson 4: The Next Five Years and Staying Effective](part-07-mastering-the-machine/chapter-25-the-limits-and-the-future/lesson-04-the-next-five-years-and-staying-effective.md)

#### Chapter 26: Building Your AI Workflow
- [Lesson 1: Choosing the Right AI for the Right Task](part-07-mastering-the-machine/chapter-26-building-your-ai-workflow/lesson-01-choosing-the-right-ai-for-the-right-task.md)
- [Lesson 2: Building Repeatable Workflows](part-07-mastering-the-machine/chapter-26-building-your-ai-workflow/lesson-02-building-repeatable-workflows.md)
- [Lesson 3: Creating Personal System Prompts](part-07-mastering-the-machine/chapter-26-building-your-ai-workflow/lesson-03-creating-personal-system-prompts.md)
- [Lesson 4: The Human-AI Collaboration Mindset](part-07-mastering-the-machine/chapter-26-building-your-ai-workflow/lesson-04-the-human-ai-collaboration-mindset.md)

---

### Appendices

- [Appendix A: Complete Glossary](appendices/appendix-a-complete-glossary.md)
- [Appendix B: The Complete Hidden Layer Map](appendices/appendix-b-the-complete-hidden-layer-map.md)
- [Appendix C: Quick Reference — Prompt Patterns](appendices/appendix-c-quick-reference-prompt-patterns.md)
- [Appendix D: Further Reading](appendices/appendix-d-further-reading.md)

---

*7 Parts. 26 Chapters. 111 Lessons. One complete journey from "I type and it answers" to "I understand every hidden layer in between."*
