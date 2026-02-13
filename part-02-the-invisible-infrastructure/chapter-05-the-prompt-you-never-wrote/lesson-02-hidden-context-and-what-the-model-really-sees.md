# Lesson 2: Hidden Context and What the Model Really Sees

## The Iceberg Under Your Message

Picture an iceberg. The part above the waterline -- the part you can see -- is small and neat. Below the surface, the mass of ice is enormous, extending hundreds of feet into the dark water. Your message to an AI is that visible tip. What the model actually processes is the entire iceberg.

In the previous lesson, we revealed the system prompt: thousands of words of invisible instructions loaded before your conversation begins. But the system prompt is only one piece of the hidden context. In this lesson, we are going to map the entire iceberg -- every piece of information the model receives that you did not write and cannot see.

By the end of this lesson, you will understand why the AI sometimes seems to know things you never told it, why it occasionally behaves inconsistently, and why context is the single most important factor in the quality of AI responses.

## The Full Context Stack

When you type a message and hit send, here is what the model actually receives, assembled in layers like geological strata:

**Layer 1: The System Prompt**
As we covered in Lesson 1, this is the foundational instruction set. Identity, rules, personality, capabilities, and behavioral guidelines.

**Layer 2: Tool Definitions**
If the AI has access to tools -- web search, code execution, file reading, image generation -- each tool comes with a detailed specification. These specifications tell the model what each tool does, what inputs it expects, and when to use it. A single tool definition can be 200-500 words. An AI with access to ten tools might have 3,000-5,000 words of tool documentation injected into its context before your message arrives.

**Layer 3: Retrieved Memories**
Many modern AI systems have persistent memory -- things you told it in previous conversations that it stored and now retrieves. If you once told the AI "I'm a teacher in Portland who specializes in middle school science," that information might be pulled from a database and injected into the context. You did not write it in this conversation, but the model sees it as if you did.

**Layer 4: Retrieved Documents (RAG)**
If the AI has access to a knowledge base -- your company's documents, a set of PDFs you uploaded, a collection of web pages it searched -- relevant snippets from those documents get injected into the context. We will explore RAG in depth in Chapter 8, but for now, know that the model might be reading excerpts from ten different documents alongside your question.

**Layer 5: Conversation History**
Everything said in the current conversation -- your messages and the AI's responses -- is included. In a long conversation, this can be tens of thousands of words. The model re-reads the entire conversation every time it generates a new response.

**Layer 6: Dynamic Injections from Classifiers**
As we will explore in Chapter 6, hidden classifier models analyze your message and can inject additional warnings or instructions into the context. If a classifier detects that your message touches on a sensitive topic, it might add something like: "The user's message involves medical advice. Remind them to consult a healthcare professional." You never see this injection, but the model does.

**Layer 7: Your Actual Message**
Finally, at the very bottom of this stack, your message. The thing you actually typed.

> **"Behind The Curtain"**
> In a production AI system, your message might account for as little as 0.5% of the total tokens the model processes. Imagine writing a one-sentence question on a sticky note and attaching it to the last page of a 200-page document. That is roughly the proportion. The model reads all 200 pages, then your sticky note, then generates a response informed by everything it just read.

## What This Looks Like in Practice

Let us trace our running example through the full context stack. You open Claude and type: "Help me plan a career change from accounting to UX design."

Here is a simplified version of what the model actually receives:

```
[SYSTEM PROMPT - ~3,000 words]
You are Claude, made by Anthropic. You are helpful, harmless, and honest...
[personality traits, behavioral rules, safety guidelines, formatting preferences,
date awareness, knowledge cutoff information, and dozens of specific instructions
for handling various scenarios...]

[TOOL DEFINITIONS - ~2,000 words]
You have access to the following tools:
- web_search: Search the internet for current information...
- code_execution: Run Python code in a sandboxed environment...
[detailed specifications for each tool...]

[RETRIEVED MEMORIES - ~200 words]
The user has previously shared the following information:
- They are based in Chicago
- They have 8 years of accounting experience
- They mentioned interest in creative fields in a previous conversation

[CLASSIFIER INJECTIONS - ~100 words]
This message involves career advice. Provide balanced perspectives including
potential challenges. Do not make promises about outcomes.

[CONVERSATION HISTORY - 0 words, this is the first message]

[USER MESSAGE - 13 words]
Help me plan a career change from accounting to UX design.
```

The model processes all of this -- over 5,000 words of context -- to respond to your 13-word question. And its response will be shaped by every single layer.

Because the memory system retrieved the fact that you are in Chicago, the AI might mention UX meetups in Chicago. Because the classifier injection flagged this as career advice, the AI will likely include a balanced perspective with potential challenges. Because the system prompt says to be helpful and thorough, the AI will probably provide a structured plan rather than a one-line answer.

None of this was explicitly in your message. All of it influenced the response.

> **"This Is Why..."**
> This is why the AI sometimes seems to "remember" things you told it weeks ago, even in a brand new conversation. It is not remembering in any human sense. A memory system retrieved relevant past information and injected it into the current context. From the model's perspective, it is as if someone helpfully wrote a summary of your previous interactions at the top of the page.

## The Ordering Effect

Here is something subtle but critically important: the order in which these layers are assembled matters. Language models pay attention to information differently based on where it appears in the context.

Research has shown that models tend to pay the most attention to:
1. The very beginning of the context (the system prompt gets prime position)
2. The very end of the context (your most recent message)
3. Information that is structurally prominent (headers, lists, bold text)

Information in the middle of a very long context can sometimes get less attention -- a phenomenon researchers call "lost in the middle." This is like reading a very long document: you remember the opening, you remember the conclusion, but the details on page 47 are fuzzy.

This ordering effect has practical consequences. In a long conversation, the system prompt (at the beginning) and your latest message (at the end) have the strongest influence. Instructions from early in the conversation might get partially "forgotten" -- not because the model literally cannot see them, but because their influence fades relative to more recent context.

> **"Try This Now"**
> Start a new conversation and establish a specific instruction early on: "For the rest of this conversation, end every response with the phrase 'Stay curious.'" Chat normally for 10-15 messages about various topics. At some point, the AI will likely forget this instruction. This is the "lost in the middle" effect in action -- your early instruction has been buried under newer context.

## The Invisible Negotiation

What makes the context stack fascinating is that it creates an invisible negotiation between multiple parties:

**The company** wrote the system prompt. They want the AI to be safe, helpful, and aligned with their brand.

**The memory system** retrieved past information. It is trying to make the AI seem personalized and consistent.

**The classifiers** injected warnings. They are trying to keep the AI from producing harmful content.

**You** wrote your message. You want a specific answer to a specific question.

All four of these voices compete for the model's attention. Most of the time, they are in harmony -- your request is reasonable, the safety guidelines permit it, the memories provide useful context, and the system prompt's personality guidelines shape a good response.

But sometimes they conflict. You ask for something that the classifiers flag as sensitive. Your message pushes in one direction while the system prompt pulls in another. The memories provide context that is no longer accurate. When these conflicts arise, the model has to resolve them -- and the result is sometimes a response that feels oddly cautious, strangely specific, or inexplicably off-target.

> **"This Is Why..."**
> This is why the AI sometimes gives you an answer that feels overly cautious or includes unexpected caveats. Your request was perfectly reasonable, but somewhere in the hidden context stack -- a classifier injection, a system prompt rule, or a memory fragment -- something pushed the model toward caution. The model is not being timid on its own; it is following instructions you cannot see.

## The Context as a Stage

Think of it this way. The model is an actor on a stage. You, the user, are the audience shouting a request: "Tell me about career changes!" But you are not the only one talking to the actor. The director (system prompt) is whispering in their ear. The prompter (memories) is feeding them lines about your past. The stage manager (classifiers) is signaling from the wings about what topics to avoid. The set designer (tool definitions) has placed certain props on stage that the actor can choose to use.

The actor has to synthesize all of these inputs into a single, coherent performance -- one that satisfies you, the audience, while also following the director's vision and the stage manager's safety signals.

This is why AI interaction is more nuanced than it appears. You think you are having a one-on-one conversation. In reality, you are one voice in a chorus, and the model is trying to harmonize with everyone.

## The Transparency Gap

This leads to one of the most important themes in this book: the transparency gap. There is a vast difference between what you see and what the model sees. You see:

- A chat interface
- Your messages
- The AI's responses

The model sees:

- Thousands of words of system instructions
- Tool specifications
- Retrieved memories
- Classifier injections
- The full conversation history
- Your message

This gap has real consequences. When the AI does something unexpected, you have no way to know whether it was caused by:
- The model itself (its training, its weights, its reasoning)
- The system prompt (a specific instruction from the company)
- A classifier injection (a safety flag triggered by your message)
- A memory retrieval (something you said weeks ago in a different context)
- A tool result (information the AI pulled from a search or document)

Understanding that this gap exists -- even without seeing the specific contents of each layer -- is itself a powerful tool for working with AI more effectively.

> **"Pro Tip"**
> When the AI gives you an unexpected response, do not assume the model is broken or stupid. Instead, consider: "What might be in the hidden context that is causing this?" Then try strategies to work around it: rephrase your request, provide more explicit context, or start a fresh conversation to clear out any accumulated hidden context that might be interfering.

## Before and After: Working With Hidden Context

**Before understanding hidden context** (bad prompt):
"I already told you I'm in Chicago. Why do you keep asking? And why are you being so cautious? Just answer my question."

The user is frustrated because they do not understand that the AI's behavior is shaped by layers of invisible context. They think the AI is being deliberately obtuse.

**After understanding hidden context** (good prompt):
"For context: I'm based in Chicago with 8 years of accounting experience. I want a direct, actionable career transition plan to UX design. Focus on practical steps rather than caveats."

The user now provides explicit context (so they do not rely on invisible memory retrieval) and explicit instructions about the type of response they want (so their voice is louder than the classifier injections pushing for caution). The result is dramatically better.

## The Expanding and Contracting Window

One final concept for this lesson. The total amount of hidden context is not static -- it expands and contracts throughout a conversation.

At the start of a fresh conversation, the context is relatively lean: the system prompt, tool definitions, and maybe some retrieved memories. As you chat, the conversation history grows, and the total context expands. If the AI searches the web or retrieves documents, even more content gets injected.

But there is a hard limit -- the context window, which we will explore in depth in Chapter 8. When the total context approaches this limit, something has to give. Old conversation history might be summarized or truncated. Retrieved documents might be pruned. The system prompt, however, almost always stays intact, because it is considered the highest-priority content.

This means that in a very long conversation, your early messages are the first to lose fidelity, while the system prompt's instructions remain sharp and clear. The company's voice never fades. Yours gradually does.

Understanding this dynamic is crucial for getting the most out of long AI conversations -- and it is something we will return to in detail when we discuss memory and context windows.

---

Now that you can see the full iceberg -- every layer of hidden context that surrounds your message -- let us examine how one of the most important layers works: the pre-defined personality, rules, and behavioral framework that turns a raw language model into the AI assistant you interact with every day.
