# Lesson 3: From ELIZA to GPT — A Brief History

## The Long Road to a Very Fast Machine

Every revolution has a backstory, and the AI revolution is no exception. Understanding how we got here — from a 1966 chatbot that fooled people with simple word-swapping tricks to today's systems that can pass bar exams — isn't just historical trivia. It reveals *why* modern LLMs work the way they do, and why the decisions made along the way matter for you as a user.

Think of it this way: if you're driving a car, it helps to know that it runs on internal combustion (or a battery), not magic. You don't need to be a mechanic, but knowing the basics means you won't put diesel in a gasoline engine. The same principle applies here. A quick tour through AI's history will help you understand the fundamental nature of the tool you're using — and stop you from "putting diesel in a gasoline engine" with your prompts.

## Act One: The Clever Impostor (1966-1990s)

Our story begins in 1966, in a lab at MIT, where a computer scientist named Joseph Weizenbaum created ELIZA. ELIZA was simple — almost embarrassingly so. It worked by pattern matching: if you typed a sentence containing the word "mother," ELIZA would respond with something like "Tell me more about your family." If you said "I feel sad," ELIZA might reply, "Why do you say you feel sad?"

ELIZA didn't understand a single word. It was a mirror with a few clever tricks — recognizing keywords and reflecting them back in the form of questions, mimicking a Rogerian psychotherapist. And yet, people who talked to ELIZA frequently became emotionally attached to it. Weizenbaum's own secretary asked him to leave the room so she could chat with ELIZA privately.

This was the first lesson about humans and AI: we are *extraordinarily* willing to see intelligence where there is none. We are pattern-recognizing creatures, and when something responds to us in language, we instinctively treat it as a mind. Keep this in mind as we discuss modern AI — it's still relevant.

After ELIZA, the AI field went through what historians call the "AI winters" — periods of hype followed by disappointment, when the technology couldn't deliver on its promises. Expert systems in the 1980s tried to capture human knowledge in rigid rules: "IF patient has fever AND patient has cough THEN consider pneumonia." These worked in narrow domains but shattered like glass when faced with anything outside their programmed rules.

The lesson from this era: **rule-based AI is brittle.** The real world is too complex, too nuanced, too full of exceptions to capture in hand-written rules. Something fundamentally different was needed.

## Act Two: The Statistical Turn (1990s-2010s)

The "something different" turned out to be statistics. Instead of hand-writing rules, researchers began feeding computers large amounts of data and letting them find patterns on their own.

In the world of language, this manifested as statistical language models. These systems would analyze large collections of text (called "corpora") and learn the statistical relationships between words. Given the phrase "the cat sat on the," the system could look at its data and determine that "mat" was more likely than "refrigerator."

These were the ancestors of today's LLMs, but they were primitive by comparison. They could only look at a few words of context at a time. They were useful for things like spell-checking and basic machine translation, but they couldn't carry on a conversation or write a coherent paragraph.

Meanwhile, a technique called **neural networks** — loosely inspired by the structure of the human brain — was quietly advancing. Neural networks had been around since the 1950s, but they needed more data and more computing power than was available. By the 2000s and 2010s, both of those constraints were dissolving. The internet provided the data. Powerful graphics cards (originally designed for video games) provided the computing power.

The stage was set.

## Act Three: Attention Is All You Need (2017)

In 2017, a team of researchers at Google published a paper with one of the most consequential titles in scientific history: "Attention Is All You Need."

This paper introduced the **Transformer** architecture — the fundamental design behind every modern LLM, including GPT, Claude, Gemini, and Llama. The Transformer was a breakthrough because it solved a problem that had plagued language models for decades: how to handle long-range dependencies.

Here's the problem in everyday terms. In the sentence "The woman who moved from Paris to Tokyo last year after finishing her PhD in computational linguistics said she missed the croissants," the word "croissants" is connected to "Paris" — but there are many words in between. Previous models had a kind of short-term memory problem: by the time they got to "croissants," they'd forgotten about "Paris."

The Transformer's key innovation was the **attention mechanism** — a way for the model to look at *every* word in a sequence simultaneously and figure out which words are most relevant to each other, regardless of how far apart they are.

Going back to our restaurant analogy: imagine a chef who, before cooking anything, reads the *entire* order from beginning to end and makes connections across the whole thing. "Ah, the guest mentioned a nut allergy in the appetizer notes, so I need to remember that for the main course too." Previous models were like a chef who could only remember the last few items in the order. The Transformer chef sees everything at once.

> **"Behind The Curtain" Sidebar**
>
> The "Attention Is All You Need" paper was originally about machine translation — getting computers to translate between languages. The researchers didn't set out to create a general-purpose text generation engine. The broader applications of Transformers — chatbots, code generation, creative writing — emerged later, as people experimented with the architecture and realized it was far more versatile than anyone initially imagined. Many of the most important inventions are repurposed discoveries.

## Act Four: The Scaling Revolution (2018-Present)

With the Transformer architecture in hand, the race was on. And the key discovery was both simple and expensive: **bigger is better.**

In 2018, OpenAI released GPT (Generative Pre-trained Transformer). It was modest by today's standards — 117 million parameters, trained on a collection of books. It could generate somewhat coherent text, but nothing that would make headlines.

GPT-2 came in 2019 with 1.5 billion parameters. OpenAI initially withheld it from the public, worried it was too good at generating convincing fake text. (In retrospect, that concern seems quaint.)

GPT-3 arrived in 2020 with 175 billion parameters and access to a vast portion of the internet. This was the model that made the world pay attention. GPT-3 could write essays, answer questions, translate languages, and even write basic code — all without being specifically trained for any of those tasks. It had learned them as emergent properties of next-token prediction at enormous scale.

Meanwhile, Anthropic was founded in 2021 by former OpenAI researchers who wanted to focus on AI safety — building powerful AI systems that are also trustworthy, honest, and aligned with human values. Their model, Claude, took a different approach to training, emphasizing helpfulness and harmlessness alongside raw capability.

Google developed Gemini (originally called Bard), Meta released the open-source Llama models, and dozens of other companies and research labs entered the race. The field exploded.

> **"This Is Why..." Box**
>
> **This is why different AI models feel subtly different to talk to.** GPT, Claude, Gemini, and Llama are all based on the Transformer architecture and all use next-token prediction. But they were trained on different data, with different objectives, and with different approaches to fine-tuning and safety. It's like how all chefs learn the same basic techniques, but each develops their own style based on their training, their teachers, and their philosophy of cooking. Understanding this helps you choose the right model for the right task.

## The Key Milestones, Translated

Let's put this timeline in terms that matter for everyday users:

**1966 — ELIZA:** AI can fake a conversation using word tricks. Teaches us that humans are eager to see intelligence in machines.

**1980s — Expert Systems:** AI can follow hand-written rules. Teaches us that rigid rules can't capture the complexity of real-world language.

**1990s-2000s — Statistical Models:** AI can learn patterns from data. Teaches us that data-driven approaches beat hand-written rules.

**2017 — Transformers:** AI can pay attention to everything at once. Teaches us that architecture matters — *how* you build the system is as important as what data you feed it.

**2018-2020 — GPT series:** AI scales up and emergent abilities appear. Teaches us that scale can produce qualitative leaps, not just quantitative improvements.

**2021-Present — The current era:** Multiple competing models, focus on safety and alignment, integration into products and workflows. Teaches us that the technology is mature enough to matter for everyone, not just researchers.

## What Didn't Change (And What That Means for You)

Here's something remarkable: from GPT to GPT-3 to GPT-4 to Claude and beyond, the *fundamental mechanism* hasn't changed. It's still next-token prediction using the Transformer architecture. The improvements have come from more data, more parameters, better training techniques, and smarter fine-tuning — not from a fundamentally new approach.

This means the strengths and limitations we'll discuss throughout this book are *structural*. They aren't bugs that will be fixed in the next update. They're inherent to how the technology works. Token boundaries will still matter. The system will still generate one token at a time. It will still be shaping text based on statistical patterns. Understanding these fundamentals gives you durable knowledge — insights that will remain useful even as the models get more powerful.

> **"Try This Now" Exercise**
>
> Try this with our running example. Ask an AI: "Help me plan a career change from accounting to UX design." Now ask it: "Pretend it's 2005 and AI assistants don't exist yet. Where would I go for advice about changing careers from accounting to UX design?" Compare the advice sources the AI suggests for 2005 (career counselors, library books, networking events) with the fact that you're getting this advice from an AI right now. This gives you a visceral sense of how far the technology has come — and highlights that the AI knows about the world *before* it existed in its current form, because it learned from text that described that world.

## The Lesson History Teaches Us

The history of AI language models teaches one overarching lesson: **the simplest approach, applied at sufficient scale, wins.** ELIZA failed because pattern-matching on keywords couldn't scale. Expert systems failed because hand-written rules couldn't scale. The Transformer succeeded because it provided an architecture that *could* scale — and when it scaled, remarkable things emerged.

This lesson should shape your expectations. The AI you're talking to isn't powered by some exotic, incomprehensible technology. It's powered by a clever architecture, an enormous amount of data, and a simple objective function: predict the next token. The magic is in the scale, not the mechanism.

And that means the more you understand about the mechanism, the better equipped you are to use the magic effectively.

> **"Pro Tip" Box**
>
> When you read headlines about new AI models — "GPT-5 released!" or "Claude gets an upgrade!" — ask yourself: what actually changed? Usually, it's some combination of more training data, more parameters, better fine-tuning, or improved safety measures. The underlying approach is the same. This means your fundamental understanding of how to work with these systems stays relevant across updates. You're learning to drive, not learning one specific car.
