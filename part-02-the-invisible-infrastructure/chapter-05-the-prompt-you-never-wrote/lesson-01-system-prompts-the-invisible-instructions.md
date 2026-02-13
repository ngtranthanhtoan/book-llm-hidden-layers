# Lesson 1: System Prompts — The Invisible Instructions

## The Conversation That Started Before You Arrived

Imagine walking into a restaurant and sitting down at your table. You open the menu, choose your dish, and tell the waiter what you want. Simple enough. But here is what you did not see: an hour before you arrived, the head chef gathered the entire kitchen staff and handed them a five-page document. It specified the restaurant's philosophy, the flavor profiles to emphasize tonight, which ingredients to avoid due to supplier issues, how to handle customers who ask for off-menu items, the correct portion sizes, how to plate each dish, and the precise level of spice that is acceptable. By the time your order reaches the kitchen, the staff has already internalized dozens of instructions you know nothing about.

This is exactly what happens every time you type a message into ChatGPT, Claude, Gemini, or any AI assistant. Before you write a single word, thousands of invisible words have already been delivered to the model. These words are called the **system prompt** -- and they are the most influential piece of text in your entire conversation.

You have never seen them. You did not write them. But they shape every response you receive.

## What Is a System Prompt, Exactly?

A system prompt is a set of instructions, written by the company that built the AI product, that is fed to the language model at the beginning of every conversation. Think of it as a detailed character brief given to an actor before they walk on stage. The audience never sees the brief, but it determines everything about the performance -- the accent, the mannerisms, the boundaries of what the character will and will not do.

In technical terms, here is what the model actually receives when you type a simple question like "What's the capital of France?":

```
[SYSTEM]: You are Claude, made by Anthropic. You are helpful, harmless, and honest.
You should provide thoughtful, well-structured responses. You should not produce
harmful content. When you are unsure about something, say so rather than making
something up. You value accuracy and nuance. You should...

[...hundreds or thousands more words of instructions...]

[USER]: What's the capital of France?
```

That single line from you -- seven words -- is dwarfed by the system prompt that precedes it. In many production systems, the system prompt can be 2,000 to 10,000 words long. Some are even longer. Your seven-word question arrives at the end of this massive document, like a sticky note appended to a legal contract.

> **"This Is Why..."**
> This is why the AI sometimes seems to "know" things about itself -- like its name, its maker, its capabilities, or its limitations. Nobody programmed that knowledge into the model's weights during training. It was written into the system prompt that gets loaded fresh at the beginning of every conversation.

## The Anatomy of a Real System Prompt

While most companies guard their system prompts as trade secrets, enough have been leaked, reverse-engineered, or officially published that we have a solid picture of what they contain. A typical production system prompt has several distinct sections:

**Identity and persona.** This is where the AI learns who it is supposed to be. "You are ChatGPT, a large language model trained by OpenAI." Or "You are Claude, made by Anthropic." This section often includes personality traits: be helpful, be concise, be warm, be professional.

**Capabilities and limitations.** The system prompt tells the model what it can and cannot do. Can it browse the internet? Execute code? Generate images? Read uploaded files? Even if the underlying model has these capabilities, the system prompt can enable or disable them. It is like telling the chef, "Tonight, no desserts. We are not offering the dessert menu."

**Behavioral rules.** This is often the longest section. It specifies how the model should handle sensitive topics, what it should refuse, how it should format responses, when it should ask clarifying questions, and how it should behave when uncertain. These rules can be extraordinarily detailed -- covering everything from how to discuss political topics to how to handle requests for medical advice to what to do when a user seems distressed.

**Knowledge boundaries.** The system prompt often tells the model about its training data cutoff date and instructs it to acknowledge when it does not have current information. "Your training data goes up to April 2024. If a user asks about events after that date, acknowledge that your information may be outdated."

**Formatting preferences.** Should the model use bullet points? Markdown? Short paragraphs? Should it default to formal or informal tone? These preferences are baked into the system prompt.

**Tool instructions.** If the model has access to tools -- web search, code execution, image generation -- the system prompt provides detailed instructions for when and how to use them. "If the user asks about current events, use the web search tool. If the user asks you to analyze data, use the code interpreter."

> **"Behind The Curtain"**
> When portions of ChatGPT's system prompt were leaked in early 2024, researchers discovered it was over 1,700 words long -- and that was just the base prompt, before any conversation-specific context was added. Claude's system prompt has been officially published by Anthropic and is similarly extensive. These are not casual instructions. They are carefully engineered documents that have gone through dozens of revisions by teams of researchers, ethicists, and product designers.

## The Restaurant's Standing Orders

Let us return to our restaurant analogy, because it illuminates something crucial about how system prompts work.

The standing orders in a restaurant kitchen do not just say "cook good food." They say things like: "If a customer asks for a steak well-done, we still serve it without judgment. If a customer asks for raw chicken, we politely decline and explain why. If a customer has an allergy, we take extra care. If a customer asks for a dish we do not serve, we suggest the closest alternative."

System prompts work the same way. They are not vague guidelines -- they are detailed decision trees for hundreds of specific scenarios. They anticipate what users will ask and pre-program how the model should respond. This is why you can ask ten different AI products the same question and get ten noticeably different responses, even when they use the same underlying model.

Consider our running example. When you type "Help me plan a career change from accounting to UX design," the system prompt has already told the model:

- Whether to be encouraging or cautiously realistic
- Whether to ask clarifying questions first or dive into advice
- How long the response should be
- Whether to use bullet points or prose
- Whether to mention potential risks or focus on the positive path
- Whether to recommend specific tools, courses, or resources
- How to handle the fact that it cannot know the user's personal financial situation

All of this is determined before the model processes a single word of your request.

## How System Prompts Actually Influence the Model

Here is something important to understand about how language models work. As we discussed in Part 1, the model generates text by predicting the most likely next token given everything that came before. The system prompt is part of that "everything that came before." It is not a separate channel of communication -- it is literally more text that the model reads as context.

This means the system prompt influences the model the same way your message does: by shifting the probability of which tokens come next. When the system prompt says "be concise," it makes shorter responses statistically more likely. When it says "always be helpful," it makes agreeable, solution-oriented language more probable. When it says "never provide instructions for making weapons," it makes refusal language much more likely when such topics arise.

Think of it like this: imagine you are giving directions to someone. If you say "take me to the nearest coffee shop," they will pick the closest one. But if you first say "I only drink specialty pour-over coffee, I refuse to go to chain restaurants, and I prefer places with outdoor seating," then the same request -- "take me to the nearest coffee shop" -- produces a completely different result. The pre-instructions changed the decision landscape.

> **"This Is Why..."**
> This is why the same AI sometimes seems to have a different personality depending on where you use it. ChatGPT, Claude, Gemini, and Copilot can all be built on similar underlying technology, but their system prompts create radically different behaviors. It is the same brain, given different instructions.

## The Scale of What You Cannot See

Let us put some numbers to this. In a typical conversation:

- **Your message**: 20-100 words
- **The system prompt**: 1,000-10,000 words
- **Conversation history** (in an ongoing chat): 0-50,000 words
- **Injected context** (retrieved memories, search results, etc.): 0-20,000 words

Your message might represent less than 1% of what the model is actually processing. You are writing a Post-it note, and the model is reading it alongside an entire filing cabinet of other instructions.

This is not a flaw -- it is a feature. The system prompt is what makes a raw language model into a useful, safe, and coherent product. Without it, the model would have no consistent identity, no safety guidelines, no formatting preferences, and no sense of what tools it can use. It would be like hiring a brilliant chef with no training, no recipes, and no health code to follow. The raw talent is there, but the results would be unpredictable and sometimes dangerous.

> **"Try This Now"**
> If you use Claude, go to your profile settings and look for "Custom Instructions" or "Style." If you use ChatGPT, check your Settings for "Custom Instructions." Write something specific -- like "Always respond as if you are explaining to a bright 12-year-old" -- and watch how dramatically the same model changes its behavior. You have just written a tiny system prompt of your own. Now imagine what a 5,000-word version can do.

## The Power and the Responsibility

System prompts represent an enormous amount of power concentrated in the hands of the companies that write them. They determine:

- What the AI will and will not discuss
- How cautious or bold the AI will be
- What values the AI appears to hold
- How the AI balances helpfulness against safety
- What personality the AI presents to millions of users

This is why system prompt design has become one of the most important -- and most debated -- activities in AI development. A single word change in a system prompt can alter the experience of millions of users. It is editorial power at a scale that no newspaper editor or television producer has ever wielded.

And yet, most users have no idea it exists.

> **"Pro Tip"**
> Understanding that system prompts exist is itself a superpower. When the AI refuses a reasonable request, gives an oddly formatted response, or seems to have a particular personality quirk, ask yourself: "Is this coming from the model, or from the system prompt?" Often, the answer is the system prompt -- and knowing that helps you work around limitations by rephrasing your request in ways that align with (rather than fight against) those invisible instructions.

## Before and After: The System Prompt Difference

**Before understanding system prompts** (bad prompt):
"Why won't you help me with this? You're useless."

The user is frustrated because the AI refused a request, and they think the AI itself is making the decision. They argue with the model as if it is a person with opinions.

**After understanding system prompts** (good prompt):
"I understand you may have guidelines about this topic. Can you help me understand what aspect you can assist with, and suggest an alternative approach for what you can't?"

The user now understands that invisible instructions are shaping the response. Instead of arguing with the model, they work within the system -- and often get much better results.

---

The system prompt is the first and most powerful hidden layer between your message and the AI's response. But it is only the beginning. In the next lesson, we will zoom out to see the full picture of what the model actually sees when you send a message -- and it is far more than you might imagine.
