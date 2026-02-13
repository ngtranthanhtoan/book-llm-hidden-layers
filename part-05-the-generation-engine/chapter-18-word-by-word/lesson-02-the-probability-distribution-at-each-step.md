# Lesson 2: The Probability Distribution at Each Step

## The 100,000-Way Decision That Happens Every Time

In the last lesson, you learned that the AI generates text one token at a time. But we glossed over something crucial: how does the model actually decide which token comes next? It doesn't just "know" the right word. At each step, it faces a staggering decision — choosing from a vocabulary of roughly 100,000 possible tokens. Every single token in that vocabulary gets a probability score. And the model must pick one.

This lesson is about that decision. It's where generation meets creativity, where certainty meets randomness, and where many of the AI behaviors you've noticed but never understood suddenly make perfect sense.

## The World's Most Elaborate Voting System

Imagine you're the mayor of a very unusual town. This town has 100,000 residents, and every time you need to make a decision, every single resident votes on what should happen next. But they don't just vote yes or no. Each resident gives a number representing how confident they are that their suggestion is the right one. Some residents are extremely confident — they might say "I'm 35% sure it should be this." Others have almost no confidence — "I'm 0.0001% sure about my suggestion." A few residents always have decent ideas, and many rarely have anything useful to contribute on any particular question.

That's essentially what happens inside the model at every token position. The model's vocabulary — roughly 100,000 tokens — is like those residents. For each position in the response, every single one of those 100,000 tokens gets assigned a probability. The token "the" might get 12%. The token "my" might get 8%. The token "banana" might get 0.001%. All 100,000 probabilities add up to 100%.

This probability assignment is called the **probability distribution**, and it is the raw output of the neural network at each step.

## What a Probability Distribution Actually Looks Like

Let's make this concrete. Suppose the AI has been generating a response to "Help me plan a career change from accounting to UX design," and it has so far produced: "The first step in your career transition is to..."

Now it needs to choose the next token. Here's a simplified version of what the probability distribution might look like:

| Token | Probability |
|-------|------------|
| "assess" | 15.2% |
| "evaluate" | 11.8% |
| "identify" | 10.4% |
| "understand" | 8.7% |
| "research" | 7.1% |
| "build" | 4.3% |
| "learn" | 3.9% |
| "explore" | 3.2% |
| "take" | 2.8% |
| "develop" | 2.4% |
| ... (thousands more tokens with smaller probabilities) |
| "banana" | 0.00002% |
| "quantum" | 0.00001% |

Look at that distribution. "Assess" is the front-runner, but it's far from a sure thing. It only has a 15.2% probability. The top ten tokens together account for maybe 70% of the probability, and the remaining 30% is spread across thousands of less likely options.

This is a critical insight: **at most token positions, the model is not certain about what should come next.** It has preferences — strong preferences — but there is always a range of reasonable options.

> **"Behind The Curtain" Sidebar**
>
> The probability distribution isn't just a flat ranking. It has a very distinctive shape that mathematicians call a "long tail." A handful of tokens capture most of the probability — maybe the top 10 tokens hold 60-80% combined. Then there's a rapid drop-off, with thousands of tokens holding tiny fractions of a percent. And at the far end of the tail, tens of thousands of tokens have probabilities so astronomically small that they'd essentially never be selected. The word "helicopter" following "The first step in your career transition is to..." has a probability that's effectively zero. The word exists in the vocabulary, and it technically has a non-zero probability, but it would take an almost inconceivable amount of randomness to select it.

## How the Distribution Gets Created

Where do these probabilities come from? They emerge from the final layer of the Transformer architecture we explored in Part 3.

Think of it this way. Your prompt enters the model and passes through all those layers — the early layers parsing grammar, the middle layers assembling meaning, the deep layers doing reasoning and planning. By the time the signal reaches the final layer, the model has built a rich, nuanced understanding of: what you asked, what it should say, what tone to use, what it's already said, and what should logically come next.

That final-layer representation gets converted into 100,000 numbers — one for each token in the vocabulary. These numbers (called "logits" in technical parlance, but think of them as "raw confidence scores") indicate how well each possible next token fits everything the model knows about the current context.

Those raw scores then get converted into proper probabilities through a process that ensures they all add up to 100%. High raw scores become high probabilities; low raw scores become tiny probabilities.

The entire thing — from prompt to probability distribution — takes a fraction of a second. And it happens from scratch for every single token position. The model doesn't remember its probability calculations from the previous step. It re-evaluates the entire context and produces a fresh distribution each time.

## The Moment of Choice

Now comes the pivotal question: given this distribution, which token does the model actually pick?

There are several strategies, and which one gets used depends on the settings chosen by whoever deployed the AI. We'll explore these in depth in Chapter 19, but let's establish the basics.

**Strategy 1: Always pick the most probable token.** This is called "greedy decoding." If "assess" has the highest probability, pick "assess." Every time. This produces the most predictable, conservative output. If you ran the same prompt a thousand times with greedy decoding, you'd get the same response every time.

**Strategy 2: Sample randomly from the distribution.** This means using the probabilities as weights in a random draw. "Assess" at 15.2% would be picked about 15 times out of 100. "Evaluate" at 11.8% would be picked about 12 times out of 100. Even "explore" at 3.2% would occasionally win the draw. This introduces genuine randomness into the output and is why you get different responses to the same prompt.

**Strategy 3: Something in between.** Most AI systems use modified sampling — they don't always pick the top token, and they don't do a fully random draw. They adjust the distribution to control how much randomness enters the process. This adjustment is what "temperature" controls, and it's the subject of our next chapter.

> **"This Is Why..." Box**
>
> **This is why the AI never gives the exact same response twice (in most settings).** The sampling process introduces randomness at every token position. Even if "assess" is the most probable first word, the model might sample "evaluate" instead. That choice cascades — "evaluate" changes the probability distribution for the next token, which changes the next, and so on. By the end of the response, the accumulated random choices have produced something that might be structurally similar but textually different from any other run. Two responses to the same prompt are like two snowflakes: built by the same process, following the same rules, yet never identical.

## The Shape of Certainty and Uncertainty

One of the most fascinating aspects of the probability distribution is how dramatically its shape changes depending on context. Sometimes the model is very confident, and sometimes it's deeply uncertain — and the distribution reflects this.

**High confidence (a "peaked" distribution):** After "The capital of France is", the token "Paris" might have a 95% probability. The distribution is sharply peaked — one token dominates, and everything else is negligible. There's very little randomness here, even with sampling. The model will almost always say "Paris."

**Low confidence (a "flat" distribution):** After "My favorite color is", the distribution might spread probability fairly evenly across many tokens — "blue" at 12%, "red" at 10%, "green" at 9%, "purple" at 7%, and so on. The model genuinely doesn't know what your favorite color is, and the distribution reflects that uncertainty honestly.

**Medium confidence (a "lumpy" distribution):** After "The first step in your career transition is to", several tokens are plausible — "assess," "evaluate," "identify," "research." The distribution has a cluster of reasonably likely options and then a rapid drop-off. This is the most common shape during natural text generation.

The shape of the distribution at each step is itself a kind of information. A peaked distribution means the context strongly constrains what comes next. A flat distribution means the model faces genuine ambiguity. And the sampling strategy determines how the model handles that ambiguity — whether it plays it safe or takes risks.

> **"Try This Now" Exercise**
>
> Here's an intuitive experiment. Ask the AI to complete these two sentences:
>
> 1. "Water freezes at a temperature of ___"
> 2. "The most beautiful city in the world is ___"
>
> Try each one five times (just regenerate the response). For the first sentence, you'll get "32 degrees Fahrenheit" or "0 degrees Celsius" almost every time — that's a peaked distribution with very little variation. For the second sentence, you'll get different cities each time — that's a flatter distribution with genuine uncertainty. You're seeing the probability distribution's shape reflected in the consistency (or inconsistency) of the output.

## The Vocabulary Constraint

There's an important limitation hiding in this process that most people never consider. The model can only produce tokens that are in its vocabulary. That vocabulary was fixed during training — typically around 100,000 tokens for modern models.

This means the model can never generate a truly novel piece of text in one step. It's always selecting from a pre-existing menu. The novelty comes from the combinations — the sequence of selections across hundreds of steps that has never been produced before.

Think of it like a piano. A piano has 88 keys. No pianist can play a note that doesn't correspond to one of those 88 keys. And yet the number of possible melodies is essentially infinite, because the creativity lies in the sequence and combination of notes, not in the individual notes themselves.

Similarly, an AI's vocabulary of 100,000 tokens is a fixed set of building blocks. But the number of possible text sequences that can be assembled from those blocks is so incomprehensibly vast that the model will never exhaust its creative possibilities. The constraint is real but not practically limiting.

> **"Behind The Curtain" Sidebar**
>
> Here's a mind-bending number: if a response is just 100 tokens long and each position could be any of 100,000 tokens, the total number of possible responses is 100,000 raised to the power of 100. That number is so large that it exceeds the number of atoms in the observable universe by a factor that itself exceeds the number of atoms in the observable universe. When people say "the AI could generate anything," they're not exaggerating by much. The combinatorial space is effectively infinite.

## Probability Does Not Mean Quality

Here's a crucial distinction that will serve you well: the most probable token is not always the best token.

Probability in this context means "most consistent with the patterns in the training data, given the current context." That often aligns with quality — the most likely next word in a well-written career advice passage is usually a good word. But not always.

Sometimes the most probable token leads to a generic, bland response. "The first step is to assess your skills" — accurate but predictable. A slightly less probable token might lead somewhere more interesting: "The first step is to shadow a UX designer for a day" — less statistically expected, but potentially more valuable advice.

This tension between probability and quality is at the heart of why temperature and sampling settings exist, and it's why the default settings for creative tasks are different from those for factual tasks. We'll explore this fully in Chapter 19.

## Our Running Example Under the Microscope

Let's revisit our career change prompt one more time, but now with probability distributions in mind.

When you type "Help me plan a career change from accounting to UX design," the model begins generating. At each step, it's producing a probability distribution shaped by:

- The system prompt (be helpful, professional, structured)
- Your prompt (career change, accounting, UX design)
- Everything it's generated so far

Early in the response, the distributions tend to be fairly spread out — there are many valid ways to begin career advice. The model might say "Making," "Planning," "Here's," "Transitioning," or many other opening tokens. This is why regenerating a response often gives you a substantially different opening — the first few distributions are broad enough to admit many paths.

As the response progresses, the distributions often narrow. If the model is mid-sentence — "UX design requires strong skills in..." — the next token is heavily constrained. "Visual," "user," "problem," and "empathy" are all likely. "Accounting" would be odd here. "Elephant" would be absurd.

By the end of the response, if the model is wrapping up with "Good luck with your career..." — the next token is almost certainly "change," "transition," or "journey." The distribution is sharply peaked.

This rhythm — broad distributions at the start, narrower distributions mid-flow, occasionally broad again at transition points — is the pulse of the generation process. You can almost feel it if you watch the response stream in token by token.

> **"This Is Why..." Box**
>
> **This is why regenerating a response sometimes gives you something dramatically different, and sometimes barely changes anything.** If the probability distributions at the key decision points were broad (many plausible options), regeneration can produce a very different response — the random sampling landed differently. If the distributions were narrow (one dominant option at most steps), regeneration produces something nearly identical. Factual questions tend to have narrow distributions (one right answer), which is why regenerating "What year was the Eiffel Tower built?" always gives you 1889. Open-ended questions have broad distributions, which is why regenerating "Write me a poem about the ocean" gives you a different poem every time.

## What You Now See

With this lesson, your X-ray vision has sharpened considerably. You no longer see the AI's response as a single, monolithic output. You see a chain of 100,000-way decisions, each one shaped by probabilities that reflect the model's training, your prompt, and everything generated so far.

This understanding prepares you for the next two lessons, where we'll explore what happens when the AI commits to a path it can't easily back out of (the commitment problem), and how you can use your understanding of the autoregressive loop to steer generation by controlling the opening words. But first, you need to sit with this image: every word the AI produces is the winner of a 100,000-way election, and the margin of victory varies from landslide to razor-thin.

That's the probability distribution at work. And it's happening right now, in real-time, every time you get a response from an AI.
