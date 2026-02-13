# Lesson 2: Vector Arithmetic and Word Relationships

## The Equation That Changed Everything

In 2013, a research team at Google published a result that stunned the AI world. They took their word embeddings — positions in semantic space — and discovered you could do *arithmetic* with them. Not arithmetic with numbers, but arithmetic with meaning.

Here's the famous example:

**King - Man + Woman = Queen**

Take the embedding (the position in semantic space) for "king." Subtract the embedding for "man." Add the embedding for "woman." The result is a position in semantic space that is closer to "queen" than to any other word.

Read that again. You can literally *compute* with meaning. You can subtract "maleness" from "king," add "femaleness," and arrive at "queen." The AI discovered, purely from statistical patterns in language, that the relationship between king and queen is the same as the relationship between man and woman.

Nobody programmed this. Nobody told the model about gender relationships in royal titles. The model learned it from the patterns of how these words are used in context.

## What "Arithmetic with Meaning" Actually Means

Let's unpack this, because it's not as magical as it first sounds — and understanding why it works is more useful than being dazzled by it.

Think of embedding space as a city again. "King" is in the royalty neighborhood. "Man" is in the male-humans area. "Woman" is in the female-humans area. "Queen" is in the royalty neighborhood too, but shifted toward the female side.

"King - Man" is like getting directions. It says: "Starting from king, move away from man." Since the main difference between king and a generic man is the royalty dimension, "King - Man" gives you a direction vector that roughly means "royalty, but with the generic-male component removed."

"King - Man + Woman" says: "Take that royalty direction and apply it to woman." The result is a point in semantic space where royalty and female-ness intersect. That point is closest to "queen."

It's like city navigation: if you know how to get from "generic man" to "king" (go toward the royalty district), you can apply that same set of directions starting from "generic woman" and end up at "queen."

This works because the embedding space has learned consistent *directions* for different kinds of relationships. The direction from "man" to "king" is roughly the same as the direction from "woman" to "queen" — both represent the concept of "adding royalty."

> **"Behind The Curtain" Sidebar**
>
> The king-queen example is the one everyone cites, but the same arithmetic works for many relationships:
> - **Paris - France + Japan = Tokyo** (capital-of relationship)
> - **Walking - Walk + Swim = Swimming** (verb tense relationship)
> - **Bigger - Big + Small = Smaller** (comparative form)
> - **Apple - Fruit + Company = Microsoft** (or similar tech company)
>
> Each of these works because the embedding space has encoded the *direction* of each relationship consistently. The distance between "France" and "Paris" is similar to the distance between "Japan" and "Tokyo" and points in the same "capital-of" direction. These aren't hand-coded rules — they're patterns that emerged from training on billions of words of human text.

## Beyond Word Pairs: The Direction of Meaning

The vector arithmetic reveals something profound about embedding space: it has consistent *directions* for different types of meaning.

Imagine a compass, but instead of north, south, east, and west, the directions represent semantic concepts. One direction might represent "increasing formality" — moving in that direction takes you from "house" toward "residence" toward "domicile." Another direction might represent "increasing size" — from "small" to "big" to "enormous." Another might represent "increasing technicality" — from "heart problem" to "cardiac condition" to "myocardial infarction."

These directions exist in the embedding space not because anyone put them there, but because human language *uses* these concepts consistently. When we talk about formal things, we use certain words. When we talk about informal things, we use other words. The embedding space captures this by giving "formality" a consistent direction.

This matters enormously for how the AI handles your prompts. When you write formally, your tokens are positioned in the "formal" regions of embedding space, and the model generates tokens from those same regions — producing a formal response. When you write casually, your tokens are in casual territory, and the response follows suit.

> **"This Is Why..." Box**
>
> **This is why the tone of your prompt strongly influences the tone of the AI's response.** If you write "Yo, what's the deal with switching from accounting to UX?", the tokens in your prompt sit in the casual, informal region of embedding space. The model generates the next tokens from that same region, producing a casual response. If you write "I would appreciate a comprehensive analysis of the professional transition from certified public accounting to user experience design," the tokens sit in the formal, professional region, and the response matches. You're not just communicating *what* you want — you're positioning the generation in a specific *tone neighborhood* of semantic space.

## The Career Change in Vector Space

Let's apply this to our running example. In embedding space, "accounting" and "UX design" are in different neighborhoods — accounting is in the finance/numbers/compliance region, while UX design is in the creativity/technology/human-centered region.

But those neighborhoods aren't completely separate. They overlap in certain dimensions. Both accountants and UX designers need analytical thinking — and in embedding space, both "accounting" and "UX design" are positioned near the "analytical" direction. Both involve attention to detail. Both require understanding user/client needs.

When you ask the AI to help with a career transition from accounting to UX design, the model is, in a sense, navigating the embedding space between these two neighborhoods. It's looking for the paths that connect them — the dimensions where they're aligned (analytical skills, attention to detail, understanding requirements) and the dimensions where they differ (creative expression, visual design, technical prototyping).

This is why AI is often surprisingly good at identifying transferable skills and unexpected connections. The embedding space is a continuous landscape, not a set of rigid categories. There's always a path between any two points, and the paths reveal genuine relationships between concepts.

## The Analogy of Related Neighborhoods

Think of two neighborhoods in a large city — say, the financial district and the arts district. They seem like completely different worlds: suits versus paint-splattered jeans, spreadsheets versus sketchbooks, quarterly reports versus gallery openings.

But look closer, and you find bridges. There's a restaurant that serves both corporate lunches and artsy Sunday brunches. There's a design firm that does financial data visualization. There's an accountant who does the books for gallery owners. The neighborhoods are distinct, but they're connected by specific paths.

Embedding space works the same way. "Accounting" and "UX design" are in different neighborhoods, but the space between them contains real connections — skills, concepts, and roles that bridge the gap. The AI can find these connections because in embedding space, they exist as actual positions along paths between the two neighborhoods.

This is fundamentally different from a keyword search, which can only find exact matches. If you Google "accounting and UX design," you need someone to have written about that exact combination. But in embedding space, the AI can navigate between the two concepts and discover connections that may never have been explicitly written about — because the connections exist in the structure of the space itself, not in any specific document.

> **"Try This Now" Exercise**
>
> Test the AI's ability to navigate embedding space. Try these prompts:
>
> 1. "What does accounting have in common with music composition?" (Two seemingly unrelated fields)
> 2. "How is cooking similar to software engineering?" (Different domains, surprising parallels)
> 3. "What connects architecture and psychology?" (Unexpected bridges)
>
> Notice how the AI finds genuine, thoughtful connections. It's not making these up from nothing — it's navigating the embedding space between two concept neighborhoods and finding the dimensions where they're actually close together. Some of these connections might surprise you and be genuinely useful for thinking about your own career or projects.

## Limitations of Vector Arithmetic

The king-queen example is elegant, but embedding arithmetic isn't perfect. It's important to understand the limitations.

**Ambiguity causes noise.** Remember, "bank" (financial) and "bank" (river) might share an embedding, or they might get slightly different embeddings depending on how the model handles polysemy (words with multiple meanings). When you do arithmetic with ambiguous embeddings, the results can be muddled.

**Cultural biases get baked in.** If the training data associates "doctor" more often with male contexts and "nurse" more often with female contexts, the embedding space will reflect those biases. "Doctor - Man + Woman" might land closer to "nurse" than to "doctor" — not because this is correct, but because the training data reflected a biased world. We'll touch on this more in the next lesson.

**Abstract concepts are slippery.** The arithmetic works best for concrete relationships with clear parallels. "King - Man + Woman = Queen" works because the gender-royalty relationship is consistent and well-represented. "Justice - Law + Art = ?" is less likely to give a clean, meaningful answer because the relationship is more abstract and less consistently represented in the training data.

**Distance isn't always meaningful.** Just because two words are close in embedding space doesn't mean they're similar in every way. "Hot" and "cold" might be close in embedding space because they appear in similar contexts (temperature discussions, weather reports). But their meanings are opposite. The space captures *association*, which often correlates with similarity — but not always.

## What This Means for You as a User

Understanding vector arithmetic and directional meaning in embedding space gives you a concrete model for why certain prompting strategies work:

**Using analogies in prompts works because analogies traverse consistent directions in embedding space.** When you say "Create a career change plan that's like a battle strategy," you're asking the model to apply the strategic-planning direction to your career context. The model navigates toward the intersection of "career change" and "strategic planning" in embedding space.

**Specifying a reference point works because it anchors the generation in a specific neighborhood.** Saying "Explain UX design the way you'd explain it to an accountant" places the generation at the intersection of the UX neighborhood and the accounting neighborhood — a much more specific and useful location than just "UX design."

**Contrasts and comparisons work because they leverage the directional structure.** Asking "How is UX design *different* from graphic design?" explicitly asks the model to find the direction between two nearby points in embedding space, highlighting the dimensions where they diverge.

The embedding space isn't just a technical detail. It's the geography of the AI's understanding, and learning to navigate it — through how you frame your prompts — makes you a more effective collaborator with the system.

> **"Pro Tip" Box**
>
> When brainstorming or exploring new ideas with AI, use "bridge prompts" that ask the model to navigate between distant points in embedding space. Prompts like "What does X have in common with Y?" or "How could principles from X be applied to Y?" leverage the continuous nature of embedding space to find connections that category-based thinking might miss. This is one of the AI's genuine superpowers — finding meaningful paths through the landscape of meaning that human category-based thinking often overlooks.
