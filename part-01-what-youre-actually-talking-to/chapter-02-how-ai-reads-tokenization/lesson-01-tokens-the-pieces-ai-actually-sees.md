# Lesson 1: Tokens — The Pieces AI Actually Sees

## The Ingredient Prep Station

Before our restaurant chef can cook anything, the ingredients need to be prepped. Whole chickens get broken down into parts. Vegetables get chopped. Spices get measured out. Nobody cooks a whole, unprepped chicken — the raw materials need to be cut into workable pieces first.

The same is true for an LLM. Before the AI can do anything with your message, your text needs to be chopped up into pieces it can work with. These pieces are called **tokens**, and they are the fundamental unit of everything the AI does. Every calculation, every prediction, every moment of "understanding" — it all happens at the token level.

If Chapter 1 gave you X-ray vision into *what* the AI is, this chapter gives you X-ray vision into *how it reads.* And what you're about to discover is that the AI reads in a way that is profoundly different from how you do.

## You See Words. The AI Sees Tokens.

When you read the sentence "I want to change careers from accounting to UX design," you see eleven words. You process them as familiar units of meaning — each word has a definition, a connotation, a role in the sentence.

The AI doesn't see eleven words. It sees something like this:

"I" | " want" | " to" | " change" | " careers" | " from" | " accounting" | " to" | " UX" | " design"

Those are tokens. In this case, each word happened to correspond to one token, but that's not always the case — and the cases where it *isn't* true are where things get interesting and sometimes go wrong.

A token is a chunk of text — sometimes a whole word, sometimes part of a word, sometimes a single character, sometimes a space plus a word. The AI's vocabulary is a fixed list of these chunks, and every piece of text you feed it must be broken down into items from that list before the AI can process it.

Think of it like Scrabble tiles, but instead of having one tile per letter, you have tiles for common words ("the," "is," "and"), tiles for word parts ("ing," "tion," "pre"), tiles for individual characters ("x," "q," "7"), and tiles for common combinations ("because," " however"). Every message you type gets decomposed into some combination of these tiles.

## The Tokenizer: The First Translator

The process of breaking text into tokens is called **tokenization**, and the software that does it is called a **tokenizer**. The tokenizer is the very first thing that processes your message — it sits between you and the AI model itself, translating your human-readable text into a sequence of token IDs (numbers) that the model can work with.

Here's the crucial thing: **the tokenizer is not the AI model.** It's a separate, pre-built piece of software that uses a fixed vocabulary. It doesn't learn, it doesn't adapt, and it doesn't understand meaning. It applies mechanical rules to chop your text into pieces.

This matters because the tokenizer makes decisions that affect everything downstream. How your text gets chopped into tokens determines what the AI "sees" — and the AI can only work with what it sees.

Going back to our restaurant: the tokenizer is like the prep cook who breaks down ingredients before the chef sees them. If the prep cook cuts the chicken into strange pieces, the chef has to work with those strange pieces. The chef (the AI model) never sees the original whole chicken (your original text) — only the prepared pieces (the tokens).

> **"Behind The Curtain" Sidebar**
>
> Every AI model has its own tokenizer with its own vocabulary. GPT-4's tokenizer chops text differently from Claude's, which chops differently from Llama's. This means the exact same sentence gets represented as different sequences of tokens in different models. It's like how the same recipe might be prepped differently in different kitchens. This is one reason why the same prompt can produce subtly different results in different models — the models are literally "reading" different things.

## How Tokenization Actually Works

Most modern tokenizers use a technique called **Byte Pair Encoding** (BPE) or something similar. Here's the intuition, without the math.

Imagine you're creating a shorthand system for writing. You start with the alphabet — 26 letters, each its own symbol. Then you look at a huge amount of text and notice that certain pairs of letters appear together extremely often: "th," "he," "in," "er," "an." So you create single symbols for these common pairs. Now your shorthand is more efficient — instead of writing two symbols for "th," you write one.

Then you look again and notice that some combinations of your new symbols appear frequently: "the," "tion," "ing." You create single symbols for those too. You keep going, building up larger and larger chunks, until you have a vocabulary of, say, 100,000 symbols that can efficiently represent any text.

That's essentially how BPE works. The result is a vocabulary where:
- Very common words like "the," "is," and "and" are single tokens
- Common words like "important" or "different" are single tokens
- Less common words get split into pieces: "tokenization" might become "token" + "ization"
- Rare words get split into smaller pieces or even individual characters
- Numbers, punctuation, and special characters each get their own tokens

The key insight: **common things get efficient representation (fewer tokens), while rare things get broken into more pieces (more tokens).** This isn't arbitrary — it's a compression scheme optimized for the kind of text the tokenizer was designed to handle.

## Seeing What the AI Sees

Let's look at our running example through the AI's eyes. When you type "Help me plan a career change from accounting to UX design," the tokenizer might break it down roughly like this:

| Your Text | Tokens |
|-----------|--------|
| Help | "Help" |
| me | " me" |
| plan | " plan" |
| a | " a" |
| career | " career" |
| change | " change" |
| from | " from" |
| accounting | " accounting" |
| to | " to" |
| UX | " UX" |
| design | " design" |

That's about 11 tokens for 11 words — a roughly one-to-one mapping. Straightforward.

But now consider a more complex sentence: "The dermatologist recommended that the patient's hyperpigmentation be treated with tretinoin." The tokenizer might produce something like:

| Your Text | Tokens |
|-----------|--------|
| The | "The" |
| dermatologist | " dermat" + "ologist" |
| recommended | " recommended" |
| that | " that" |
| the | " the" |
| patient's | " patient" + "'s" |
| hyperpigmentation | " hyper" + "pig" + "mentation" |
| be | " be" |
| treated | " treated" |
| with | " with" |
| tretinoin | " tret" + "in" + "oin" |

See the difference? Common words are single tokens. Specialized words get broken into pieces. And sometimes the pieces are surprising — "hyperpigmentation" might get split as "hyper" + "pig" + "mentation," which doesn't correspond to how a human would break down the word (hyper + pigmentation).

> **"This Is Why..." Box**
>
> **This is why AI sometimes seems to struggle with unusual words, technical jargon, or names.** When a word gets broken into multiple tokens, the AI has to reconstruct its meaning from the pieces — and sometimes those pieces are misleading. The tokenizer splits based on statistical frequency patterns, not on meaning. So a rare medical term or an unusual name might get chopped into pieces that make no semantic sense, forcing the AI to work harder (and sometimes less accurately) to handle it.

## Tokens Are Not Characters, Not Words, Not Syllables

One of the most common misconceptions is that tokens correspond to some familiar linguistic unit. They don't. Tokens are an entirely AI-native concept. They're optimized for *statistical efficiency of representation*, not for human readability.

- Sometimes a token is a whole word: "the," "computer," "running"
- Sometimes a token is a word fragment: "un" + "believ" + "able"
- Sometimes a token is a single character: "x," "7," "@"
- Sometimes a token includes a leading space: " the" (space-the as a single token)
- Sometimes a token is a common multi-word pattern: some tokenizers might encode very frequent phrases as single tokens

The average token in English is roughly four characters long, so a rough rule of thumb is that 100 tokens is about 75 words. But this varies significantly with the type of text.

> **"Try This Now" Exercise**
>
> Most AI providers have online tokenizer tools. Search for "OpenAI tokenizer" or "token counter" and paste in a few sentences. Try these:
> 1. A simple English sentence: "The cat sat on the mat."
> 2. A sentence with unusual words: "The archaeopteryx exhibited plesiomorphic characteristics."
> 3. A sentence with numbers and symbols: "My email is john.doe@example.com and my phone is +1-555-0123."
> 4. A sentence in another language, if you speak one.
>
> Count the tokens for each and notice how the complexity of the text affects the token count. Simple English is efficient; specialized terms, numbers, and non-English text are often less efficient.

## Why This Matters: The Invisible First Step

Tokenization is invisible to you as a user. You never see the tokens. You type text; the AI responds with text. The tokenization happens silently, behind the curtain.

But it matters enormously because tokenization is the first filter your message passes through. Every word you type gets broken down into tokens, and the AI can only work with those tokens. It's like the resolution of a camera — you can only see details that the camera's sensor can capture. If the sensor is low-resolution, fine details get lost. Similarly, if a word gets tokenized into awkward pieces, the AI's ability to work with that word is compromised.

In the next lesson, we'll see exactly how this invisible first step can cause very visible problems — starting with a puzzle that has stumped millions of AI users: why can't the AI count the letters in "strawberry"?

> **"Pro Tip" Box**
>
> When you're working with an AI and getting unexpected results — especially with names, technical terms, or non-English text — consider that the issue might start at the tokenization layer. If a word is being split into confusing pieces, the AI is working at a disadvantage. You can sometimes help by breaking down complex terms yourself. Instead of using the jargon word, briefly define it: "Hyperpigmentation (darkening of the skin)" gives the AI clean, common tokens to work with alongside the specialized term.
