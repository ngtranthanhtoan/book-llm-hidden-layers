# Lesson 3: Why Complex Requests Fail

## The Dropped Plate Problem

You're at a packed restaurant. Your table of six orders simultaneously: a steak, a salmon, a vegetarian pasta, a child's meal, a salad with dressing on the side, and a gluten-free dessert. The kitchen is competent. Each dish, ordered alone, would arrive perfectly. But when they all arrive together, something's off. The steak is perfect. The salmon is great. The pasta is good. The child's meal is there. But the salad came with the dressing mixed in — not on the side. And the dessert? Not gluten-free. Two out of six items had their specific requirements dropped.

This is what happens when complex requests fail in AI. The model doesn't catastrophically collapse. It doesn't refuse or give gibberish. Instead, it delivers a response that's mostly good but quietly drops one or more parts of your request. The parts it handles well mask the parts it missed, which is exactly why this failure mode is so insidious — you might not even notice what's missing unless you check.

Understanding why this happens — the specific mechanisms behind dropped, distorted, or degraded sub-tasks — gives you the ability to prevent it. And preventing it is surprisingly straightforward once you know what's going wrong.

## Failure Mode 1: The Priority Cliff

The AI doesn't give equal attention to all parts of your request. It prioritizes sub-tasks based on several factors: how prominently they appear in your message, how familiar the topic is, how much the sub-task matches common response patterns, and — crucially — where in your message the sub-task appears.

The priority cliff is what happens when some sub-tasks fall below an invisible attention threshold. They're not ignored entirely, but they receive so much less processing attention that the result is thin, generic, or outright missing.

Here's a real example. Suppose you ask:

"Help me plan a career change from accounting to UX design. Include specific resources for learning, a realistic timeline, salary expectations, and strategies for dealing with imposter syndrome during the transition."

The first three sub-tasks — learning resources, timeline, salary — are standard career change topics. The AI has seen thousands of career change discussions that cover these areas. They get strong decomposition and thorough treatment.

But the fourth item — imposter syndrome strategies — is more unusual. It's a psychological topic embedded in a practical planning request. It crosses domains. And it appears last in the list. All three of these factors push it below the priority cliff. The AI might address imposter syndrome in a single sentence ("Remember that feeling uncertain is normal during any career change!") when you wanted a genuine, substantive discussion of psychological strategies.

The sub-task wasn't ignored — it was deprioritized to the point of being useless.

> **"This Is Why..." Box**
>
> **This is why the last item in a list of requests often gets the weakest treatment.** The AI's attention mechanism gives more weight to items that appear earlier and more prominently. The last item in a list, especially if it's different in nature from the others, frequently falls below the priority cliff. If you have a sub-task that's particularly important to you, don't bury it at the end of a list — put it first, or make it a separate request entirely.

## Failure Mode 2: Sub-task Merging

Sometimes the AI doesn't drop a sub-task — it merges it with another one, losing the distinction you cared about.

Example: "Compare the pros and cons of bootcamps versus self-study for learning UX design. Also compare online versus in-person bootcamps."

You asked for two comparisons: (1) bootcamps vs. self-study, and (2) online vs. in-person bootcamps. But the AI might merge these into a single, blended discussion that covers all three options (self-study, online bootcamps, in-person bootcamps) without clearly separating the two comparisons you asked for.

The result contains relevant information, but the structure doesn't match your request. You wanted two distinct analyses, and you got one blended overview. The AI didn't fail at the task — it failed at the decomposition. It recognized the topics as related and combined them into a single sub-task instead of treating them as two separate ones.

Sub-task merging is especially common when:
- Multiple sub-tasks are related (as in the bootcamp example)
- The sub-tasks would produce overlapping content
- The model is trying to avoid being repetitive

The merge isn't irrational — from a pure information standpoint, the blended response might cover the same facts. But it doesn't serve your purpose, because the structure itself was part of what you needed.

## Failure Mode 3: Wrong Decomposition

This is the most fundamental failure: the AI breaks your request into the wrong sub-tasks entirely.

Consider: "I want to understand the UX design hiring process — what happens from the moment I submit an application to the moment I get an offer?"

You're asking for a chronological walkthrough of the hiring pipeline. The correct decomposition is sequential: application screening, portfolio review, phone screen, design challenge, on-site interview, offer negotiation.

But the AI might decompose this differently — by topic instead of chronology: "preparing your application," "what companies look for," "common interview questions," "salary negotiation tips." This is useful information, but it's the wrong decomposition. You asked for a process description; you got a topic collection. The information is relevant, but the structure doesn't match your mental model.

Wrong decomposition happens when the model's pattern matching selects the wrong template. "Tell me about UX hiring" most commonly leads to topic-based advice in the training data, so that's the decomposition the model defaults to — even though your specific request called for a chronological process walkthrough.

> **"Behind The Curtain" Sidebar**
>
> Researchers have tested this by asking the same question with different phrasings and measuring how often the AI's decomposition structure changes. The results are striking: minor rephrasing can flip the entire organizational structure of the response. "Walk me through the UX hiring process step by step" produces chronological decomposition. "Tell me about getting hired in UX" produces topical decomposition. "What should I expect at each stage of UX job applications?" produces stage-by-stage decomposition. The AI isn't choosing the "right" decomposition — it's choosing the decomposition most associated with the phrasing you used.

## Failure Mode 4: Depth Imbalance

Even when the AI correctly identifies all the sub-tasks, it often allocates attention unevenly — and not always in the way you'd want.

Depth imbalance typically follows a pattern: the AI spends the most words on topics it has the richest training data for, regardless of whether those topics are the most important to you.

For a career change plan, the AI might produce 300 words on learning resources (a topic with abundant training data) and 50 words on financial planning during the transition (a more specialized topic). The depth allocation doesn't reflect importance — it reflects the density of the model's training data on each topic.

This creates a response that feels detailed and thorough in some sections and frustratingly superficial in others. And the thin sections are often the ones where you most needed depth, because the common topics are the ones you could have easily found through a basic search.

## Failure Mode 5: The Multi-Part Cascade

This failure mode is specific to requests with multiple distinct parts separated by conjunctions: "Do X and Y," "Compare A and B, then also explain C."

The cascade works like this: the AI starts addressing the first part, generates substantial content, and by the time it reaches the second part, one of two things happens:

**Shortened treatment:** The model realizes it has already produced a long response and compresses the remaining parts to keep the total length manageable. You get a thorough answer to the first question and a cursory answer to the second.

**Complete drop:** In extreme cases, the model simply ends its response after addressing the first part, never getting to the second. It doesn't acknowledge the second part or apologize for skipping it. It just... stops, as if the second part of your request never existed.

The multi-part cascade is amplified by the AI's tendency toward lengthy responses (a bias learned from RLHF, where raters often preferred longer responses). The model spends its "response budget" on the first part, leaving insufficient budget for subsequent parts.

> **"This Is Why..." Box**
>
> **This is why the AI sometimes answers only half your question — and doesn't even acknowledge the other half.** If you asked "What are the benefits of transitioning to UX, and what are the risks?" you might get a detailed analysis of benefits and then either a brief mention of risks or no mention at all. The model didn't deliberately ignore your second question. It spent its attention and response budget on the first part, and the second part fell off the end. The fix is simple: make the second part a separate message, or put it first.

## Failure Mode 6: Context Window Competition

In long conversations, a different failure mechanism emerges. Your complex request isn't just competing with itself for the model's attention — it's competing with the entire conversation history.

If you're 15 messages into a conversation and send a complex request, the model's context window contains all previous messages. Your new request has to compete with that accumulated history for the model's attention. Sub-tasks that overlap with earlier conversation topics might get reinforced (the model has more context for them). Sub-tasks that introduce entirely new topics might get weakened (the model has to shift its focus significantly).

This is why the same complex request can produce a better response at the start of a fresh conversation than in the middle of a long one. It's not that the model is tired — it's that your request has more competition for attention in a longer context.

## The Compound Effect: Multiple Failures at Once

In practice, complex requests often experience multiple failure modes simultaneously. A request might have one sub-task dropped (priority cliff), two sub-tasks merged (merging), and the remaining sub-tasks treated with imbalanced depth. The result is a response that's maybe 60% of what you wanted — good enough to be useful, but far short of what the AI is actually capable of producing.

This compound effect is why many people have an intuition that "AI is better for simple questions than complex ones." It's not that the AI's underlying knowledge is worse for complex topics. It's that the decomposition process introduces cumulative failure risk as complexity increases.

> **"Try This Now" Exercise**
>
> Try this experiment: send a five-part request to an AI in a single message, covering five distinct topics. Then count how many parts receive thorough treatment in the response. Common results: two or three parts get good coverage, one or two get thin treatment, and zero or one gets dropped entirely. Now send the same five topics as five separate messages. Compare the quality of each topic's coverage. The separate-message approach almost always produces better results because each topic gets full decomposition without competing against the others.

## The Fundamental Insight

All six failure modes share a common root cause: the AI has a finite attention budget and a finite response budget, and complex requests force it to allocate those budgets across competing sub-tasks. When the budget is sufficient — simple requests with few sub-tasks — the results are excellent. When the budget is stretched — complex requests with many sub-tasks — something has to give.

This isn't a flaw that will be fixed with bigger models or better training (though both help at the margins). It's an inherent characteristic of the sequential generation process. The model produces one token at a time, in a single pass, without the ability to go back and revise. Any process with that constraint will struggle with complex, multi-part tasks.

But here's the empowering part: now that you understand the failure modes, you can structure your requests to avoid them. And that's exactly what we'll cover in the next lesson — the chapter's culminating practical toolkit for getting complete, thorough responses to even the most complex requests.

> **"Pro Tip" Box**
>
> **When you have a genuinely complex request, ask yourself: "Am I asking the AI to do one hard thing, or five medium things at once?"** If the answer is five medium things, split them up. Not because the AI can't handle complexity — it can — but because five separate focused requests will each receive full decomposition, full attention, and full response budgets. The total output will be dramatically more thorough than a single overloaded request that triggers multiple failure modes simultaneously.
