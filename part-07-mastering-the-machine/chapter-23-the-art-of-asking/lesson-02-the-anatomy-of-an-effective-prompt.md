# Lesson 2: The Anatomy of an Effective Prompt

## The Six Ingredients of a Great Order

Every great dish at a great restaurant has essential components. Not just any ingredients thrown together, but the right elements in the right proportions: protein, acid, fat, salt, heat, and something unexpected. Miss one, and the dish is flat. Include them all, and every bite works.

Effective prompts work the same way. After studying thousands of interactions -- what works, what fails, and why -- a clear anatomy emerges. The best prompts, across every domain and task, tend to include six components. Not every prompt needs all six. A simple factual question might only need two. But for any task where quality matters, these six ingredients are your recipe.

Let us name them: **Role, Context, Task, Constraints, Format, and Examples.**

And let us understand why each one exists -- not as arbitrary best practice, but as a component that feeds a specific hidden layer you now understand.

## Ingredient 1: Role

**What it is:** An instruction that tells the model who to "be" when generating the response.

**Why it works (the hidden layer connection):** When you assign a role, you are doing something powerful to the model's probability distributions. Remember, the model generates text by predicting what tokens are most likely to come next given the context. When you write "You are an experienced UX hiring manager," you shift the entire probability landscape. The tokens that are likely after that framing are different from the tokens that are likely after "You are a friendly chatbot." The vocabulary changes. The level of detail changes. The assumptions change. The tone changes.

It is like the difference between asking a random person on the street for restaurant advice versus asking a food critic. The food critic does not just know more -- they communicate differently, prioritize different things, and frame their recommendations from a fundamentally different perspective.

**The analogy:** A role assignment is like telling an actor their character before the scene begins. The same actor playing a detective will walk, talk, and observe differently than when playing a poet. The underlying talent is the same, but the performance is shaped by the character brief.

**Good role assignments:**
- "You are a senior data analyst who specializes in presenting complex findings to non-technical executives."
- "You are an experienced career coach who has helped 50+ professionals transition from finance to tech."
- "Act as a skeptical but fair editor reviewing my draft for logical gaps."

**Weak role assignments:**
- "You are a helpful assistant." (Too generic -- this is basically the default.)
- "You are the world's greatest genius." (Too vague -- does not point to specific patterns.)
- "You are Albert Einstein." (Activates Einstein-associated patterns but might produce responses that mimic his historical voice rather than being genuinely useful.)

> **"This Is Why..."**
> This is why adding "You are an expert in [topic]" to your prompts often improves response quality. It is not flattery. It is not magic. You are activating a specific region of the model's learned patterns -- the patterns associated with expert-level discourse in that domain. The model has seen thousands of examples of how experts communicate, and the role instruction tells it to generate from that distribution rather than from the generic "helpful answer" distribution.

## Ingredient 2: Context

**What it is:** Background information the model needs to generate a relevant response. Your situation, your constraints, your audience, what you have already tried, what you already know.

**Why it works (the hidden layer connection):** Context feeds the attention mechanism directly. Every piece of context you provide becomes a node in the web of relationships the model builds. More relevant context means more connections for the attention heads to work with, which means a response more finely tuned to your actual situation.

Think of context as giving the chef information about the diner. "Table four has a nut allergy, prefers their steak medium-rare, just came from a long flight, and this is their anniversary dinner." That information completely changes what the chef prepares, even if the order itself is simple.

**What to include as context:**
- Your background and expertise level
- The audience for the output (who will read/use the result)
- What you have already done or tried
- Relevant constraints (time, budget, tools available)
- What you already know (so the model does not waste time on basics)

**Example -- career change context:**
"I am a 35-year-old CPA with 8 years in corporate accounting at a Fortune 500 company. I have strong skills in data analysis (Excel, SQL), stakeholder communication, and process documentation. I have 6 months of savings and a supportive spouse. I have already taken one online UX course (Google UX Design Certificate) and completed two personal projects. I am applying for junior UX designer roles."

This context paragraph eliminates dozens of assumptions the model would otherwise have to make. Without it, the model might spend half its response explaining what UX design is or suggesting you start with an introductory course you have already completed.

> **"Pro Tip"**
> There is such a thing as too much context, but the threshold is much higher than most people think. For a complex task, providing 200-300 words of context is not excessive -- it is helpful. The model's attention mechanism is designed to handle long inputs. What hurts is *irrelevant* context -- information that has nothing to do with the task, which introduces noise. The rule: be generous with relevant context, ruthless about cutting irrelevant details.

## Ingredient 3: Task

**What it is:** The specific thing you want the model to do. The verb. The action.

**Why it works (the hidden layer connection):** The task statement is what the model's intent resolution system locks onto first. It answers the most fundamental question: "What is the user asking me to do?" A clear task statement means clean intent resolution. An ambiguous task statement means the model has to guess -- and guessing is where things go wrong.

**The key to a good task statement:** Be specific about the *action* and the *output.*

**Weak task statements:**
- "Help me with my career change." (What kind of help? A plan? Encouragement? A resume review? Research?)
- "Tell me about UX design." (Tell you what? History? Definition? How to learn it? Salary data?)

**Strong task statements:**
- "Create a week-by-week study plan for the next 8 weeks to prepare me for the Google UX Design Professional Certificate."
- "Review my resume and suggest five specific changes that reframe my accounting experience as UX-relevant skills."
- "Compare three UX bootcamps (General Assembly, Springboard, Designlab) on cost, time commitment, job placement rate, and curriculum quality."

Notice how each strong task statement contains a specific verb (create, review, compare) and a specific output (study plan, five changes, comparison table). The model knows exactly what to decompose and execute.

## Ingredient 4: Constraints

**What it is:** The boundaries, rules, and limitations the response must respect.

**Why it works (the hidden layer connection):** Constraints directly feed the constraint-tracking attention heads we discussed in Chapter 10 and the intent stack priorities from Chapter 15. When you specify constraints, you are programming the model's internal priority system. Without them, the model resolves tradeoffs using its default training, which may not match your preferences.

**Types of constraints:**
- **Length:** "Keep this under 300 words." / "Be comprehensive -- length is not a concern."
- **Tone:** "Professional and formal." / "Casual and conversational."
- **Scope:** "Focus only on free resources." / "Include both free and paid options."
- **Exclusions:** "Do not suggest going back to school full-time." / "Skip anything that requires coding."
- **Priorities:** "Prioritize speed over thoroughness." / "Accuracy matters more than completeness."
- **Audience:** "This will be read by someone with no design background."

**Example -- constraints in our career change prompt:**
"Constraints: I cannot quit my current job for at least 4 months. Budget for education is $2,000 maximum. I am not willing to relocate. I need options that work around a 9-to-5 schedule. Do not recommend full-time bootcamps."

Each constraint eliminates a category of responses the model might otherwise generate. Without them, you might get a beautifully detailed plan that involves quitting your job immediately and attending a $15,000 full-time bootcamp in another city -- technically good advice, but useless for your situation.

> **"Behind The Curtain"**
> Researchers have found that constraints are among the most reliably followed elements in a prompt. The model's attention mechanism gives high weight to negation words ("do not," "never," "avoid") and boundary words ("only," "maximum," "no more than"). This is because constraints appeared frequently and prominently in the model's training data -- in instructions, guidelines, and rules. The model has learned that constraint language carries high importance. Use this to your advantage.

## Ingredient 5: Format

**What it is:** An instruction for how you want the output structured.

**Why it works (the hidden layer connection):** Format instructions leverage the autoregressive generation mechanism from Chapter 18. When you specify a format, you are constraining the structure of the model's first generated tokens, which then shape everything that follows. "Give me a numbered list" means the model generates "1." early, locking it into list-generation mode. "Write this as a narrative" means the opening tokens will be prose-style, pulling the rest of the response along.

**Common format specifications:**
- "Respond in bullet points."
- "Use a table with columns for: Option, Cost, Time, Pros, Cons."
- "Give me three short paragraphs: the problem, the solution, the next step."
- "Structure this as: Executive Summary (2 sentences), Key Findings (bullet points), Detailed Analysis (paragraphs), Recommendations (numbered list)."
- "Write this as an email I can send directly."

**Why format matters more than you think:** The format of a response is not just cosmetic. It changes the *content*. A bulleted list forces the model to distill ideas into concise points. A narrative paragraph invites elaboration and connection. A table forces structured comparison. By choosing the format, you are choosing the type of thinking the model does.

**Example:**
Same task -- "summarize the pros and cons of leaving accounting for UX design" -- but with different format instructions:

Format: "Give me a simple pros and cons list" -- produces a clean, quick comparison.
Format: "Write this as a persuasive memo to my spouse" -- produces an argument with emotional awareness and practical details.
Format: "Create a decision matrix with weighted criteria" -- produces an analytical framework with scoring.

Same content. Completely different outputs. The format instruction is not decoration -- it is a thinking instruction.

## Ingredient 6: Examples

**What it is:** One or more samples of the output you want, showing the model exactly what "good" looks like.

**Why it works (the hidden layer connection):** Examples are the most direct way to program the model's generation patterns. They work because of the core mechanism we covered in Chapter 2 -- the model generates text that is statistically consistent with the patterns in its context. When you provide an example in the prompt, that example becomes part of the context. The model's prediction engine will generate text that follows the same patterns.

This is called **few-shot prompting**, and we will explore it in depth in the next lesson. For now, understand the principle: showing is more powerful than telling.

**Example:**
"Convert my accounting skills into UX-relevant descriptions. Here's the format I want:

Accounting skill: Financial data analysis
UX translation: Quantitative user research -- experienced in analyzing large datasets to identify patterns, trends, and actionable insights. Fluent in translating numbers into stakeholder-friendly narratives.

Now do the same for:
- Budget forecasting and planning
- Stakeholder presentation and reporting
- Process documentation and compliance
- Risk assessment and mitigation"

The example does what no amount of description could do as efficiently: it shows the exact output pattern, tone, level of detail, and transformation logic the model should follow. One example is worth a hundred words of instruction.

> **"Try This Now"**
> Take a task you regularly ask AI to help with. Write the prompt as you normally would. Then rewrite it using all six ingredients: Role, Context, Task, Constraints, Format, and one Example. Compare the two responses. The difference is usually dramatic -- not because you wrote more words, but because each ingredient reduced a specific type of guessing the model had to do.

## Assembling the Ingredients: A Complete Example

Let us put all six ingredients together for our running example. Watch how each ingredient does specific work.

---

**[Role]** You are an experienced career transition coach who has helped dozens of professionals move from finance and accounting into UX and product design roles. You give honest, specific, actionable advice -- never vague platitudes.

**[Context]** I am a 35-year-old CPA with 8 years at a Fortune 500 company. My strengths: data analysis (Excel, SQL, Tableau), stakeholder presentations, process documentation, and detail-oriented work. I completed the Google UX Design Certificate and built two personal UX case studies. I have 6 months of savings and a supportive partner. I am applying for junior to mid-level UX designer roles.

**[Task]** Create a 90-day action plan to make me a competitive UX design job candidate. For each month, identify the top three priorities, specific deliverables, and one potential obstacle with a mitigation strategy.

**[Constraints]** I am working full-time for the next 60 days, so activities must fit evenings and weekends (roughly 15 hours per week). Budget: $1,500 total. Do not recommend full-time bootcamps or relocation. Focus on strategies that leverage my accounting background as a competitive advantage rather than treating it as irrelevant.

**[Format]** Structure as:
- Month 1 header, then three priorities as sub-sections, each with deliverables and obstacle/mitigation
- Month 2, same structure
- Month 3, same structure
- Final section: "Your Competitive Edge" -- how to position my accounting background in interviews

**[Example of the tone and specificity I want]**
"Month 1, Priority 1: Build a case study that proves you can do UX research, not just read about it. Deliverable: A complete case study redesigning your company's expense reporting process, including user interviews (ask 5 coworkers), journey mapping, wireframes, and a prototype in Figma. Obstacle: Imposter syndrome -- you will feel like this is not 'real' UX work. Mitigation: It absolutely is. Hiring managers care about process and thinking, not whether you had a fancy client."

---

That is a prompt assembled by someone who understands the hidden layers. It is not long for the sake of being long. It is precise, structured, and designed to work with the model's processing pipeline rather than against it.

## The Minimum Viable Prompt

Not every interaction needs all six ingredients. Asking "What's the capital of France?" does not require a role assignment and three examples. The six-ingredient framework is for when the task matters and the quality of the output matters.

Here is a quick guide for calibrating your effort:

**Simple factual question** -- Task only: "What year was the Eiffel Tower built?"
**Moderate task** -- Task + Context + Constraints: "Summarize this article for a non-technical audience in under 200 words."
**Important task** -- All six ingredients: Use the full framework when you are writing something you will actually use, making a decision, or working on a project.

The goal is not to write long prompts. The goal is to write *complete* prompts -- ones that give the model everything it needs to produce the response you actually want, without wasting your time on information the model does not need.

> **"This Is Why..."**
> This is why copy-pasting "prompt templates" from the internet often produces mediocre results. A template gives you format but not substance. The Context ingredient -- your specific situation, background, and constraints -- is what transforms a generic template into a prompt that produces genuinely useful output. The template is the recipe. Your context is the fresh ingredients. You need both.

---

You now have the anatomy of an effective prompt. In the next lesson, we will dive deep into the most powerful single ingredient -- examples -- and the technique called few-shot prompting that turns them into a precision tool.
