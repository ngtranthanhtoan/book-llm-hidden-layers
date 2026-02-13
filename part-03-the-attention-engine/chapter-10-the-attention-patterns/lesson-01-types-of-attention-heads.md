# Lesson 10.1: Types of Attention Heads --- The Specialists in the Room

## Not All Attention Is Created Equal

In the previous chapter, we learned that a Transformer uses dozens of attention heads running in parallel, each one capturing different relationships between words. We compared them to jurors, to orchestral sections, to witnesses at a crime scene.

But we left a crucial question unanswered: what *specifically* do these different heads look at?

This is where our X-ray vision gets sharper. Researchers have spent years peering inside large language models, examining individual attention heads, and what they have found is remarkable. These heads are not random. They are not chaotic. They self-organize into distinct types, each one specializing in a particular kind of linguistic relationship.

Nobody programmed these specializations. During training, the model discovered --- entirely on its own --- that the best way to understand language is to assign different heads to different jobs. It is as if you hired ninety-six analysts and told them only "figure out what this text means," and they spontaneously organized themselves into departments: grammar, references, meaning, structure, position, and task analysis.

Let us meet these specialists.

## The Six Types of Attention Heads

While real Transformer models have far more nuance and overlap than a clean taxonomy suggests, researchers have identified six broad categories of attention head specialization. Think of these as departments in an organization, each with its own mandate and expertise.

### 1. Syntactic Heads: The Grammarians

These heads focus on grammatical structure --- the scaffolding that holds a sentence together. They track which noun goes with which verb, which adjective modifies which noun, where clauses begin and end, and how the sentence is architecturally organized.

When you type "Help me plan a career change from accounting to UX design," the syntactic heads are parsing the grammatical skeleton:

- "Help" is the main verb
- "me" is the object of "Help"
- "plan" is a verb in the infinitive, controlled by "Help"
- "career change" is the object of "plan"
- "from accounting" and "to UX design" are prepositional phrases modifying "change"

This might seem boring compared to understanding the *meaning* of your words, but it is essential. Without knowing the grammatical structure, the model cannot determine who is doing what to whom. Consider the difference between "The accountant designed the UX" and "The UX designer did the accounting." Same words, same concepts, completely different meanings --- and only the grammatical structure distinguishes them.

Think of syntactic heads as the structural engineers of a building. They do not decide what the building looks like or what happens inside it, but without them, nothing else stands up.

### 2. Coreference Heads: The Pronoun Detectives

These heads specialize in one of the most critical and deceptively difficult tasks in language understanding: figuring out what pronouns and other reference words point to.

When you write, "My boss suggested I consider UX design. She said it would suit my analytical nature," the coreference heads determine that "She" refers to "My boss" and "it" refers to "UX design" and "my" refers to "I" (the user).

This sounds trivial, but it is one of the hardest problems in natural language processing. Consider this example:

"The accountant told the designer that her portfolio impressed the hiring manager, but she needed more experience in her target field."

Who is "her" in "her portfolio"? The designer's. Who is "she" in "she needed more experience"? Probably the accountant (who is trying to switch careers). Who is "her" in "her target field"? The accountant's target field.

Humans resolve these references almost effortlessly, using a combination of grammar, meaning, world knowledge, and context. Coreference heads learn to do the same thing, forming strong attention connections between pronouns and their referents, even when those referents are many sentences away.

> **This Is Why...**
>
> ...the AI can track complex references like "she said that he told them about it" across long passages. Dedicated coreference attention heads form direct connections between each pronoun and its most likely referent, weighing grammatical cues, semantic plausibility, and positional information. When the AI occasionally gets a pronoun reference wrong, it is often because the coreference heads weighted the wrong candidate --- usually in genuinely ambiguous situations where even humans might disagree.

### 3. Semantic Heads: The Meaning Makers

These heads focus on conceptual and thematic relationships between words, regardless of their grammatical role or position in the sentence. They connect words that are related in meaning, even when those words are far apart or in different grammatical roles.

In our career change prompt, semantic heads might form strong connections between:

- "Accounting" and "UX design" (both are professional fields)
- "Career" and "change" (both relate to professional transitions)
- "Plan" and "Help" (both relate to problem-solving and guidance)

But semantic heads also make more surprising connections. They might connect "accounting" to implicit concepts like "numbers," "stability," "corporate," and "structured" --- even though those words do not appear in the prompt. They connect "UX design" to implicit concepts like "creativity," "technology," "user research," and "portfolio." These implicit connections come from the training data, where these words frequently appeared in similar semantic contexts.

Semantic heads are the reason the AI can understand metaphors, detect themes, and make conceptual leaps. When you write "I feel like I am in a cage," semantic heads connect "cage" not to a literal metal enclosure but to the concepts of restriction, dissatisfaction, and desire for freedom --- because that is how "cage" functions semantically in this context.

### 4. Positional Heads: The Proximity Trackers

These heads pay special attention to the position of words relative to each other. Some positional heads focus on adjacent words (what is immediately before and after this word?). Others focus on more distant positional relationships (what was at the beginning of this message? What was at the end?).

Positional heads capture patterns that depend on word order and proximity. For example:

- "From accounting" works differently than "accounting from" --- the positional relationship between "from" and "accounting" matters.
- Words near the beginning of your message often establish the overall framing.
- Words near the end often contain the specific request or question.
- Words that appear together frequently (like "career change" or "UX design") are recognized as units partly through positional proximity.

Think of positional heads as the spatial awareness system. They answer the question: "Where is this word in the overall landscape of the sentence, and what is near it?"

> **Behind The Curtain**
>
> One fascinating finding from attention head research is that some positional heads develop a "primacy bias" --- they pay disproportionate attention to the very first tokens in a prompt. Other heads develop a "recency bias," focusing heavily on the most recent tokens. This is not a bug; it reflects genuine patterns in language. The opening of a message often sets the frame (primacy), while the most recent words often contain the specific question or request (recency). Understanding this is why the advice to "put your most important information at the beginning or end of your prompt" actually has a mechanistic basis.

### 5. Task-Framing Heads: The Mission Classifiers

These heads specialize in determining *what kind of communication this is.* Is the user asking a question? Giving a command? Making a request? Sharing information? Expressing frustration? Setting up a creative exercise?

Task-framing heads look at structural cues like question marks, imperative verbs ("Help," "Explain," "Write"), conversational markers ("I was wondering if..."), and genre indicators ("Once upon a time" versus "According to the data").

For our running example, the task-framing heads detect:

- "Help" signals a request for assistance (not a question, not a command)
- "Plan" signals that the expected output is a structured plan
- "Career change" signals the domain is professional development
- The overall tone is personal and slightly uncertain

This classification happens automatically and influences how the model shapes its response. A prompt identified as a "personal help request" will generate a different response tone than the same information framed as an "analytical question."

### 6. Constraint Heads: The Rule Enforcers

These heads focus on restrictions, limitations, conditions, and specifications in your message. They detect phrases like "but not," "only if," "must include," "no more than," "in the style of," and other constraint language.

In a more detailed version of our prompt --- "Help me plan a career change from accounting to UX design, but I cannot afford to quit my job before having a new position, and I need the plan to be realistic for someone with family obligations" --- the constraint heads would form strong connections around:

- "Cannot afford to quit" (financial constraint)
- "Before having a new position" (sequencing constraint)
- "Realistic" (quality constraint)
- "Family obligations" (lifestyle constraint)

These heads ensure that the model does not just understand what you want, but also what you *do not* want and what boundaries the response must respect.

> **Pro Tip**
>
> Now that you know about constraint heads, you can use them strategically. When your AI responses are too generic, too ambitious, or too impractical, the problem is often that you have not given the constraint heads enough material to work with. Try adding explicit constraints: "Keep the plan under six months." "Assume I can only dedicate ten hours per week to this." "Do not suggest going back to school full-time." Each constraint activates the constraint heads and narrows the response toward what is actually useful for you.

## How These Heads Work Together

The real power is not in any single type of attention head but in how they combine. Let us trace how all six types process a single word from our prompt: "change."

- **Syntactic heads** identify "change" as a noun modified by "career" and taking prepositional phrases "from accounting" and "to UX design."
- **Coreference heads** note that later in the conversation, "it" or "the transition" might refer back to this "change."
- **Semantic heads** connect "change" to concepts like transition, transformation, risk, growth, new beginnings, and uncertainty.
- **Positional heads** note that "change" appears in the first half of the sentence, near "career," and is preceded by a modifier.
- **Task-framing heads** note that "change" is part of the task definition, not a constraint or a question.
- **Constraint heads** note that the type of change is specified ("from accounting to UX design") and is therefore bounded, not open-ended.

The combined output is a representation of "change" that is simultaneously grammatically grounded, semantically rich, positionally aware, and task-relevant. This multi-faceted representation is far richer than any single perspective could produce.

## The Self-Organizing Principle

Here is what makes this particularly remarkable: nobody designed these specializations. Nobody wrote code that says "Head 47 should track grammar" or "Head 12 should resolve pronouns." The specializations emerged spontaneously during training.

During the training process (which we covered in Part 1), the model's attention heads started out random. They formed arbitrary, meaningless connections between words. But as the model was trained on billions of examples of human language, the heads that happened to specialize --- that happened to focus on grammar, or meaning, or references --- performed better than heads that tried to do everything at once. Through the training process, this specialization was reinforced and refined.

It is strikingly similar to how specialized roles emerge in human organizations. A startup with five people has everyone doing everything. But as the company grows, people naturally specialize --- one person becomes the finance expert, another becomes the design lead, another handles operations. Nobody mandated it. Specialization emerged because it was more effective.

The Transformer's attention heads underwent the same organizational evolution, compressed into the training process rather than played out over years.

> **Try This Now**
>
> You can see different attention head types in action with this experiment. Ask your AI the following and note how different aspects of its analysis correspond to different head types:
>
> "Analyze this sentence for me: 'The bank approved the loan for the developer who wanted to build near the river bank.'"
>
> Ask the AI to identify: (1) the grammatical structure, (2) what "bank" means in each usage, (3) who "who" refers to, (4) what the overall request is about, and (5) any constraints or conditions.
>
> Each of these analyses is dominated by a different type of attention head: (1) syntactic, (2) semantic, (3) coreference, (4) task-framing, (5) constraint. The AI can perform all these analyses because it has specialized heads for each one.

## What This Means for Your Prompts

Understanding attention head types gives you a practical framework for constructing better prompts. Think of each type as a channel you can deliberately activate:

- **Activate syntactic heads** by using clear, well-structured sentences. Ambiguous grammar forces the model to guess.
- **Activate coreference heads** by being explicit about who and what you are referring to. Instead of "it" and "they," use specific names and terms.
- **Activate semantic heads** by including relevant context words, even if they seem obvious. Mentioning "creativity" and "analytical thinking" in your career change prompt gives semantic heads more material.
- **Activate positional heads** by placing key information at the beginning or end of your prompt, where positional heads concentrate their attention.
- **Activate task-framing heads** by being explicit about what kind of response you want: "Create a plan," "Explain the tradeoffs," "Give me a pros and cons list."
- **Activate constraint heads** by stating your limitations, requirements, and exclusions explicitly.

A prompt that activates all six head types gives the model a complete, multi-dimensional understanding of what you need. A prompt that activates only one or two types produces a response that is strong in those dimensions but weak in the others.

In the next lesson, we will explore how these attention patterns combine to create something truly remarkable: a non-linear reading of your message that processes relationships as a web rather than a chain.
