# Appendix C: Quick Reference Prompt Patterns

A comprehensive cheat sheet of prompting strategies organized by task type. For each pattern, you will find when to use it, a template with placeholders, and an explanation of which hidden layer it leverages and why it works.

Keep this at your desk. Reach for the right pattern before reaching for the AI.

---

## 1. Writing and Editing

### The Audience-First Draft

**When to use:** You need to write anything for a specific reader -- emails, reports, articles, proposals.

**Template:**
```
Write a [format] for [audience]. They care most about [priority].
The tone should be [tone]. Keep it to [length].

Key points to include:
1. [Point 1]
2. [Point 2]
3. [Point 3]

Context: [Any background the reader needs to know]
```

**Why it works:** Specifying the audience activates the intent stack (Ch. 15) -- the model simultaneously optimizes for the reader's knowledge level, expectations, and emotional state. Without an audience, the model defaults to a generic "helpful assistant" voice.

---

### The Revision Surgeon

**When to use:** You have a draft that needs specific improvement, not a total rewrite.

**Template:**
```
Here is my draft:
[Paste your text]

Revise ONLY for [specific issue: clarity / conciseness / stronger verbs /
more persuasive tone / smoother transitions]. Do not change the overall
structure or meaning. Explain each significant change you make.
```

**Why it works:** Constraining the task activates task decomposition (Ch. 16) on a narrow scope. Without the "ONLY" constraint, the model decomposes broadly and may rewrite everything, losing your voice.

---

### The Style Match

**When to use:** You need the AI to write in a voice that matches an existing document, brand, or personal style.

**Template:**
```
Here is an example of the writing style I want you to match:
[Paste 2-3 paragraphs of example text]

Now write [your task] in this same style. Match the sentence length,
vocabulary level, tone, and formatting patterns.
```

**Why it works:** This is few-shot prompting (Ch. 23) applied to style. The attention mechanism (Ch. 9) identifies patterns in sentence structure, word choice, and rhythm from your example, then the autoregressive loop (Ch. 18) generates text that continues those patterns.

---

## 2. Research and Analysis

### The Multi-Source Synthesizer

**When to use:** You need to combine information from multiple angles into a coherent analysis.

**Template:**
```
I'm researching [topic]. Analyze it from these perspectives:
1. [Perspective 1, e.g., economic impact]
2. [Perspective 2, e.g., social implications]
3. [Perspective 3, e.g., historical precedent]

For each perspective, provide:
- The key argument
- The strongest evidence
- The main counterargument

Then synthesize: where do these perspectives agree, and where do they conflict?
```

**Why it works:** The explicit multi-perspective structure forces the extended thinking process (Ch. 12) to consider each angle independently before synthesizing. Without this structure, the model tends to blend perspectives into a single, muddled narrative.

---

### The Gap Finder

**When to use:** You want to identify what is missing from an analysis, plan, or argument.

**Template:**
```
Here is [a plan / an argument / an analysis]:
[Paste content]

Act as a critical reviewer. Identify:
1. What assumptions is this based on that could be wrong?
2. What important considerations are missing entirely?
3. What evidence would you need to verify the key claims?
4. Who would disagree with this, and what would their strongest objection be?
```

**Why it works:** This activates the model's self-critique and internal debate capabilities (Ch. 14). By asking it to play devil's advocate, you shift the generation trajectory away from agreement and toward critical analysis, leveraging the model's training on argumentative and evaluative text.

---

### The Source Evaluator

**When to use:** You need to assess the reliability or quality of information.

**Template:**
```
Evaluate the following claim: "[specific claim]"

Consider:
- What would make this claim true? What would make it false?
- What type of evidence would be most relevant?
- What are the common misconceptions about this topic?
- On a scale of high/medium/low, how confident should someone be
  in this claim, and why?

Important: If you are unsure or if this is outside your reliable
knowledge, say so clearly rather than speculating.
```

**Why it works:** The "if you are unsure, say so" instruction directly engages policy reasoning and confidence calibration (Ch. 14, 17). Without it, the model's default is to sound confident regardless of actual certainty. Explicitly permitting uncertainty produces more honest, calibrated responses.

---

## 3. Decision Making

### The Decision Matrix

**When to use:** You face a choice between multiple options and need structured evaluation.

**Template:**
```
I need to decide between:
A. [Option A]
B. [Option B]
C. [Option C]

My priorities (in order of importance):
1. [Most important factor]
2. [Second factor]
3. [Third factor]

My constraints:
- [Constraint 1]
- [Constraint 2]

For each option, evaluate it against each priority and constraint.
Then recommend which option best fits my situation and explain why.
Be honest about tradeoffs -- no option is perfect.
```

**Why it works:** Numbered priorities tell the intent stack (Ch. 15) exactly how to resolve tradeoffs. Without explicit priorities, the model guesses which factors matter most -- and often guesses wrong. The "no option is perfect" instruction prevents the model from overselling one choice.

---

### The Pre-Mortem

**When to use:** You have a plan and want to stress-test it before committing.

**Template:**
```
Here is my plan: [describe the plan]

Imagine it is [timeframe] from now and this plan has failed badly.
Write a realistic post-mortem explaining:
1. What went wrong
2. What warning signs we should have seen
3. Which assumptions turned out to be incorrect
4. What we should have done differently

Be specific and realistic, not catastrophic.
```

**Why it works:** By asking the model to generate from the perspective of future failure, you shift the autoregressive trajectory (Ch. 18) into analytical, cautionary territory. The first generated tokens frame the entire response as diagnostic rather than optimistic, which produces genuinely useful risk analysis.

---

### The Stakeholder Simulator

**When to use:** You need to anticipate how different people will react to a proposal or decision.

**Template:**
```
Here is a [proposal / decision / announcement]: [describe it]

Simulate the likely reaction from each of these stakeholders:
1. [Stakeholder 1, e.g., the finance team]
2. [Stakeholder 2, e.g., end users]
3. [Stakeholder 3, e.g., regulators]

For each, describe:
- Their likely first reaction
- Their main concern
- What would make them supportive
- What question they would ask first
```

**Why it works:** Role prompting (Ch. 23) combined with multi-perspective analysis. The attention mechanism activates different regions of the model's training data for each stakeholder role, producing genuinely different viewpoints rather than the same analysis repackaged.

---

## 4. Learning and Tutoring

### The Adaptive Explainer

**When to use:** You want to understand a concept and need the explanation matched to your level.

**Template:**
```
Explain [concept] to me. Here is what I already know:
[Describe your current understanding, even if it is rough or wrong]

Start from where my understanding is and build up.
Use analogies from [a domain you know well].
If I have any misconceptions, correct them gently.
After explaining, give me a question to test whether I understood it.
```

**Why it works:** Providing your current knowledge level gives the intent resolution system (Ch. 13) precise calibration. The model adjusts vocabulary, depth, and pacing to meet you where you are. Without this, it defaults to a generic explanation that may be too basic or too advanced.

---

### The Socratic Tutor

**When to use:** You want to learn by thinking, not just by reading.

**Template:**
```
I want to understand [topic]. Instead of explaining it directly,
guide me through it using questions. Ask me one question at a time.
After I answer, tell me what I got right, correct any mistakes,
and ask the next question that builds on my answer.

Start with the most fundamental question.
```

**Why it works:** This template restructures the autoregressive loop (Ch. 18) so the model generates questions rather than answers. Each response is short and targeted, keeping the conversation in a pedagogical pattern. The model's training on educational text, Socratic dialogues, and tutoring transcripts gets activated by this frame.

---

### The Concept Bridge

**When to use:** You understand concept A but not concept B, and they are related.

**Template:**
```
I understand [Concept A] well. I am trying to understand [Concept B].
Explain Concept B by showing how it relates to and differs from Concept A.
What is the same? What is different? Where does my knowledge of A
help me understand B, and where might it mislead me?
```

**Why it works:** This leverages the embedding and semantic space (Ch. 3) where related concepts occupy nearby regions. By anchoring the explanation in a concept the model knows you understand, the attention mechanism can trace meaningful connections rather than starting from scratch.

---

## 5. Code and Technical

### The Rubber Duck Debugger

**When to use:** Your code is not working and you need help finding the problem.

**Template:**
```
Here is my code:
[Paste code]

Expected behavior: [What it should do]
Actual behavior: [What it actually does]
What I have already tried: [List your debugging steps]

Walk through the code step by step. Identify where the actual behavior
diverges from the expected behavior and explain why.
```

**Why it works:** The "step by step" instruction activates chain-of-thought reasoning (Ch. 12), forcing the model to trace execution rather than pattern-match to a common bug. Listing what you have already tried prevents the model from wasting time on solutions you have already ruled out -- it removes those from the generation probability space.

---

### The Code Translator

**When to use:** You need to understand technical code but are not a programmer.

**Template:**
```
Here is a piece of code:
[Paste code]

Explain what this code does in plain English, as if you are explaining
it to an intelligent person who does not program. Use an analogy
to something in everyday life. Then list the 3 most important things
this code does, in order.
```

**Why it works:** The explicit "non-programmer" audience instruction shifts intent resolution (Ch. 13) away from technical jargon and toward explanatory patterns. The analogy request activates cross-domain connections in the semantic space (Ch. 3), producing explanations that stick.

---

### The Architecture Advisor

**When to use:** You are making a technical design decision and want to think through the options.

**Template:**
```
I am building [describe what you are building].

Requirements:
- [Requirement 1]
- [Requirement 2]
- [Requirement 3]

I am considering these approaches:
A. [Approach A]
B. [Approach B]

For each approach, analyze:
- How well it meets each requirement
- Where it would struggle as the project grows
- What hidden costs or complexities it introduces
- What I might regret choosing it in 6 months

Then give me your recommendation with honest caveats.
```

**Why it works:** Structured requirements activate task decomposition (Ch. 16) so each constraint is evaluated systematically. The "what I might regret" framing shifts the generation trajectory toward long-term thinking rather than quick-fix recommendations.

---

## 6. Data Analysis

### The Pattern Spotter

**When to use:** You have data and want to identify trends, outliers, or patterns.

**Template:**
```
Here is my data:
[Paste data or describe the dataset]

Analyze this data and identify:
1. The 3 most significant patterns or trends
2. Any notable outliers or anomalies
3. What might be causing each pattern
4. What additional data would help confirm or disprove these patterns

Present each finding with: the pattern, the evidence, and your
confidence level (high/medium/low).
```

**Why it works:** The confidence-level request engages calibration (Ch. 14), producing more honest assessments. The "additional data" question forces the extended thinking process (Ch. 12) to evaluate the limits of the analysis rather than presenting findings as definitive.

---

### The Chart Narrator

**When to use:** You need to turn data into a narrative for a presentation or report.

**Template:**
```
Here is [data / chart description / key findings]:
[Paste data or describe findings]

Write a narrative summary for [audience]. Lead with the most
important finding. Explain what it means for [their specific concern].
Use concrete numbers but make them meaningful -- don't just state
the number, explain why it matters.

Keep it to [length] and end with one clear takeaway.
```

**Why it works:** The "lead with the most important finding" instruction shapes the autoregressive opening (Ch. 18), which cascades through the entire response. Specifying the audience's concern activates the right region of the intent stack (Ch. 15) so the narrative is relevant, not just accurate.

---

### The Assumption Auditor

**When to use:** You need to validate the methodology or reasoning behind a dataset or analysis.

**Template:**
```
Here is an analysis and its conclusions:
[Paste or describe the analysis]

Audit this analysis. Specifically:
1. What assumptions does this analysis make? List them explicitly.
2. Which assumptions are reasonable and which are questionable?
3. How would the conclusions change if the most questionable
   assumptions were wrong?
4. What alternative explanations exist for the same data?
```

**Why it works:** The internal debate mechanism (Ch. 14) is activated by the adversarial framing. The model generates, self-critiques, and refines, producing analysis that is more rigorous than a simple "summarize this data" request.

---

## 7. Strategic Planning

### The Roadmap Builder

**When to use:** You need to break a large goal into phases and milestones.

**Template:**
```
My goal: [Describe the end state you want to reach]
My current situation: [Where you are now]
My constraints: [Time, budget, resources, etc.]
My biggest risks: [What could go wrong]

Create a phased roadmap to get from my current situation to my goal.
For each phase:
- What to accomplish
- Key milestones and how to measure success
- Dependencies (what must happen first)
- Estimated timeline
- The biggest risk in this phase and how to mitigate it

Be realistic about timelines. Assume things will take longer
than expected.
```

**Why it works:** Providing constraints and risks activates the full extended thinking process (Ch. 12), which checks plans against limitations rather than generating idealized roadmaps. The "be realistic" instruction shifts the policy reasoning (Ch. 17) toward honest assessment over optimistic encouragement.

---

### The Competitive Landscape

**When to use:** You need to understand how you compare to alternatives or competitors.

**Template:**
```
I am [describe your situation or offering].

My main competitors / alternatives are:
1. [Competitor 1]
2. [Competitor 2]
3. [Competitor 3]

For each competitor, analyze:
- Their core strength (what they do better than me)
- Their core weakness (where I have an advantage)
- Who they serve best (their ideal customer)
- The trend: are they getting stronger or weaker, and why?

Then identify: what is the gap in the market that none of us
are serving well?
```

**Why it works:** The multi-entity comparison structure forces task decomposition (Ch. 16) to handle each competitor independently before synthesizing. The final "gap" question activates reasoning in the deep Transformer layers (Ch. 11) that goes beyond simple comparison into genuine strategic insight.

---

### The Scenario Planner

**When to use:** You need to prepare for multiple possible futures.

**Template:**
```
Current situation: [Describe the present state]

Develop 3 plausible scenarios for what happens over the next [timeframe]:
1. Optimistic scenario (things go better than expected)
2. Realistic scenario (roughly what we'd expect)
3. Pessimistic scenario (significant challenges emerge)

For each scenario:
- What would cause it to happen
- What early signals would tell us this scenario is unfolding
- What we should do now to prepare for it
- What we should do if it starts happening

Make each scenario specific and plausible, not generic.
```

**Why it works:** The three-scenario structure gives the autoregressive loop (Ch. 18) three distinct generation trajectories. The "early signals" and "prepare now" requirements force the extended thinking (Ch. 12) past vague speculation into actionable, concrete planning.

---

## 8. Creative Work

### The Creative Brief Expander

**When to use:** You have a vague creative idea and want to develop it into something concrete.

**Template:**
```
I have a creative idea: [Describe the seed of your idea]

Help me develop this by exploring:
1. Three different directions this idea could go
2. For each direction: the tone, the central conflict or tension,
   and what makes it compelling
3. Which direction has the most potential for [your goal:
   emotional impact / originality / audience engagement]
4. The first three steps to bring that direction to life

Don't play it safe. Push the idea somewhere unexpected.
```

**Why it works:** "Don't play it safe" explicitly raises the temperature of the generation (Ch. 19) conceptually -- the model is more likely to explore lower-probability, more creative token paths. The structured exploration prevents creative chaos by giving the task decomposition system (Ch. 16) clear phases to work through.

---

### The Perspective Shifter

**When to use:** Your creative work feels flat and you need a fresh angle.

**Template:**
```
Here is my [story / essay / pitch / concept]:
[Paste your work]

Now reimagine this from a completely different angle:
- What if the main point was the opposite of what I wrote?
- What if the most minor detail was actually the most important?
- What if this was told from the perspective of [an unexpected voice]?

Give me 3 radically different takes. For each, write the opening
paragraph so I can feel the difference.
```

**Why it works:** Asking for "the opposite" or "unexpected" perspectives overrides the model's tendency toward the most probable continuation (Ch. 18). By generating opening paragraphs, each take establishes a distinct autoregressive trajectory that you can evaluate and choose from.

---

### The World Builder

**When to use:** You are creating a fictional setting, game, or scenario and need depth and consistency.

**Template:**
```
I am building [describe the creative world / setting / scenario].

What I have so far:
[Describe what you've already decided]

Help me deepen this world by developing:
1. Three details I haven't thought of that would make it feel real
2. One internal contradiction or tension that creates interest
3. How an everyday person in this world would describe their daily life
4. One thing about this world that would surprise a visitor

Stay consistent with what I've already established.
Do not change anything I've decided -- only add.
```

**Why it works:** The "stay consistent" and "only add" constraints activate the constraint heads in the attention mechanism (Ch. 10), which track rules and requirements throughout generation. The everyday-life question grounds the creative output in concrete detail, pulling the model away from abstract world-building toward vivid specifics.

---

## 9. General Improvement Patterns

These patterns can be applied to almost any prompt to improve the quality of AI responses. Each one leverages a specific hidden layer.

---

### Step-by-Step Reasoning

**When to use:** Any task requiring logic, analysis, or multi-step thinking.

**Template addition:**
```
Think through this step by step before giving your final answer.
```

**Why it works:** Activates chain-of-thought and extended thinking (Ch. 12). Without this, the model may jump to conclusions. With it, the model reasons through intermediate steps, catching errors and producing more accurate results. This single phrase boosted accuracy by 40-60 percentage points on some reasoning benchmarks.

---

### Role Assignment

**When to use:** You want expertise, a specific tone, or a particular perspective.

**Template addition:**
```
You are a [specific role] with [years] of experience in [domain].
Your specialty is [narrow focus]. Respond as this expert would.
```

**Why it works:** Role prompting shifts the probability distribution for token generation (Ch. 18, 19) toward the language patterns, vocabulary, and reasoning style associated with that role in the training data. A "senior financial analyst" produces different output than a "creative director," even for the same question, because the attention mechanism activates different knowledge regions.

---

### Few-Shot Examples

**When to use:** You want output that follows a very specific pattern or format.

**Template:**
```
Here are examples of what I want:

Input: [Example input 1]
Output: [Example output 1]

Input: [Example input 2]
Output: [Example output 2]

Now do the same for:
Input: [Your actual input]
Output:
```

**Why it works:** The attention mechanism (Ch. 9) identifies the pattern across your examples and applies it to the new input. This is more reliable than describing the pattern in words because you are showing the model exactly what "good" looks like, giving the autoregressive loop a concrete template to follow.

---

### Chain-of-Thought Prompting

**When to use:** Complex reasoning, math, logic puzzles, or any task where showing work matters.

**Template addition:**
```
Work through this problem step by step. For each step:
1. State what you're doing
2. Do it
3. Check whether the result makes sense before moving on
```

**Why it works:** This structured chain-of-thought (Ch. 12) not only activates reasoning but builds in self-checking at each stage. The model is less likely to make an error in step 3 and carry it silently through steps 4-10 because it is forced to verify before continuing.

---

### Explicit Priority Setting

**When to use:** Anytime you want to control the tradeoff between competing goals.

**Template addition:**
```
Prioritize [accuracy over speed / brevity over completeness /
creativity over correctness / practical advice over comprehensive theory].
If you must sacrifice one for the other, always choose [your priority].
```

**Why it works:** Directly configures the intent stack (Ch. 15). Without this instruction, the model makes its own tradeoff decisions -- often defaulting to a safe, balanced middle ground that satisfies nobody perfectly. Explicit priorities remove ambiguity from the intent resolution process (Ch. 13).

---

### Output Format Control

**When to use:** You need a specific structure, length, or format.

**Template addition:**
```
Format your response as: [bullet points / numbered list / table /
single paragraph / JSON / email format]
Length: [specific word count or constraint like "fit on one page"]
Include: [headers / examples / citations]
Do not include: [caveats / introductions / summaries]
```

**Why it works:** Format instructions constrain the autoregressive loop from the very first token (Ch. 18). When the model generates "1." as its first character, the entire response follows a numbered-list trajectory. These constraints are processed by the constraint-tracking attention heads (Ch. 10) throughout generation.

---

### The Self-Critique Loop

**When to use:** High-stakes responses where quality matters more than speed.

**Template addition:**
```
After generating your response, review it and ask yourself:
1. Did I actually answer the question that was asked?
2. Is anything I said incorrect or misleading?
3. What is the weakest part of my response?
4. If I had to cut this in half, what would I remove?

Then give me the improved version.
```

**Why it works:** This makes the internal debate (Ch. 14) explicit and visible. The model generates a first draft, evaluates it against specific criteria, and then produces a revised version. The revision benefits from everything in the first draft plus the critique -- it has strictly more context to work with.

---

### Context Front-Loading

**When to use:** Always. Put the most important information first.

**Template structure:**
```
[Your role / the AI's role]
[The most critical context]
[The specific task]
[Constraints and format]
[Examples if needed]
[The actual question / request -- last]
```

**Why it works:** Positional attention heads (Ch. 10) give extra weight to text that appears early in the prompt. The system prompt already occupies the earliest positions, but within your message, the attention mechanism processes initial context more thoroughly. Burying the most important information at the end of a long prompt means it competes with more prominently positioned text.

---

### The Anti-Hallucination Shield

**When to use:** Factual questions where accuracy is critical.

**Template addition:**
```
Only include information you are confident about. If you are unsure
about any specific fact, date, number, or name, explicitly say
"I'm not certain about this" rather than guessing. It is better
to be incomplete and accurate than comprehensive and wrong.
```

**Why it works:** This directly modifies policy reasoning (Ch. 17) by giving explicit permission to be uncertain. The model's default training pushes it toward confident, complete answers. This instruction overrides that tendency, shifting the probability distribution away from fabrication and toward honest qualification.

---

## Master Template: The Complete Prompt

When the stakes are high, combine the patterns above into one comprehensive prompt.

```
[ROLE] You are a [specific expert role].

[CONTEXT] Here is the situation: [background information]

[TASK] I need you to [specific task].

[PRIORITIES] Prioritize [X] over [Y]. If uncertain, say so.

[FORMAT] Format the response as [specific format].
Keep it to [length constraint].

[CONSTRAINTS]
- Do: [what to include]
- Don't: [what to exclude]

[EXAMPLES] Here is an example of what good output looks like:
[Example]

[REASONING] Think through this step by step before finalizing
your response.
```

**Why the order matters:** This structure mirrors the natural processing sequence of the hidden layers. Role sets the generation context. Background activates relevant knowledge. The task defines the objective. Priorities configure the intent stack. Format constrains the output. Examples calibrate quality. And the reasoning instruction activates the scratchpad. Each element feeds into the next, producing a response that is focused, accurate, and structured exactly as you need it.

---

*These patterns are derived from the hidden-layer architecture described throughout The Hidden Layers. For the full explanation of why each technique works, see the referenced chapters.*
