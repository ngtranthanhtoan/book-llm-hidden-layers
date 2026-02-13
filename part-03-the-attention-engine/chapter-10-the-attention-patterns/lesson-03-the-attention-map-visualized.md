# Lesson 10.3: The Attention Map Visualized --- Seeing What the AI Sees

## Making the Invisible Visible

Throughout this book, we have been developing X-ray vision --- the ability to see inside AI conversations and understand the hidden mechanics behind every response. In this lesson, we take that metaphor literally. We are going to look at the visual representations that researchers use to examine what the AI is actually paying attention to.

These visualizations are called **attention maps**, and they are as close as we can get to watching the AI "think." They are the X-rays of the attention engine.

You do not need to be a researcher to understand them. They are surprisingly intuitive once you know what you are looking at. And once you can read them, you will never think about your prompts the same way again.

## What an Attention Map Looks Like

An attention map is a grid. Think of it as a spreadsheet or a chessboard. Both the rows and the columns represent the words (tokens) in a piece of text. Each cell in the grid contains a value between zero and one, representing how much attention one word is paying to another.

- The rows represent the words that are *doing* the attending (the word asking: "Who is relevant to me?").
- The columns represent the words *being* attended to (the words answering: "Here is what I offer").
- A dark or brightly colored cell means strong attention. A light or faded cell means weak attention.

For a ten-word sentence, you get a ten-by-ten grid with one hundred cells. Each cell answers the question: "How much does word X care about word Y?"

Let us build a simplified attention map for our running example: "Help me plan a career change from accounting to UX design."

Imagine a grid where the rows and columns are both labeled with these words. The cells are colored from white (no attention) to dark blue (maximum attention). Here is what a simplified version of one attention head might look like:

**A syntactic attention head** would show dark cells connecting:
- "Help" to "me" and "plan" (verb-object-complement structure)
- "career" to "change" (compound noun)
- "from" to "accounting" (prepositional phrase)
- "to" to "UX" and "design" (prepositional phrase)

The pattern would look like a series of dark spots near the diagonal (adjacent words) with some longer-range connections (verbs to their objects).

**A semantic attention head** would show a different pattern:
- "Accounting" strongly attending to "UX design" (the two fields being compared)
- "Career" strongly attending to "change," "accounting," and "UX design" (the core concepts)
- "Plan" strongly attending to "career change" (what needs planning)

This pattern would show dark spots scattered more broadly across the grid, connecting thematically related words regardless of their position.

**A positional attention head** would show yet another pattern:
- Strong attention along the diagonal (each word attending to its immediate neighbors)
- Moderate attention to the first and last few words
- Fading attention for distant words

This pattern would look like a dark diagonal stripe across the grid, fading as it moves away from the center.

> **Behind The Curtain**
>
> Researchers actually create these attention maps and publish them in papers. One of the most famous tools for this is called BertViz (originally designed for the BERT model, a Transformer variant). When researchers examine attention maps for large models, they often find strikingly clean patterns --- certain heads produce attention maps that look almost like hand-drawn diagrams of sentence structure. The model has learned, without any explicit instruction, to parse grammar, resolve references, and track thematic connections in ways that are visible in these maps.

## Reading the Patterns

Once you know what to look for, attention maps reveal distinctive visual signatures for different types of processing.

### The Diagonal Pattern

A strong diagonal --- where each word primarily attends to itself and its immediate neighbors --- indicates **local processing.** The head is focused on adjacent word relationships: compound nouns ("career change"), prepositional phrases ("from accounting"), and local grammatical structures.

Think of this as the AI reading each neighborhood of your sentence closely, understanding the local word clusters before worrying about long-range connections.

### The Vertical Stripe Pattern

A vertical stripe --- where many words strongly attend to one particular word --- indicates that the word is an **anchor.** It is a key concept that many other words need to reference to establish their own meaning.

In our career change prompt, you might see a vertical stripe on "change" --- many other words attend to it because "change" is the central concept that defines the meaning of everything else in the sentence. "Career" is about this change. "Accounting" is the origin of this change. "UX design" is the destination of this change. "Plan" is what you want to do about this change.

When you see a vertical stripe in an attention map, you are looking at the most important word in the sentence, as determined by the model.

### The Block Pattern

A block pattern --- where a group of words all strongly attend to each other --- indicates a **conceptual cluster.** The model has identified a set of words that form a meaningful unit.

For example, "career change from accounting to UX design" might show up as a block of mutual attention. These seven words form a coherent concept, and the attention heads recognize them as a unit even though they span multiple grammatical structures.

### The Long-Range Connection Pattern

Scattered dark spots far from the diagonal indicate **long-range semantic connections.** The model is connecting words that are distant in the sentence but related in meaning.

In a longer prompt --- "I studied finance in college, worked at a Big Four firm for a decade, and now I want to learn about designing user interfaces for mobile applications" --- you might see long-range connections between "finance" (near the beginning) and "user interfaces" (near the end), reflecting the model's recognition of the career transition theme.

### The Diffuse Pattern

A nearly uniform, low-intensity pattern --- where attention is spread thinly across all words --- indicates a head that is **gathering global context.** Rather than forming specific connections, it is computing an overall sense of the message: its tone, its length, its complexity, its general topic.

Think of this as the head that steps back and asks, "What is the overall vibe here?" rather than analyzing specific word relationships.

## Multiple Heads, Multiple Maps

Remember from the previous chapter that a Transformer has dozens of attention heads operating simultaneously. Each head produces its own attention map. When researchers visualize the full set of attention maps for a single layer, it looks like a gallery of grid images, each one showing a different pattern.

Some maps show clean diagonal patterns (local processing). Others show vertical stripes (anchor words). Others show scattered long-range connections (semantic links). Others show block patterns (conceptual clusters). The diversity of these patterns is striking --- and it corresponds to the diversity of perspectives we discussed in Lesson 9.3.

When all these maps are combined, the result is a single, richly textured representation of the text. No single map captures everything, but together they form a comprehensive web of relationships.

> **This Is Why...**
>
> ...the AI sometimes focuses on an aspect of your message you did not consider important. A word that seems minor to you might be an anchor word in one of the attention maps --- a word that many other words attend to strongly. For example, in the prompt "Just give me a quick career plan for switching from accounting to UX," the word "quick" might anchor an entire attention head, causing many other words to attend to it and the model to prioritize brevity. If you did not mean "quick" as a strong constraint (maybe you just typed it casually), the response might be frustratingly brief. The AI weighted "quick" more than you intended because it became an anchor in the attention map.

## Attention Maps Across Layers

So far, we have been discussing attention maps for a single layer. But a Transformer has many layers (we will explore this in detail in Chapter 11), and the attention maps change from layer to layer.

Early-layer attention maps tend to show simple, local patterns: diagonal stripes, adjacent-word connections, basic grammatical structures. The model is doing surface-level parsing.

Middle-layer attention maps become more complex. Long-range connections appear. Semantic clusters form. The model is building meaning.

Deep-layer attention maps are often the most interesting. They show highly abstract patterns that do not correspond to any obvious linguistic relationship. The model has moved beyond word-level analysis into something more like conceptual reasoning. The attention patterns at this depth are connecting abstract ideas, not just words.

Think of it like zooming out on a satellite photo. At ground level (early layers), you see individual buildings and streets. At city level (middle layers), you see neighborhoods and transportation networks. At country level (deep layers), you see geographic patterns, trade routes, and population centers. The same territory, but the patterns visible at each zoom level are fundamentally different.

## A Practical Visualization Exercise

You cannot easily create your own attention maps (that requires specialized research tools and access to model internals), but you can *infer* the attention web by observing the AI's behavior. Here is how.

Write a prompt with multiple distinct elements and see which elements the AI prioritizes in its response. The elements it emphasizes most strongly are likely the anchor words in its attention maps.

For example, try this prompt:

"I am an experienced accountant (CPA, twelve years at Deloitte), I recently completed a Google UX Design Certificate, my neighbor is a UX designer at a tech startup and says the field is booming, and I want to create a career transition plan that is financially safe and professionally strategic."

Now examine the AI's response. Does it focus most on:
- Your credentials (CPA, Deloitte)? The professional-experience words were attention anchors.
- Your certification (Google UX Design Certificate)? The recent-credential words were anchors.
- Your neighbor's anecdote? The social-proof words were anchors.
- Financial safety? The constraint words were anchors.
- Strategic planning? The task-framing words were anchors.

Whatever the response emphasizes is a window into which words formed the strongest attention connections. You are inferring the attention map from the output.

> **Try This Now**
>
> Run the experiment described above. Write a prompt with five or six distinct elements --- task, context, credentials, constraints, examples, and emotional tone. Then read the response carefully and rank which elements received the most attention.
>
> Now rewrite the prompt, promoting one underweighted element to the beginning and emphasizing it with stronger language. Watch how the response shifts. You are manually adjusting the attention map by changing which words are positioned and phrased to become anchors.
>
> For instance, if the first response underweighted financial safety, rewrite the prompt to begin: "My absolute top priority is financial safety. I cannot afford any income gap. With that critical constraint in mind, help me plan a career change from accounting (CPA, twelve years) to UX design (Google UX certificate)."

## The Limits of Attention Maps

Attention maps are powerful diagnostic tools, but they have limitations worth acknowledging.

First, they show *correlation*, not *causation.* A strong attention connection between two words tells you the model considered them related, but it does not tell you exactly how that relationship influenced the final output. Two words might have a strong attention connection in one head but a weak one in another, and the combined effect depends on the integration step.

Second, attention maps show only one layer and one head at a time. The full picture requires examining dozens of heads across dozens of layers --- thousands of maps. Researchers have tools for this, but even for them, it is challenging to synthesize the full picture.

Third, and most importantly for us, attention maps are a view of the *mechanism*, not the *experience.* The AI does not "see" its own attention maps any more than your neurons "see" their own firing patterns. The attention map is a researcher's tool for understanding the model, not the model's own experience of processing text.

Despite these limitations, attention maps remain one of the best windows we have into how the AI processes your words. They transform the abstract concept of "attention" into something visible and interpretable. And for our purposes --- understanding what the AI is doing with your words and how to write better prompts --- they provide invaluable insight.

> **Pro Tip**
>
> You do not need to literally see attention maps to benefit from understanding them. The key practical insight is this: your words are not all weighted equally. Some words become anchors that disproportionately shape the response. These tend to be (1) words with strong semantic content (nouns, verbs, adjectives), (2) words in prominent positions (beginning and end of the prompt), (3) words that are repeated or emphasized, and (4) words that relate to many other words in the prompt (central concepts).
>
> If your AI responses are not hitting the right notes, ask yourself: "Which words in my prompt are likely to be the anchors? Are they the right words?" If "quick" is accidentally anchoring the attention but your real priority is "thorough," adjust accordingly.

## What Comes Next

Now that you can visualize --- at least conceptually --- how the AI distributes its attention across your words, we are ready to explore a question that might seem simple but turns out to be surprisingly nuanced: does word order matter?

You might expect the answer to be "obviously yes." But remember, the AI reads non-linearly. It sees everything at once. So does it matter whether you put your constraints at the beginning or the end? Whether you state your goal first or your context first? Whether you list items in a particular order?

The answer, as you might suspect, is "it is complicated" --- and understanding the nuances will give you a genuine edge in crafting effective prompts.
