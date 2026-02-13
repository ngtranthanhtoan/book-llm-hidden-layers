# Lesson 4: Steering Generation with Opening Words

## Taking the Wheel Before the AI Starts Driving

You now know three things that put you ahead of most AI users on the planet. You know the AI generates one token at a time (the autoregressive loop). You know each token is selected from a probability distribution of 100,000 options. And you know that once tokens are generated, they can't be taken back (the commitment problem), which means the opening tokens have outsized influence on everything that follows.

This lesson brings those three insights together into a single, remarkably powerful strategy: you can steer the AI's entire response by influencing what it says first.

If the first sentence shapes everything after it, then controlling the first sentence is the closest thing to a cheat code in AI interaction.

## The Steering Wheel Analogy

Think about driving a car on a long highway. A tiny adjustment to the steering wheel — just a few degrees — barely changes your position over the next ten feet. But maintain that slight angle for a mile, and you'll end up in a completely different lane. Maintain it for ten miles, and you're on an entirely different road.

The opening tokens of an AI response work the same way. A small difference in the first few words creates a slight shift in trajectory. But because every subsequent token builds on what came before, that slight shift compounds through hundreds of token decisions. By the end of the response, two different openings have produced fundamentally different content, structure, and tone.

Your job as a skilled AI user is to grip that steering wheel at the very beginning.

## Three Ways to Steer the Opening

There are three primary techniques for influencing how the AI starts its response, ranging from subtle to explicit.

### Technique 1: Frame the Task to Imply the Response Shape

The way you phrase your request strongly influences how the AI begins its response. Compare these variations of the same underlying question:

**Prompt A:** "Tell me about career changes from accounting to UX design."

The AI is likely to begin with something broad and informational: "Career changes from accounting to UX design have become increasingly common..." This opening commits to an overview essay.

**Prompt B:** "Give me a step-by-step plan for changing careers from accounting to UX design."

The AI is likely to begin with: "Here's a step-by-step plan for your career transition..." or "Step 1: Assess your transferable skills." This opening commits to a structured, actionable format.

**Prompt C:** "What are the three biggest risks of changing careers from accounting to UX design, and how do I mitigate each one?"

The AI is likely to begin with: "The three biggest risks..." and is now committed to a risk-focused analysis with mitigation strategies.

Same underlying topic. Three completely different responses. The difference isn't just formatting — it's the substance of what the AI covers, the depth it goes into, and the practical value it delivers. And that difference was determined before the AI generated its first token, simply by how you framed the request.

> **"Pro Tip" Box**
>
> When you're dissatisfied with AI responses, before you blame the AI, look at how you framed the task. A vague frame ("tell me about X") produces a vague opening, which produces a generic response. A specific frame ("give me the three most counterintuitive insights about X, with evidence for each") produces a focused opening, which produces a detailed, surprising response. The frame is the steering wheel.

### Technique 2: Provide the Opening Words Yourself

This is the most direct and powerful steering technique. Many AI interfaces allow you to literally provide the first few words of the response, either through special syntax or by including them in your prompt.

For example:

**Prompt:** "Help me plan a career change from accounting to UX design. Start your response with: 'The unconventional approach that most career coaches won't tell you about is...'"

By providing the opening words, you've made several powerful commitments on the AI's behalf:

- The response will focus on an unconventional approach (not the standard advice)
- The tone will be insider-knowledge, slightly contrarian
- The framing implies that the standard advice is insufficient
- The model is now committed to delivering something genuinely surprising

Compare that to what you'd get without the steering: probably a conventional response starting with skills assessment and online courses.

> **"Try This Now" Exercise**
>
> Try this exact experiment. Send this prompt to your AI:
>
> "Help me plan a career change from accounting to UX design."
>
> Read the response. Then send this:
>
> "Help me plan a career change from accounting to UX design. Begin your response with: 'Forget everything you've read in generic career change articles. Here's what actually works, based on the specific advantages accountants have in UX:'"
>
> Compare the two responses. The second one will be dramatically more specific, more actionable, and more interesting — not because the AI has different knowledge, but because you steered its opening tokens into a more productive trajectory. You changed the destination by turning the steering wheel at the start.

### Technique 3: Use Format Instructions to Constrain the Opening

Telling the AI what format to use implicitly controls how it begins, which controls everything after.

**"Give me your answer as a table comparing..."** — The model will begin with a table header, committing to a structured, comparative format.

**"Give me your answer as a conversation between a skeptic and an advocate..."** — The model will begin with dialogue format, committing to exploring both sides.

**"Give me your answer as a timeline from month 1 to month 12..."** — The model will begin with "Month 1:" and commit to a chronological, specific plan.

**"Give me your answer as a letter to my future self..."** — The model will begin with a personal, reflective tone that produces entirely different content than any of the above.

Each format instruction doesn't just change how the information is arranged — it changes which information the AI covers, how deeply it explores each point, and what tone it adopts. Format is not just presentation. Format is a steering mechanism.

> **"Behind The Curtain" Sidebar**
>
> AI researchers and prompt engineers have a name for the technique of providing opening tokens: "prefix forcing" or "completion steering." In the API world (where developers interact with AI programmatically rather than through a chat interface), you can literally set the first few tokens of the AI's response as a fixed prefix. The model then continues from where you left off. This technique is so powerful that it's one of the primary tools used in prompt engineering research. What researchers discovered is that you can change the model's effective "personality," domain expertise, reasoning style, and even factual accuracy simply by changing the opening tokens. The same model, with the same prompt, produces expert-level medical analysis when forced to start with "As a medical professional reviewing this case..." and produces casual layperson speculation when forced to start with "I'm not a doctor, but..." The opening tokens don't just set tone — they activate entirely different knowledge patterns.

## The Before/After Pattern

Let's see this steering principle in action with a clear before-and-after comparison.

**Before (unsteered prompt):**

"What should I know about transitioning from accounting to UX design?"

**Typical AI response opening:** "Transitioning from accounting to UX design is an exciting career move that many professionals are making. Here are some key things to consider..."

This is fine. It's accurate. It's also generic, predictable, and indistinguishable from the first page of a Google search.

**After (steered prompt):**

"What should I know about transitioning from accounting to UX design? Structure your response as 'The 5 things nobody tells you,' and for each one, explain why my accounting background is specifically relevant."

**Typical AI response opening:** "Here are five things nobody tells you about the accounting-to-UX pipeline — and why your background gives you a surprising edge in each: 1. You already think in user flows (you just call them 'workflows')..."

Night and day. The steered version is more specific, more interesting, more personally relevant, and more actionable. The AI's knowledge hasn't changed. The underlying model is identical. What changed is the trajectory established by the opening tokens, which you controlled through your prompt design.

## Steering Across Different Task Types

This principle applies to virtually every interaction you have with an AI, not just career advice.

**For research and analysis:**
- Unsteered: "Tell me about climate change solutions."
- Steered: "Rank the five most cost-effective climate change interventions based on estimated impact per dollar spent, starting with the most effective."

**For writing tasks:**
- Unsteered: "Write an email asking for a raise."
- Steered: "Write an email asking for a raise. Open with a specific recent accomplishment, not with pleasantries."

**For problem-solving:**
- Unsteered: "My team isn't communicating well. What should I do?"
- Steered: "My team isn't communicating well. Diagnose the three most likely root causes based on common team dynamics, then give me one specific fix for each cause."

**For creative work:**
- Unsteered: "Write a short story about loneliness."
- Steered: "Write a short story about loneliness. Begin with the sentence: 'The party had 200 guests, and she knew every single one of them by name.'"

In each case, the steered version doesn't just produce a better-formatted response — it produces a fundamentally different and more valuable one. The steering constrains the opening, which constrains the path, which determines the destination.

## The Compound Effect of Good Steering

Here's something beautiful about steering the opening: the benefits compound as the response grows longer.

In a short response (50 words), steering matters a little. The response is so brief that most openings lead to roughly the same content.

In a medium response (200-300 words), steering matters a lot. Different openings lead to different points being covered, different levels of specificity, and different structures.

In a long response (500+ words), steering matters enormously. The trajectory established by the opening carries through multiple paragraphs, sections, and ideas. A well-steered long response might cover entirely different ground than an unsteered one — different examples, different recommendations, different conclusions.

This compound effect is a direct consequence of the autoregressive loop and the commitment problem working together. Every token is influenced by everything before it, and the opening tokens are "before" every other token in the response. Their influence is maximal and inescapable.

> **"This Is Why..." Box**
>
> **This is why asking the AI to "start with the conclusion" completely changes the response structure.** When the AI normally generates a response, it often follows the pattern of its training data: introduction, evidence, analysis, conclusion. The conclusion comes last, built on everything before it. But if you ask the model to start with the conclusion, the opening tokens are now a strong claim or recommendation. The autoregressive loop then generates tokens that support and elaborate on that opening claim. The response becomes more direct, more confident, and often more useful — because the model isn't building toward a point, it's defending a point it's already made. This is a powerful technique for getting decisive, actionable advice instead of wishy-washy overviews.

## When Not to Steer

There are situations where minimal steering is actually the better strategy:

**Open-ended exploration.** If you genuinely don't know what angle you want and you're using the AI to brainstorm, an unsteered prompt lets the model's default trajectory surprise you. You might discover an approach you'd never have thought to request.

**When you want diversity.** If you plan to regenerate multiple times and compare results, less steering allows the natural randomness of the probability distributions to produce genuinely different responses each time.

**When you trust the model's expertise.** For well-defined tasks where the AI is likely to have strong patterns (like explaining a scientific concept or summarizing a well-known topic), minimal steering often produces excellent results because the training data contains many high-quality examples of exactly that type of output.

The key is intentionality. Steer when you know what you want. Leave room when you want to be surprised.

---

## Chapter 18 Summary

The AI generates text the way a bricklayer builds a wall — one piece at a time, each piece placed based on everything already in position. This is the autoregressive loop. At each step, the model faces a 100,000-way probability distribution, selecting one token that becomes an irrevocable part of the response. This one-directional process creates the commitment problem: once the AI starts down a path, it cannot backtrack. Early tokens have outsized influence on everything that follows. Understanding this mechanism transforms you from a passive recipient of AI output into an active steering force, shaping responses from their very first word.

## Five Key Takeaways

1. **The AI generates one token at a time**, not complete thoughts. Each token is selected from roughly 100,000 options based on a probability distribution that reflects the full context — your prompt, the system prompt, conversation history, and every token already generated.

2. **The probability distribution varies dramatically** from peaked (one dominant option, like a factual answer) to flat (many plausible options, like creative writing), and this shape determines how much variation you'll see across regenerated responses.

3. **The commitment problem means early tokens disproportionately shape the response.** The AI cannot backtrack, so the opening sentences establish the tone, framing, structure, and intellectual direction for everything that follows.

4. **Extended thinking helps mitigate the commitment problem** by allowing the model to reason through different approaches before committing to visible output, reducing the frequency of wrong-path commitments.

5. **You can steer the autoregressive loop** by framing your task to imply a response shape, providing the opening words directly, or specifying a format that constrains the opening tokens.

## Now You Know Why...

- **The AI never gives the exact same response twice.** Random sampling from probability distributions at each of hundreds of token positions creates cascading differences that produce unique outputs every time.

- **Regenerating a response sometimes gives you something dramatically better.** Different random samples at key early decision points send the response down a completely different path — one that might be far more relevant, specific, or insightful.

- **Adding "start with the conclusion" or "begin with the most important point" to your prompt produces more decisive, useful responses.** You're steering the opening tokens away from cautious throat-clearing and toward strong claims that the autoregressive loop then supports and elaborates.

## Three Actionable Strategies

1. **Steer the opening explicitly.** When you want a specific type of response, tell the AI how to begin. "Start your response with..." or "Begin by stating your single strongest recommendation, then explain why." This gives you control over the most influential tokens in the entire response.

2. **Use regeneration strategically, not randomly.** When a response misses the mark, don't just mash the regenerate button. Instead, adjust your prompt to steer the opening in a different direction, then regenerate. You'll get better results faster than hoping random sampling lands on a better path.

3. **Match your steering intensity to your certainty.** When you know exactly what you want, steer aggressively — provide format, opening words, and specific constraints. When you're exploring, steer lightly — give a clear topic but let the model's default trajectory surprise you. The right amount of steering depends on how well-defined your goal is.
