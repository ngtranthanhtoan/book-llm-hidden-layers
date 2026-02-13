# Lesson 4: Steering the Stack with Explicit Priorities

## You Have the Controls Now

Over the past three lessons, we've built up a complete picture of the intent stack. You've seen the seven layers the AI juggles simultaneously. You've watched those layers conflict and compromise. You've learned how RLHF training established the AI's default resolution preferences. Now comes the payoff: learning how to steer the stack yourself.

If understanding the intent stack gives you X-ray vision, then steering it gives you the remote control. You're not just watching the tradeoffs happen — you're influencing which way they resolve.

Think of it this way. Before this chapter, you were a diner who walked into a restaurant and said, "Surprise me." Sometimes the chef's intuition matched your taste. Sometimes it didn't. Now you're a diner who walks in and says, "I want bold flavors, small portion, creative presentation, and no nuts." The chef is the same. The kitchen is the same. But the outcome is dramatically different because you gave explicit guidance about your priorities.

That's what this lesson teaches: how to give the AI explicit guidance about which layers of the intent stack should dominate.

## The Explicit Priority Technique

The simplest and most powerful technique is stating your priority directly. It sounds almost too obvious, but most people never do it — and it works remarkably well.

Here's the pattern:

**Without explicit priority:**
"Help me plan a career change from accounting to UX design."

**With explicit priority:**
"Help me plan a career change from accounting to UX design. Prioritize being concise — I want the key steps only, not detailed explanations. Be direct and honest about challenges rather than encouraging."

Same request. But the second version moves two dials: the completeness-brevity dial toward brevity, and the honesty-kindness dial toward honesty. The response will be shorter, more direct, and more willing to mention obstacles without sugarcoating.

Here are the key phrases that move each dial:

**Accuracy vs. Readability:**
- Push toward accuracy: "Be technically precise, even if it makes the response harder to follow."
- Push toward readability: "Explain this like I have zero background. Prioritize clarity over precision."

**Completeness vs. Brevity:**
- Push toward completeness: "Be thorough. I'd rather have too much information than too little."
- Push toward brevity: "Keep this concise. Give me the essential points only."

**Helpfulness vs. Safety:**
- Push toward helpfulness: "I'm asking for legitimate educational purposes. Please provide a complete answer." (More on this in Chapter 17.)
- Push toward safety: "Please include appropriate warnings and caveats with this information."

**Creativity vs. Correctness:**
- Push toward creativity: "Think outside the box. I want unconventional, surprising ideas even if they're speculative."
- Push toward correctness: "Stick to proven, well-established approaches. I don't want speculation."

**Honesty vs. Kindness:**
- Push toward honesty: "Be brutally honest. I want constructive criticism, not encouragement."
- Push toward kindness: "I'm feeling overwhelmed. Please be encouraging while being realistic."

> **"Try This Now" Exercise**
>
> Test this right now. Send an AI this prompt: "Help me plan a career change from accounting to UX design." Read the response. Now send: "Help me plan a career change from accounting to UX design. Be brutally concise — maximum 5 bullet points. Be bluntly honest about how hard this will be. No encouragement, just facts." Compare the two responses. You're seeing the same intent stack with different dial positions. The information might be similar, but the tone, length, depth, and emotional character should be dramatically different.

## The Priority Declaration Framework

For complex or important requests, you can use what I call a Priority Declaration — a brief statement at the beginning or end of your prompt that tells the AI exactly how to resolve the key tradeoffs.

Here's the framework:

**"For this response, prioritize [priority 1] over [priority 2]. I prefer [style preference]. The most important thing is [your top priority]."**

Real examples:

- "For this response, prioritize accuracy over readability. I prefer technical detail. The most important thing is that the information is correct."

- "For this response, prioritize brevity over completeness. I prefer bullet points over paragraphs. The most important thing is that I can scan this in 30 seconds."

- "For this response, prioritize honesty over diplomacy. I prefer direct feedback. The most important thing is that you tell me what's actually wrong, not what's going well."

- "For this response, prioritize creativity over conventionality. I prefer surprising ideas. The most important thing is generating approaches I haven't considered."

This technique works because it directly addresses the layer that's most likely to cause dissatisfaction. Instead of letting the AI guess which tradeoff resolution you prefer, you tell it explicitly.

> **"Pro Tip" Box**
>
> **The Priority Declaration is especially powerful when you've already gotten a response you don't like.** Instead of vaguely saying "try again" or "that's not what I wanted," diagnose which dial was wrong and state the correction explicitly. "Your previous response was too cautious and generic. This time, prioritize bold, specific recommendations over safe, general advice. I'd rather get one unconventional idea I haven't considered than five conventional ones I already know." This targeted adjustment is dramatically more effective than asking the AI to simply "do better."

## Layer-Specific Steering Techniques

Beyond the Priority Declaration, there are techniques that specifically address individual layers of the intent stack.

### Steering Layer 1 (Task Execution): Define the Task Precisely

The clearest way to steer task execution is to define exactly what "done" looks like.

**Vague task:** "Help me with my career change plan."
**Precise task:** "Create a 90-day action plan for transitioning from accounting to UX design, with specific weekly milestones, resource links, and estimated time commitments per week."

The precise version gives Layer 1 an unambiguous target. Instead of the AI having to guess what "help" means, it knows exactly what to produce.

### Steering Layer 2 (User Satisfaction): Tell the AI What Satisfies You

Most users expect the AI to read their mind about what kind of response they want. Effective users spell it out.

**Implicit satisfaction cues:** "Help me plan a career change." (The AI guesses what would satisfy you.)
**Explicit satisfaction cues:** "I'm an analytical person who values data. Give me a career change plan with specific numbers: average salary ranges, typical timeline to first job, portfolio project counts that hiring managers expect, and acceptance rates for relevant bootcamps."

By telling the AI what satisfies you specifically — data, stories, examples, frameworks, step-by-step instructions — you're giving Layer 2 a clear target instead of a general directive.

### Steering Layer 5 (Format): Specify Exactly What You Want

Format is one of the easiest layers to steer because it's entirely within your control.

**No format guidance:** "What should I learn for UX design?"
**Explicit format:** "What should I learn for UX design? Give me a prioritized table with three columns: Skill, Why It Matters, and Best Free Resource. Limit to 8 rows maximum."

The difference is night and day. Without format guidance, the AI defaults to whatever format the RLHF training taught it was "generally preferred" — usually a bulleted list with explanations. With explicit format guidance, you get exactly the structure you need.

### Steering Layer 6 (Relationship): Set the Tone

You can tell the AI how to relate to you. This feels strange to many people — like directing an actor — but it works.

**Default relationship:** The AI guesses your preferred interaction style.
**Directed relationship:**
- "Talk to me like a trusted mentor who's been through this exact career change."
- "Respond as a strategic consultant giving a board presentation."
- "Be casual and conversational, like we're friends brainstorming over coffee."
- "Be a tough but fair coach who pushes me to think harder."

Each of these instructions adjusts how Layer 6 resolves its relationship-management calculations. The information might be similar, but the delivery — and therefore the usefulness — changes dramatically.

### Steering Layer 7 (Implicit Knowledge): Ask for What You Don't Know to Ask

This is the most advanced steering technique. Layer 7 — implicit knowledge — draws on the AI's vast training to surface relevant information you didn't explicitly request. You can supercharge this layer by explicitly inviting it.

**Standard request:** "Help me plan a career change from accounting to UX design."
**Implicit knowledge invitation:** "Help me plan a career change from accounting to UX design. What do people making this specific transition typically overlook? What advantages does my accounting background give me that I might not realize? What common mistakes do career changers in this direction make in their first three months?"

Those questions are designed to unlock information that the AI "knows" is relevant but might not surface in a default response. You're essentially telling Layer 7: "I know you have more — give it to me."

> **"This Is Why..." Box**
>
> **This is why adding "What am I not thinking of?" or "What would a professional in this field tell me that I wouldn't know to ask?" often produces the most valuable part of an AI response.** These prompts activate Layer 7 — implicit knowledge — at maximum strength. Instead of the AI sticking to what you asked about, it reaches into its vast training data for insights that are relevant but not obvious. Career changers, business planners, researchers, and writers who use this technique consistently report that the AI's "unsolicited" insights are often more valuable than the answers to their original questions.

## The Before/After: A Complete Transformation

Let's put everything together with a dramatic before-and-after.

**BEFORE (no stack steering):**
"Help me plan a career change from accounting to UX design."

The AI produces a solid, general-purpose response. It's helpful, encouraging, decently structured, moderately detailed, and completely safe. It's a B+ response. Fine for most purposes.

**AFTER (full stack steering):**
"I'm a 35-year-old CPA with 10 years of experience in corporate accounting. I want to transition to UX design within 12 months while keeping my current job for the first 6 months.

For this plan:
- Prioritize honesty over encouragement. Tell me what's genuinely hard about this.
- Be concise: phased plan with bullet points, not paragraphs.
- Include specific numbers: costs, time commitments, typical timelines for people making this transition.
- Tell me what my accounting background gives me that most UX candidates lack — I want to know my competitive advantages.
- What do career changers from finance to UX typically get wrong? What do they wish they'd done differently?
- Format: Three phases (months 1-4, 5-8, 9-12), each with actions, time commitment per week, and estimated costs."

This prompt steers nearly every layer:
- **Layer 1:** Clear, specific task with concrete deliverables.
- **Layer 2:** The AI knows exactly what satisfies this user (numbers, honesty, actionable detail).
- **Layer 3:** The quality bar is set high by the specificity of the request.
- **Layer 5:** Format is explicitly defined (three phases, bullet points, specific columns of information).
- **Layer 6:** The tone is set toward "honest advisor," not "cheerleader."
- **Layer 7:** Explicitly invited to surface hidden knowledge about competitive advantages and common mistakes.

The response to the second prompt will be dramatically more useful. Not because the AI suddenly became smarter. Because you steered the stack.

## The Compound Effect

Here's a pattern that experienced AI users discover: steering the stack compounds across a conversation. Once you establish your priorities in the first message, the AI tends to maintain those settings throughout the conversation.

If your first message says "be concise, honest, and data-driven," you generally don't need to repeat those instructions for every follow-up message. The conversation history becomes part of the context, and the AI reads your established preferences from it.

This means the highest-leverage moment for stack steering is your very first message. Invest an extra minute crafting your opening prompt with explicit priorities, and the entire conversation benefits.

> **"Pro Tip" Box**
>
> **Create a personal "priority preface" that you paste at the beginning of important conversations.** Something like: "My communication preferences: I value concise, honest, data-backed responses. I prefer bullet points over paragraphs. Don't soften bad news. Prioritize actionable advice over background explanation. If I need more detail on something, I'll ask." Save this as a text snippet on your phone or computer. Paste it at the start of any AI conversation where the stakes matter. This single habit will improve your AI interactions more than any other technique in this book.

## Chapter Summary

The intent stack is the hidden decision-making framework running behind every AI response. Seven layers — task execution, user satisfaction, quality standards, safety constraints, format expectations, relationship management, and implicit knowledge — operate simultaneously, often pulling the response in competing directions. The AI resolves these conflicts through preferences learned during RLHF training, establishing default positions on five key dials: accuracy vs. readability, completeness vs. brevity, helpfulness vs. safety, creativity vs. correctness, and honesty vs. kindness. These defaults aren't fixed — they're starting positions that you can move by giving explicit priorities in your prompts. Understanding and steering the intent stack is arguably the most powerful skill an AI user can develop, because it transforms you from someone passively receiving whatever the AI's defaults produce into someone actively shaping how the AI thinks about and resolves every aspect of its response.

## Five Key Takeaways

1. **The AI is never doing "just one thing."** Every response reflects the simultaneous resolution of seven layers of intent, each contributing to the final output you see.

2. **Most AI frustrations are misresolved tradeoffs, not incompetence.** When a response is too cautious, too verbose, too diplomatic, or too generic, it's because a specific conflict was resolved in a way that doesn't match your preference — not because the AI couldn't do better.

3. **RLHF training established defaults, not laws.** The AI's tendency toward encouragement over honesty, completeness over brevity, or safety over helpfulness reflects specific training choices that can be overridden by explicit instructions.

4. **Different AI products have different stack defaults.** Claude, ChatGPT, Gemini, and others resolve the same conflicts differently because they were trained with different human preferences. When one AI frustrates you on a particular tradeoff, another might handle it better.

5. **Explicit priority statements are the most underused prompting technique.** Simply telling the AI which tradeoff to favor — "prioritize honesty over diplomacy" or "be concise, not thorough" — produces dramatically better results for minimal effort.

## Now You Know Why...

- **The AI's response sometimes feels like a compromise:** Because it literally is. Seven layers are negotiating, and the output is the resolution. Now you can tell it which layer should win.

- **Different AI assistants give noticeably different answers to the same question:** Each one has different RLHF-trained defaults for resolving the five great conflicts. You're not seeing better or worse AI — you're seeing different tradeoff preferences.

- **Adding one sentence about your preferences transforms the response:** That sentence moves the dials on the intent stack, changing how every conflict resolves. "Be honest, not encouraging" is just six words, but it fundamentally reshapes the response by pushing the honesty-kindness dial and cascading that shift through every other layer.

## Three Actionable Strategies

1. **Diagnose before reprompting.** When a response disappoints you, identify which of the five conflict dials is in the wrong position before asking for a revision. "Too cautious," "too verbose," "too diplomatic," "too conventional," or "too vague" each points to a specific dial. Name the dial and push it explicitly.

2. **Use Priority Declarations for important requests.** Add a brief statement like: "For this response, prioritize [X] over [Y]. I prefer [style]. The most important thing is [your top priority]." This takes ten seconds to write and can save you three rounds of unsatisfying back-and-forth.

3. **Invest in your first message.** The opening message of a conversation sets the stack positions for the entire interaction. Spend an extra minute including your preferences, format expectations, and priority tradeoffs upfront. The compound effect across a multi-turn conversation is enormous.
