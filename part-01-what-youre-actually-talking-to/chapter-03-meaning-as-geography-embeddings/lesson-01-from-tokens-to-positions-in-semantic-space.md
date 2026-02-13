# Lesson 1: From Tokens to Positions in Semantic Space

## The Second Translation

In the last chapter, you watched the first translation: your text getting chopped into tokens. But tokens are just the raw material — numbered IDs in a vocabulary list. A token for "career" is, at this stage, just the number 7,458 (or whatever its ID happens to be). A token for "accounting" is just the number 12,203. These numbers don't carry any meaning. They're labels on bins in a warehouse, not ingredients a chef can cook with.

Before the AI can do anything intelligent with your message, it needs a second translation — one that transforms meaningless token IDs into rich representations of meaning. This is where the concept of **embeddings** enters the picture, and it is one of the most beautiful ideas in all of artificial intelligence.

## The Map Analogy

Think about a map of a city. The map isn't the city — it's a representation. But it captures something essential: *spatial relationships.* Things that are close together in the city are close together on the map. Things that are far apart in the city are far apart on the map. And the relationships are consistent — if the hospital is between the school and the park in real life, it's between them on the map too.

Embeddings work on the same principle, except the "city" being mapped is the entire landscape of human meaning, and the "map" exists in a space with hundreds or thousands of dimensions instead of just two.

When the AI processes the token "career," it doesn't just see a number. It converts that number into a position — a set of coordinates — in a vast mathematical space. The token "job" gets mapped to a nearby position, because "career" and "job" have similar meanings. The token "banana" gets mapped to a distant position, because a banana has little to do with careers.

This mathematical space is called the **embedding space**, or **semantic space** (semantic meaning "related to meaning"), and it is where the magic of language understanding begins.

## What Does a Position Look Like?

In everyday life, a position needs coordinates. Your house might be at latitude 40.7128, longitude -74.0060. That's two numbers — two dimensions — and it tells you exactly where the house is on a flat map of the Earth.

An embedding is similar, but instead of two dimensions, it uses hundreds. A typical embedding might have 768 dimensions, or 1,536, or even 4,096. Each dimension captures some aspect of a token's meaning — though what each dimension represents isn't always easy for humans to interpret.

So the embedding for "career" might look something like:

[0.23, -0.87, 0.45, 0.12, -0.33, 0.76, ... ]

That's a list of hundreds of numbers. Together, these numbers define a unique position in the embedding space — the "address" of the concept "career" in the landscape of meaning.

Now, I know what you might be thinking: "Hundreds of dimensions? I can barely visualize three." You're not alone. Nobody can visualize hundreds of dimensions. But here's the good news: you don't need to visualize them to understand what they do. The important thing is the *relationships* between positions, not the positions themselves.

> **"Behind The Curtain" Sidebar**
>
> Why so many dimensions? Because meaning is extraordinarily complex. Think about the word "bank." It can mean a financial institution, the edge of a river, a pool shot, or a verb meaning to rely on something. A two-dimensional space couldn't capture all these meanings and their relationships to other words. But in a 768-dimensional space, there's enough room for "bank" (financial) to be close to "loan" and "savings," while "bank" (river) is close to "shore" and "water," and for the model to keep these senses separate when context demands it. More dimensions mean more room for nuance.

## The Neighborhood Principle

The most important property of embedding space is this: **words with similar meanings end up near each other.** This isn't programmed in by hand — it emerges from the training process. During training, the model learns that "career" and "profession" tend to appear in similar contexts, surrounded by similar words. Over billions of training examples, the model adjusts their embeddings until they're close together in the space.

The result is a semantic neighborhood structure that mirrors human intuition:

- "Career," "profession," "vocation," "occupation" — all in the same neighborhood
- "Happy," "joyful," "pleased," "delighted" — clustered together
- "Dog," "puppy," "canine," "hound" — close neighbors
- "Run," "jog," "sprint," "dash" — in the same region

But it goes beyond simple synonyms. Words that are related but not synonymous also have meaningful spatial relationships:

- "Doctor" is near "hospital," "patient," "medicine," "diagnosis"
- "Teacher" is near "school," "student," "lesson," "education"
- "Accountant" is near "tax," "audit," "financial," "spreadsheet"

These neighborhoods form organically from the statistics of language. Nobody told the model that doctors work in hospitals — it figured that out from the fact that "doctor" and "hospital" appear near each other in text far more often than, say, "doctor" and "surfboard."

> **"This Is Why..." Box**
>
> **This is why AI can understand paraphrases and synonyms without being explicitly told they mean the same thing.** When you say "I want to switch careers" and "I'd like to change professions," the AI doesn't need a synonym dictionary. In embedding space, "switch" and "change" are nearby, "careers" and "professions" are nearby, and "want to" and "would like to" are nearby. The two sentences map to similar regions of semantic space, so the AI treats them as conveying similar meanings. This is not lookup — it's geometry.

## Watching the Transformation: Our Running Example

Let's trace what happens to our running example, "Help me plan a career change from accounting to UX design," at the embedding stage.

After tokenization, the model has a sequence of token IDs. Now, each token ID gets mapped to its embedding — its position in semantic space.

The token "career" lands in the neighborhood of professional-life concepts. "Change" lands in a region associated with transition and transformation. "Accounting" lands in the financial-domain neighborhood. "UX" and "design" land in the creative-technology neighborhood.

But here's the crucial detail: at this early stage, each token's embedding is based only on what the token *generally* means — its default position in the space. "Change" gets the same initial embedding whether it appears in "career change" or "climate change" or "spare change." The embedding captures the word's general meaning, not its meaning in *this specific context.*

That context-dependent adjustment happens later, in the attention layers (which we'll explore in depth in a later chapter). For now, the embedding stage sets the starting positions — reasonable initial guesses about what each token means, which the rest of the model will then refine based on context.

Think of it like placing pins on a map before a road trip. You put a pin at "accounting" and a pin at "UX design" and a pin at "career change." Those pins aren't the trip itself — they're starting positions that help you plan the route. The journey (which the model's deeper layers will compute) connects them in meaningful ways.

## Why Embeddings Are Learned, Not Designed

A critical point: nobody hand-designed the embedding space. No engineer sat down and said "career should be at position [0.23, -0.87, 0.45, ...]." The embeddings are learned during training, adjusted incrementally over billions of examples until they capture the statistical relationships between tokens as accurately as possible.

This is important because it means the embedding space reflects the *actual patterns of language use* rather than any human designer's preconceptions. The model doesn't know what "career" means in the way you do — it knows where "career" fits in the statistical landscape of language. And that statistical fit turns out to capture remarkable amounts of meaning.

It's like a city that grew organically over centuries rather than being planned from scratch. Nobody designed Paris to have certain neighborhoods — they evolved based on the patterns of human activity. Similarly, the neighborhoods in embedding space evolved from the patterns in human language. And like a real city, the resulting structure is both surprisingly coherent and occasionally quirky.

> **"Try This Now" Exercise**
>
> Ask an AI: "What words are most closely related to 'accountant'?" Then ask: "What words are most closely related to 'UX designer'?" Look at the two lists. Now ask: "What words appear in both neighborhoods — related to both 'accountant' and 'UX designer'?" The overlap (things like "analytical," "detail-oriented," "user-focused research") represents the bridge in embedding space between these two careers — the area where the two neighborhoods overlap. This is roughly what the AI "sees" when you ask about transitioning from one to the other.

## The Embedding as a First Impression

Think of embeddings as the AI's first impression of your text. Before any sophisticated reasoning happens, before any context is considered, before the model starts generating a response — your tokens get placed in semantic space. These initial placements are like first impressions of each word: "career" = professional-life territory, "accounting" = finance territory, "UX" = design-technology territory.

These first impressions get refined and enriched as your text moves through the model's deeper layers. But they set the stage. If the embeddings place tokens in roughly the right semantic neighborhoods, the deeper layers have a strong foundation to work with. If the embeddings are off — say, for a rare or ambiguous word — the deeper layers have to work harder to compensate.

This is one more reason why common, well-represented vocabulary works better than rare, fragmented terminology. Common words have well-trained embeddings — the model has seen them in millions of contexts and has refined their positions in semantic space. Rare words have less well-trained embeddings — the model has seen them in fewer contexts and their positions may be less accurate.

> **"Pro Tip" Box**
>
> When you use an AI for brainstorming or exploring connections between ideas, you're essentially asking it to navigate embedding space. The AI can find surprising connections because, in its semantic space, concepts that seem unrelated to humans may have neighborhoods that overlap. Try asking: "What unexpected skills from accounting would transfer well to UX design?" The AI traverses the embedding space between these two concept neighborhoods and finds bridges — overlapping regions that represent transferable skills. This is one of the AI's genuine strengths: finding connections in the vast landscape of meaning that humans might miss because we think in categories, not in continuous spatial relationships.
