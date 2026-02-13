# Lesson 2: Research, Analysis, and Decision-Making

## When You Need the AI to Think, Not Just Write

Writing tasks ask the model to produce polished output. Research and analysis tasks ask the model to do something different: organize information, identify patterns, evaluate evidence, compare options, and surface insights you might have missed. These tasks activate the deeper layers of the model's processing -- the reasoning circuits from Chapter 12, the self-critique mechanisms from Chapter 14, and the complex task decomposition from Chapter 16.

The patterns in this lesson are designed to leverage those deeper layers deliberately. Each one is structured to push the model beyond surface-level responses and into the kind of structured thinking that produces genuinely useful analysis.

## Pattern 1: The Research Synthesizer

**The task:** Gather and organize information about a topic, identifying key themes, contradictions, and gaps.

**Which hidden layers this activates:** The model's knowledge retrieval across its training data, attention patterns that track thematic connections across large amounts of information, and the reasoning layers that identify patterns and contradictions.

**The pattern:**

"I need a comprehensive research briefing on [topic]. Structure it as:

1. **Key Facts** -- The most important established facts (5-7 bullet points)
2. **Major Perspectives** -- The 3-4 main viewpoints or schools of thought on this topic, with the strongest argument for each
3. **Areas of Agreement** -- What do most experts agree on?
4. **Areas of Debate** -- Where do experts disagree, and why?
5. **What I Should Be Cautious About** -- Common misconceptions, outdated information, or areas where your training data might not be current
6. **Further Questions** -- Based on this briefing, what follow-up questions would help me deepen my understanding?

Context: [why you are researching this, your current level of knowledge, what you plan to do with the information]."

**Why the "What I Should Be Cautious About" section matters:** This activates the model's self-awareness about its own limitations. Remember from Chapter 14 that the model can evaluate its own confidence levels. By explicitly asking it to flag areas of uncertainty, you are giving the self-critique mechanism a dedicated space to operate. Without this section, the model's uncertainty is still there -- it is just hidden, blended into responses that sound equally confident whether they are reliable or not.

**Example -- researching the UX design job market:**

"I need a research briefing on the current state of the UX design job market for career changers. I am a 35-year-old accountant considering this transition and I need honest, unvarnished information to make a good decision.

Include the six sections above. For 'What I Should Be Cautious About,' specifically flag any information that might have changed since your training data was collected. For 'Further Questions,' suggest questions I could ask actual UX professionals to validate your briefing."

> **"This Is Why..."**
> This is why asking the AI "tell me about X" produces a bland overview, while a structured research prompt produces genuine insight. The unstructured request lets the model default to the most generic, consensus-level response in its training data. The structured prompt forces it to engage multiple reasoning circuits: compare perspectives, identify tensions, assess its own reliability, and generate actionable follow-up paths. You are not getting more information -- you are getting better-organized and more honestly presented information.

## Pattern 2: The Comparison Framework

**The task:** Evaluate multiple options against each other to support a decision.

**Which hidden layers this activates:** The intent stack (managing tradeoffs between criteria), constraint tracking (ensuring all options are evaluated consistently), and the reasoning layers that hold multiple entities in working memory simultaneously.

**The pattern:**

"Compare these [number] options: [list them].

Evaluate each on these criteria (in order of importance to me):
1. [Most important criterion] -- weight: HIGH
2. [Second criterion] -- weight: HIGH
3. [Third criterion] -- weight: MEDIUM
4. [Fourth criterion] -- weight: LOW

For each option, rate it as Strong, Adequate, or Weak on each criterion, with a one-sentence justification.

Then give me:
- A summary table
- Your overall recommendation with reasoning
- The scenario where each option would be the best choice (because context matters)
- What information I should verify before committing"

**Why weighted criteria matter:** Without explicit weights, the model resolves tradeoffs using its default training -- which tends toward balanced, "on the one hand / on the other hand" responses that do not help you decide. By weighting criteria, you program the intent stack to prioritize what you actually care about.

**Example -- comparing UX learning paths:**

"Compare these three UX education options for a career changer with a full-time accounting job:
A) Google UX Design Certificate (Coursera, self-paced)
B) Springboard UX Career Track (mentor-based, 6 months)
C) General Assembly UX Immersive (full-time bootcamp, 12 weeks)

Criteria in order of importance:
1. Compatibility with full-time employment -- weight: HIGH
2. Portfolio quality at completion -- weight: HIGH
3. Job placement support and outcomes -- weight: MEDIUM
4. Total cost -- weight: MEDIUM
5. Industry recognition -- weight: LOW

Follow the evaluation format above. Be specific about what 'Strong' and 'Weak' mean for each criterion, not vague."

## Pattern 3: The Devil's Advocate

**The task:** Stress-test an idea, plan, or decision by finding its weaknesses.

**Which hidden layers this activates:** The self-critique mechanism from Chapter 14, forced into an adversarial mode rather than a supportive one. Also activates the model's exposure to critical analysis patterns in its training data -- debate formats, editorial critiques, peer reviews.

**The pattern:**

"I am considering [decision/plan/idea]. I have already decided I want to do this, so I do not need encouragement. What I need is for you to be my toughest critic.

1. What are the 5 biggest risks or failure modes?
2. What am I probably not seeing because I am too close to the decision?
3. What assumptions am I making that might be wrong?
4. Who would argue against this, and what would their strongest argument be?
5. What would need to be true for this to go badly wrong?

Be specific and concrete. 'It might not work out' is not useful feedback. 'The average career changer takes 14 months to land their first UX role, not the 9 months you are planning for, based on bootcamp placement data' -- that is useful feedback."

**Why this pattern requires explicit instructions to be critical:** The model's default training optimizes for helpfulness, which often manifests as agreement and encouragement. The RLHF training from Chapter 22 taught the model that users prefer supportive responses. To get genuine critical analysis, you must explicitly override this default by making it clear that critical feedback is what you want and that agreement would be unhelpful.

> **"Pro Tip"**
> The Devil's Advocate pattern is most powerful when combined with the Perspective Shift iteration pattern from Chapter 23. After getting the critical analysis, follow up with: "Now be my strategic advisor. Given all these risks, which ones are dealbreakers and which are manageable? For the manageable ones, give me a mitigation strategy." This two-step approach gives you criticism followed by actionable solutions -- the most useful combination for real decision-making.

## Pattern 4: The Decision Matrix

**The task:** Make a structured decision when you are torn between options or overwhelmed by factors.

**Which hidden layers this activates:** Task decomposition (breaking a complex decision into evaluable components), the reasoning layers (holding multiple factors in working memory), and the intent stack (resolving tradeoffs explicitly).

**The pattern:**

"Help me make a decision about [topic]. Here is my situation: [context].

I am torn because: [describe the tension -- what pulls you toward each option].

Walk me through this decision using this framework:
1. What are the actual options? (List them clearly, including 'do nothing')
2. What are the decision criteria that matter most to me? (Infer from my context, but check with me)
3. For each option, what is the best-case outcome and the worst-case outcome?
4. What is the reversibility of each option? (Can I undo it if it does not work?)
5. What would I need to know to make this decision with confidence, and how could I find that information?
6. Based on all of the above, what do you recommend and why?"

**Why including "do nothing" matters:** The model's training data is full of advice-giving patterns that bias toward action. By explicitly including "do nothing" as an option, you force the model to evaluate the status quo on its merits rather than assuming that change is always better. Sometimes the best decision is to wait, and the model needs permission to say so.

**Example:**

"Help me decide whether to accept a junior UX designer position that pays $55K, versus staying in my accounting role that pays $85K. My situation: 35, married, 6 months savings, spouse earns $70K. I have been offered the UX role at a mid-size tech company. The accounting role is stable but I find it unfulfilling.

I am torn because: the financial hit is real and scary, but I do not want to be doing accounting at 45 and regretting that I never made the leap.

Use the six-step framework above. Be specific with numbers where possible."

## Pattern 5: The Brainstorming Facilitator

**The task:** Generate ideas, possibilities, and creative solutions.

**Which hidden layers this activates:** Higher temperature sampling (the model explores less probable but potentially more interesting token paths), the vast breadth of the training data (connecting concepts from different domains), and the autoregressive generation (each idea in the list influences the next).

**The pattern:**

"Brainstorm [number] ideas for [topic]. Context: [your situation and goals].

Rules:
- The first 5 should be conventional and practical
- The next 5 should be creative and unconventional
- The last 3 should be wild and unexpected -- things I would never think of

For each idea, give it a name and one sentence explaining why it might work.

After the list, identify which ideas could be combined for even stronger approaches."

**Why the three-tier structure works:** The model's default brainstorming tends toward a homogeneous list of medium-quality ideas -- all reasonable, none remarkable. The three-tier structure forces the model to shift its generation parameters across the list. The "conventional" tier comes from high-probability token paths. The "creative" tier pushes toward medium-probability paths. The "wild" tier forces the model into low-probability territory where the genuinely surprising ideas live.

**The combination instruction at the end is also deliberate:** It activates a second pass of reasoning where the model looks for connections between ideas it generated independently -- often producing insights that neither tier would have generated alone.

> **"Try This Now"**
> Use the Brainstorming Facilitator pattern for a problem you are currently facing -- professional or personal. Pay special attention to the "wild and unexpected" tier. You will probably dismiss most of those ideas immediately, but at least one will contain a seed of something genuinely useful that you would not have considered. That is the value of pushing the model into low-probability territory.

## Pattern 6: The Pros/Cons with Hidden Dimensions

**The task:** Evaluate the advantages and disadvantages of a decision, but going beyond the obvious.

**Which hidden layers this activates:** The reasoning layers that identify non-obvious connections, the model's broad training data (which includes perspectives from many different domains and life situations), and the self-critique mechanism (evaluating its own analysis for completeness).

**The pattern:**

"Give me a pros and cons analysis of [decision], but go beyond the obvious. Structure it as:

**Obvious Pros** (the benefits everyone mentions)
**Hidden Pros** (benefits that are real but rarely discussed)
**Obvious Cons** (the risks everyone mentions)
**Hidden Cons** (risks that people discover only after committing)
**The Question Nobody Asks** (the one consideration that changes everything if you think about it)

Context: [your specific situation]"

**Example:**

"Give me this analysis for accepting a junior UX designer role at $55K when I currently make $85K as an accountant. Go beyond standard career advice. I want the insights that only someone who has actually made this kind of transition would know."

This pattern consistently produces more interesting and useful analysis than a standard pros/cons request, because it explicitly asks the model to move past its default (most common) responses into less-accessed regions of its training data.

> **"Behind The Curtain"**
> The "Hidden Pros" and "Hidden Cons" sections work because they explicitly signal to the model that first-order, obvious responses are not what you want. The model's attention mechanism registers these labels and shifts the generation away from the most common patterns. In effect, you are telling the model: "I already know the obvious stuff -- give me what I have not thought of." This is the textual equivalent of adjusting the temperature dial toward more creative, less predictable output.

## Combining Patterns for Complex Decisions

For truly important decisions, the most effective approach is to chain multiple patterns across several exchanges:

**Exchange 1:** Use the Research Synthesizer to build your knowledge base.
**Exchange 2:** Use the Comparison Framework to evaluate specific options.
**Exchange 3:** Use the Devil's Advocate to stress-test your leading option.
**Exchange 4:** Use the Decision Matrix to structure your final evaluation.
**Exchange 5:** Use the Pros/Cons with Hidden Dimensions to catch anything you missed.

This five-exchange sequence gives you a research foundation, a structured comparison, critical pressure-testing, a decision framework, and a final check for blind spots. It is the equivalent of having a research analyst, a strategic advisor, a skeptical mentor, a decision coach, and a wise friend -- all in one conversation.

---

Research and analysis are where the model's deep reasoning layers shine -- but only when you give them room to operate. Unstructured requests produce unstructured thinking. The patterns in this lesson provide the structure that transforms raw AI capability into genuinely useful analysis. Next, we explore patterns for learning, tutoring, and working with code -- domains where the model becomes not just an analyst but a teacher.
