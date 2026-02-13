# Lesson 1: How AI Converts Complex Requests to Subtasks

## The Wedding Planner Inside the Machine

Imagine you walk up to a wedding planner and say: "Plan my wedding." That's it. No date, no budget, no venue preference, no guest count — just "plan my wedding."

A bad planner would freeze. A mediocre planner would ask a hundred questions before doing anything. But a great planner would do something remarkable: they would immediately, instinctively break that vague request into a structured set of sub-tasks, prioritize them, identify which ones need your input and which ones they can start on independently, and begin working — all within seconds of hearing those three words.

That is exactly what happens when you send a complex message to an AI. Before the model writes a single word of its response, it performs an invisible act of task decomposition: breaking your request into manageable sub-tasks, organizing them into a logical sequence, and executing them one by one as it generates its reply.

This process is one of the most impressive things the AI does — and also one of the most fragile. When it works, complex requests produce beautifully organized, comprehensive responses. When it fails, you get answers that miss the point, skip important parts, or address something you never asked about. Understanding how decomposition works (and how it breaks) will dramatically improve how you communicate with AI.

## What Decomposition Actually Looks Like

Let's trace what happens when you send our running example: "Help me plan a career change from accounting to UX design."

Your request is nine words long, but the AI effectively interprets it as a bundle of at least half a dozen sub-tasks:

1. **Assess the transition:** What's involved in moving from accounting to UX design? How different are these fields? What's the realistic difficulty level?

2. **Identify transferable skills:** What does an accountant already bring to UX design? Where are the gaps?

3. **Map the learning path:** What skills and knowledge need to be acquired? In what order?

4. **Suggest resources and methods:** Bootcamps, courses, self-study, mentorship — what are the options?

5. **Address the practical logistics:** Timeline, financial considerations, whether to quit or transition gradually.

6. **Provide job search guidance:** Portfolio building, networking, how to position the career change to employers.

You didn't ask for six separate things. You asked one question. But the AI recognized that answering your one question well requires completing six sub-tasks, and it organized them — roughly in this order — before beginning to write.

This is task decomposition: the invisible process of converting a single complex request into a structured plan of sub-tasks.

> **"Behind The Curtain" Sidebar**
>
> Task decomposition isn't a separate module or a distinct step that runs before generation. It happens within the same neural network computation that produces the response. The model doesn't literally create a to-do list and then check items off. Instead, as it begins generating text, its internal representations organize around the sub-task structure. The first few tokens of the response are heavily influenced by the decomposition — they set up the structure that the rest of the response follows. This is why the opening of an AI response often reveals its entire plan: "Here's a step-by-step plan for your career transition" signals that the AI has decomposed your request into sequential steps and is about to address them in order.

## Simple vs. Complex: The Decomposition Spectrum

Not every request requires decomposition. The AI handles a wide spectrum of complexity:

**No decomposition needed:**
"What's the capital of France?"
This is a single, atomic task. Retrieve the fact, present it. No sub-tasks required. The AI just answers: "Paris."

**Minimal decomposition:**
"What are the three largest cities in France?"
Slightly more complex — the AI needs to recall multiple items and present them in a specific format. But the sub-tasks are trivial: recall cities, rank by size, present the top three.

**Moderate decomposition:**
"Compare living in Paris versus Lyon for a young professional."
Now the AI needs to identify comparison dimensions (cost of living, job market, culture, transportation, etc.), assess each city on each dimension, and structure a balanced comparison. Multiple sub-tasks, but they're relatively straightforward.

**Heavy decomposition:**
"Help me plan a career change from accounting to UX design."
As we traced above, this requires identifying multiple distinct aspects of the problem, organizing them logically, and addressing each one with appropriate depth. The sub-tasks are interconnected — the learning path depends on the transferable skills analysis, the timeline depends on the learning path, the job search strategy depends on the timeline.

**Maximum decomposition:**
"I'm a 35-year-old CPA in Denver thinking about UX design. I have $15,000 saved, a mortgage, two kids, and my spouse works part-time. Help me plan this transition including education, finances, timeline, risk management, and job search strategy. Also compare this path to staying in accounting and pursuing a finance leadership track."

This is the wedding planner equivalent of "Plan my wedding, my honeymoon, and also evaluate whether I should even get married." The AI now needs to decompose into at least a dozen sub-tasks, manage dependencies between them, and produce a coherent, unified response. This is where decomposition gets both most impressive and most likely to go wrong.

## The Restaurant Kitchen Analogy

Our restaurant analogy works beautifully here. When a single diner orders a simple dish — say, a green salad — the kitchen barely needs to coordinate. One station, one cook, a few minutes, done.

But when a table of eight orders a full tasting menu with wine pairings, dietary restrictions, and a birthday cake, the kitchen shifts into a completely different mode. The head chef (the decomposition process) mentally breaks the order into courses, assigns each course to the right station, sequences them so they arrive in the right order and at the right temperature, coordinates the wine pairings with the sommelier, notes the dairy allergy at seat three, and makes sure the birthday cake arrives at the right moment.

The head chef doesn't cook every dish. They organize, sequence, and coordinate. That's decomposition — the organizational intelligence that turns a complex order into a series of manageable tasks executed in the right order.

And just as a kitchen can be overwhelmed by too many complex orders at once, the AI's decomposition process can be overwhelmed by requests that are too complex, too multi-layered, or too interconnected. When that happens, dishes get dropped. In AI terms: parts of your request go unanswered.

## How the AI Recognizes Sub-tasks

How does the model know that "help me plan a career change" contains six implicit sub-tasks? It's not following a rulebook. It's pattern matching against its training data.

During training, the model saw thousands of examples of career advice, career change discussions, planning conversations, and advisory interactions. From these examples, it learned what a "complete" answer to this type of question looks like. It knows — from pattern recognition, not from understanding — that career change advice typically covers skills assessment, learning paths, resources, logistics, and job search strategy.

This pattern-based decomposition is usually remarkably good. The AI recognizes the implicit structure of requests across an enormous range of topics because it has seen so many examples of how humans address similar requests.

But pattern-based decomposition has a crucial limitation: it works best for common request types. When you ask something that closely resembles requests the model has seen many times in training, the decomposition is excellent. When you ask something truly novel — a combination of topics or a type of request the model hasn't seen before — the decomposition can be flawed, incomplete, or oddly structured.

> **"This Is Why..." Box**
>
> **This is why the AI handles some complex requests brilliantly and stumbles on others that seem equally complex.** A request like "plan my career change" gets excellent decomposition because the model has seen thousands of similar requests during training. But a request like "design a curriculum that combines accounting principles, UX design methodology, and marine biology for homeschooled teenagers" gets shakier decomposition because the model has far fewer training examples of that particular combination. The complexity isn't the issue — the novelty is. Common complex requests are decomposed better than unusual simple ones.

## Implicit vs. Explicit Sub-tasks

Here's a crucial distinction that will change how you prompt. Your request contains two types of sub-tasks:

**Implicit sub-tasks** are things the AI infers you need even though you didn't ask for them. When you say "help me plan a career change," you didn't explicitly ask for transferable skills analysis, but the AI correctly infers that you need it as part of a complete plan.

**Explicit sub-tasks** are things you specifically mention. "Help me plan a career change, including a timeline, budget, and resource list" — now timeline, budget, and resources are explicit sub-tasks.

The important pattern: the AI is much more reliable at handling explicit sub-tasks than implicit ones. When you explicitly mention something, it gets prioritized in the decomposition. When you leave it implicit, the AI might include it or might not, depending on how strongly the pattern match suggests it's needed.

This is why experienced AI users learn to make their sub-tasks explicit. Not because the AI can't infer them — it usually can — but because explicit sub-tasks are more reliably addressed than implicit ones.

> **"Try This Now" Exercise**
>
> Try this comparison. First, ask: "Help me plan a career change from accounting to UX design." Note which sub-topics the AI covers. Then ask: "Help me plan a career change from accounting to UX design. Specifically address: (1) which of my accounting skills transfer to UX, (2) the most time-efficient learning path, (3) how to build a portfolio while still employed, (4) realistic salary expectations during transition, and (5) how to explain the career change in job interviews." Compare the two responses. The second should be more complete and more aligned with what you actually need — because you made the sub-tasks explicit.

## The Decomposition Decision Point

There's a fascinating moment in every AI response generation: the point where the model commits to its decomposition plan. This happens in the very early tokens of the response — often in the first sentence or even the first few words.

When the model begins its response with "Here's a step-by-step plan for your career transition:" it has committed to a sequential decomposition. When it begins with "There are several key areas to consider:" it has committed to a categorical decomposition. When it begins with "Great question! The transition from accounting to UX is..." it has committed to a narrative decomposition.

This commitment point matters because of the autoregressive nature of text generation (which we covered in earlier chapters). Once the model commits to a structure in its opening, it tends to follow through on that structure. If the opening implies five categories, the model will usually produce five categories. If it implies a chronological plan, it will usually maintain chronological order.

This is both a strength and a vulnerability. The strength: once committed to a good decomposition, the model reliably executes it. The vulnerability: if the initial decomposition is wrong — if it commits to addressing the wrong set of sub-tasks — the error propagates through the entire response.

> **"Pro Tip" Box**
>
> **You can influence the decomposition decision point by providing the structure yourself.** Instead of letting the AI decide how to break down your request, give it the structure: "Address these five areas in order: (1) skills gap analysis, (2) learning plan, (3) portfolio strategy, (4) financial planning, (5) job search approach." Now the model doesn't need to decompose your request — you've done it. The model's job is simply to execute each sub-task well. This eliminates decomposition errors entirely and is one of the most reliable techniques for getting comprehensive responses.

## What Happens After Decomposition

Once the model has decomposed your request into sub-tasks, it doesn't execute them all at once. Remember, the AI generates text sequentially — one token at a time, left to right. So the sub-tasks are addressed in order, one after another, as the response unfolds.

This sequential execution means earlier sub-tasks influence later ones. When the model addresses transferable skills first, that analysis shapes how it discusses the learning path. When it covers the learning path before the timeline, the timeline reflects the learning plan.

This is generally a good thing — it creates a coherent, interconnected response. But it also means that if the model makes an error or takes a wrong turn on an early sub-task, that error can cascade into later sub-tasks. A flawed transferable skills analysis leads to a flawed learning path, which leads to an unrealistic timeline.

The practical implication: the order of sub-tasks matters. And the first sub-task gets the freshest, most focused attention from the model. Later sub-tasks, generated after the model has already produced significant text, may receive less careful treatment. This is one of the reasons why the last part of a long AI response is often weaker than the beginning — a phenomenon we'll explore in the next lesson.

Understanding decomposition gives you a powerful new lens for working with AI. You're no longer just asking questions — you're providing the blueprints for how those questions should be answered. In the next lesson, we'll zoom in on the six-phase decomposition hierarchy that the AI follows for complex tasks, and why each phase matters.
