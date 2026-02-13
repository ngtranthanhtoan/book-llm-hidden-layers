# Lesson 2: Complexity Estimation and Its Failures

## The Art of Judging a Book by Its Cover

Imagine you are the manager of a consulting firm, and projects arrive at your desk as one-page summaries. You need to assign each project to the right team: junior consultants for simple work, senior consultants for moderate complexity, and your top partners for the most challenging engagements. You have about thirty seconds to read each summary and make the call.

Most of the time, you get it right. A request to "update the quarterly spreadsheet" is obviously simple. A request to "develop a five-year market entry strategy for Southeast Asia" is obviously complex. But sometimes the summaries are misleading. A request that sounds simple -- "reconcile last month's accounts" -- might hide a catastrophic mess of missing data and conflicting records. A request that sounds complex -- a long, detailed description of a technically straightforward task -- might be simpler than it appears.

This is the challenge facing the complexity estimation system in AI routing. It needs to judge the difficulty of your request in milliseconds, based solely on the surface features of your message. And it gets it wrong more often than you might expect.

## How Complexity Estimation Works

The complexity estimator evaluates your message using several surface-level signals:

**Message length.** Longer messages tend to correlate with more complex requests. A 200-word prompt with multiple sub-questions is probably more complex than a 10-word prompt. But this correlation is imperfect -- some of the hardest questions in the world can be expressed in five words ("What is consciousness?"), and some of the longest messages are just verbose versions of simple requests.

**Question structure.** The presence of multiple sub-questions, conditional logic ("if X then Y, otherwise Z"), comparison requests ("compare A and B across these five dimensions"), or multi-step instructions all signal higher complexity.

**Vocabulary and domain signals.** Technical vocabulary, domain-specific terminology, and references to specialized fields suggest that the request requires more sophisticated knowledge and reasoning.

**Task type signals.** Certain task types are inherently more complex than others. "Translate this sentence" is typically simpler than "analyze the rhetorical strategy of this essay." Planning and strategy tasks are typically more complex than factual recall.

**Explicit complexity markers.** Words and phrases like "comprehensive," "detailed analysis," "consider multiple perspectives," "thorough," and "nuanced" directly signal that the user expects a complex response.

## When the Estimator Gets It Wrong

The complexity estimator fails in predictable ways, and understanding these failure modes helps you avoid them.

### Failure Mode 1: The Deceptively Simple Question

Some of the most profoundly complex questions look trivially simple on the surface.

"Is it ethical to lie to protect someone?" -- Six words. Enormous philosophical complexity.

"Why do we dream?" -- Four words. Requires synthesizing neuroscience, psychology, and ongoing scientific debate.

"Should I change careers?" -- Four words. Requires understanding the person's entire life context, financial situation, emotional state, and market conditions.

These questions look like simple factual queries to the complexity estimator. They might get routed to a smaller model that produces a superficial answer when what was needed was deep, nuanced reasoning.

**The analogy:** It is like receiving a postcard-sized project brief that reads "Fix the company culture." Looks like a one-liner. Is actually a multi-year organizational transformation.

### Failure Mode 2: The Deceptively Complex Message

The opposite problem: a message that appears complex but is actually straightforward.

"I have been thinking a lot lately about various different types of fruit, and I was wondering, after much deliberation and consideration of the many options available, if you could perhaps tell me, in your best estimation, what particular fruit is considered the most popular in the United States of America, taking into account various surveys and studies that may or may not have been conducted on this specific topic?"

That is 70 words. It contains hedging language, multiple clauses, and references to studies. The complexity estimator might flag this as a moderate or complex request. The actual answer is: "The banana." This was a simple factual question dressed up in verbose clothing.

### Failure Mode 3: The Hidden Dependencies

Some requests look simple but contain implicit dependencies that make them complex.

"What should I cook for dinner tonight?" -- seems simple. But a good answer depends on: What ingredients do you have? What are your dietary restrictions? How much time do you have? What is your cooking skill level? How many people are you cooking for? What did you eat recently?

The complexity estimator sees a short, simple-looking question. The actual complexity is hidden in the implicit context the question requires.

### Failure Mode 4: The Escalating Conversation

In a multi-turn conversation, each individual message might be simple, but the cumulative conversation might be highly complex. The routing layer typically evaluates each message independently, which means it might route a crucial follow-up question to a smaller model, even though the follow-up requires understanding and reasoning about the entire preceding conversation.

"And what about the tax implications?" -- In isolation, this looks like a simple factual question. In the context of a complex career planning conversation where you have been discussing financial transitions, it requires sophisticated reasoning that connects to everything discussed so far.

> **"This Is Why..."**
> This is why the AI sometimes gives a surprisingly shallow answer to what you thought was a deep question. The complexity estimator judged your message by its surface features -- length, vocabulary, structure -- and assigned it a lower complexity rating than it deserved. The result: a less capable model was assigned, and the response lacked the depth you expected. It is not that the AI system could not have provided a better answer -- it is that the best brain for the job was never called in.

## The Consequences of Misrouting

When complexity estimation fails, the consequences ripple through the entire response.

**Under-routing (complex request sent to a simple model):**
- Shallow, generic responses
- Missing nuances and edge cases
- Failure to consider multiple perspectives
- Shorter responses that do not fully address the question
- Incorrect answers to reasoning-heavy questions

**Over-routing (simple request sent to a complex model):**
- Unnecessarily slow response times
- Wasted computational resources (which contribute to higher costs and environmental impact)
- Sometimes, paradoxically, over-complicated answers to simple questions (the large model might overthink a straightforward request)

The asymmetry of consequences is worth noting. Under-routing produces a noticeably bad user experience -- you feel like the AI did not try hard enough. Over-routing produces a slightly slow but generally good response -- the user rarely complains that the answer was "too thoughtful." This asymmetry is why companies tend to err on the side of over-routing for paying customers: the cost of a disappointed user who got a shallow answer is higher than the cost of a few extra cents of compute.

> **"Behind The Curtain"**
> Some AI companies have found that even imperfect routing saves enormous amounts of money. If 60% of requests are genuinely simple and can be handled by a model that costs one-tenth as much per query, imperfect routing still reduces costs dramatically. The complexity estimator does not need to be perfect to be valuable. It just needs to be right often enough that the savings from correctly routing simple requests outweigh the cost of occasionally misrouting complex ones.

## How to Help the Estimator

The good news is that you can influence complexity estimation in your favor. Since the estimator uses surface-level signals, you can provide signals that accurately reflect the true complexity of your request.

**Be explicit about complexity.** If your question is genuinely complex, say so. "This is a nuanced question" or "I need a thorough analysis" or "Please consider multiple factors." These phrases are not just good prompting for the model -- they are signals that the routing layer uses.

**Match your message length to your request's complexity.** Do not express a complex request in five words. Expand it. Provide context, sub-questions, and constraints. The additional length serves as a complexity signal and also gives the model better material to work with.

**Use structural markers.** Numbered lists, sub-questions, conditional scenarios, and explicit multi-part requests all signal complexity. "Please address: (1) the skills gap, (2) the financial implications, (3) the timeline, and (4) the market demand" is both a better prompt and a stronger complexity signal than "Tell me about UX design careers."

**Avoid burying the complexity.** If your question starts with a simple preamble and buries the complex part at the end, the complexity estimator (which must make quick judgments) might not weigh the complex part heavily enough. Front-load the complexity: "I need a detailed, multi-factor analysis of..." rather than "I had a quick question -- actually, it's kind of complicated..."

> **"Try This Now"**
> Take a question you know is complex and try expressing it in two ways: first, as concisely as possible (five to ten words), and second, with full context, sub-questions, and explicit complexity markers (50-100 words). Send both versions to the same AI assistant (in separate conversations). Compare the depth and quality of the responses. The difference you see is partly the model's response to more context, but it is also partly the routing system's response to stronger complexity signals.

## The Future of Complexity Estimation

Complexity estimation is one of the areas where AI systems are improving most rapidly. Future approaches include:

**Preliminary model evaluation.** Instead of estimating complexity from surface features alone, some systems run a very quick "preview" of the request through a small model to see how confidently it can handle it. If the small model's confidence is high, it keeps the request. If the small model hesitates, the request gets bumped to a larger model.

**Adaptive routing.** Rather than making a single routing decision at the start, the system monitors the quality of the response as it is being generated. If the quality starts to drop -- the model becomes repetitive, contradicts itself, or produces generic content -- the system can interrupt and re-route to a more capable model mid-generation.

**User feedback loops.** When users consistently provide negative feedback (thumbs down, regeneration requests) for responses to certain types of questions, the system learns that those question types are more complex than the estimator originally judged and adjusts future routing accordingly.

## Before and After: Helping the Complexity Estimator

**Before understanding complexity estimation** (bad prompt):
"Career change tips?"

Three words. The complexity estimator sees a short, simple-looking question. Routing: small, fast model. Response: a generic list of career change tips that could apply to anyone, anywhere, changing from anything to anything.

**After understanding complexity estimation** (good prompt):
"I need expert-level guidance on a significant career transition. I'm a senior CPA with 8 years in public accounting, considering a move to UX design. This involves substantial factors: a skills gap in design and research, financial risk during the transition, market conditions in Chicago, timeline pressure to complete within 12 months, and my need to maintain my professional network. Please provide a comprehensive, multi-dimensional analysis with actionable recommendations."

The complexity signals are loud and clear. This gets routed to the most capable model. The response will be proportionally more detailed, nuanced, and useful -- not just because the prompt is better, but because a better brain was assigned to answer it.

---

In the next lesson, we pull back the curtain on the infrastructure that keeps the whole operation running: load balancing, rate limiting, and the queue management systems that determine whether your message is processed immediately or waits in line -- and what happens when the system is overwhelmed.
