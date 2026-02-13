# Lesson 3: Languages, Scripts, and Unequal Tokenization

## Not All Languages Are Created Equal (In the Eyes of an AI)

Here's an uncomfortable truth that doesn't get enough attention: if you write to an AI in English, your message is read efficiently — most words map to one or two tokens. If you write in Japanese, Korean, Thai, or many other languages, the same *meaning* might cost you two, three, or even ten times as many tokens.

This isn't a design choice anyone made on purpose. It's a consequence of how tokenizers are built, and it has real implications — practical, economic, and ethical — that matter for anyone working with AI in a multilingual world.

## Why English Gets VIP Treatment

Remember how tokenizers are built: they look at a huge pile of text and create tokens for the most common chunks. The "huge pile of text" used to train most tokenizers is overwhelmingly in English. English text dominates the internet. It dominates the datasets. It dominates the training.

When the tokenizer learns its vocabulary from this English-heavy dataset, it naturally creates many tokens that correspond to common English words and word parts. "The," "and," "important," "running," "tion," "ing" — these all get efficient single-token representation because they appeared millions of times in the training data.

But a Chinese character, a Hindi word in Devanagari script, or an Arabic phrase? They appeared far less frequently in the training data, so the tokenizer didn't create efficient tokens for them. Instead, these characters and words get broken down into smaller, less meaningful pieces — sometimes down to individual bytes of the underlying character encoding.

Think of it this way. Imagine a chef who learned to cook in France. She has specialized knives for every French ingredient — a perfect blade for julienning carrots, a precise tool for mincing shallots. But when she encounters a coconut, she doesn't have a coconut machete. She has to hack at it with tools designed for other things. The coconut gets opened, but it takes more effort and more cuts.

Non-English text is the coconut. It gets processed, but with more tokens, more effort, and sometimes less precision.

## The Numbers Tell the Story

Let's make this concrete. Consider the phrase "Help me plan a career change" and its equivalent in several languages:

**English:** "Help me plan a career change" — roughly 7 tokens.

**Spanish:** "Ayúdame a planificar un cambio de carrera" — roughly 12 tokens. About 70% more.

**Japanese:** "キャリアチェンジの計画を手伝ってください" — roughly 20-25 tokens. Three times as many.

**Thai:** "ช่วยฉันวางแผนการเปลี่ยนอาชีพ" — roughly 30+ tokens. More than four times as many.

**Hindi:** "करियर बदलने की योजना बनाने में मेरी मदद करें" — roughly 25-30 tokens.

The same *meaning*, the same *request*, but wildly different token costs. And since AI services typically charge by the token, and since models have fixed token limits for how much text they can process at once, this disparity creates real-world inequality.

> **"This Is Why..." Box**
>
> **This is why AI conversations in non-English languages sometimes feel shorter, less detailed, or more expensive.** It's not that the AI doesn't "care" about other languages. It's that the tokenization is less efficient, which means (1) the same message uses more tokens, (2) the AI has less "room" in its context window for content, and (3) the cost per equivalent message is higher. A Japanese speaker might hit the model's token limit in half the conversation length that an English speaker can sustain.

## The Script Factor

The disparity isn't just about language — it's about script (the writing system).

Languages written in the Latin alphabet (English, Spanish, French, German, etc.) benefit from tokenizers that were heavily trained on Latin-script text. They get efficient tokenization.

Languages written in logographic scripts (Chinese, Japanese kanji) face a particular challenge. Each character carries meaning (unlike Latin letters, which are mostly meaningless individually), but the tokenizer may not have efficient tokens for most of these characters. A single Chinese character that conveys a complete concept might get broken into two or three tokens representing its UTF-8 byte encoding — the raw computer code for the character, which carries no linguistic meaning at all.

It's as if the prep cook at our restaurant, encountering an unfamiliar ingredient, didn't just chop it differently — she broke it down into its molecular components instead of recognizing it as a food item. The chef can still work with molecular components, but it's much harder than working with a recognizable ingredient.

Languages written in Cyrillic (Russian, Ukrainian), Devanagari (Hindi, Marathi), Arabic script, or other non-Latin writing systems fall somewhere in between — less efficient than Latin-script languages, but often more efficient than logographic scripts.

> **"Behind The Curtain" Sidebar**
>
> Some newer tokenizers are designed to be more equitable across languages. They're trained on more balanced multilingual datasets, and they use techniques that ensure reasonable token efficiency for a wider range of scripts. This is an active area of improvement — AI companies are aware of the disparity and working to reduce it. But as of this writing, significant differences remain, and they affect everyone who works with AI in non-English contexts.

## Real-World Impact: Three Stories

**The Business Report:** A Japanese executive asks an AI to help write a market analysis report. The English version of the same report would use about 2,000 tokens. The Japanese version uses about 5,000 tokens. In a model with a 128,000-token context window, this means the Japanese version can sustain a conversation with about 40% less back-and-forth before hitting the limit. The executive gets a less iterative, less refined result — not because of any difference in the AI's capabilities, but because of tokenization overhead.

**The Student's Homework:** A Thai university student uses AI to help with an essay. She types the same number of paragraphs as her American classmate, but her text consumes three to four times as many tokens. She hits usage limits faster, pays more for API access, and has less room for the AI to provide detailed feedback.

**The Code-Switching Conversation:** A bilingual user in India writes a prompt that mixes Hindi and English (a natural communication pattern called "code-switching"). The English portions tokenize efficiently; the Hindi portions do not. The AI processes a confusing mix of well-formed tokens and fragmented byte sequences, potentially affecting the quality of its response.

## The Hidden Cost of Inefficient Tokenization

There's a deeper consequence beyond just "using more tokens." When text gets tokenized into many small, meaningless pieces, the model has to work harder to reconstruct meaning from those pieces. Each token goes through the model's processing layers, and there's a limit to how many tokens the model can handle. When a single Chinese character that means "love" becomes three meaningless byte-level tokens, the model uses three slots of its processing capacity on something that should have been one.

This can affect response quality. Not dramatically — modern models are impressively good at handling multilingual text despite tokenization inefficiency — but in subtle ways. Responses in languages with inefficient tokenization may be slightly less nuanced, slightly more prone to errors, and slightly less able to maintain long, complex arguments.

It's the restaurant analogy again: if the prep cook gives the chef an ingredient broken into ten tiny pieces instead of one recognizable piece, the chef can usually still figure out what to do. But it takes more mental effort, and the dish might not be quite as refined as when the chef received a clean, recognizable ingredient.

> **"Try This Now" Exercise**
>
> If you speak more than one language, try this experiment. Ask an AI the same question in English and in your other language. Compare:
> 1. The length and detail of the responses (measured in paragraphs, not tokens)
> 2. The quality and nuance of the advice
> 3. How many back-and-forth turns you can have before the conversation seems to lose context
>
> If you only speak English, try comparing how the AI handles a prompt in plain English versus one that includes many technical terms, unusual proper nouns, or emoji. You're observing tokenization efficiency differences in action.

## What Can You Do About It?

If you're working in a non-English language, here are practical strategies:

**Consider bilingual prompting.** For some tasks, you can write your prompt in English (to get efficient tokenization and access to patterns that are richest in English) and ask the AI to respond in your target language. This isn't always appropriate — it depends on the task — but for tasks where the thinking matters more than the input language, it can improve results.

**Be more concise.** Since your text costs more tokens, efficiency matters more. This doesn't mean dumbing down your prompts — it means being precise and cutting unnecessary filler.

**Manage context deliberately.** In long conversations, summarize earlier exchanges rather than relying on the model to remember everything. This conserves tokens, which is especially important when your language has a higher token cost.

**Provide key terms in both languages.** If you're discussing a specialized topic, giving the key terms in both your language and English can help the model access the most relevant patterns. "UXデザイン (UX Design) への転職を計画しています" gives the model both the Japanese and English tokens to work with.

> **"Pro Tip" Box**
>
> If you're building an application that uses AI and your users speak multiple languages, tokenization disparity is a critical design consideration. Budget more tokens for non-English users. Test your application in multiple languages and scripts. Don't assume that a feature that works well within token limits for English users will work equally well for users writing in Japanese, Arabic, or Hindi. The tokenization tax is invisible but real.

## The Bigger Picture: Language Equity in AI

The tokenization disparity is a microcosm of a larger issue in AI: the technology works best for the people and languages that were best represented in the training data. English speakers get the most efficient tokenization, the richest patterns, and the most nuanced responses — not because anyone decided it should be this way, but because the internet (and therefore the training data) is disproportionately English.

This is gradually improving. AI companies are investing in multilingual training data, more equitable tokenizers, and models that perform more consistently across languages. But progress is slow, and the fundamental architecture — tokenization based on statistical frequency — means that majority languages will always have an inherent advantage.

For you as a user, the practical takeaway is this: understanding that the AI reads your language through a filter that was optimized for English helps you set appropriate expectations and adopt strategies that mitigate the disparity. You're not imagining that the AI seems to work better in English. It probably does. And now you know why.
