# Lesson 3: The Commitment Problem

## Why the AI Can't Take Back What It Already Said

Imagine you're telling a story at a dinner party. You begin with: "So there I was, standing in the middle of the airport in Tokyo..." Now you're committed. You can't suddenly say the story takes place in a small town in Nebraska without confusing everyone. Every sentence you add builds on that Tokyo airport opening. The characters, the setting details, the cultural references — all of them must be consistent with what you've already established.

You could, of course, stop and say, "Actually, wait — it wasn't Tokyo, it was Omaha." Humans do this all the time. We backtrack, correct ourselves, start over.

An AI cannot.

This is the commitment problem, and it's one of the most important — and least understood — aspects of how AI generates text. Once the autoregressive loop produces a token, that token becomes an irrevocable part of the context. The model cannot go back and erase it. It cannot reconsider. It cannot rewrite its third sentence after generating its tenth. Every token is a one-way door, and the AI walks through hundreds of them in every response.

## The One-Way Assembly Line

Let's return to our restaurant analogy, but with a twist. Imagine the chef is plating a dish on a conveyor belt that moves steadily forward. She places the protein on the plate. The belt moves. She places a vegetable. The belt moves. She adds a sauce. The belt moves.

Here's the catch: the belt only moves forward. Once the protein is placed and the belt has advanced, the chef cannot reach back and reposition it. She can only add new elements, always at the front of the moving belt. If she realizes after placing the sauce that the protein would have been better on the other side of the plate — too late. She has to work with the plate as it is and make the best of the remaining decisions.

This is precisely the constraint the autoregressive loop imposes. The model generates token 1, and it's locked in. Then token 2, locked in. Then token 3. By the time the model is generating token 200, it has 199 irrevocable decisions behind it. Each of those decisions constrains what's possible going forward.

The model can acknowledge something it said earlier was incomplete. It can add nuance or caveats later. What it cannot do is literally erase and replace previous tokens. The response is a one-direction stream.

## How Commitment Creates Momentum

The commitment problem isn't purely a limitation. It's also a powerful force that creates coherence and momentum. Because each token builds on what came before, the response develops a kind of narrative gravity — a tendency to continue in the direction it's already heading.

Consider our career change example. If the model begins its response with:

"Transitioning from accounting to UX design is absolutely achievable, and many professionals have made this exact switch successfully."

That opening has created momentum in several directions:

- **Tone:** Encouraging and optimistic. The model will now maintain this supportive tone throughout. It would feel jarring to suddenly become discouraging at paragraph three.
- **Framing:** The transition is presented as "achievable." The rest of the response will provide evidence and steps supporting this claim, not reasons it might fail.
- **Authority stance:** The phrase "many professionals have made this exact switch" establishes that the model is positioning itself as knowledgeable about this topic. It will continue in that authoritative register.

None of these commitments were explicit decisions. The model didn't "choose" to be encouraging. It generated tokens that happened to be encouraging, and now the autoregressive loop's momentum will keep pushing in that direction because encouraging follow-up tokens are the most probable continuation of encouraging opening tokens.

> **"This Is Why..." Box**
>
> **This is why the AI sometimes seems to double down on a wrong answer rather than correcting itself.** If the model generates a confident but incorrect statement in its third sentence, the commitment problem kicks in. Every subsequent token is influenced by that incorrect statement. The model may generate supporting "evidence" that reinforces the error, not because it's trying to deceive you, but because the most probable tokens following a confident assertion are tokens that support and elaborate on that assertion. The error becomes embedded in the momentum of the response. This is why asking in a follow-up message "Are you sure about that?" can produce a correction — you've given the model a fresh context that includes the possibility of error, allowing the autoregressive loop to take a different path.

## The Path Dependency Problem

Here's where the commitment problem becomes truly consequential. In complex topics, the opening sentences don't just set tone — they determine which entire line of reasoning the model pursues.

Suppose you ask: "What's the best approach to learning UX design for someone coming from accounting?"

The model might start with any of these openings:

**Path A:** "The most efficient approach is to leverage your analytical skills..." — This commits the model to a response focused on transferable skills and how to build on existing strengths.

**Path B:** "Start by enrolling in a formal UX bootcamp..." — This commits the model to a response structured around formal education, with specific program recommendations and timelines.

**Path C:** "Before investing time and money, try a low-risk experiment..." — This commits the model to a cautious, experimental approach, emphasizing validation before commitment.

Each of these is a perfectly valid response. But once the model starts down Path A, it will not also cover Paths B and C in any depth — because the autoregressive momentum is pulling it deeper into the "leverage your skills" narrative. The model's own commitment to its opening sentences narrows the space of what follows.

This is path dependency. The model's early token choices constrain its later token choices in ways that determine not just the style but the substance of the response.

> **"Behind The Curtain" Sidebar**
>
> Researchers have studied this phenomenon by intervening in the generation process — forcing the model to start with different opening tokens and then letting it generate freely. The results are striking. The same model, given the same prompt, produces substantively different advice depending on whether it's forced to begin with "The most important thing is..." versus "There are several approaches..." versus "Many people make the mistake of..." The content isn't just rephrased — the model actually covers different topics, recommends different actions, and arrives at different conclusions. The opening tokens don't just shape the surface; they determine the intellectual territory the response explores.

## When Commitment Goes Wrong

The commitment problem becomes genuinely problematic in several scenarios:

**Scenario 1: The confident wrong start.** The model begins with an incorrect fact stated confidently. Because of commitment momentum, it then builds an entire argument on that false foundation. The rest of the response might be internally consistent and well-reasoned — but it's all built on quicksand.

**Scenario 2: The suboptimal framing.** The model starts answering the wrong interpretation of an ambiguous question. By the time enough tokens have been generated to reveal the misinterpretation, the model is deep into an irrelevant response. It might try to course-correct mid-stream, but it can't undo the paragraphs already generated.

**Scenario 3: The structure lock-in.** The model begins with "There are three main approaches..." and is now committed to delivering exactly three approaches, even if there are really four important ones or if two would have been sufficient. The number was locked in at the beginning and must be honored.

**Scenario 4: The tone trap.** The model opens with a casual, breezy tone that turns out to be inappropriate for the seriousness of the request. It can gradually shift toward a more serious register, but it can't retroactively make the opening paragraphs match the gravity of what follows.

## The Human Advantage: You Can Restart

Here's the good news: the commitment problem is a constraint on the model, not on you.

When you read a response and sense that it went down the wrong path — that the framing is off, the tone is wrong, or a key point is missing — you have tools the model lacks. You can regenerate the response entirely, getting a fresh roll of the dice that might commit to a better path. You can provide a follow-up message that redirects: "That's helpful, but I was looking for more focus on formal education options." You can even do something remarkably powerful that we'll explore in the next lesson: tell the model what its opening words should be, thereby choosing the path before the model starts walking.

> **"Try This Now" Exercise**
>
> Try this revealing experiment. Give the AI an open-ended prompt: "Give me advice about investing for beginners."
>
> Now regenerate the response three or four times (most AI interfaces have a "regenerate" button, or you can just paste the same prompt again).
>
> Notice how each response starts differently — and how that different start leads to substantially different advice. One might focus on index funds, another on emergency funds, another on mindset. Each response is internally coherent, but the path each one takes was largely determined by its opening tokens. You're watching the commitment problem in action: different starting commitments, different destinations.

## The Commitment Problem and Extended Thinking

Remember Chapter 12, where we explored the AI's extended thinking process? The commitment problem is one of the key reasons extended thinking was developed.

Here's the connection: if the model starts generating its visible response immediately, it's making commitment-laden decisions (tone, framing, approach) before it's fully reasoned through the problem. Extended thinking gives the model a "scratchpad" — a hidden space where it can explore different paths, weigh options, and plan its approach before committing to the first visible token.

Think of it as the difference between a speaker who starts talking the moment they reach the podium (commitment problem in full force) versus a speaker who pauses, gathers their thoughts, and then delivers a considered opening (extended thinking mitigating the commitment problem).

When the model uses extended thinking, it might internally consider: "I could approach this as a skills-transfer story, or as an education roadmap, or as a risk-management plan. The user's phrasing suggests they want a practical plan, so I'll go with the education roadmap approach." Only after this internal deliberation does it produce its first visible token — a token that reflects genuine planning rather than a hasty first guess.

> **"This Is Why..." Box**
>
> **This is why AI responses have improved so dramatically in recent model versions.** Extended thinking is, in large part, a solution to the commitment problem. Older models that didn't have a thinking phase would sometimes commit to a poor approach in their first few tokens and then be stuck with it. Newer models with extended thinking can reason about the best approach before producing any visible output, dramatically reducing the frequency of wrong-path commitments. When you notice that a modern AI's response feels more thoughtful and well-structured than what you got a year ago, you're partly seeing the commitment problem being managed more effectively.

## The Commitment Problem in Creative Writing

The commitment problem has an especially interesting dimension in creative tasks. If you ask the AI to write a short story, the first few sentences establish not just tone and setting but genre expectations, character voice, narrative perspective, and thematic direction. These early commitments compound throughout the story.

An opening like "The rain hadn't stopped for three days" commits the model to an atmospheric, somewhat melancholy tone. An opening like "Detective Marquez hated Mondays" commits to a character-driven, slightly humorous mystery. An opening like "In the year 2847, nobody remembered what trees looked like" commits to science fiction with an ecological theme.

For creative writers working with AI, this means the opening is disproportionately important. Getting the first sentence right — or providing it yourself — gives you enormous leverage over the entire piece. We'll explore this practical strategy in the next lesson.

## Path Dependency in Real Life

The commitment problem isn't unique to AI. It's actually a well-known phenomenon in many fields. Economics calls it "path dependency" — the idea that early decisions constrain later options. Urban planners know it well: a road built in a certain direction in 1850 determines the shape of a city in 2025. Software engineers call it "technical debt" — early architectural decisions that become increasingly expensive to change as the system grows.

What makes the commitment problem particularly notable in AI is its scale and speed. The model makes hundreds of irrevocable decisions in seconds. Each one is individually small — just one token — but collectively, they determine the entire character of the response. It's like path dependency operating at hyperspeed.

And unlike a city planner who can (expensively) tear down a road and rebuild, the AI truly cannot modify its previous output mid-generation. The only options are to continue forward from the current state or to start over entirely.

> **"Pro Tip" Box**
>
> When you get a response that's headed in the wrong direction, don't try to fix it with incremental follow-up instructions. The model will try to accommodate your correction while also maintaining consistency with everything it already said, often producing an awkward hybrid. Instead, start fresh. Regenerate the response, or begin a new message that reframes the task entirely. It's faster and produces better results than trying to redirect a response that's already committed to the wrong path.

## The Deeper Lesson

The commitment problem reveals something profound about the nature of AI-generated text. These responses are not the product of careful deliberation and revision, the way a human essay might be. They are the product of an irreversible sequence of probabilistic choices, each one locking in a tiny piece of the final output.

This means that the quality of an AI response is heavily front-loaded. The first few tokens carry outsized influence. They set the trajectory that everything else follows. In the next lesson, we'll turn this insight into a practical tool: the ability to steer the AI's generation by controlling those all-important opening words. If the commitment problem is the constraint, steering the opening is the solution.

You now understand why the AI sometimes doubles down on errors, why regenerating gives surprisingly different results, and why the beginning of a response matters so much more than the middle. That's X-ray vision applied to one of the most consequential dynamics in AI generation.
