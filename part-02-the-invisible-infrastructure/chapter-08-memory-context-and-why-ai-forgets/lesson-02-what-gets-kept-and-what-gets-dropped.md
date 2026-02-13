# Lesson 2: What Gets Kept and What Gets Dropped

## The Librarian's Impossible Choice

Imagine you are the librarian of a very unusual library. It has exactly one hundred shelves, and every shelf is full. Every day, new books arrive. For every new book that must go on a shelf, an existing book must be removed. Your job is to decide which books to keep and which to discard -- knowing that once a book leaves the library, it is gone forever, and anyone who needed that book will find an empty space instead.

This is the daily dilemma of the context management system in every AI conversation. The context window has a fixed size. New information constantly arrives: your latest message, the AI's latest response, fresh tool results, updated memory retrievals. When the window fills up, something must go. The decisions about what stays and what goes are among the most consequential -- and least visible -- operations in the entire AI infrastructure.

## The Priority Hierarchy

Not all content in the context window is treated equally. There is an implicit hierarchy of importance, and when space gets tight, the system starts trimming from the bottom of the hierarchy upward.

**Priority 1: The System Prompt (almost never removed).** The system prompt is the most protected content in the context window. It defines who the AI is, what rules it follows, and how it behaves. Removing the system prompt mid-conversation would be like removing a chef's knowledge of cooking mid-service. The AI would lose its identity, its safety guidelines, and its behavioral framework. For this reason, the system prompt is almost always preserved in full, regardless of how long the conversation grows.

**Priority 2: Your Most Recent Message (never removed).** The message you just sent is obviously essential -- it is the request the model needs to respond to. This is always preserved.

**Priority 3: The Most Recent AI Response (usually preserved).** The model's last response is important because follow-up questions often reference it. "Can you expand on point three?" only makes sense if the model can see what "point three" was.

**Priority 4: Recent Conversation History (preserved as long as possible).** The last several exchanges are typically preserved because they provide the immediate conversational context. Most follow-up questions and continuations make sense only in the context of what was just discussed.

**Priority 5: Older Conversation History (first to be trimmed).** As the context window fills up, the oldest messages are the first candidates for removal or summarization. The system assumes that recent context is more relevant than distant context -- an assumption that is usually but not always correct.

**Priority 6: Tool Definitions (preserved but sometimes condensed).** If the AI has access to many tools, their definitions take up significant space. Under pressure, the system might remove definitions for tools unlikely to be needed in the current conversation, keeping only the most relevant ones.

**Priority 7: Retrieved Context (can be refreshed).** Memories, retrieved documents, and search results can be re-retrieved if needed. This makes them lower priority for preservation -- the system knows it can go get them again if they become relevant later.

> **"Behind The Curtain"**
> The priority hierarchy is not standardized across AI companies. Different products make different choices about what to preserve. Some aggressively protect conversation history at the expense of tool definitions. Others prioritize tool access and are more willing to summarize old conversations. These design decisions create subtle but noticeable differences in how different AI products handle long conversations.

## Strategies for Trimming

When the context window approaches its limit, the system has several strategies for making room.

### Strategy 1: Hard Truncation

The simplest approach: cut off the oldest messages entirely. Everything before a certain point is simply removed from the context.

**Pros:** Simple to implement, no information distortion, predictable behavior.
**Cons:** Abrupt loss of context. Important details from early in the conversation vanish completely.

**The analogy:** It is like clearing your desk by picking up the bottom half of the paper stack and throwing it in the trash. Fast and effective, but you might lose something important.

### Strategy 2: Summarization

A more sophisticated approach: before discarding old messages, a smaller, faster model creates a compressed summary of them. The summary replaces the original messages, preserving key points while using far fewer tokens.

For example, twenty messages of detailed career planning discussion might be summarized as:

"Previous conversation summary: User is a senior CPA (8 years, Chicago) planning to transition to UX design within 12 months. Key constraints discussed: $5,000 budget, family of four, need to maintain income during transition. Skills gaps identified: user research methods, prototyping tools (Figma), UX writing. Agreed plan includes online courses, portfolio building, and networking at local meetups. User expressed concern about age bias in tech industry."

This summary captures the essential information in perhaps 100 tokens, replacing what might have been 5,000 tokens of full conversation. The space savings are dramatic -- but detail is lost. The specific examples discussed, the nuances of the AI's recommendations, the back-and-forth exploration of ideas -- all of this is compressed into a telegraphic summary.

**Pros:** Preserves key information, saves significant space, allows much longer effective conversations.
**Cons:** Loses nuance, can miss important details, introduces potential distortion (the summary model might emphasize the wrong things).

> **"This Is Why..."**
> This is why the AI sometimes seems to remember the broad strokes of your earlier conversation but gets the details wrong. It is working from a summary, not the original messages. It knows you discussed budget constraints, but it might not remember the exact number. It knows you talked about skills gaps, but it might not recall the specific tool you asked about. The summary preserved the themes but lost the specifics.

### Strategy 3: Selective Retention

The most advanced approach: instead of treating conversation history as a simple timeline (keep recent, drop old), the system tries to identify which earlier messages are most relevant to the current conversation state and keeps those selectively.

For example, if the conversation has evolved from career planning into a detailed discussion of Figma tutorials, the system might retain the early messages about UX design goals and skill gaps (relevant to the current Figma discussion) while discarding early messages about financial constraints (not currently relevant).

**Pros:** Keeps the most relevant context regardless of age.
**Cons:** Requires sophisticated relevance estimation that can make mistakes. Sometimes information that seems irrelevant becomes relevant again later.

### Strategy 4: Hybrid Approaches

Most production systems use a combination of strategies:

1. The most recent N messages are always preserved in full (hard preservation)
2. Older messages are summarized into a compressed history (summarization)
3. Certain "pinned" pieces of information from the system prompt or user preferences are always retained (selective retention)
4. Retrieved context is refreshed as needed rather than permanently occupying space

This hybrid approach tries to get the benefits of all strategies while minimizing the drawbacks of each.

## The Information Triage

Let us watch information triage happen in our running example.

You are in message 30 of a career planning conversation. The context window is getting full. Here is what the system has to work with, and the decisions it makes:

**Keep (high priority):**
- System prompt (identity, rules, safety)
- Your latest message: "What Figma courses do you recommend?"
- The AI's last response about prototyping tools
- Recent exchange about building a UX portfolio
- Summary of earlier conversation

**Summarize (medium priority):**
- Detailed back-and-forth about financial planning from messages 5-10
- Discussion of networking strategies from messages 12-15
- Analysis of the Chicago job market from messages 8-9

**Drop (low priority):**
- Your initial greeting and the AI's welcome response
- A tangent about a friend's career change experience
- Some back-and-forth about formatting preferences ("Can you use bullet points?")

The result: the context window now contains a focused, relevant conversation context that prioritizes your current topic (Figma courses) while maintaining awareness of the broader career transition plan (through the summary). The greeting, the tangent, and the formatting preferences -- deemed least relevant -- are gone.

> **"Try This Now"**
> In a long conversation, try referencing something very specific from early in the chat -- not just the topic, but a specific detail. For example, if in message 3 you discussed a specific salary figure, ask about it in message 25: "What was the salary range we discussed earlier?" If the AI provides the exact number, the original message is still in the context. If it hedges or gives a slightly different number, it is probably working from a summary. If it has no idea what you are talking about, the information was dropped entirely. This test reveals which context management strategy your AI product uses.

## The Asymmetry of Loss

One of the most important things to understand about context trimming is that the loss is asymmetric -- the AI does not know what it has forgotten.

When information is removed from the context window, the AI has no awareness that the information ever existed. It cannot tell you "I used to know your budget but I've forgotten it." It simply does not have the budget information and does not know it ever did. If you ask about the budget, the AI will either ask you to provide it (if it is well-designed) or make assumptions (if it is not).

This asymmetry creates a dangerous illusion. The AI responds confidently at every point in the conversation. When it has full context, its confidence is justified. When it has lost context, its confidence is misleading. It does not sound any less sure of itself -- it just has less information to be sure about.

**The analogy:** Imagine a consultant who has amnesia. They walk into every meeting fully confident and competent, drawing on whatever documents are on their desk. But some crucial documents were removed without their knowledge. They will give advice based on incomplete information with the same confidence they would give if they had everything. This is the context window problem in a nutshell.

> **"Pro Tip"**
> For critically important conversations, do not rely on the AI's memory of previous exchanges. Treat every message in a long conversation as if it might be the AI's first encounter with key facts. Restate important constraints, key numbers, and critical context when they are relevant to your current question. This is not redundant -- it is insurance against context loss. Think of it as always keeping the most important documents on top of the desk where they cannot be buried.

## The Context Window and Conversation Design

Understanding context management changes how you should design your conversations with AI.

**Short, focused conversations outperform long, meandering ones.** A 10-message conversation where every message is on-topic and builds on the previous one will produce better results than a 50-message conversation that wanders across multiple topics. Less context to manage means less information loss.

**Topic changes are context-expensive.** When you change topics mid-conversation, the old topic information becomes less relevant and is a prime candidate for trimming. If you need to discuss multiple topics, consider using separate conversations for each one.

**Restating context is not redundant; it is strategic.** Repeating key information at appropriate points keeps it in the active context window. "Given my budget of $5,000 and my 12-month timeline..." is not wasted words -- it is a context preservation technique.

**Front-loading matters.** In a long conversation, put your most important context in your first and most recent messages -- the two positions that are most reliably preserved.

## Before and After: Managing Context Loss

**Before understanding context management** (bad approach):
User message 1: "My budget is $5,000, I'm in Chicago, and I need to transition within 12 months."
[...25 messages of discussion...]
User message 27: "So what's the best boot camp given my constraints?"

The AI recommends a $15,000 boot camp in San Francisco that takes 18 months. It violated all three constraints because they were pushed out of the context window fifteen messages ago.

**After understanding context management** (good approach):
User message 1: "My budget is $5,000, I'm in Chicago, and I need to transition within 12 months."
[...25 messages of discussion...]
User message 27: "Remembering my key constraints -- $5,000 budget, Chicago-based, 12-month maximum timeline -- what's the best boot camp option?"

The AI recommends an affordable online program with in-person meetup options in Chicago that fits within the budget and timeline. The restated constraints ensured they were in the active context window when the recommendation was made.

---

The context window limits what the AI can hold during a single conversation. But what about between conversations? In the next lesson, we explore the persistent memory systems that are trying to solve a much harder problem: giving the AI a lasting memory across sessions.
