# Lesson 2: The Decomposition Hierarchy

## Six Phases, One Response

In the previous lesson, we watched the AI break a complex request into sub-tasks — the *what* of decomposition. Now we need to understand the *how*: the structured process the AI follows to go from understanding your request to delivering a finished response.

Think of it as the difference between knowing that a house needs to be built (decomposition into rooms and features) and understanding the construction process itself (foundation first, then framing, then wiring, then plumbing, then walls, then finishing). The construction process has a specific order, and skipping or botching any phase compromises everything that follows.

The AI follows a similar internal process. For any complex request, it moves through six phases — not as a rigid checklist, but as an emergent pattern that researchers have observed in how large language models handle sophisticated tasks. Understanding these phases reveals why some AI responses feel thorough and brilliant while others feel like they missed the point entirely.

## The Six Phases

### Phase 1: Understand

**The question behind the question:** "What is this person actually asking me to do?"

Before the AI can plan or execute anything, it needs to comprehend the request — and comprehension goes far deeper than parsing the words. We explored this in Chapter 13 (Intent Resolution), but here's how it manifests specifically in the decomposition context.

During the Understand phase, the model is resolving several things simultaneously:

- **The literal request:** What words did the person use? What task are they describing?
- **The scope:** How broad or narrow is this request? Are they asking for a quick answer or a comprehensive treatment?
- **The domain:** What field of knowledge does this fall into? What expertise is relevant?
- **The user's knowledge level:** Is this a beginner question or an expert question? Should the response assume background knowledge or build from basics?
- **The implicit requirements:** What didn't they say but clearly need?

For "Help me plan a career change from accounting to UX design," the Understand phase resolves: this is a career planning request (domain: career advice + UX design + accounting), asking for a comprehensive plan (scope: broad), from someone who presumably knows accounting but not UX (knowledge level: beginner in UX, expert in accounting), with implicit requirements for practicality, actionability, and realism.

This phase happens fast — it's integrated into the earliest processing of your prompt. But its accuracy is critical. A misunderstanding in Phase 1 cascades through every subsequent phase. If the model interprets "plan" as "explain" instead of "create a structured plan," the entire response shifts from actionable steps to abstract description.

> **"This Is Why..." Box**
>
> **This is why starting your request with clear action verbs dramatically improves results.** "Create a plan" produces different Phase 1 understanding than "tell me about." "Compare option A and option B" produces different understanding than "what do you think about option A and option B." The more precisely Phase 1 can resolve what you want, the better every subsequent phase performs. Ambiguous requests force the AI to guess during Phase 1, and wrong guesses ripple through the entire response.

### Phase 2: Plan

**The question behind the question:** "How should I structure my response to address this completely?"

Once the AI understands what you're asking, it needs to decide how to organize its answer. This is where sub-task decomposition lives, but it also includes decisions about:

- **Order:** What should come first? What depends on what?
- **Depth allocation:** How much attention does each sub-topic deserve? Should skills assessment get one paragraph or three?
- **Format choice:** Should this be a numbered list, a narrative, a table, or a combination?
- **Transitions:** How do the sections connect to each other?

The Plan phase is where the model's implicit "template matching" is most visible. For a career change request, the model is drawing on patterns from thousands of similar advisory responses it encountered during training. It's not inventing a plan structure from scratch — it's selecting and adapting a template that fits the request.

Think of it like an architect. A good architect doesn't design every house from a blank sheet of paper. They draw on established patterns — ranch-style, colonial, modern — and adapt them to the specific client's needs and site constraints. The AI's Plan phase works similarly: it selects a structural template (for career advice, that might be "situation assessment, learning plan, practical steps, timeline") and adapts it to your specific details.

### Phase 3: Research

**The question behind the question:** "What do I know that's relevant to this request?"

This might be the most misunderstood phase. The AI doesn't literally search a database (unless it has tool access, which we cover in Chapter 20). Instead, it activates relevant knowledge from its parameters — the vast web of information encoded during training.

The Research phase is when the model's internal representations light up with relevant facts, patterns, and connections:

- UX design skills: user research, wireframing, prototyping, information architecture, usability testing
- Accounting-to-UX connections: analytical thinking, data interpretation, attention to detail, understanding business processes
- Learning resources: Google UX Design Certificate, Coursera, bootcamps like Designlab or Springboard
- Industry context: UX job market trends, typical salaries, hiring expectations
- Career change logistics: portfolio importance, networking strategies, how to position a non-traditional background

Not all of this knowledge will make it into the response. The Research phase activates a broad set of relevant information. Subsequent phases filter and prioritize it.

Here's the critical insight: the Research phase is limited by what the model was trained on. If a fact, resource, or trend emerged after the training data cutoff, the model doesn't have it. This is why AI career advice might recommend resources that no longer exist or miss new developments in a field.

> **"Behind The Curtain" Sidebar**
>
> The Research phase reveals one of the most important limitations of AI: it doesn't know what it doesn't know. When the model activates relevant knowledge for a career change plan, it can't flag gaps in its own knowledge. It won't say, "I should mention the new UX apprenticeship program that launched last month, but I don't know about it." It simply proceeds with whatever knowledge is available. This is why AI responses can feel authoritative and comprehensive while missing important current information. The confidence comes from the model's genuine knowledge about the topic structure; the gaps come from the training data cutoff.

### Phase 4: Execute

**The question behind the question:** "Now let me actually produce the content for each sub-task."

This is where the rubber meets the road. The model begins generating the actual text of the response, working through the plan it created in Phase 2, drawing on the knowledge activated in Phase 3.

Execution happens sequentially — the model writes the first section, then the second, then the third. Each section is generated token by token, with each new token influenced by everything that came before.

The Execute phase is where quality variation is most noticeable. The first section tends to be the strongest because:
- The model's "attention budget" is freshest
- The plan is clearest in memory
- The generated text hasn't yet consumed context window space

Later sections can show signs of what researchers informally call "generation fatigue" — not because the model gets tired (it doesn't), but because:
- The growing response competes for attention with the original prompt
- The model has committed to positions in earlier sections that may constrain later ones
- The remaining context window is smaller, which can affect quality

This is a real, measurable phenomenon. If you've ever noticed that the last section of a long AI response feels thinner or more generic than the first section, you've witnessed the Execute phase's quality gradient.

### Phase 5: Format

**The question behind the question:** "How should I present this information for maximum clarity and usefulness?"

Formatting might sound trivial, but it's deeply intertwined with execution. The model doesn't generate raw content and then format it — formatting decisions are made as the content is generated.

This phase handles:
- Headers and sub-headers
- Bullet points versus paragraphs
- Bold text for emphasis
- Numbered lists for sequential items
- Spacing and structure
- Length calibration (are we running too long? Too short?)

The Format phase is guided by the intent stack's Layer 5 (format expectations), which we covered in Chapter 15. The model has learned from RLHF training that well-formatted responses are rated higher than wall-of-text responses, so it defaults to heavy formatting.

One important nuance: formatting can actually improve content quality. When the model commits to a numbered list of five items, it's forced to identify five distinct points. When it commits to a comparison table, it's forced to evaluate each item on the same dimensions. Format creates structure, and structure creates completeness. This is another reason why specifying a format in your prompt often improves the substance of the response, not just its appearance.

### Phase 6: Verify

**The question behind the question:** "Does this response actually answer what was asked?"

The Verify phase is the quality check — the moment where the model (implicitly) evaluates whether its response addresses the original request. This isn't a separate pass over the generated text. Rather, it's integrated into the final portion of generation, where the model checks whether the response feels complete and coherent.

Verification manifests in several ways:
- **Completeness check:** Did I address all the sub-tasks I identified? (This is where you see conclusions like "In summary, the key steps are..." — the model is verifying coverage.)
- **Consistency check:** Do the different sections contradict each other?
- **Tone check:** Does the overall response match the appropriate tone?
- **Closing signal:** Should I invite follow-up questions? Should I summarize?

The Verify phase is often the weakest link. Because the model generates text sequentially, it can't easily go back and revise earlier sections if the verification reveals problems. If the model realizes in the last paragraph that it forgot to address a sub-task, the options are limited: it can add the missing content at the end (which feels tacked on), mention it briefly in a closing note, or simply miss it. It can't insert it where it logically belongs.

> **"This Is Why..." Box**
>
> **This is why AI responses sometimes have a "catch-all" paragraph at the end that covers things that feel out of place.** You'll see something like a structured career plan followed by a final paragraph that says, "Oh, and it's also worth considering the financial implications of this transition and making sure your partner is on board." That's the Verify phase catching a missed sub-task and patching it in at the end — because the model can't go back and weave it into the appropriate earlier section. The advice is still there, but the structure reveals that it was an afterthought.

## The Hierarchy in Action: A Complete Trace

Let's watch all six phases work on our career change request, compressing the process into a narrative trace:

**Phase 1 (Understand):** User wants a career transition plan. Source field: accounting. Target field: UX design. No constraints mentioned (budget, timeline, location). Implicit requirement: be practical and actionable. Knowledge level: presumably no UX background.

**Phase 2 (Plan):** Structure as a phased plan. Start with transferable skills (encouraging — shows they're not starting from zero). Then learning path. Then portfolio building. Then job search strategy. Include estimated timeline. Keep each section focused.

**Phase 3 (Research):** Activate knowledge about UX skills, accounting overlap, learning resources (Google UX Certificate, bootcamps), portfolio expectations, networking in UX, salary ranges, career change patterns.

**Phase 4 (Execute):** Generate each section, starting with the transferable skills analysis, moving through the learning path, portfolio advice, and job search strategy. Apply earlier analysis to later sections (e.g., the learning path prioritizes skills not covered by transferable accounting skills).

**Phase 5 (Format):** Use headers for each phase. Bullet points for specific resources. Bold for key takeaways. Moderate length — comprehensive but not overwhelming.

**Phase 6 (Verify):** Does this cover the main aspects of a career change plan? Yes — skills, learning, portfolio, job search, timeline. Did I miss anything important? Financial planning during transition... add a note at the end. Does the tone feel right? Encouraging but realistic. Complete.

The response you read looks like a seamless, thoughtful plan. Now you know it was built in six phases, each one building on the last.

## When Phases Go Wrong

Each phase can fail independently, and the type of failure tells you where the process broke down:

- **Phase 1 failure (Misunderstanding):** The response addresses the wrong question entirely. Solution: rephrase your request more clearly.
- **Phase 2 failure (Bad plan):** The response addresses the right question but is organized poorly or misses major aspects. Solution: provide the structure yourself.
- **Phase 3 failure (Knowledge gap):** The content is well-organized but contains outdated or incorrect information. Solution: provide the key facts yourself or use an AI with web search.
- **Phase 4 failure (Execution weakness):** The structure is good and the knowledge is there, but individual sections are thin or generic. Solution: ask the AI to expand on specific sections.
- **Phase 5 failure (Format mismatch):** The content is good but presented in a format that doesn't work for your needs. Solution: specify the format explicitly.
- **Phase 6 failure (Missed verification):** The response is mostly good but missed an important sub-task or has internal inconsistencies. Solution: point out the gap and ask for completion.

> **"Pro Tip" Box**
>
> **When an AI response disappoints you, diagnose which phase failed before reprompting.** This is much more productive than saying "try again." If the structure was wrong (Phase 2), provide your own structure. If the knowledge was thin (Phase 3), provide relevant context. If the format didn't work (Phase 5), specify the format you want. Targeted corrections are faster and more effective than starting from scratch.

## The Hierarchy Is Not Rigid

An important caveat: the six phases aren't rigidly sequential in the way that "mix ingredients, then bake, then frost" is sequential for a cake. They're more like overlapping waves — the model begins understanding while already starting to plan, and begins planning while already activating knowledge. The phases blend into each other.

But the conceptual hierarchy holds: understanding must substantially precede planning, planning must substantially precede execution, and execution must substantially precede verification. Disrupting this order — trying to execute before understanding, or trying to verify without having a plan — produces exactly the kind of confused, incomplete responses that frustrate users.

> **"Try This Now" Exercise**
>
> Ask an AI to respond to a complex request of your choice. Then, immediately after, ask: "Walk me through how you approached that response. What did you need to understand first? How did you decide to structure it? What knowledge did you draw on? What format choices did you make? Is there anything you realized you missed at the end?" The AI's self-report won't be a perfect description of its actual computational process, but it will give you a fascinating window into how the model conceptualizes its own decomposition hierarchy — and you may spot phases where the process could have gone better.

The decomposition hierarchy is the AI's construction blueprint. In the next lesson, we'll examine what happens when the blueprint goes wrong — why complex requests sometimes produce disappointing results, and what specific failure modes you should watch for.
