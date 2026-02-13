# Lesson 5: Token Limits and Conversation Constraints

## The Size of the Kitchen Counter

Every kitchen counter has a fixed amount of space. No matter how talented the chef, she can only work with as many ingredients as the counter can hold. Pile on too many, and things start falling off the edge. The counter doesn't expand to accommodate more ingredients — it's a hard physical limit.

An LLM has a similar hard limit called the **context window**. This is the maximum number of tokens the model can "see" at once — the total size of the text it can process in a single interaction. Everything must fit on this counter: your messages, the AI's previous responses, any system instructions running behind the scenes, and the response the AI is currently generating.

When the conversation grows beyond the context window, something has to go. And understanding what goes — and when — is essential for using AI effectively, especially in long conversations.

## The Context Window: How Big Is It?

Context windows have grown dramatically over the past few years, but they're still finite. To give you a sense of scale:

- Early models (2020-2022): roughly 2,000 to 4,000 tokens — about 1,500 to 3,000 words. Barely enough for a detailed prompt and response.
- GPT-3.5 era (2023): about 4,000 to 16,000 tokens.
- Current frontier models (2024-2025): 100,000 to 200,000 tokens — roughly 75,000 to 150,000 words. That's the length of a full novel.
- Some specialized models: up to 1,000,000 tokens or more.

A 128,000-token context window sounds enormous. And for many tasks, it is. But it fills up faster than you think, for reasons that aren't immediately obvious.

## Where Do the Tokens Go?

Here's what most people don't realize: your messages are not the only thing consuming tokens. In a typical AI conversation, the context window is shared among:

**1. System instructions (the "kitchen's standing orders").** Behind the scenes, the AI provider includes a system prompt — instructions that tell the model how to behave, what safety guidelines to follow, what persona to adopt. You usually don't see this, but it can consume hundreds or even thousands of tokens. It's like the permanent orders posted in the kitchen: "All dishes must be nut-free. No raw shellfish. Always include a garnish." These orders are always on the counter, taking up space.

**2. Your conversation history.** Every message you've sent and every response the AI has generated in the current conversation. This grows with every turn. A ten-turn conversation can easily reach 5,000-10,000 tokens.

**3. Any attached documents or context.** If you've pasted a document, uploaded a file, or included reference material, that all counts against the context window.

**4. The response being generated.** The AI needs room to produce its response. A detailed, multi-paragraph response might use 500-1,500 tokens.

The practical implication: even with a 128,000-token context window, you can run out of space much faster than you'd expect if you're having long conversations, including large documents, or working in languages with inefficient tokenization.

> **"This Is Why..." Box**
>
> **This is why AI seems to "forget" things you said earlier in a long conversation.** It's not that the AI has a bad memory. It's that your earlier messages may have been pushed out of (or de-prioritized within) the context window as the conversation grew. The AI can only work with what's currently on the counter. If your important context from message three is no longer in the active window, the AI literally cannot see it. This isn't forgetfulness — it's a hard architectural limit.

## The Falling Off the Counter Problem

What happens when the conversation exceeds the context window? Different systems handle this differently, but the common approaches are:

**Truncation:** The oldest messages get dropped. Your first few messages in a long conversation simply disappear from the AI's view. It's as if the earliest ingredients fell off the kitchen counter and were swept away — the chef no longer knows they existed.

**Sliding window:** The system maintains the most recent N tokens, continuously dropping the oldest content as new content is added. The window "slides" forward in time.

**Summarization:** Some systems automatically summarize older parts of the conversation, replacing detailed early messages with a compressed summary. This preserves some context but loses detail — like a prep cook writing "customer wants a healthy meal" instead of keeping the full three-paragraph dietary requirements.

**Selective attention:** More sophisticated systems may try to keep the most *relevant* older content while dropping less relevant portions. This is better but not foolproof — the system's judgment of what's "relevant" may not match yours.

No matter which approach is used, the result is the same: **in long conversations, earlier context gets lost or compressed.** The AI isn't choosing to ignore your earlier messages. It physically cannot see them anymore.

> **"Behind The Curtain" Sidebar**
>
> Here's a detail that surprises most people: the system prompt — those hidden instructions from the AI provider — is typically re-injected at the beginning of every turn. This means those 500-2,000 tokens of system instructions are consuming context window space in *every single exchange.* It's like having a permanent sign on the kitchen counter that never gets moved. In a model with a 128,000-token context window, this overhead is negligible. But in a model with a smaller window, or in a very long conversation where every token counts, the system prompt's footprint matters.

## The Economics of Tokens

Tokens aren't just a technical concept — they're a unit of currency. AI services charge by the token. When you're using an API (as developers and businesses do), you pay for every token in your prompt and every token in the response. When you're using a consumer-facing chatbot, the cost is hidden but still real — it's built into your subscription or absorbed by the provider.

This creates an interesting economics. Every word in your prompt costs something. Every word in the response costs something. And importantly, as the conversation grows, you're paying for the *entire conversation* to be re-processed every turn, because the model reads the full context window each time it generates a response.

A ten-turn conversation doesn't cost ten times as much as a one-turn conversation — it costs more, because each turn includes all previous turns in the context. The cost grows quadratically-ish with conversation length, which is why AI providers offer API pricing that distinguishes between "input tokens" and "output tokens," and why long conversations can get expensive quickly.

For individual users on consumer plans, this mostly manifests as rate limits — you can only have so many conversations or generate so many tokens per day. For businesses using the API, this directly affects their costs.

## Practical Strategies for Working Within Token Limits

Understanding token limits transforms how you manage AI conversations. Here are strategies that work:

**Start fresh for new topics.** If you're switching from one task to another, start a new conversation. The old context is just consuming tokens without adding value to your new task. Don't ask the AI to "forget everything we discussed" — just open a new chat.

**Front-load your most important context.** Since the beginning of a conversation is most likely to be retained (or at least processed most fully), put your most critical instructions and context in your first message. The system prompt + your first message form the foundation that influences everything that follows.

**Summarize and reset periodically.** In long working sessions, periodically ask the AI to summarize the key decisions and context, then start a new conversation with that summary as the starting point. You're manually doing what the system might do automatically — but with more control over what's preserved.

**Be concise but complete.** Every unnecessary word costs tokens. This doesn't mean being terse or cryptic — it means being precise. "I'm an accountant transitioning to UX" is better than "So basically what I'm trying to do is, like, change my entire career, you know? I've been working in accounting for a while now and I think maybe UX design might be something I'd be good at." Same information, far fewer tokens.

**Manage attachments wisely.** If you paste a 20-page document into the chat, that's thousands of tokens consumed immediately. Consider pasting only the relevant sections, or summarizing the document and pasting the summary.

> **"Try This Now" Exercise**
>
> Start a conversation with an AI and have a substantial back-and-forth — at least ten turns — about our running example (planning a career change from accounting to UX design). In your eleventh message, reference something very specific that you mentioned in your first or second message. See if the AI remembers it accurately. Then start a new conversation and try to get the same quality of response in a single, well-crafted prompt. Compare the efficiency and quality of the two approaches.

## The Before/After: Token-Aware Conversation Management

**Before (token-unaware):**

You have a rambling 30-turn conversation where you gradually reveal your situation, change topics twice, include long tangents about your weekend, and eventually ask for a career transition plan. The AI's response in turn 30 is generic because it can no longer see your specific context from the early turns.

**After (token-aware):**

You start with a focused, well-structured prompt that includes your full context. After 8-10 turns of productive refinement, you ask the AI to summarize the key points and decisions. You copy that summary, start a new conversation, paste the summary as context, and continue with fresh token budget. The AI's responses stay specific and high-quality because the relevant context is always within the active window.

The difference isn't about being robotic or formal. It's about understanding that the AI has a finite counter space and managing that space intelligently.

## Token Limits and the Illusion of Memory

One of the most persistent misconceptions about AI is that it "remembers" your conversation the way a human would. It doesn't. Every time you send a new message, the entire conversation — your messages, the AI's responses, the system prompt — is fed to the model from scratch. The model doesn't "remember" the previous turn; it re-reads the entire conversation history and generates a response based on that full context.

This means the AI's "memory" is literally the text in the context window. Nothing more. If text leaves the context window, it's gone. The AI doesn't have a separate long-term memory where old conversations are stored (though some newer systems are experimenting with external memory features, these work differently from the model's native context).

Understanding this transforms the "forgetful AI" problem from frustrating to manageable. The AI isn't forgetful — it has perfect recall of everything in its context window and zero recall of everything outside it. Your job is to ensure that the important stuff stays inside the window.

> **"Pro Tip" Box**
>
> For important, multi-session projects (like planning a career change over several weeks), keep a running document where you summarize the key decisions, insights, and context from each AI conversation. At the beginning of each new session, paste the relevant portions of this document into the conversation. You become the AI's external memory, ensuring that important context is always available regardless of context window limits. Think of it as a handoff note between shifts at the restaurant — the new chef (each fresh conversation) gets a briefing on what's been decided so far.

---

## Chapter 2 Summary

The AI doesn't read text the way you do. Before processing a single word of your message, a tokenizer chops your text into tokens — pieces that may be whole words, word fragments, or even individual characters. These tokens are the fundamental unit of everything the AI does. The tokenizer uses a fixed vocabulary of roughly 32,000 to 100,000 tokens, optimized for common patterns in the training data (which is overwhelmingly English). This creates a cascade of consequences: character-level tasks like letter counting are unreliable, non-English languages are tokenized less efficiently (costing more and sometimes performing worse), specialized terminology gets fragmented, and every conversation operates within a hard token limit called the context window. Understanding tokenization gives you practical tools: you can work with the grain of the system, manage conversations more effectively, and recognize when apparent AI failures are really tokenization artifacts.

## Five Key Takeaways

1. **Tokens, not words, are the AI's native unit.** Everything the AI does happens at the token level. A token might be a word, a word fragment, a character, or a common phrase. Understanding this distinction explains many of the AI's quirks and limitations.

2. **The token boundary problem is real and predictable.** When a task requires working at the character level (counting letters, anagrams, exact string manipulation), you're working against the grain of token-level processing. Workarounds exist (ask the model to spell out words character by character), but the limitation is fundamental.

3. **Tokenization is unequal across languages.** English text gets the most efficient tokenization. Non-English languages, especially those using non-Latin scripts, consume more tokens for the same meaning. This affects cost, context window usage, and potentially response quality.

4. **The vocabulary is fixed and culturally biased.** The tokenizer's vocabulary was created from a specific dataset and doesn't change. New words, unusual names, and specialized terms may be poorly represented, requiring fragmentation that makes them harder for the model to process.

5. **Context windows are finite and shared.** Every conversation operates within a hard token limit. Your messages, the AI's responses, system instructions, and any attached documents all compete for space. Managing this space intelligently is key to maintaining conversation quality.

## Now You Know Why...

1. **Now you know why** AI can pass a bar exam but might fail to count the letters in "strawberry." The bar exam requires meaning-level reasoning, which aligns perfectly with token-level processing. Letter counting requires character-level analysis, which cuts across token boundaries. The model's intelligence isn't the issue — the mismatch between the task level and the processing level is.

2. **Now you know why** AI conversations seem to "lose the thread" after many exchanges. The context window is finite, and older messages get truncated or compressed. The AI literally cannot see what was said earlier if it's fallen outside the window. This isn't forgetfulness — it's a hard limit of the architecture.

3. **Now you know why** AI can seem more fluent and capable in English than in other languages. English gets the most efficient tokenization, meaning more meaning per token, more room in the context window, and richer pattern access. The model's underlying capability is the same, but the tokenization layer creates an uneven playing field.

## Three Actionable Strategies

1. **Work with the grain of token-level processing.** For tasks that naturally operate at the meaning level — analysis, writing, strategy, explanation — the AI is in its element. For tasks that require character-level precision — letter counting, exact formatting, string manipulation — restructure your request to make character-level information explicit. Ask the model to spell things out, work step by step, and show its work.

2. **Manage your context window like a budget.** Start conversations with focused, complete context. Avoid sprawling conversations when a fresh start with a good prompt would serve you better. For long projects, periodically summarize and restart. Every token counts — spend them on what matters.

3. **Be your own external memory.** For projects that span multiple conversations, maintain a running document of key decisions, context, and outputs. Paste the relevant portions into each new conversation. Don't rely on the AI's "memory" across sessions — there isn't one. You are the bridge between conversations, and the quality of that bridge directly affects the quality of the AI's responses.
