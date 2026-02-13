# Lesson 1: Chain-of-Thought — The Hidden Scratchpad

## The Most Important Room You've Never Seen

If you've been following our restaurant analogy, you've watched your order travel from the front-of-house (the chat interface), through the health inspectors (the classifiers), past the routing system that picks which chef handles it, and into the kitchen where the attention engine reads every word of your request simultaneously. You've seen how the 80-story building of Transformer layers processes your message from raw text into deep understanding.

But now we arrive at the room that matters most — and it's a room most diners never know exists.

Imagine a chef who receives a complicated order: "I'd like a meal that's suitable for a dinner party of eight, where two guests are vegan, one is allergic to nuts, the cuisine should be Mediterranean, and it needs to be impressive but not require last-minute preparation." A mediocre chef reads the order and immediately starts grabbing ingredients. A brilliant chef pauses. She walks into a small planning room behind the kitchen, pulls out a notebook, and starts working through the problem. She lists the constraints. She considers three possible menus. She thinks about which one best satisfies all the requirements. She spots a problem — one dish uses pine nuts, which violates the nut allergy constraint — and adjusts. Only after this planning process does she step out and begin cooking.

That planning room is what we're about to explore. In the world of large language models, it's called the **thinking scratchpad** — a hidden space where the AI reasons through your request before you see a single word of the response.

And here's the remarkable thing: for most of the history of modern AI, this room didn't exist. The chef was just... grabbing ingredients and hoping for the best.

---

## What Is Chain-of-Thought Reasoning?

Let's start with a deceptively simple question. Ask an AI:

*"If a shirt costs $25 and is on sale for 20% off, and you also have a $5 coupon, how much do you pay?"*

For a human, this is straightforward. You probably just did the math in your head: 20% off $25 is $5, so the sale price is $20, minus the $5 coupon gives you $15. Easy.

But here's what's interesting: even though it felt instant, your brain went through steps. You didn't just see the problem and hallucinate "$15" from thin air. You calculated the discount, applied it, then subtracted the coupon. You reasoned through it.

Early large language models didn't do this. They looked at the whole problem and produced an answer in one shot — like trying to guess the final number without doing any arithmetic. Sometimes they got it right (pattern matching from similar problems in training data), but on anything requiring multiple steps, they frequently stumbled.

**Chain-of-thought reasoning** changed everything. It's the technique of having the AI work through problems step by step, writing out its reasoning as it goes — exactly the way a student shows their work on a math test. When AI researchers at Google first demonstrated this in 2022, the results were stunning: on some reasoning tasks, simply adding "Let's think step by step" to the prompt boosted accuracy from around 18% to nearly 80%.

Think about how extraordinary that is. The same brain, with the same knowledge, suddenly became dramatically better at reasoning — just because it was asked to show its work.

> **"This Is Why..."**
>
> This is why adding "think step by step" or "explain your reasoning" to your prompts often produces noticeably better answers. You're not just asking for more text — you're activating a fundamentally different problem-solving process. You're asking the chef to use the planning room instead of grabbing ingredients blindly.

---

## From Showing Work to Hidden Thinking

Chain-of-thought was a breakthrough, but it had a limitation: all that reasoning was visible in the response. If you asked a complex question, you'd get paragraphs of "First, let me consider... Then, I need to account for... Now, looking at this from another angle..." before finally reaching the answer. Useful, but noisy.

The next evolution was **extended thinking** — sometimes called "thinking mode" or the "thinking scratchpad." This is chain-of-thought reasoning that happens before the response begins, in a space the user typically doesn't see.

Imagine the difference between two math students. One writes all their work on the final answer sheet, mixing calculations with the answer. The other uses scratch paper, works through the problem completely, then writes only a clean final answer on the submission page. Both are reasoning through the problem — but the second student's work is hidden from the viewer.

That's extended thinking. The AI gets a private scratchpad where it can:

- Break down complex problems
- Consider multiple approaches
- Check its own reasoning
- Spot errors and correct them
- Organize its thoughts before responding

When you use a model with extended thinking enabled — like Claude's "thinking" mode — there's often a pause before the response appears. During that pause, the AI isn't frozen or loading. It's actively reasoning in its scratchpad, sometimes generating thousands of words of internal deliberation that you'll never see.

> **"Behind The Curtain"**
>
> The thinking scratchpad can be remarkably long. For a complex question, an AI might generate 3,000 to 10,000 words of internal reasoning before producing a 500-word response. That's like a chef spending forty-five minutes planning a meal that takes ten minutes to plate. The thinking-to-output ratio can be 10:1 or even 20:1 for difficult problems.

---

## What Does the Scratchpad Actually Look Like?

You might be wondering: what's actually written on this hidden scratchpad? Is it neat and organized, or chaotic? Is it in complete sentences or shorthand?

The answer is somewhere in between — and it's fascinating. Let's revisit our running example. Imagine you type:

*"Help me plan a career change from accounting to UX design."*

If the AI has extended thinking enabled, here's a simplified version of what might happen on the scratchpad before you see any response:

---

*"The user wants to transition from accounting to UX design. Let me think about what this involves...*

*First, what do I know about both fields? Accounting is analytical, detail-oriented, involves financial reporting and compliance. UX design is about user research, interface design, usability testing, information architecture.*

*What transferable skills exist? Analytical thinking, attention to detail, understanding user needs (clients in accounting are like users in UX), data interpretation...*

*What gaps would they need to fill? Design tools (Figma, Sketch), user research methodologies, visual design principles, portfolio building...*

*The user didn't specify their experience level, budget for education, timeline, or whether they want to freelance or work in-house. I should address common paths while noting these variables.*

*I should structure this as: (1) transferable skills they already have, (2) skills they need to develop, (3) concrete steps for the transition, (4) realistic timeline expectations.*

*Wait — I should also address the emotional/practical side. Career changes are stressful. They might need reassurance that the accounting background is actually an advantage, not a handicap...*

*Let me also consider whether to mention the financial reality — UX designers and accountants have different salary ranges depending on level. I should be honest but encouraging.*

*Okay, I'll structure the response as a practical roadmap with those four sections..."*

---

Notice what's happening here. The AI is doing several things simultaneously: understanding the question, assessing its own knowledge, planning the response structure, considering what the user didn't say but probably needs, and even thinking about emotional tone. This is the planning room in action.

> **"This Is Why..."**
>
> This is why the AI sometimes takes 15 to 30 seconds before responding to a complex question. It's not broken or slow — it's doing exactly what a thoughtful human expert would do: thinking before speaking. That pause is actually a sign that you're getting a more carefully considered answer.

---

## The Scratchpad as a Thinking Amplifier

Here's the deep insight that makes chain-of-thought and extended thinking so powerful, and it's a bit counterintuitive.

Remember from Part 1 that an LLM generates text one token at a time. Each token is influenced by everything that came before it. This is key: the AI's "thinking" is literally shaped by the words it has already generated.

When the AI writes on its scratchpad, "The user is asking about a career change, and they probably have concerns about..." — that written thought now becomes part of the context for the next thought. The scratchpad isn't just a place where thinking is recorded. The act of writing on the scratchpad *is* the thinking.

This is more like human cognition than you might expect. When you're working through a complex problem, writing your thoughts down doesn't just record them — it clarifies them. The act of putting vague ideas into words forces you to make them concrete. You see connections you missed when the ideas were just floating in your head.

The AI's scratchpad works the same way. Each sentence of reasoning creates a foundation for the next sentence. It's thinking that builds on itself, layer by layer — a ladder where each rung only exists because the previous one was constructed.

This is why chain-of-thought produces better answers than direct responses. Without the scratchpad, the AI has to generate a final answer based only on the original prompt. With the scratchpad, it generates a final answer based on the original prompt *plus* an entire internal analysis. It's the difference between solving a complex equation in your head versus working it out on paper.

> **"Try This Now"**
>
> Open your favorite AI tool and ask this question twice:
>
> **Version A:** "What are the pros and cons of remote work?"
>
> **Version B:** "Think carefully about this before answering. Consider multiple perspectives, potential counterarguments, and nuances. What are the pros and cons of remote work?"
>
> Compare the two responses. Version B will almost certainly be more nuanced, better organized, and more thorough — because you activated the planning room.

---

## The Revolution in Three Acts

The development of AI reasoning happened in three distinct stages, and understanding them helps you see where the technology is today.

**Act One: Direct Response (Pre-2022).** The AI reads your question and immediately starts generating the answer. No planning, no reasoning, no scratchpad. Like a student blurting out an answer before fully reading the question. This works fine for simple requests ("What's the capital of France?") but falls apart for anything requiring multiple logical steps.

**Act Two: Chain-of-Thought (2022-2023).** Researchers discover that asking the AI to "think step by step" dramatically improves reasoning. The AI now shows its work, writing out each step before reaching a conclusion. The reasoning is visible to the user. Like a student who writes all their calculations on the answer sheet.

**Act Three: Extended Thinking (2024-present).** The thinking process moves to a hidden scratchpad. The AI reasons extensively before responding, but the user only sees the final, polished answer. The reasoning is more thorough because the AI can explore dead ends, correct mistakes, and restructure its approach — all without cluttering the response. Like a student who uses scratch paper and submits only a clean final answer.

We're now firmly in Act Three, and it represents the single biggest leap in the quality of AI responses since the Transformer architecture itself.

> **"Behind The Curtain"**
>
> The "thinking" you see when an AI model shows its reasoning (in products that offer this feature) is actually a curated summary of the internal process, not the raw scratchpad itself. The actual internal reasoning can be messier, more repetitive, and much longer than what's displayed. What you see is the highlight reel; the full process is more like the unedited footage.

---

## What the Scratchpad Means for You

Understanding the hidden scratchpad fundamentally changes how you should interact with AI. Here are the practical implications:

**1. Complex questions deserve thinking time.** If you're asking something that requires analysis, comparison, planning, or multi-step reasoning, you want the AI to use its scratchpad. Many AI tools now let you enable "thinking" or "extended thinking" modes. Use them for important questions.

**2. You can activate better thinking with your words.** Even without a dedicated thinking mode, phrases like "think step by step," "consider multiple angles," or "reason through this carefully" can trigger more deliberate reasoning. You're essentially telling the chef to use the planning room.

**3. The scratchpad explains the pause.** When there's a delay before the response appears, the AI may be doing extensive reasoning. This is usually a good sign, not a technical problem. A thoughtful pause is better than a hasty answer.

**4. Simple questions don't need the scratchpad.** Asking "What's the capital of Japan?" doesn't benefit from extended thinking. The AI would just write "The user is asking a straightforward factual question. The answer is Tokyo." on its scratchpad and produce the same answer it would have anyway. The scratchpad earns its keep on complex, multi-step, or nuanced questions.

> **"Pro Tip"**
>
> When you have a truly important question — one where the quality of the answer really matters — use these scratchpad-activating strategies:
>
> - Start with: "This is important. Take your time and think carefully."
> - Add: "Consider what could go wrong with your initial answer."
> - Include: "Before answering, identify what assumptions you're making."
>
> These phrases don't just ask for a better answer. They literally trigger more extensive internal reasoning, which produces genuinely better output.

---

## The Biggest Shift in AI History

The hidden scratchpad represents something profound about how AI has evolved. Early language models were impressive mimics — they could produce text that sounded human, but they weren't reasoning in any meaningful sense. They were the chef who grabbed ingredients based on vibes.

Chain-of-thought and extended thinking moved AI from pattern-matching into something closer to deliberate problem-solving. The AI still doesn't "think" the way humans do — it doesn't have consciousness, emotions, or true understanding. But it now has a structured process for working through problems, and that process produces dramatically better results.

As we're about to see in the next lesson, this thinking process isn't random or unstructured. It follows a remarkably consistent pattern — six distinct phases that the AI moves through every time it tackles a complex question. Understanding these phases is like getting the blueprint to the planning room.

The chef has a method. And you're about to learn exactly what it is.
