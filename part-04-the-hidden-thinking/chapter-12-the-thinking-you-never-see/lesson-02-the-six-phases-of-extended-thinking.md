# Lesson 2: The Six Phases of Extended Thinking

## The Blueprint of the Planning Room

In the last lesson, we discovered the hidden scratchpad — the private space where an AI reasons through your question before crafting a response. But if you could actually step inside that planning room and watch the process unfold, you'd notice something surprising: it isn't chaos. It's structured. The AI moves through a remarkably consistent sequence of steps, almost like a surgeon following a protocol or a pilot running a pre-flight checklist.

This isn't because someone programmed a rigid six-step algorithm. It's because the AI learned from millions of examples of human experts reasoning through problems — doctors diagnosing patients, lawyers analyzing cases, engineers solving design challenges — and extracted the underlying pattern that effective thinkers share.

That pattern has six phases. Understanding them doesn't just satisfy curiosity. It gives you the ability to write prompts that activate each phase more effectively, producing dramatically better results.

Let's walk through them.

---

## Phase 1: Comprehension — "What Is the User Actually Asking?"

The first thing any good problem-solver does is make sure they understand the problem. A doctor doesn't start prescribing medication before understanding the symptoms. A lawyer doesn't begin drafting arguments before reading the case file. The AI's thinking process begins the same way.

During comprehension, the AI is doing something more sophisticated than reading your words. It's parsing the full meaning of your request — including what you said, what you implied, and what you probably need but didn't articulate.

Let's see this with our running example. You type:

*"Help me plan a career change from accounting to UX design."*

On the scratchpad, Phase 1 might look something like:

*"The user wants to transition careers from accounting to UX design. This is a planning request, not just a question. They want actionable guidance. They're probably currently working in accounting, so this is about moving FROM something, not just TO something. The word 'plan' suggests they want a structured approach, not just general advice. I should note: they didn't mention their experience level, timeline, or constraints — I may need to address multiple scenarios."*

Notice what's happening: the AI is reading between the lines. It identified that "plan" implies structure. It noted the missing information. It recognized the emotional subtext — this person is probably feeling uncertain about a big life decision.

This is the foundation for everything that follows. If comprehension goes wrong, every subsequent phase builds on a misunderstanding. It's like a chef who misreads "shellfish" as "selfish" — every decision after that first error will be off.

> **"This Is Why..."**
>
> This is why vague prompts get vague answers. When your request is ambiguous, the AI spends its comprehension phase trying to resolve the ambiguity, often picking the most common or generic interpretation. The more clearly you state what you want, the more accurately Phase 1 locks onto your actual need — and the better every subsequent phase performs.

---

## Phase 2: Constraint Mapping — "What Rules Do I Need to Follow?"

Once the AI understands what you're asking, it immediately shifts to mapping constraints. Think of this as the moment a contractor reviews the building code before starting construction. It's not the most exciting phase, but skipping it leads to disasters.

Constraints come from everywhere:

- **Your explicit instructions:** "Keep it under 500 words" or "Use bullet points" or "Focus on free resources"
- **The system prompt:** The hidden instructions that define the AI's personality, rules, and boundaries
- **Safety policies:** Topics the AI must handle carefully or decline to engage with
- **Implicit expectations:** If you're asking for professional advice, the response should sound professional. If you're being casual, the response should match that tone.
- **Factual accuracy:** What does the AI know for certain versus what it's uncertain about?

For our career change example, the constraint mapping might look like:

*"Constraints: No explicit word limit stated. No format specified — I should pick the most useful format. I need to be encouraging but honest (don't oversell UX design or undersell the difficulty of career transitions). I should avoid specific salary claims since these vary enormously by location and experience. I should suggest resources but not recommend specific paid courses without caveats since I don't know the user's budget. My information about specific tools and bootcamps may be outdated — I should flag this..."*

This phase is where the AI's guardrails activate. If you asked something that bumps against a safety policy, this is when the AI notices and begins deciding how to handle it. If your request has contradictory requirements ("Write something creative and unique" combined with "Follow this template exactly"), the AI identifies the tension here.

> **"Behind The Curtain"**
>
> The constraint-mapping phase is one reason why AI responses can sometimes feel overly cautious or hedged. The AI has identified so many constraints and caveats that it tries to honor all of them simultaneously. When you read a response full of "however" and "it depends" and "it's worth noting" — that's the constraint-mapping phase bleeding into the output. If you want more direct answers, you can explicitly say: "Be direct and opinionated. Skip the caveats."

---

## Phase 3: Knowledge Assessment — "What Do I Know? What Am I Uncertain About?"

This is the phase that separates thoughtful reasoning from confident guessing. The AI takes inventory of its knowledge — and, critically, its knowledge gaps.

Think of a doctor who examines a patient with chest pain. A good doctor mentally reviews: "What do I know? The patient has chest pain, shortness of breath, and a family history of heart disease. What don't I know? We haven't done an ECG, blood work, or imaging yet. What am I fairly confident about? This needs urgent attention. What's uncertain? Whether this is cardiac, pulmonary, or musculoskeletal."

The AI runs a similar assessment:

*"What I know well: The general landscape of UX design as a career, common transition paths, transferable skills between analytical and design roles, the typical tools used in UX design.*

*What I'm less certain about: Current job market conditions (my training data has a cutoff), the latest bootcamp reviews and pricing, specific regional salary data.*

*What I should be transparent about: My advice is general — a career counselor or someone who has made this specific transition would offer more personalized guidance."*

This phase is crucial because it determines the AI's confidence calibration in the final response — whether it says "you should definitely" versus "you might consider" versus "I'm not certain, but." We'll explore confidence calibration in depth in Chapter 14, but it begins here.

> **"This Is Why..."**
>
> This is why AI sometimes volunteers that it's uncertain about something or suggests you verify information — even when you didn't ask it to. During Phase 3, it identified gaps in its knowledge and decided that transparency was more important than sounding authoritative. This is actually the AI working as designed. A model that's always confident is more dangerous than one that admits its limits.

---

## Phase 4: Planning — "How Should I Structure My Response?"

With comprehension locked, constraints mapped, and knowledge assessed, the AI enters the planning phase. This is the architectural moment — the blueprint before construction begins.

Here, the AI decides:

- **What to include and what to omit.** Not everything it knows is relevant. A five-thousand-word treatise on UX design history isn't helpful when someone wants a practical transition plan.
- **What order to present information in.** Should it start with transferable skills (encouraging) or with the challenges ahead (realistic)? Should it give the big picture first or dive into step-by-step specifics?
- **What format to use.** Paragraphs? Bullet points? Numbered steps? A timeline? Headings?
- **What tone to strike.** Professional and authoritative? Warm and encouraging? Direct and no-nonsense?

For our career change example:

*"Structure plan: Start with an encouraging framing — accounting skills are more transferable than most people think. Then cover the key areas: (1) skills they already have, (2) skills they need to develop, (3) a concrete step-by-step transition plan, (4) realistic timeline expectations. End with encouragement and practical next steps. Use a mix of paragraphs for explanation and bullet points for actionable items. Keep the tone warm but practical — this is someone making a big life decision."*

The planning phase is where the overall quality of the response is largely determined. A brilliant plan executed well produces a great response. A poor plan executed perfectly still produces a mediocre response. The AI is essentially deciding what kind of response you're going to get.

> **"Pro Tip"**
>
> You can directly influence Phase 4 by telling the AI how you want the response structured. Try phrases like:
>
> - "Start with the most important point, then give supporting details"
> - "Give me a timeline-based plan with quarterly milestones"
> - "Structure this as: current situation, desired outcome, gap analysis, action plan"
>
> When you specify structure, you're doing the planning phase for the AI — and the result almost always matches your needs better than whatever structure it would have chosen on its own.

---

## Phase 5: Drafting and Self-Critique — "Let Me Try... Wait, That's Not Right"

Now comes the phase most people don't realize exists: the AI doesn't just generate its response in one clean pass. It drafts, evaluates, and revises — sometimes multiple times — within the scratchpad before committing to the output you see.

This is like watching an artist sketch. They draw a line, step back, decide they don't like the angle, erase it, and try again. The final drawing looks effortless, but behind it lies a process of constant evaluation and adjustment.

In the scratchpad, this might look like:

*"Draft opening: 'Making a career change from accounting to UX design is a significant but achievable goal.' Hmm — that's generic. Let me try: 'Here's what most career advice gets wrong about the accounting-to-UX transition: your analytical background isn't a liability — it's your biggest advantage.' Better — that's more engaging and immediately challenges an assumption the user might have."*

*"Wait — I said UX designers need to learn 'coding.' That's misleading. Some UX roles involve no coding at all, while others require front-end skills. I should clarify this distinction instead of making a blanket statement."*

*"I listed five transferable skills, but I'm not sure 'project management' belongs here. It's transferable, but it's not specific to the accounting-to-UX path. Let me replace it with something more directly relevant... 'Data interpretation and evidence-based decision making' — yes, that's much more specific to both accounting and UX research."*

This internal self-critique is one of the most powerful aspects of extended thinking. Without it, the AI commits to its first draft — which, like any first draft, is rarely the best version. With the scratchpad, the AI can catch errors, improve clarity, and refine its approach before you ever see a word.

> **"Behind The Curtain"**
>
> The self-critique phase can be quite harsh. Researchers who have examined AI scratchpad contents have found the AI writing things like "That explanation is confusing — let me try a different approach" or "Actually, I was wrong about that claim — let me reconsider." The AI is genuinely arguing with itself, not just going through the motions. This internal debate is the subject of Chapter 14, and it's one of the most fascinating aspects of modern AI.

---

## Phase 6: Final Check — "Does This Actually Answer the Question?"

Before the response is released, the AI performs a final verification pass. Think of this as the moment a surgeon counts the instruments before closing — one last check to make sure nothing was missed and nothing went wrong.

The final check asks:

- **Completeness:** Did I address every part of the user's request? If they asked three questions, did I answer all three?
- **Consistency:** Does anything in my response contradict itself? Did I recommend something in paragraph two that I warned against in paragraph four?
- **Accuracy:** Am I confident in my factual claims? Did I accidentally state something as certain when I'm actually unsure?
- **Tone:** Does the overall feeling of the response match what the user seems to need? Did I come across as dismissive when they needed encouragement?
- **Constraint compliance:** Did I follow all the format instructions, length requirements, and other explicit constraints?

*"Final check: The user asked for help planning a career change from accounting to UX design. My response covers transferable skills, necessary new skills, a step-by-step plan, and realistic timeline. I've been encouraging but honest about the challenges. I haven't made specific salary promises. I've suggested both free and paid learning resources. I've noted that my information about specific programs may not be current. The structure is clear and scannable. The tone is warm and practical. I think this is ready."*

This phase is the reason well-formed AI responses feel polished and complete. The AI has already caught the obvious problems before you see them.

> **"Try This Now"**
>
> To see the effect of these phases in action, try this experiment:
>
> **Prompt A:** "Career change advice."
>
> **Prompt B:** "Help me plan a career change from accounting to UX design. I have 5 years of accounting experience, a modest budget for courses, and I want to make the switch within 18 months. Please structure your response as: (1) my transferable skills, (2) skills I need to develop, (3) a month-by-month plan, (4) realistic expectations."
>
> Prompt B will produce a dramatically better response — not just because it has more information, but because it supercharges every one of the six phases. Comprehension is precise. Constraints are clear. Knowledge assessment is focused. Planning is pre-structured. Self-critique has specific criteria to evaluate against. And the final check has a clear checklist.

---

## The Six Phases in Action: A Complete Example

Let's put it all together with a different example to see the full flow. Imagine you ask:

*"Is it better to rent or buy a home in today's market?"*

Here's a compressed version of how the six phases might play out:

**Phase 1 (Comprehension):** "This is a financial decision question. The user wants personalized-ish guidance, but they haven't given me their specific situation. 'Today's market' means they want current analysis, but my training data has a cutoff. I should address the framework for deciding rather than giving a definitive answer."

**Phase 2 (Constraint Mapping):** "I shouldn't act as a financial advisor. I should present balanced perspectives. I can't make promises about market directions. I should note that this varies enormously by location."

**Phase 3 (Knowledge Assessment):** "I know the general rent-vs-buy framework well: price-to-rent ratio, opportunity cost of down payment, transaction costs, tax implications, flexibility vs. equity building. I'm less certain about current interest rates and market conditions."

**Phase 4 (Planning):** "I'll present the key factors to consider, organized as pros and cons of each option, with a framework for how to evaluate based on personal situation. I'll end with the key variables that tip the decision one way or the other."

**Phase 5 (Drafting and Self-Critique):** "My first draft leaned too heavily toward buying. Let me rebalance. Also, I stated that mortgage interest is 'always' tax-deductible — that's not accurate for all situations. Let me qualify that."

**Phase 6 (Final Check):** "Response is balanced, acknowledges uncertainty about current market, provides a decision framework rather than a directive, notes the importance of local conditions and personal financial situation. Good."

Six phases. Each one builds on the previous. The result is a response that's comprehensive, balanced, accurate, and well-structured — not because the AI is magic, but because it followed a process.

---

## Why This Matters for You

Understanding the six phases gives you a practical superpower: you can write prompts that feed each phase exactly what it needs. Think of it this way — you're not just asking a question anymore. You're staging the planning room for success.

- **Help Phase 1** by being explicit about what you want: "I need a decision framework" versus "I need a direct recommendation" versus "I need a pros and cons list."
- **Help Phase 2** by stating your constraints upfront: word count, format, audience, tone, what to include, what to exclude.
- **Help Phase 3** by providing relevant context the AI might not have: "I'm based in Austin, TX," or "My budget is $50,000," or "I have no design experience."
- **Help Phase 4** by suggesting the structure: "Organize this as a timeline" or "Start with the conclusion, then explain your reasoning."
- **Help Phase 5** by asking for self-critique: "After drafting your answer, check it for any assumptions that might not apply to my situation."
- **Help Phase 6** by giving clear success criteria: "A good answer would address cost, timeline, and skill requirements."

When you do this, you're not just writing a better prompt. You're collaborating with the AI's thinking process — giving the chef in the planning room a head start on every phase of their work.

In the next lesson, we'll explore a question you might already be wondering about: if this thinking process exists, does the AI always use it? The answer is fascinating — and it explains why the same AI can be brilliant one moment and bafflingly shallow the next.
