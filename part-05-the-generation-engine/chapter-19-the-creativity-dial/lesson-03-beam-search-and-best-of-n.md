# Lesson 3: Beam Search and Best of N

## What If the AI Could Try Multiple Paths at Once?

Everything we've discussed so far — the autoregressive loop, temperature, top-p, top-k — shares a common limitation. The model generates one response, making one token choice at a time. If the first few choices happen to lead down a mediocre path, the commitment problem means the entire response is mediocre. The model gets one shot, and whatever randomness produces on that shot is what you see.

But what if the model could explore multiple paths simultaneously and then choose the best one? What if, instead of committing to a single trajectory at each step, it could keep several promising trajectories alive and compare them?

This is the idea behind **beam search** and **best of N** — two strategies that approach the quality problem not by fine-tuning randomness at each step, but by generating multiple candidates and selecting the winner.

## The Hallway of Doors

Imagine you're navigating a building where every room has multiple doors leading to the next room. Behind each door, the next room also has multiple doors, and so on, for dozens of rooms. You're trying to reach the best possible final room.

**Standard sampling** (what we've covered so far) is like walking through the building making one choice at each room. You pick a door, walk through, pick the next door, walk through. Once you've left a room, you can't go back. You end up in whichever final room your sequence of choices leads to. Maybe it's great. Maybe it's mediocre. You'll never know what was behind the other doors.

**Beam search** is like being able to send multiple versions of yourself through the building simultaneously. At each room, every version of you opens every door and peeks into the next room. Then you eliminate the weakest-looking paths and keep only the top few ("beams"). Your team of selves continues forward, always pruning down to the best options. At the end, you compare the final rooms that your surviving selves reached and pick the best one.

**Best of N** takes a simpler approach. You send N independent versions of yourself through the building, each making their own random choices. They all navigate independently, arriving at N different final rooms. Then you simply compare the N rooms and pick the best one.

Both strategies accept the same fundamental insight: with randomness in the system, trying multiple times and selecting the best result is often better than trying once and hoping for the best.

## Beam Search in Detail

Beam search is one of the oldest and most studied text generation strategies. Here's how it works in plain English.

The model starts generating a response. At the very first token position, instead of sampling one token, it considers the top few options — let's say three. These three options become three "beams" — three parallel, in-progress responses.

**Beam 1:** "The..."
**Beam 2:** "Your..."
**Beam 3:** "Making..."

Now, for each beam, the model generates the next token. But it doesn't just extend each beam with one token — it considers multiple options for each beam and keeps only the best combinations overall.

After two tokens, the model might be tracking:

**Beam 1:** "The first..." (probability score: 0.87)
**Beam 2:** "Your accounting..." (probability score: 0.84)
**Beam 3:** "Making a..." (probability score: 0.81)

At each step, the model scores every possible extension of every beam and keeps only the top three (or whatever the beam width is). Some original beams might get eliminated entirely if their extensions aren't scoring well. New beams might emerge from strong extensions of other beams.

This continues until all beams reach a stopping point. The model then selects the beam with the highest overall probability score as its output.

The key insight: beam search avoids the commitment problem's worst effects. If "The first..." turns out to lead to a mediocre continuation, beam search has "Your accounting..." and "Making a..." as backups. The final response is the best of all the explored paths, not just the result of a single random walk.

> **"Behind The Curtain" Sidebar**
>
> Beam search was the dominant text generation strategy before modern sampling techniques emerged. Early machine translation systems relied on it heavily — when translating a sentence, the model would explore multiple possible translations simultaneously and select the most probable complete translation. But beam search has a well-known weakness: it tends to produce "safe" output. Because it optimizes for overall probability, it favors common, predictable phrases over creative or unusual ones. A beam search response to "Write me a poem about the ocean" would likely produce technically correct but uninspired verse, because the most probable sequences of words tend to be the most generic ones. This is why most modern conversational AI systems favor sampling-based approaches — they produce more natural, diverse, and engaging text, even if individual responses are less "optimal" by probability measures.

## The Quality Problem with Beam Search

Beam search sounds perfect in theory: explore multiple paths, choose the best one. But "best" in beam search means "highest probability," and highest probability doesn't always mean highest quality.

Consider two possible responses to our career change prompt:

**Response A (higher probability):** "A career change from accounting to UX design requires careful planning. First, assess your transferable skills. Second, research UX programs. Third, build a portfolio."

**Response B (lower probability):** "Here's what nobody tells you about the accounting-to-UX pipeline: your ability to trace numbers through complex systems is the exact same skill as tracing users through complex interfaces. Don't start with a bootcamp. Start by redesigning one internal tool at your current job."

Response B is arguably more useful, more interesting, and more actionable. But it uses less common phrasings and takes a less conventional approach, making it lower probability. Beam search would almost certainly select Response A.

This is the core limitation of probability-based optimization: probable is not the same as good. The most probable restaurant meal is something like "grilled chicken with vegetables" — perfectly fine, never memorable. The best meal might be something less expected — something a creative chef discovers by taking a risk.

## Best of N: The Simple, Powerful Alternative

Best of N (sometimes called "rejection sampling" or "reranking") takes a beautifully simple approach to the quality problem.

Step 1: Generate N complete responses using standard sampling (with temperature, top-p, and all the usual settings).

Step 2: Score each response using some quality measure.

Step 3: Return the highest-scoring response to the user.

The elegance of this approach is that it separates generation from evaluation. The generation process can be creative, diverse, and risky — high temperature, high top-p, lots of randomness. The evaluation process can be careful, critical, and quality-focused. You get the best of both worlds: creative generation plus careful selection.

The big question, of course, is: what scores the responses? There are several approaches:

**The same model as judge.** The AI generates three responses, then is asked to evaluate which is best. This is like asking the chef to cook three dishes and then taste-test them. It adds computation time but often selects genuinely better responses.

**A separate reward model.** A specialized, smaller model trained specifically to evaluate response quality scores each candidate. This reward model was trained on human preferences — it learned what humans consider helpful, accurate, and well-structured by studying thousands of human evaluations. It's like having a food critic sample the chef's three dishes and select the winner.

**Rule-based scoring.** Simple metrics like response length, vocabulary diversity, or structural completeness can be used to filter obviously bad responses. This is like checking that the dish actually has all the required components before even tasting it.

> **"This Is Why..." Box**
>
> **This is why regenerating a response sometimes gives you something dramatically better — and why AI companies encourage you to try it.** When you hit "regenerate," you're essentially performing manual best-of-N sampling with N=2 (the original and the regeneration). Each generation is an independent sample from the probability distributions, exploring a different path through the space of possible responses. The second might land on a better opening, a more interesting framing, or a more relevant set of examples. Some AI power users routinely regenerate two or three times and pick the best response — they're intuitively doing best-of-N selection. Understanding this, you can see regeneration not as "hoping the AI does better" but as "sampling again from a distribution that contains better options."

## Best of N in Practice

Let's see how best of N might work with our career change prompt. The system generates three responses:

**Response 1:** A structured, conventional five-step plan. Good advice, well-organized, but generic. Quality score: 7/10.

**Response 2:** A creative reframing that draws unexpected parallels between accounting and UX. Original angle, some advice less actionable. Quality score: 8/10.

**Response 3:** A detailed but rambling exploration that covers too many topics without depth. Quality score: 5/10.

The best-of-3 system returns Response 2 to you. Without best-of-N, you'd have a one-in-three chance of getting the best response and a one-in-three chance of getting the worst one. With best-of-N, you're guaranteed the best of the three.

The improvement scales with N. Best of 5 is better than best of 3. Best of 10 is better still. But there are diminishing returns — the jump from best of 1 to best of 3 is much larger than the jump from best of 10 to best of 12. And each additional generation costs computation time and money, so there's a practical limit.

> **"Try This Now" Exercise**
>
> Perform your own best-of-N experiment. Ask the AI the same complex question three times (or use the regenerate button three times). Compare the three responses carefully. Which one has the best opening? The most useful specific advice? The most engaging writing? Pick the best one.
>
> You'll likely notice that the quality difference between the best and worst of three responses is significant — sometimes dramatically so. This is the same quality variation that automated best-of-N systems are designed to exploit. The difference is that automated systems do the comparison for you, at machine speed, before you ever see the result.

## The Economics of Multiple Generations

There's an important practical consideration hiding in both beam search and best-of-N: they're expensive.

Beam search with a beam width of 3 requires roughly three times the computation of standard sampling. Best of 5 requires roughly five times the computation. And computation translates directly into cost (electricity, hardware) and latency (time waiting for a response).

This is why you don't see beam search or large-N best-of-N in most consumer AI products. The cost would be enormous at scale. If a billion messages per day each required five full generations, the infrastructure costs would multiply fivefold.

Instead, AI companies make strategic choices:

**For consumer chat (Claude, ChatGPT, etc.):** Standard sampling with carefully tuned temperature and top-p. One generation, served directly to you. The parameters are optimized so that single samples are usually good enough.

**For high-stakes applications (medical, legal, financial):** Best-of-N or similar strategies may be used, because the cost of a bad response outweighs the cost of extra computation.

**For creative and research applications:** Some systems generate multiple candidates internally and use a reward model to select the best one before you see it. You might not know this is happening — it just seems like the AI gives consistently good responses.

**For API users (developers building applications):** The tools to implement your own best-of-N are readily available. Developers can generate multiple responses and implement custom selection logic for their specific use case.

> **"Behind The Curtain" Sidebar**
>
> There's an emerging technique called "speculative decoding" that cleverly reduces the cost of generating multiple options. Instead of running the full, expensive model multiple times, a smaller, faster model generates several candidate sequences quickly. The large model then evaluates these candidates rather than generating from scratch. It's like having a team of apprentice chefs quickly plate several versions of a dish, and then having the master chef taste each one and pick the best — much faster than having the master chef cook three full dishes from scratch. This and related techniques are making multi-candidate generation increasingly practical.

## Beam Search, Best of N, and You

Even without direct access to these settings, understanding beam search and best-of-N changes how you interact with AI.

First, it reframes regeneration. Every time you regenerate a response, you're performing best-of-N manually. You're sampling another trajectory through the space of possible responses and comparing it to the previous one. This isn't a sign that the AI failed — it's a legitimate strategy that even AI engineers use systematically.

Second, it explains quality variance. Now you understand why two responses to the same prompt can be so different in quality. The probability space contains both excellent and mediocre responses. A single sample might land anywhere in that space. Best-of-N increases your chances of landing on the excellent end.

Third, it connects to a practical strategy: for high-stakes tasks, generate multiple responses yourself. If you're using AI to draft an important email, write a business proposal, or develop a strategic plan, don't just accept the first response. Generate three. Pick the best elements from each. This manual best-of-N approach is one of the simplest and most effective ways to improve AI output quality.

> **"Pro Tip" Box**
>
> For important tasks, adopt a systematic best-of-3 approach. Generate three responses to the same prompt. Don't just pick the best whole response — look for the best opening from Response 1, the best middle section from Response 2, and the best conclusion from Response 3. Then ask the AI to synthesize: "Combine the opening approach from Response A with the detailed analysis from Response B and the specific recommendations from Response C." You're using multiple samples to construct a response better than any single generation could produce. This is best-of-N thinking applied at a human level.

## The Connection to Extended Thinking

There's a subtle but important connection between best-of-N and the extended thinking we explored in Chapter 12. During extended thinking, the model internally considers multiple approaches before committing to a visible response. In a sense, extended thinking is a form of internal best-of-N — the model explores several reasoning paths in its scratchpad and selects the most promising one before generating the response you see.

This means that models with strong extended thinking capabilities are already doing a version of best-of-N "for free" — without the computational cost of generating complete multiple responses. The quality improvement from extended thinking and the quality improvement from best-of-N come from the same underlying principle: considering multiple options before committing to one.

This is why modern AI responses feel significantly better than what older models produced. The combination of extended thinking (internal exploration), better sampling strategies (top-p over older methods), and sometimes hidden best-of-N selection (reward model reranking) means that the single response you see has been implicitly selected from a much larger space of possibilities than you might realize.

In the next lesson, we'll bring all of these randomness controls together into a practical framework: how to match the right sampling strategy to the right task, turning your understanding of temperature, top-p, beam search, and best-of-N into actionable rules for getting better results.
