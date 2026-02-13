# Lesson 4: The Vocabulary — A Fixed Menu of Pieces

## The Restaurant With a Fixed Menu

Every restaurant has a menu. Some have enormous menus with hundreds of options; some have streamlined menus with twenty carefully chosen dishes. But no restaurant offers literally everything. There's always a boundary — a set of dishes you can order and, implicitly, an infinite set of things you cannot.

An LLM's tokenizer works the same way. It has a **vocabulary** — a fixed list of tokens, typically around 32,000 to 100,000 items — and every piece of text you ever send to the AI must be decomposed into items from this list. No more, no less. If your text contains something that doesn't match any vocabulary item neatly, it gets broken down into smaller pieces until it can be represented by items on the list.

This fixed menu is one of the most important constraints in the entire AI system, and understanding it reveals why certain things are easy for the AI and certain things are surprisingly hard.

## What's on the Menu

Let's peek at the vocabulary list. While the exact vocabulary varies between models, a typical tokenizer vocabulary includes:

**Common English words** (each as a single token): "the," "is," "and," "for," "that," "with," "this," "from," "have," "are," "not," "but," "what," "all," "can," "her," "was," "one," "our"

**Less common but still frequent words**: "important," "different," "information," "experience," "development," "understand," "technology," "international"

**Word fragments and prefixes/suffixes**: "un," "re," "pre," "ing," "tion," "ment," "ness," "able," "ful," "less," "ly"

**Individual characters and digits**: every letter of the alphabet, digits 0-9, punctuation marks, common symbols

**Special tokens**: markers for the beginning and end of text, separators between different parts of a conversation, padding tokens

**Tokens for other languages**: common words and character combinations from major world languages, though (as we saw in Lesson 3) with less coverage than English

**Byte-level fallback tokens**: for anything that doesn't match anything else — raw byte representations that can encode any character in any language, even if inefficiently

The vocabulary is determined *before* the AI model is trained, and it doesn't change afterward. It's baked in. Frozen. The AI model and the tokenizer are married for life.

> **"Behind The Curtain" Sidebar**
>
> The vocabulary size is a carefully considered engineering trade-off. A larger vocabulary means more words get their own single token, which is more efficient — but it also means the model needs more parameters (and thus more computing power) to process the larger vocabulary. A smaller vocabulary means less computing power but more token-splitting for unusual words. Most modern models land between 32,000 and 100,000 tokens, which turns out to be a sweet spot that handles common text efficiently while keeping computational requirements manageable. This trade-off was decided by engineers before you ever typed your first prompt.

## The Fixed Menu Problem

Here's where the fixed vocabulary creates real consequences. The vocabulary was created from a specific dataset at a specific point in time. Anything that wasn't well-represented in that dataset may be poorly represented in the vocabulary. This includes:

**New words and neologisms.** The word "ChatGPT" didn't exist before 2022. If the tokenizer was built before then, "ChatGPT" doesn't have its own token — it gets split into something like "Chat" + "G" + "PT" or "Chat" + "GP" + "T." The model can still handle it (it learned about ChatGPT during training, even if the tokenizer doesn't have a token for it), but the representation is less clean.

**Brand names and product names.** "iPhone" might be a single token (it's common enough), but "Anthropic" might get split into "Anthrop" + "ic." Specialized product names, startup names, and newly coined terms are almost always multi-token.

**Personal names.** "Michael" is probably a single token. "Xiomara" might become "Xi" + "om" + "ara." "Tchaikovsky" might become four or five tokens. The more unusual the name, the more tokens it costs — and the more the model has to work to process it as a single name rather than a sequence of unrelated fragments.

**Domain-specific terminology.** "Photosynthesis" might be a single token, but "photoelectrochemical" might become "photo" + "elect" + "roch" + "emical." The more specialized the term, the more likely it is to be fragmented.

**Emoji and symbols.** Most emoji get tokenized into multiple tokens representing their underlying Unicode byte sequences. The AI doesn't "see" a smiley face — it sees a sequence of byte-level tokens that it has learned to associate with the concept of a smiley face.

> **"This Is Why..." Box**
>
> **This is why AI sometimes misspells unusual names, mangles technical terms, or handles emoji inconsistently.** The tokenizer's fixed menu doesn't have clean entries for everything. When a word gets split into fragments, the model must reconstruct the whole from parts that may not carry meaningful information. It usually succeeds, but with more effort and less reliability than when working with common words that are single tokens.

## The Analogy: Describing Colors with a Limited Palette

Imagine you're a painter, but you only have 100 colors of paint. For most paintings, 100 colors is plenty — you can mix and blend to create almost any shade. But occasionally you need a very specific color — a particular teal, say — and you don't have it. You can approximate it by mixing blue and green and white, but it's never quite exact.

The tokenizer's vocabulary is like that palette. For common text, 100,000 tokens is more than enough to represent everything cleanly. But for unusual text — rare names, technical jargon, non-English scripts — the vocabulary has to approximate, splitting text into available pieces and relying on the model to reconstruct the intended meaning from those pieces.

The model is a remarkably good mixer of paint. But there's a limit to how accurately you can represent "Xiomara Tchaikovsky's photoelectrochemical research" when you're working with a palette that was optimized for "The cat sat on the mat."

## How the Vocabulary Shapes What the AI Is Good At

The vocabulary isn't just a technical detail — it shapes the AI's strengths and weaknesses at a fundamental level.

**Efficient vocabulary items = high competence.** Topics that are well-represented in the vocabulary (common English, standard technical terms, popular programming languages) get clean tokenization. The model processes these efficiently and performs well.

**Inefficient vocabulary items = more variable competence.** Topics that require many fragmented tokens (rare terminology, non-Latin scripts, highly specialized domains) are processed less cleanly. The model still works, but with more variability and more room for error.

This creates an invisible hierarchy. The AI is implicitly better at tasks where the vocabulary is efficient and implicitly weaker where it isn't — and this hierarchy tracks closely with what was common in the training data.

Consider our career-change example. "Help me plan a career change from accounting to UX design" uses common, well-tokenized vocabulary. The model processes this cleanly. But "Help me plan a career change from cost accountancy to human-computer interaction research" might tokenize less cleanly ("accountancy" might split into "account" + "ancy," and "human-computer interaction" is more fragmented than "UX design"). The response quality will likely still be good, but the tokenization overhead means the model is working slightly harder.

> **"Try This Now" Exercise**
>
> Test the fixed-vocabulary effect yourself. Ask an AI these two questions and compare the fluency and accuracy of the responses:
>
> 1. "Explain the main principles of marketing strategy." (Common vocabulary)
> 2. "Explain the main principles of psychoneuroimmunology." (Rare vocabulary)
>
> Both are legitimate fields with substantial bodies of knowledge. But the first uses tokens that appear constantly in the training data, while the second uses a highly specialized term that likely gets fragmented. Notice any differences in confidence, detail, or accuracy.

## When the Menu Doesn't Have What You Need

So what happens when you try to order something that's not on the menu? The tokenizer's byte-level fallback ensures that literally *anything* can be represented — every Unicode character, every emoji, every symbol from every language on Earth. Nothing is completely unrepresentable.

But there's a difference between "representable" and "efficiently representable." A Chinese character that gets encoded as three byte-level tokens is representable — the model can work with it — but it's using three times the processing capacity of a common English word that gets a single token.

This is where the analogy of the fixed menu really shines. Imagine a restaurant where everything on the menu costs one unit of the chef's attention. If you order off-menu, the chef will accommodate you, but it might take three or four units of attention to figure out what you want and how to prepare it. The chef still produces a dish, but at the cost of reduced attention for the rest of your order.

In the same way, inefficiently tokenized text still gets processed, but it costs more tokens (reducing how much can fit in the context window), more processing effort (potentially affecting quality), and more literal cost (since API pricing is per-token).

## The Vocabulary as a Cultural Artifact

Step back and consider what the vocabulary really represents. It's a snapshot of what was linguistically common and important in the dataset used to build the tokenizer. It's a cultural artifact — an encoding of whose language, whose words, whose concerns were most represented in the training data.

Common English words? Single tokens. They're first-class citizens in the vocabulary. Hindi words? Split into fragments. They're second-class citizens — not by design or intent, but by the mathematics of frequency-based compression.

This isn't an abstract philosophical point. It has practical implications for equity, access, and who benefits most from AI technology. A tool that works better for some languages and cultural contexts than others — not because of any deliberate choice but because of the training data distribution — is a tool whose benefits are unequally distributed.

Awareness of this is the first step. Using strategies to mitigate it (as we discussed in Lesson 3) is the second. Advocating for more equitable tokenizer design is the third.

> **"Pro Tip" Box**
>
> When working with specialized terminology, consider providing a "vocabulary bridge" in your prompt. For example: "I'm going to ask about psychoneuroimmunology — the study of how psychological processes affect the nervous and immune systems." This gives the model clean, common tokens ("study," "psychological," "nervous," "immune") alongside the specialized term, helping it access the right patterns even if the specialized term itself is poorly tokenized. You're essentially translating from the rare vocabulary into the common vocabulary, making the chef's job easier.

## The Big Picture: Tokens Are the Atoms of AI

After four lessons on tokenization, let's put it all together. Tokens are the atoms of the AI's universe. Everything the system does — every calculation, every pattern match, every prediction — operates at the token level. The vocabulary of available tokens is fixed, finite, and optimized for common patterns in the training data.

This means:
- Common text is processed efficiently and reliably
- Unusual text is processed less efficiently and sometimes less reliably
- Different languages and scripts face different tokenization costs
- Character-level tasks work against the grain of token-level processing
- The vocabulary is a cultural artifact that reflects the biases of the training data

Understanding tokens is the foundation for understanding everything else in this book. In the next lesson, we'll see how token limits create hard constraints on every AI conversation you'll ever have.
