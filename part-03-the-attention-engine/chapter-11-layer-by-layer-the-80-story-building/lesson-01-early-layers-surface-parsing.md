# Lesson 11.1: Early Layers (1-20) --- Surface Parsing

## Welcome to the Building

In the previous two chapters, we examined the attention mechanism from the inside: how it works, what types of heads exist, and how the AI reads your words as a web of relationships. Now we are going to zoom out and watch the entire process unfold from beginning to end.

Think of a modern large language model as an eighty-story building. Your words enter at the ground floor. They travel upward, floor by floor, and with each floor they pass through, they become something more. Raw text becomes tokens. Tokens become patterns. Patterns become meaning. Meaning becomes understanding. Understanding becomes a response.

Each floor contains the same basic machinery: an attention mechanism and a feed-forward processing step. But what happens at each floor is dramatically different, because each floor builds on the enriched representations from the floor below.

In this lesson, we explore floors one through twenty: the early layers. This is where your words first come alive inside the machine.

## What Arrives at the Ground Floor

Before we can understand what the early layers do, we need to know what they receive.

When you type "Help me plan a career change from accounting to UX design," the model does not receive English words. It receives tokens --- pieces of text (as we covered in Part 1) --- each represented as a long list of numbers called an embedding. Each embedding captures the general, context-free meaning of a token, plus its position in the sentence.

At this point, "career" is just a generic concept: professional work, vocation, employment. It does not yet know that in this sentence, it is part of a "career change" or that it relates to accounting and UX design. Similarly, "change" is still generic: it could mean coins, transformation, or a verb meaning to alter. The early layers' job is to begin resolving these ambiguities and connecting these isolated points of meaning into something coherent.

Think of the ground floor as a reception desk where eleven visitors (your eleven tokens) arrive independently. Each visitor has a name tag with some basic information, but they have not yet met each other. They do not yet know why they are all in the same building.

## Floors 1-5: Basic Recognition and Grouping

The very first layers perform the most fundamental parsing tasks. They are the initial handshake between words.

**Token grouping.** The model begins to recognize which tokens belong together. "UX" and "design" start to merge into a conceptual unit. "Career" and "change" start to bond. These are not yet deep semantic connections --- the model is simply recognizing frequently co-occurring pairs, much like recognizing that "New" and "York" belong together without yet knowing anything about the city.

**Part-of-speech-like recognition.** The model begins to distinguish between different types of words. "Help" and "plan" register as action words. "Accounting" and "UX design" register as entities or topics. "From" and "to" register as structural connectors. "Me" registers as a reference to the speaker.

This is not conscious grammatical analysis. It is more like the first impression you form when you glance at a sentence: you can tell the nouns from the verbs and the structure words from the content words, almost before you consciously process the meaning.

**Local context building.** Each word starts absorbing information from its immediate neighbors. "Career" starts to incorporate the influence of "change" (which comes right after it) and "a" (which comes right before it). These local connections are handled primarily by the positional and syntactic attention heads we discussed in Chapter 10.

> **Behind The Curtain**
>
> Researchers have a remarkable technique for examining what each layer "knows." They can extract the hidden representations at each layer and probe them with simple tests: can you determine the part of speech from this representation? Can you identify the subject and object? Can you determine the sentiment? They have found that part-of-speech information is strongly present by layer two or three in most large models. The model figures out nouns, verbs, and adjectives almost immediately. Syntactic structure takes a few more layers but is largely in place by layer ten. This mirrors how quickly humans parse the basic structure of a sentence --- nearly instantaneously.

## Floors 5-10: Grammatical Architecture

Once the basic recognition is done, the next set of layers assembles the grammatical scaffolding of your sentence.

**Subject-verb-object relationships.** The model identifies who is doing what to whom. In our prompt, "you" (implied by the imperative) are asking someone to "Help" "me," and the thing being planned is a "career change."

**Clause structure.** The model recognizes that "from accounting to UX design" is a modifier of "career change," not a separate instruction. It recognizes that "Help me plan" is the main clause and everything after it provides details.

**Prepositional attachment.** The model resolves which prepositional phrases attach to which nouns or verbs. "From accounting" attaches to "change" (changing from accounting), not to "plan" (planning from accounting). "To UX design" similarly attaches to "change."

This stage is like an architect looking at a building blueprint and identifying the load-bearing walls, the floors, and the roof. The architect is not yet thinking about interior design or how people will live in the building --- she is just establishing the structure that will support everything else.

For our running example, by around layer 10, the model has built something like this structural skeleton:

- **Request type:** imperative (do something for me)
- **Action requested:** plan
- **Object of action:** career change
- **Direction of change:** from accounting, to UX design
- **Beneficiary:** me (the user)

The meaning is not yet deep --- the model does not yet "understand" what a career change entails, what accounting and UX design are like as professions, or what kind of plan would be useful. But the structural understanding is in place.

## Floors 10-15: Disambiguation

As the representations continue to be refined, the model resolves ambiguities that the early layers flagged but could not resolve.

**Word sense disambiguation.** "Change" is definitively interpreted as "transition" rather than "coins" or "to alter." This resolution happens through the cumulative attention connections: "career" (professional context) and "from...to" (transition structure) overwhelmingly favor the "transition" interpretation.

**Reference resolution begins.** If there are pronouns or other reference words, the coreference heads start forming connections. In our simple prompt there are no pronouns, but in a longer version --- "My boss suggested I consider this. She thinks it would suit my skills" --- layers 10-15 would begin linking "She" to "My boss" and "it" to "this" (meaning the career change).

**Negation and modifier scope.** The model determines the scope of any negation or modification. "I do not want to stay in accounting" --- the "not" applies to "want to stay," not to "accounting." This seems obvious to a human, but computationally, getting negation scope right requires several layers of refinement.

> **This Is Why...**
>
> ...the AI occasionally misinterprets double negatives or complex modifier chains. Sentences like "I am not unhappy with accounting, but I do not think I would not prefer UX design" have multiple layers of negation that must be resolved across several processing layers. Each negation reverses the polarity of what follows, and if one layer gets a negation wrong, the error compounds through subsequent layers. When the AI mishandles these constructions, it is often because the disambiguation layers produced a slightly incorrect parse that then corrupted the downstream processing.

## Floors 15-20: Surface Meaning Assembly

The final stretch of the early layers is where isolated structural understanding begins to gel into basic meaning.

**Phrase-level meaning.** "Career change" is no longer just two structurally linked tokens. It is starting to activate the concept of a professional transition --- a significant life event with emotional, financial, and practical dimensions. The model is beginning to access its stored knowledge about what career changes involve.

**Sentence-level meaning.** The overall gist of the sentence starts to emerge: someone is asking for help planning a transition from one specific profession to another. This is still a surface-level reading --- the model knows *what* is being said but has not yet deeply processed the implications, constraints, or appropriate response strategies.

**Task classification.** The model begins to identify what *kind* of request this is. Is it a question? A creative writing prompt? A coding task? A request for advice? By layer 20, the task-framing heads have usually settled on a classification. Our prompt registers as a "planning/advice request" --- the model knows it needs to produce a structured, helpful plan, not a story or a factual answer.

Think of this stage as the moment when you glance at a letter and grasp its general purpose. You can see it is a job application (not an invoice, not a love letter, not a complaint). You know the general topic and the general intent. But you have not yet carefully considered the specific qualifications, the nuances of the candidate's situation, or how to respond. That deeper processing happens in the middle layers.

## The Restaurant at Floor Twenty

Let us check in with our restaurant analogy. At floor 20, the chef has:

- Read the entire order (token processing)
- Identified the individual dishes requested (token grouping)
- Understood the grammatical structure of the order ("the salmon, grilled, with a side of asparagus, no butter" --- she knows the salmon is grilled, not the asparagus)
- Resolved any ambiguities ("dressing on the side" applies to the salad, not to the main course)
- Classified the type of meal (a formal dinner, not a quick lunch)

What the chef has *not* yet done:

- Considered how the dishes interact with each other (will the flavors complement?)
- Thought about the diner's likely preferences based on the overall order
- Planned the timing and presentation
- Retrieved specialized knowledge about the specific techniques needed
- Formed a strategy for the overall meal experience

Those deeper considerations happen in the middle layers, which we will explore in the next lesson.

> **Try This Now**
>
> You can observe the early layers at work by giving the AI a grammatically complex but semantically simple sentence and asking it to parse the structure:
>
> "The dog that the cat that the rat bit chased ran away."
>
> Ask the AI to identify who bit whom, who chased whom, and who ran away. This sentence is a nightmare of nested clauses, and parsing it requires exactly the kind of structural analysis that the early layers perform. If the AI gets it right (the rat bit the cat, the cat chased the dog, the dog ran away), you are seeing the early layers' grammatical machinery in action. If it struggles, you are seeing the limits of that machinery on extreme cases.

## What the Early Layers Do Not Do

It is equally important to understand what these layers are *not* doing. The early layers do not:

- **Reason about the content.** They do not consider whether a career change from accounting to UX design is a good idea. They do not weigh pros and cons. They do not assess feasibility.
- **Retrieve deep knowledge.** They do not pull up detailed information about accounting career paths or UX design job markets. Knowledge retrieval happens in the middle layers.
- **Plan the response.** They do not decide how to structure the answer, what to include, or what tone to use. Response planning happens in the deep layers.
- **Generate any words.** The output is not being formed yet. That happens in the final layers.

The early layers are purely about *understanding the input.* They take raw tokens and produce structured, disambiguated, grammatically parsed representations. They are the foundation upon which everything else is built.

> **Pro Tip**
>
> Since the early layers focus on grammatical parsing and structural understanding, you can help them by writing clearly structured prompts. Ambiguous grammar forces the model to make guesses in the early layers, and a wrong guess here can cascade through all subsequent layers. Instead of "Plan my change career from accounting to design UX," write "Plan my career change from accounting to UX design." The clearer your grammar, the more accurately the early layers parse your intent, and the better the foundation for everything that follows.

## Looking Up

We are standing at the twentieth floor of our eighty-story building. We have a solid structural understanding of the input: what words are present, how they relate grammatically, what basic meaning they carry, and what kind of task this is.

But we are barely a quarter of the way up. The views from the next thirty floors --- the middle layers --- are where things get truly interesting. That is where the model moves from understanding the words to understanding the *meaning* behind the words. From parsing the surface to assembling the depth.

Let us keep climbing.
