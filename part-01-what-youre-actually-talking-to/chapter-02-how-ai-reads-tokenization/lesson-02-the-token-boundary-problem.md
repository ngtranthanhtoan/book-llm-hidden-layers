# Lesson 2: The Token Boundary Problem

## The Strawberry Puzzle

In 2024, a simple question broke the internet: "How many R's are in the word 'strawberry'?"

Millions of people tried it. The answer is three — s-t-r-a-w-b-e-r-r-y — and most humans can count them in seconds. But AI after AI got it wrong. Many confidently answered "two." Some said "one." The world's most sophisticated language models, capable of passing the bar exam and writing working software, couldn't count the letters in a common English word.

This wasn't a mystery to anyone who understood tokenization. It was the token boundary problem in its most visible, most embarrassing form. And understanding it will give you practical insight into one of the AI's most predictable blind spots.

## Where the Boundaries Fall

Remember from Lesson 1: the AI doesn't see letters. It sees tokens. When the word "strawberry" arrives at the model, the tokenizer chops it into pieces — and those pieces don't respect letter boundaries.

Depending on the specific tokenizer, "strawberry" might get broken into something like:

"str" + "aw" + "berry"

or:

"straw" + "berry"

or even:

"st" + "raw" + "ber" + "ry"

Notice what's happening. The letter "r" might end up split across different tokens. In "str" + "aw" + "berry," there's one "r" at the end of "str," and two "r"s inside "berry." But the model doesn't process these as individual letters — it processes them as tokens. It would need to look *inside* the tokens, decompose them back into individual characters, and count specific characters across token boundaries.

This is not what the model was trained to do. The model works at the token level. Asking it to count letters within tokens is like asking someone to count the individual threads in a piece of fabric — possible, but not what the fabric was designed for.

> **"This Is Why..." Box**
>
> **This is why AI struggles with letter-counting, spelling tasks, anagrams, and character-level puzzles.** The model never sees individual characters as its primary unit of operation. It sees tokens. Any task that requires character-level analysis — counting specific letters, reversing words letter by letter, solving crossword puzzles, or judging whether a word is a palindrome — is working against the grain of how the system processes text. It's not that the AI is "dumb." It's that you're asking a tool designed for meaning-level processing to do character-level work, like asking a telescope to look at something under a microscope.

## The Boundary Problem Goes Beyond Letters

The strawberry example is famous, but the token boundary problem extends far beyond letter-counting. It shows up whenever the meaningful boundaries of your text don't align with the token boundaries created by the tokenizer.

**Names and proper nouns:** A name like "Tchaikovsky" might get tokenized as "Tch" + "a" + "ik" + "ov" + "sky." Each piece is a meaningless fragment, and the model has to reconstruct the whole name from these fragments. Common names like "John" or "Sarah" are usually single tokens. Unusual names get fragmented, and the model may handle them less reliably.

**Code and technical syntax:** The string `backgroundColor` might become "background" + "Color" or "back" + "ground" + "Color." The token boundaries might not match the camelCase boundaries that carry meaning in programming. This can affect how well the AI understands and generates code.

**URLs and email addresses:** Something like `john.doe@company.com` might get split into many tokens, with the structural elements (@, ., com) scattered among other token fragments. The model has to work harder to understand this as a structured address.

**Numbers:** The number "1,234,567" might be tokenized as "1" + "," + "234" + "," + "567" or some other split. The model doesn't natively understand that this is one number — it sees a sequence of tokens that it has learned, statistically, tend to represent a large number.

## The Scrabble Tile Problem

Here's another way to think about it. Imagine playing Scrabble, but instead of tiles with individual letters, your tiles have multi-letter chunks on them. You have a tile that says "STR," another that says "AWB," another that says "ERRY." You can spell "strawberry" by putting these tiles in order — but if someone asks you "how many R tiles did you use?", you'd have to look at the letters *within* each tile, which isn't how the game is designed to be played.

The model is playing Scrabble with multi-letter tiles. It's optimized for arranging tiles into meaningful sequences, not for analyzing the letters printed on each tile.

## Real-World Consequences

The token boundary problem isn't just a party trick for stumping AI. It has practical consequences that affect everyday use.

**Rhyming and poetry:** Rhyming depends on the sounds at the *ends* of words — which often fall in the middle of a token or across a token boundary. This is why AI-generated poetry sometimes has near-rhymes or unexpected sound patterns. The model is working with tokens, not with phonemes (units of sound).

**Word games and puzzles:** If you ask the AI to help with a crossword puzzle, an anagram, or a word game that depends on individual letters, expect inconsistent results. The AI might solve some by recognizing the pattern from its training data (it's seen many word game solutions) but fail at others that require genuine character manipulation.

**Exact string manipulation:** Tasks like "reverse this word," "remove all vowels from this sentence," or "replace every third character with an asterisk" require character-level operations that don't map well to token-level processing.

**Formatting and whitespace:** Tokens sometimes include leading whitespace (a space before a word), which can cause subtle issues with formatting, alignment, and whitespace-sensitive contexts like code indentation.

> **"Behind The Curtain" Sidebar**
>
> Here's a surprising fact: some newer models have been specifically trained to handle character-level tasks better, despite the token boundary problem. They do this not by changing the tokenization (the fundamental architecture still uses tokens) but by including character-level tasks in their training data. The model has seen enough examples of "How many R's are in strawberry? Let me check: s-t-r-a-w-b-e-r-r-y. There are 3 R's" that it has learned the *pattern* of counting letters, even though it doesn't naturally operate at the character level. This is a beautiful example of how training can partially compensate for architectural limitations — but it's a workaround, not a fundamental fix.

## The Before/After: Working With the Grain

Understanding the token boundary problem immediately tells you how to get better results.

**Before (working against the grain):**

"How many times does the letter 'e' appear in 'entrepreneurship'?"

The AI might get this wrong because it's asking for character-level analysis across token boundaries.

**After (working with the grain):**

"I need to count specific letters in a word. Please spell out the word 'entrepreneurship' one character at a time, numbering each character, and then count how many times the letter 'e' appears."

By asking the model to spell out the word character by character, you're forcing it to generate tokens that *correspond* to individual characters. Once the characters exist as separate tokens in the generation, the model can work with them more reliably. You're essentially doing the prep cook's job — breaking the ingredient down into the right pieces — before asking the chef to work with it.

> **"Try This Now" Exercise**
>
> Try both versions of the letter-counting task with an AI:
>
> **Version 1:** "How many R's are in the word 'strawberry'?"
>
> **Version 2:** "Please spell out the word 'strawberry' character by character, then count the R's."
>
> Try it with a few different words of varying complexity. Notice when the AI gets it right and when it struggles. You're developing an instinct for when you're running into token boundary issues.

## When the Prep Cook Makes Strange Cuts

Here's one more dimension to the token boundary problem: the tokenizer's decisions are based on statistical frequency, not meaning. This means words can get split in ways that are misleading.

Consider the word "understand." A tokenizer might split it as "under" + "stand." Now, "under" and "stand" are both meaningful English words, but their meanings have nothing to do with the meaning of "understand." The model, thankfully, is sophisticated enough to handle common cases like this — it's seen "understand" so many times in training that it has learned to treat "under" + "stand" as a unit. But with rarer words, the misleading split can genuinely confuse things.

For instance, the word "therapist" might get tokenized as "the" + "rapist" — a split that is meaningless and inappropriate, but the tokenizer doesn't understand meaning; it just follows statistical patterns. (This particular example has been widely discussed in the AI community and is one reason why tokenizer design gets careful attention.)

The broader point: the tokenizer is a blunt instrument. It applies statistical rules without understanding. And while the model is usually smart enough to work around the tokenizer's limitations, there are edge cases where the first translation from text to tokens introduces problems that ripple all the way through to the response.

## A Practical Framework

Here's how to think about the token boundary problem in your daily AI use:

**Likely fine:** Tasks involving meaning, semantics, ideas, arguments, explanations, creative writing, analysis. These operate at the level where tokens work well.

**Potentially problematic:** Tasks involving character-level operations, exact formatting, precise string manipulation, unusual proper nouns, specialized terminology. These can run into token boundary issues.

**Workaround available:** For character-level tasks, ask the model to spell things out, work step by step, or show its work. This creates token-level representations of character-level information, bridging the gap.

The token boundary problem is your first concrete example of a theme we'll return to throughout this book: understanding the AI's internal representation — what it actually "sees" — lets you structure your requests to work *with* the system's design rather than against it.

> **"Pro Tip" Box**
>
> When you encounter an AI error that seems bafflingly simple — "How can it possibly get *that* wrong?" — before blaming the model's intelligence, check whether the task requires character-level processing. Many of the AI's most embarrassing failures happen at the tokenization level, not the reasoning level. The fix is often straightforward: restructure your request so the critical information exists as separate, clean tokens rather than hidden inside token fragments.
