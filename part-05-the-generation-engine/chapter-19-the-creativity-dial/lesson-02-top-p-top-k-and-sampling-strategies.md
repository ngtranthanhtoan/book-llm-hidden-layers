# Lesson 2: Top-p, Top-k, and Sampling Strategies

## The Other Controls on the Creativity Console

Temperature is the most famous randomness control, but it's not the only one. Sitting alongside it on the creativity console are two other important settings: **top-p** and **top-k**. While temperature reshapes the entire probability distribution, these two controls take a different approach — they cut off the bottom of the distribution entirely, deciding which tokens are even allowed to participate in the selection process.

If temperature adjusts how adventurous the chef is, top-p and top-k decide how many ingredients the chef is allowed to consider in the first place.

## Top-k: Only the Best Candidates Need Apply

Let's start with top-k, because it's the simpler of the two.

Imagine a talent show with 100,000 contestants (our vocabulary of tokens). A panel of judges (the model's probability calculation) ranks all 100,000 contestants from best to worst for this particular spot in the response. With no filtering, any contestant could theoretically be chosen, even the worst one, if the random draw happened to land there.

Top-k says: "Only the top k contestants are allowed on stage. Everyone else goes home."

If k is set to 50, the model calculates probabilities for all 100,000 tokens, then throws away everything except the top 50. Those 50 tokens get their probabilities renormalized — adjusted so they add up to 100% among just the survivors — and sampling happens only among those 50 candidates.

**Top-k of 1** is the most restrictive: only the single most probable token is considered. This is identical to greedy decoding (temperature zero). The response is completely deterministic.

**Top-k of 50** means the model always has 50 options to choose from. This prevents wildly improbable tokens from ever being selected, while still allowing meaningful variety among the plausible candidates.

**Top-k of 1,000** is more permissive, allowing tokens well into the long tail of the distribution to have a shot. More room for surprises, but also more room for nonsense.

**No top-k limit** (all 100,000 tokens remain in play) lets temperature be the only control. Even astronomically unlikely tokens have a non-zero chance.

> **"Behind The Curtain" Sidebar**
>
> Top-k was one of the first sampling refinements developed for language models, and it has a practical origin story. Early researchers noticed that pure temperature sampling — even at reasonable temperatures — would occasionally select bizarre tokens from deep in the tail of the distribution. A long passage of coherent text would suddenly include a completely random word, like a typo in an otherwise clean document. Top-k was a simple, elegant fix: cut off the tail entirely. By eliminating the bottom 99,950 tokens, those random "typos" disappeared. The approach was crude but effective, and it remained the standard for years before top-p arrived with a more nuanced solution.

## The Problem with Top-k

Top-k has a limitation that becomes obvious once you think about it: it uses the same fixed number of candidates regardless of how confident the model is.

Remember the different distribution shapes from Chapter 18? Sometimes the model is very confident — one token has 95% probability. Other times, the model is deeply uncertain — probability is spread across hundreds of plausible options.

With top-k of 50:

- In the confident case (one token dominates), 50 candidates are too many. Most of the 49 runners-up are garbage that should never be selected. Top-k is letting in contestants who have no business being on stage.

- In the uncertain case (many plausible options), 50 candidates might be too few. Maybe the 51st most probable token is genuinely plausible — "evaluate" at 1.8% — but it got cut because 50 tokens with slightly higher probabilities filled the roster. Top-k is eliminating a viable contestant.

A fixed number doesn't adapt to the shape of the distribution. And that's exactly what top-p was designed to fix.

## Top-p: The Adaptive Cutoff

Top-p (also called **nucleus sampling**) takes a fundamentally different approach. Instead of picking a fixed number of candidates, it picks the smallest set of candidates whose combined probabilities reach a certain threshold.

Here's the analogy. Imagine you're filling a jar with marbles, where each marble represents a token and its size represents its probability. You start with the biggest marble (most probable token) and add it to the jar. Then the next biggest. Then the next. You keep going until the jar is "full enough" — meaning the total probability represented by the marbles in the jar reaches your target threshold, say 90%.

If the top token alone has 95% probability (a confident prediction), your jar is full after one marble. Top-p says: "That's enough. Only one candidate." This is appropriate — the model knows what should come next.

If the distribution is flat and it takes 200 tokens to accumulate 90% probability (an uncertain prediction), your jar holds 200 marbles. Top-p says: "All 200 candidates are in play." This is also appropriate — the model is genuinely uncertain, so many options should be considered.

**Top-p of 0.9** (a very common setting) means: include the minimum set of tokens whose combined probability is at least 90%. This automatically adapts to the distribution's shape.

**Top-p of 0.5** is more restrictive — only the most probable tokens covering 50% of the total probability are considered. This results in less variety but more consistency.

**Top-p of 1.0** includes all tokens — no filtering at all. Equivalent to turning off top-p entirely.

**Top-p of 0.1** is extremely restrictive — only the very top of the distribution. This produces nearly deterministic output, since you're only sampling from the handful of tokens that make up 10% of the probability mass.

> **"This Is Why..." Box**
>
> **This is why AI responses are almost always coherent at the word-to-word level, even when the overall direction might be questionable.** Top-p sampling (which most production AI systems use) ensures that only contextually plausible tokens are ever selected. The 99% of the vocabulary that would produce gibberish is eliminated before sampling even begins. You'll essentially never see an AI write "The career transition requires elephant mathematics" — because "elephant" would never make it into the top-p nucleus after "requires." The incoherent tokens are cut before they ever had a chance.

## Top-p Versus Top-k: A Practical Comparison

Let's see both in action with a concrete example. The model is generating the next token after "Your accounting experience gives you a strong..."

The probability distribution's top entries might look like:

| Rank | Token | Probability | Cumulative |
|------|-------|------------|------------|
| 1 | "foundation" | 22% | 22% |
| 2 | "advantage" | 18% | 40% |
| 3 | "background" | 12% | 52% |
| 4 | "basis" | 8% | 60% |
| 5 | "starting" | 7% | 67% |
| 6 | "edge" | 5% | 72% |
| 7 | "set" | 4% | 76% |
| 8 | "skill" | 3.5% | 79.5% |
| 9 | "understanding" | 3% | 82.5% |
| 10 | "grasp" | 2.5% | 85% |
| 11 | "platform" | 2% | 87% |
| 12 | "toolkit" | 1.5% | 88.5% |
| 13 | "grounding" | 1.2% | 89.7% |
| 14 | "footing" | 0.8% | 90.5% |

**Top-k of 5** would only consider: "foundation," "advantage," "background," "basis," and "starting." Five candidates, regardless of the distribution shape. "Edge" and everything below it is eliminated.

**Top-p of 0.9** would include tokens until cumulative probability reaches 90%: "foundation" through "grounding" — that's 13 candidates. Notice that "footing" at 90.5% cumulative barely didn't make the cut. The model has more room for interesting word choices like "edge," "toolkit," and "grounding," which are less expected but perfectly valid.

Now imagine the next token position happens to be after "The capital of France is" — where "Paris" has 97% probability. Top-k of 5 still allows 5 tokens. Top-p of 0.9 allows essentially just 1. Top-p automatically adapts to the model's confidence, while top-k does not.

This adaptive behavior is why top-p has become the dominant sampling strategy in production AI systems. It's smarter about when to allow creativity and when to enforce the obvious choice.

## How Temperature, Top-p, and Top-k Work Together

In practice, these controls are often used in combination. The typical order of operations is:

1. **The model produces raw probability scores** for all 100,000 tokens.
2. **Temperature is applied**, reshaping the distribution (sharpening or flattening it).
3. **Top-k filtering** removes all but the top k tokens (if top-k is set).
4. **Top-p filtering** removes additional tokens until the remaining ones cover the target probability mass.
5. **Sampling** draws one token from whatever candidates survived all the filters.

Think of it as a three-stage funnel. Temperature adjusts the probabilities. Top-k provides a hard cap on the number of candidates. Top-p provides a probability-aware cap. Together, they define the "pool" of tokens from which the final selection is made.

A common production configuration might be something like: temperature 0.7, top-p 0.9, no top-k limit. This gives moderate creativity (temperature flattens the distribution somewhat), with a safety net (top-p ensures only the most plausible 90% probability mass is in play).

A more conservative configuration: temperature 0.3, top-p 0.5. Low creativity, narrow candidate pool — great for factual tasks where you want consistency.

A creative configuration: temperature 1.0, top-p 0.95. Full creative range with just the wildest tokens trimmed off.

> **"Try This Now" Exercise**
>
> If your AI tool exposes top-p settings (sometimes labeled "nucleus sampling" or simply alongside the temperature slider), try this experiment:
>
> 1. Set temperature to 0.7 and top-p to 0.5. Ask for creative writing: "Write the opening paragraph of a novel about a time traveler." Note how constrained and conventional the output feels.
>
> 2. Keep temperature at 0.7 but change top-p to 0.95. Ask the same question.
>
> 3. Notice the difference: the higher top-p version will use more varied vocabulary, less predictable sentence structures, and more surprising imagery. You've widened the candidate pool without changing the overall adventurousness level.
>
> If your tool doesn't expose these settings, don't worry — the next lessons will focus on strategies you can use regardless of what settings are available to you.

## Other Sampling Strategies Worth Knowing

Beyond the big three (temperature, top-p, top-k), there are a few other sampling approaches that appear in production systems:

**Repetition penalty** reduces the probability of tokens that have already appeared recently in the response. Without it, the model sometimes gets stuck in loops — repeating the same phrase or cycling through the same set of ideas. Repetition penalty gently pushes the model toward fresh vocabulary and new thoughts. Think of it as a conversational rule: "Try not to use the same word twice in the same paragraph."

**Frequency penalty** is similar but works on a sliding scale — the more times a token has been used, the more its probability is reduced. This prevents not just immediate repetition but overuse of favorite words throughout a long response.

**Presence penalty** reduces the probability of any token that has appeared at all in the response, regardless of how many times. This is a stronger push toward vocabulary diversity — if you've used the word "important" once, it becomes slightly less likely to appear again.

**Min-p** is a newer strategy that sets a minimum probability threshold relative to the top token. If the top token has 40% probability and min-p is set to 0.1, only tokens with at least 4% probability (10% of 40%) are considered. Like top-p, this adapts to the distribution's shape, but it uses a different mathematical approach.

> **"Behind The Curtain" Sidebar**
>
> The search for the perfect sampling strategy is an active area of research, and there is no consensus winner. Different strategies work better for different tasks, different model sizes, and even different languages. Production AI systems often use custom combinations tuned through extensive testing — running thousands of prompts through different sampling configurations and measuring which produces the most helpful, coherent, and appropriate responses. The settings you experience as a user are the result of this extensive optimization, and they may be different from what you'd find in a research paper's default configuration.

## The Sampling Strategy as an Invisible Filter

Here's a perspective that brings this all together: the sampling strategy is an invisible filter between the model's raw knowledge and the text you actually read.

The model "knows" many possible continuations at each step. The probability distribution is the model's honest assessment of all those options. But the sampling strategy — temperature, top-p, top-k, penalties — determines which of those options you actually see.

It's like having access to a brilliant advisor who has ten thoughts on every question but whose answers are filtered through a secretary. A conservative secretary (low temperature, low top-p) only relays the advisor's safest, most mainstream thoughts. An adventurous secretary (high temperature, high top-p) passes along unusual ideas that the advisor considered less likely but still worth mentioning.

The model itself doesn't change. The knowledge doesn't change. The probability distributions don't change (well, temperature reshapes them, but the underlying model computations are the same). What changes is the selection process — the final step that turns probabilities into actual text.

> **"Pro Tip" Box**
>
> When you're working with an AI tool that allows you to adjust sampling parameters, start with the default settings and adjust one parameter at a time. If responses feel too generic or predictable, increase temperature slightly (try 0.1 increments). If responses feel too erratic or unfocused, decrease temperature. If responses repeat themselves, look for a repetition penalty setting. Making multiple changes at once makes it impossible to know which adjustment helped. Think of it like tuning a guitar — one string at a time.

## What This Means for You

Even if you never touch a sampling parameter directly, understanding these controls changes how you interpret AI behavior.

When the AI gives you a surprisingly creative response, you now know it's not because the AI "felt inspired." A random sample from the probability distribution happened to land on an unexpected token, which cascaded into a creative trajectory. The "inspiration" was sampling randomness interacting with the autoregressive loop.

When the AI feels repetitive and dull, you now know it's likely operating at low temperature or with restrictive top-p settings. The creative options exist in the model's probability distribution — they're just being filtered out before you see them.

When you regenerate a response and get something dramatically different, you know that the sampling process drew different tokens from the same distributions. The model's assessment of what's plausible didn't change — the random selection did.

And when you notice that different AI products feel like they have different "personalities" — one more conservative, another more playful — you now know that a significant part of that personality difference comes from different default sampling parameters, not necessarily from different underlying models.

This understanding will become actionable in Lesson 4, where we'll explore how to match these randomness controls to specific tasks. But first, there's one more generation strategy to meet: beam search and the "best of N" approach, which take a fundamentally different approach to the quality problem.
