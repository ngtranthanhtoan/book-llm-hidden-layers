# Appendix B: The Complete Hidden Layer Map

A single-page reference showing every step between your message and the AI's response. Keep this at your desk. The next time you chat with an AI, you will know exactly what is happening behind the screen.

---

## The Journey of a Message: From Your Keyboard to the AI's Response

```
╔══════════════════════════════════════════════════════════════════════╗
║                                                                      ║
║   YOU TYPE A MESSAGE                                                 ║
║   "Help me plan a career change from accounting to UX design"        ║
║                                                                      ║
╚══════════════════════════════════════╦═══════════════════════════════╝
                                       ║
                                       ▼
┌──────────────────────────────────────────────────────────────────────┐
│  STAGE 1: INPUT CLASSIFIERS  (Ch. 6)                                 │
│  Dozens of small, specialized AI models scan your message            │
│  before the main LLM ever sees it.                                   │
│                                                                      │
│  Safety Classifiers:                                                 │
│    ├── Toxicity detector ──────── Is this message abusive?           │
│    ├── Self-harm detector ─────── Does this indicate crisis?         │
│    ├── CSAM detector ──────────── Child safety screening             │
│    ├── Violence/weapons ───────── Dangerous content check            │
│    ├── CBRN threat detector ───── Chemical/bio/nuclear screening     │
│    ├── Jailbreak detector ─────── Prompt injection attempt?          │
│    ├── PII detector ───────────── Personal information present?      │
│    ├── Copyright detector ─────── IP/licensing concerns?             │
│    ├── Sexual content detector ── Explicit material check            │
│    └── Cyber/malware detector ─── Malicious code request?            │
│                                                                      │
│  If any classifier flags a serious threat ──► REQUEST BLOCKED        │
│  If classifiers flag a moderate concern ───► Warning injected        │
│                                              into system prompt      │
│  If classifiers pass ─────────────────────► Continue to Stage 2      │
└──────────────────────────────────────╥───────────────────────────────┘
                                       ║
                                       ▼
┌──────────────────────────────────────────────────────────────────────┐
│  STAGE 2: INTENT CLASSIFICATION  (Ch. 6, 13)                        │
│  More classifiers determine what kind of request this is.            │
│                                                                      │
│    ├── Task type ──────── Question? Command? Creative? Analysis?     │
│    ├── Complexity ─────── Simple lookup or multi-step reasoning?     │
│    ├── Domain ─────────── Career advice, technical, medical, etc.    │
│    ├── Language ───────── Which language is the user writing in?     │
│    ├── Tool needs ─────── Does this require search, code, files?    │
│    ├── Sensitivity ────── Politically/emotionally charged topic?     │
│    └── Image content ──── (If images attached) NSFW, faces, etc.    │
│                                                                      │
│  Result: a metadata package describing your request                  │
└──────────────────────────────────────╥───────────────────────────────┘
                                       ║
                                       ▼
┌──────────────────────────────────────────────────────────────────────┐
│  STAGE 3: SYSTEM PROMPT ASSEMBLY  (Ch. 5)                            │
│  The invisible instructions are constructed.                         │
│                                                                      │
│  The full prompt the model sees:                                     │
│    ┌─────────────────────────────────────────────────────────┐       │
│    │  Base system prompt (1,000-10,000 words)                │       │
│    │    ├── Identity & persona                               │       │
│    │    ├── Behavioral rules                                 │       │
│    │    ├── Safety guidelines                                │       │
│    │    ├── Formatting preferences                           │       │
│    │    ├── Tool instructions                                │       │
│    │    └── Knowledge cutoff disclaimer                      │       │
│    ├─────────────────────────────────────────────────────────┤       │
│    │  Dynamic injections from classifiers                    │       │
│    │    └── "This message was flagged for [topic].           │       │
│    │         Handle with extra caution."                     │       │
│    ├─────────────────────────────────────────────────────────┤       │
│    │  User's custom instructions / preferences               │       │
│    ├─────────────────────────────────────────────────────────┤       │
│    │  Conversation history (previous messages)               │       │
│    ├─────────────────────────────────────────────────────────┤       │
│    │  Retrieved context (from memory/RAG — see Stage 5)      │       │
│    ├─────────────────────────────────────────────────────────┤       │
│    │  YOUR MESSAGE  ◄── often less than 1% of total context  │       │
│    └─────────────────────────────────────────────────────────┘       │
└──────────────────────────────────────╥───────────────────────────────┘
                                       ║
                                       ▼
┌──────────────────────────────────────────────────────────────────────┐
│  STAGE 4: MODEL ROUTING  (Ch. 7)                                     │
│  The system decides which AI brain handles your request.             │
│                                                                      │
│    ├── Simple question? ──────────► Smaller, faster model            │
│    ├── Complex reasoning? ────────► Larger, more capable model       │
│    ├── Specialized task? ─────────► Domain-specific model            │
│    └── Load balancing ────────────► Whichever server is available    │
│                                                                      │
│  Also decides: temperature, thinking mode, token budget              │
└──────────────────────────────────────╥───────────────────────────────┘
                                       ║
                                       ▼
┌──────────────────────────────────────────────────────────────────────┐
│  STAGE 5: CONTEXT & MEMORY RETRIEVAL  (Ch. 8)                        │
│  The system searches for additional relevant information.            │
│                                                                      │
│    ├── Persistent memory ──── Has this user chatted before?          │
│    │                          Retrieve stored preferences/facts.     │
│    ├── RAG pipeline ─────────  If documents are available:           │
│    │     ├── Embed the query as a vector                             │
│    │     ├── Search the document index for relevant passages         │
│    │     ├── Rank results by relevance                               │
│    │     └── Inject top passages into the context                    │
│    └── Tool pre-fetch ─────── Pre-load tool results if needed        │
│                                                                      │
│  Retrieved information is added to the assembled prompt above        │
└──────────────────────────────────────╥───────────────────────────────┘
                                       ║
                                       ▼
┌──────────────────────────────────────────────────────────────────────┐
│  STAGE 6: TOKENIZATION  (Ch. 2)                                      │
│  The entire assembled prompt is chopped into tokens.                 │
│                                                                      │
│  "Help me plan a career change" ──► ["Help", " me", " plan",        │
│                                      " a", " career", " change"]    │
│                                                                      │
│  Everything — system prompt, history, your message — becomes         │
│  a sequence of token IDs from a fixed vocabulary of ~100,000.        │
└──────────────────────────────────────╥───────────────────────────────┘
                                       ║
                                       ▼
┌──────────────────────────────────────────────────────────────────────┐
│  STAGE 7: EMBEDDING  (Ch. 3)                                         │
│  Each token is converted into a numerical position in                │
│  a high-dimensional meaning space.                                   │
│                                                                      │
│  Token "career" ──► [0.23, -0.87, 0.14, ..., 0.52]                  │
│                     (thousands of numbers encoding meaning)          │
│                                                                      │
│  At this stage, each word knows what it means in general,            │
│  but not yet what it means in THIS specific context.                 │
│  Positional encoding is also added so the model knows word order.    │
└──────────────────────────────────────╥───────────────────────────────┘
                                       ║
                                       ▼
┌──────────────────────────────────────────────────────────────────────┐
│  STAGE 8: THE TRANSFORMER LAYERS  (Ch. 9, 10, 11)                   │
│  The message passes through 80+ layers of processing.                │
│  Each layer contains attention + feed-forward processing.            │
│                                                                      │
│  ┌────────────────────────────────────────────────────────────┐      │
│  │  EARLY LAYERS (1-20): Surface Parsing                      │      │
│  │  Grammar, token grouping, basic pattern recognition.       │      │
│  │  "career" + "change" start to merge into a concept.        │      │
│  └────────────────────────────────────────────────────────────┘      │
│                          │                                           │
│                          ▼                                           │
│  ┌────────────────────────────────────────────────────────────┐      │
│  │  MIDDLE LAYERS (20-50): Semantic Assembly                  │      │
│  │  Meaning formation, intent recognition, knowledge          │      │
│  │  retrieval from parameters. The model "understands"        │      │
│  │  this is about a professional transition.                  │      │
│  └────────────────────────────────────────────────────────────┘      │
│                          │                                           │
│                          ▼                                           │
│  ┌────────────────────────────────────────────────────────────┐      │
│  │  DEEP LAYERS (50-70): Reasoning & Planning                 │      │
│  │  Cross-referencing, constraint resolution, planning        │      │
│  │  the response structure. The "aha moment."                 │      │
│  │  By ~layer 60, the model has largely "decided" WHAT        │      │
│  │  to say.                                                   │      │
│  └────────────────────────────────────────────────────────────┘      │
│                          │                                           │
│                          ▼                                           │
│  ┌────────────────────────────────────────────────────────────┐      │
│  │  FINAL LAYERS (70-80+): Output Preparation                 │      │
│  │  Word selection, tone calibration, format commitment.      │      │
│  │  The model decides HOW to say it.                          │      │
│  └────────────────────────────────────────────────────────────┘      │
│                                                                      │
│  Throughout all layers: the RESIDUAL STREAM carries information      │
│  forward, each layer adding its contribution like tributaries        │
│  feeding a river.                                                    │
│                                                                      │
│  ATTENTION at each layer:                                            │
│  Multi-head attention runs dozens of parallel perspectives:          │
│    ├── Syntactic heads ──── tracking grammar structure               │
│    ├── Coreference heads ── resolving pronouns ("she" = whom?)      │
│    ├── Semantic heads ───── tracking meaning and themes              │
│    ├── Positional heads ─── tracking word order and recency          │
│    ├── Task-framing heads ─ identifying the type of request          │
│    └── Constraint heads ─── tracking rules and requirements          │
└──────────────────────────────────────╥───────────────────────────────┘
                                       ║
                                       ▼
┌──────────────────────────────────────────────────────────────────────┐
│  STAGE 9: EXTENDED THINKING / REASONING  (Ch. 12-17)                 │
│  For complex requests, the model reasons on a hidden scratchpad      │
│  before generating the visible response.                             │
│                                                                      │
│  The thinking process follows these phases:                          │
│    1. Comprehension ──────── "What is the user actually asking?"     │
│    2. Constraint mapping ─── "What rules do I need to follow?"      │
│    3. Knowledge assessment ─ "What do I know? What am I unsure of?" │
│    4. Planning ──────────── "How should I structure my response?"    │
│    5. Drafting & critique ── "Let me try... wait, that's wrong..."  │
│    6. Final check ─────────  "Does this answer the question?"       │
│                                                                      │
│  Simultaneously managing the INTENT STACK:                           │
│    ├── Literal task execution                                        │
│    ├── User satisfaction                                             │
│    ├── Quality standards                                             │
│    ├── Safety constraints                                            │
│    ├── Format expectations                                           │
│    ├── Relationship management                                       │
│    └── Implicit knowledge application                                │
│                                                                      │
│  POLICY REASONING also occurs here:                                  │
│    "Is this safe? Is this appropriate? How should I handle this?"    │
│                                                                      │
│  This stage can generate 3,000-10,000 tokens of hidden reasoning    │
│  for a 500-token visible response. (Thinking-to-output ratio: ~10:1)│
└──────────────────────────────────────╥───────────────────────────────┘
                                       ║
                                       ▼
┌──────────────────────────────────────────────────────────────────────┐
│  STAGE 10: TOKEN GENERATION — THE AUTOREGRESSIVE LOOP  (Ch. 18, 19) │
│  The AI produces its visible response one token at a time.           │
│                                                                      │
│  ┌──────────────────────────────────────────────────────────┐        │
│  │                                                          │        │
│  │  For each position in the response:                      │        │
│  │    1. Model ranks all ~100,000 possible next tokens      │        │
│  │    2. Temperature setting shapes the distribution:       │        │
│  │       Low temp (0.0-0.3) = focused, predictable          │        │
│  │       Mid temp (0.4-0.7) = balanced                      │        │
│  │       High temp (0.8-1.0+) = creative, surprising        │        │
│  │    3. Top-p / Top-k filtering narrows the candidates     │        │
│  │    4. One token is sampled from the remaining options    │        │
│  │    5. That token is appended to the context              │        │
│  │    6. Process repeats for the next token                 │        │
│  │                     ▲                                    │        │
│  │                     │                                    │        │
│  │           ┌─────────┴─────────┐                          │        │
│  │           │  TOOL USE? (Ch.20)│                          │        │
│  │           │  If the model     │                          │        │
│  │           │  decides it needs │                          │        │
│  │           │  external help:   │                          │        │
│  │           │  • Web search     │                          │        │
│  │           │  • Code execution │                          │        │
│  │           │  • File read      │                          │        │
│  │           │  • API call       │                          │        │
│  │           │  Result is fed    │                          │        │
│  │           │  back into the    │                          │        │
│  │           │  generation loop. │                          │        │
│  │           └───────────────────┘                          │        │
│  │                                                          │        │
│  │  Each token is influenced by:                            │        │
│  │    • The entire system prompt                            │        │
│  │    • Full conversation history                           │        │
│  │    • Retrieved context / memory                          │        │
│  │    • Every token generated so far in this response       │        │
│  │    • Results from any tool calls                         │        │
│  │                                                          │        │
│  │  First token shapes everything that follows.             │        │
│  │  Loop continues until: stop token, max length,           │        │
│  │  or completion signal.                                   │        │
│  └──────────────────────────────────────────────────────────┘        │
└──────────────────────────────────────╥───────────────────────────────┘
                                       ║
                                       ▼
┌──────────────────────────────────────────────────────────────────────┐
│  STAGE 11: OUTPUT CLASSIFIERS  (Ch. 21)                              │
│  The generated response is scanned before you see it.                │
│                                                                      │
│    ├── Toxicity check ─────── Did the response contain harmful text? │
│    ├── PII leakage check ──── Did the model expose private data?     │
│    ├── Copyright check ────── Did it reproduce copyrighted text?     │
│    ├── Policy compliance ──── Did it properly refuse when needed?    │
│    ├── Coherence check ────── Is the response garbled or repetitive? │
│    ├── Language check ─────── Does it match the input language?      │
│    └── Factual consistency ── Do claims match cited sources?         │
│                                                                      │
│  If a check fails ──► Response blocked, truncated, or regenerated    │
│  If all checks pass ──► Continue to Stage 12                         │
└──────────────────────────────────────╥───────────────────────────────┘
                                       ║
                                       ▼
┌──────────────────────────────────────────────────────────────────────┐
│  STAGE 12: REWARD MODEL SCORING  (Ch. 21, 22)                       │
│  A separate AI scores the response for quality.                      │
│                                                                      │
│  The reward model evaluates:                                         │
│    ├── Helpfulness ────── Does it actually answer the question?      │
│    ├── Safety ─────────── Is it appropriate and harmless?            │
│    ├── Accuracy ───────── Are the claims factually correct?          │
│    ├── Coherence ──────── Is it well-organized and clear?            │
│    └── Instruction       Does it follow the system prompt's          │
│       following ──────── formatting and behavioral rules?            │
│                                                                      │
│  In some systems, multiple responses are generated and the           │
│  highest-scoring one is selected ("best of N" approach).             │
└──────────────────────────────────────╥───────────────────────────────┘
                                       ║
                                       ▼
╔══════════════════════════════════════════════════════════════════════╗
║                                                                      ║
║   THE RESPONSE APPEARS ON YOUR SCREEN                                ║
║                                                                      ║
║   Total time elapsed: typically 1-30 seconds                         ║
║   Hidden processing steps: 12 stages                                 ║
║   Hidden text processed: potentially 10,000+ tokens you never see    ║
║   Models involved: potentially 20+ (main LLM + all classifiers)     ║
║                                                                      ║
╚══════════════════════════════════════╦═══════════════════════════════╝
                                       ║
                                       ▼
┌──────────────────────────────────────────────────────────────────────┐
│  AFTER THE RESPONSE: THE FEEDBACK LOOP  (Ch. 22)                     │
│  Your reaction shapes future AI.                                     │
│                                                                      │
│    ├── Thumbs up/down ──────► Becomes RLHF training signal           │
│    ├── Regeneration ────────► Indicates dissatisfaction               │
│    ├── Follow-up question ──► Suggests the response was incomplete   │
│    ├── Conversation flow ───► Patterns inform future training         │
│    └── A/B test data ───────► Compared against alternative versions  │
│                                                                      │
│  Every conversation is a tiny data point shaping the next model.     │
└──────────────────────────────────────────────────────────────────────┘
```

---

## Quick Summary: The 12 Stages

| Stage | What Happens | You Experience It As... |
|-------|-------------|----------------------|
| 1. Input Classifiers | Safety screening of your message | Instant (imperceptible) |
| 2. Intent Classification | System figures out what kind of request this is | Instant (imperceptible) |
| 3. System Prompt Assembly | Invisible instructions are combined with your message | Instant (imperceptible) |
| 4. Model Routing | The right AI brain is selected | Instant (imperceptible) |
| 5. Context & Memory Retrieval | Relevant documents and memories are gathered | Brief delay if RAG is involved |
| 6. Tokenization | Text is chopped into pieces | Instant (imperceptible) |
| 7. Embedding | Tokens become positions in meaning-space | Instant (imperceptible) |
| 8. Transformer Layers | 80+ layers of deep processing | The "thinking" pause |
| 9. Extended Thinking | Hidden scratchpad reasoning | The longer pause before complex answers |
| 10. Token Generation | Response is built one word at a time | Words streaming onto your screen |
| 11. Output Classifiers | Response is scanned for problems | Instant (imperceptible) |
| 12. Reward Model Scoring | Response quality is evaluated | Instant (imperceptible) |

---

*This map represents the complete pipeline as described throughout The Hidden Layers. Individual AI products may vary in which stages they implement, but the general architecture is consistent across all major LLM-based systems as of 2025.*
