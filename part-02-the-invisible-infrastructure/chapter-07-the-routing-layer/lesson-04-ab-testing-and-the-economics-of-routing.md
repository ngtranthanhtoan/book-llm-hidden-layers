# Lesson 4: A/B Testing and the Economics of Routing

## The Experiment You Did Not Consent To

Here is a fact that unsettles some people when they first learn it: you might be part of an experiment right now. Not a dramatic, sci-fi experiment. A quiet, statistical one. The AI model that responded to your last message might be a slightly different version than the one that responded to your colleague's identical message ten minutes ago. You were both assigned to different groups in an **A/B test** -- and neither of you knew it.

A/B testing is a standard practice across the technology industry. Every major website, app, and digital service runs them constantly. But in the context of AI, A/B testing takes on a unique significance, because the "thing being tested" is not a button color or a page layout -- it is the very brain that processes your thoughts and generates your responses.

## How A/B Testing Works in AI

The concept is simple. The company wants to know whether Model Version A or Model Version B produces better user outcomes. So they split their user traffic: 50% of users get Version A, 50% get Version B. Then they measure the results.

The split is random. You do not get to choose. You are not informed. The interface looks identical for both groups. The only difference is which model is processing your messages behind the scenes.

What kinds of differences might exist between the two versions?

**Model size variations.** Version A might be the current production model. Version B might be a newer, slightly larger model. The company wants to know if the larger model produces measurably better user satisfaction.

**Training variations.** Both versions might be the same size, but trained slightly differently. Version A might have more reinforcement learning from human feedback. Version B might have a different mix of training data. The company wants to know which training approach users prefer.

**System prompt variations.** Same model, but with different system prompts. Version A might have a more verbose, detailed system prompt. Version B might have a more concise one. The company wants to know which produces better engagement.

**Generation setting variations.** Same model, same system prompt, but different temperature or top-p settings. Version A at temperature 0.7 versus Version B at temperature 0.8. The company wants to know which feels more "natural" to users.

**Feature variations.** Version A might have access to web search. Version B might not. The company wants to know how tool access affects user satisfaction and engagement.

> **"Behind The Curtain"**
> Major AI companies run dozens of A/B tests simultaneously. You might be in the "test" group for one experiment, the "control" group for another, and not included in a third. The routing layer manages this complexity, tagging each user with their experiment assignments and ensuring they consistently receive the correct version throughout each test period. It is like being a customer at a restaurant where the kitchen is secretly testing five different recipes for the same dish, and you are eating version three without knowing four other versions exist.

## What Gets Measured

The metrics that A/B tests track reveal what AI companies actually optimize for:

**Engagement metrics.** How many messages does the user send per conversation? How many conversations do they start per day? How long is each session? Higher engagement generally means the user finds the AI more useful and enjoyable.

**Satisfaction signals.** Thumbs up versus thumbs down. Explicit ratings if the platform collects them. These are direct but noisy -- most users never bother to rate responses.

**Regeneration rate.** How often do users click "regenerate" or "try again"? A high regeneration rate suggests the user was not satisfied with the initial response. This is one of the most valuable signals -- it indicates dissatisfaction at the exact moment it occurs.

**Conversation depth.** Do users follow up with deeper questions, or do they abandon the conversation after one exchange? Deeper conversations suggest the AI's initial responses were engaging enough to warrant further exploration.

**Retention.** Does the user come back tomorrow? Next week? Next month? This is the ultimate metric -- a satisfied user returns, an unsatisfied one does not.

**Task completion.** In product-specific contexts (coding assistants, customer service bots), the company can sometimes measure whether the user actually accomplished their goal. Did the code run? Was the customer issue resolved?

**Revenue impact.** For businesses, the most important metric of all: does this model version generate more subscriptions, higher usage, or better customer retention than the alternative?

> **"This Is Why..."**
> This is why the AI you are using today might feel subtly different from the AI you used last week -- even if no major update was announced. You might have been moved to a different A/B test group, or a test might have concluded and the winning version was rolled out to everyone. These changes are often small enough that you cannot quite pinpoint what changed, but you notice something feels different. You are not imagining it.

## The Ethics of AI A/B Testing

A/B testing AI models raises ethical questions that do not arise with traditional A/B testing of website designs.

**Informed consent.** When a website tests two button colors, the stakes are low. When an AI service tests two model versions, the stakes can be higher. One version might give better medical information. One might be better at detecting when a user is in distress. One might produce more accurate financial analysis. Users in the "worse" group are receiving an inferior product -- and they do not know it.

**Outcome inequality.** During a test, some users receive materially better AI responses than others, through no choice or action of their own. If you are in the group with the better model, you get better career advice, better writing assistance, better analysis. If you are in the other group, you do not.

**Feedback asymmetry.** If you are in the test group with the worse model and you give negative feedback, that feedback helps the company improve. But it does not help you in the moment. Your actual experience was worse, and that worse experience contributed to someone else eventually getting a better one.

Most AI companies address these concerns by keeping the variations relatively small. They do not test a brilliant model against a terrible one -- they test two models that are both "good enough" to be in production, looking for marginal improvements. But the ethical questions remain, and as AI becomes more consequential in people's lives, they will become more pressing.

## The Economics of Routing: Why Money Drives Every Decision

Now let us talk about what is perhaps the most powerful force shaping the invisible infrastructure: economics. Behind every routing decision, every model selection, every capacity allocation, there is a financial calculation.

**The cost equation is staggering.** Running a large language model at scale costs an enormous amount of money. Consider the basic math:

- A large, state-of-the-art model might cost between one and ten cents per complex response
- A smaller, more efficient model might cost a fraction of a cent per response
- At millions of responses per day, the difference between routing to the large model versus the small model can amount to millions of dollars per month

This is why routing exists in the first place. If computational costs were zero, every request would go to the largest, most capable model. There would be no need for complexity estimation, load balancing, or model selection. But costs are very real, and they create an inescapable pressure to route as many requests as possible to the cheapest model that can handle them adequately.

**The subscription math.** A typical AI subscription costs roughly $20 per month. If a heavy user sends 100 complex messages per day, and each complex response costs the company five cents to generate, that user costs the company $150 per month -- seven and a half times their subscription fee. The company loses money on that user.

This is why routing is so aggressively optimized. The company needs to ensure that the expensive model is only used when it is genuinely necessary, and that the cheap model handles as much as possible. The routing layer is, in a very real sense, a cost management system disguised as a quality optimization system.

> **"Behind The Curtain"**
> Some AI companies have publicly acknowledged that their subscription pricing is not profitable at current usage levels. They are subsidizing the cost, betting that future efficiency improvements (smaller, cheaper models that are just as capable) will eventually make the business model work. In the meantime, aggressive routing -- sending as many requests as possible to cheaper models -- is one of the primary mechanisms for controlling losses.

## The Three-Way Tradeoff

Every routing decision involves balancing three competing objectives:

**Quality.** The best possible response for the user. This favors routing everything to the largest, most capable model.

**Speed.** The fastest possible response time. This favors routing to the smallest, fastest model -- or to whichever model currently has the shortest queue.

**Cost.** The lowest possible expense per request. This favors routing to the cheapest model that can produce an adequate response.

These three objectives are in constant tension. You cannot maximize all three simultaneously. Improving quality means using a bigger model, which is slower and more expensive. Improving speed means using a smaller model, which reduces quality. Reducing cost means using the cheapest model, which reduces both quality and potentially speed (if the cheap model is overloaded because everything is being routed to it).

The routing layer's job is to find the optimal point in this three-way tradeoff for each individual request. Simple requests can maximize all three: they are fast, cheap, and high-quality on a small model. Complex requests force harder tradeoffs: the company has to decide how much quality to sacrifice for speed and cost savings.

**The analogy:** Think of the routing tradeoff like choosing transportation. Walking is cheap and healthy (small model: low cost, good for simple trips). A taxi is fast and comfortable but expensive (large model: high quality but expensive). A bus is a compromise -- reasonably fast, reasonably cheap, reasonably comfortable (medium model: balanced). The routing layer is choosing your transportation for each trip based on how far you need to go, how much the company can afford to spend, and how busy the roads are.

## How Economics Shape Your Experience

The economic pressures behind routing have visible effects on your AI experience:

**Free tiers exist to attract users, not to provide the best experience.** Free-tier users are almost always routed to the cheapest models with the strictest rate limits. The free tier is a marketing tool -- it gets users hooked so they will eventually subscribe.

**Peak-hour quality can decline.** When servers are busy, cost pressure increases (more GPUs running means more electricity, more cooling, more expense). The system responds by routing more aggressively to cheaper models. The user experiences this as a subtle decline in response quality during busy times.

**Response length is economically constrained.** Longer responses cost more to generate. This is why some platforms seem to produce shorter responses than others -- it is often a cost optimization, not a quality decision.

**Tool use is expensive and therefore gated.** Web search, code execution, and other tools add cost to every request. Some systems are conservative about activating tools, preferring to have the model answer from its training data even when a tool would produce a better result.

> **"Pro Tip"**
> Understanding the economics of AI helps you be a more strategic user. If you are on a free tier and hitting quality limitations, the most impactful upgrade is not a better prompt -- it is a paid subscription, which gets you access to better models and more generous rate limits. If you are already a paid subscriber, understanding that complex requests are expensive helps you appreciate why the system sometimes feels like it is trying to give you a shorter answer. When you need depth, explicitly request it: "Please provide a comprehensive, detailed response. Length is not a concern -- quality and thoroughness are."

## Before and After: Working With Economic Realities

**Before understanding the economics** (bad approach):
The user is on a free tier and sends their most important career planning question during peak hours. They receive a short, somewhat generic response from a small model operating under load. They conclude: "AI is not ready for serious professional use."

**After understanding the economics** (good approach):
The user recognizes that their free-tier, peak-hour experience is not representative of the system's capabilities. They subscribe to a paid tier, schedule their important session for an off-peak time, and craft their prompt with clear complexity signals. They receive a response from the best available model with full processing resources. The difference is night and day.

---

## Chapter Summary

Between your message and the AI's response, an invisible routing layer makes a critical decision: which brain will answer your question? This routing layer evaluates the complexity of your request, considers the available models and their current load, factors in your subscription tier and the system's economic constraints, and directs your message to the most appropriate model. The same system also manages the fundamental infrastructure challenges of serving millions of simultaneous users -- load balancing across thousands of servers, rate limiting to ensure fair access, queue management during peak demand, and graceful degradation when the system is overwhelmed. And running alongside all of this, A/B tests continuously experiment with different model versions, system prompts, and settings to optimize the experience for future users. The AI product you interact with is not a single brain answering all questions equally; it is a sophisticated traffic management system directing each question to the most appropriate brain under the current conditions.

## Five Key Takeaways

1. **Your message may not go to the model you think it goes to.** The routing layer evaluates each request and directs it to the most appropriate model based on complexity, task type, user tier, and system load. Simple questions often go to faster, cheaper models. Complex questions go to larger, more capable ones.

2. **Complexity estimation is the weakest link.** The system judges your request's complexity from surface-level signals -- length, vocabulary, structure. Short, deceptively complex questions get under-routed. Verbose, deceptively simple ones get over-routed. You can improve your experience by matching your prompt's surface complexity to its true complexity.

3. **Infrastructure directly affects response quality.** Load balancing, rate limiting, and queue management create the variable experience of AI -- fast responses sometimes and slow ones other times, deep answers sometimes and shallow ones other times. These are often infrastructure effects, not model capabilities.

4. **You are probably in an A/B test right now.** AI companies continuously experiment with different model versions, system prompts, and settings. Your experience might be subtly different from another user's, and both of you might be unaware that an experiment is running.

5. **Economics drive routing decisions.** Every routing choice balances quality, speed, and cost. The pressure to minimize costs means simpler models handle as much traffic as possible. Understanding this helps you position your requests to receive the resources they deserve.

## Now You Know Why...

- **...response speed varies dramatically for seemingly similar questions.** Different questions get routed to different models. A question classified as simple goes to a fast, small model. A question classified as complex goes to a slower, more capable one. The speed difference is a routing difference, not a thinking difference.

- **...the AI sometimes feels less capable than usual.** During peak hours, under heavy load, or in a free tier, your request might be routed to a smaller model or processed under resource constraints. The AI's apparent capability is partly a function of infrastructure conditions.

- **...the AI you use today might feel subtly different from last week.** A/B tests, model updates, system prompt revisions, and configuration changes happen continuously. The product's name stays the same, but the brain and its surrounding infrastructure evolve constantly.

## Three Actionable Strategies

1. **Signal the true complexity of your request.** Use explicit complexity markers ("comprehensive analysis," "consider multiple factors," "expert-level reasoning"), provide structure (numbered sub-questions, conditional scenarios), and match your message length to your request's genuine complexity. These signals influence both the routing layer and the model itself.

2. **Time your important requests strategically.** For work that truly matters -- business analysis, creative projects, career planning -- avoid peak hours when possible. Off-peak usage means better routing to top-tier models, shorter queues, and more available resources. Think of it like choosing to fly on a Tuesday instead of a Friday.

3. **When quality feels inconsistent, adjust your approach rather than your expectations.** If a response feels shallow, try regenerating it (you might get a different model or a different sample). If responses consistently feel thin, check whether you are hitting rate limits, try during off-peak hours, or consider whether a paid tier would unlock better model access. Inconsistency in AI is often an infrastructure signal, not a capability limitation.
