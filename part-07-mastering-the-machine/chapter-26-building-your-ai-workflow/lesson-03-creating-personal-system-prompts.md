# Lesson 3: Creating Personal System Prompts

## Writing Your Own Standing Orders

In Chapter 5, you discovered that every AI conversation begins with invisible instructions -- the system prompt -- written by the company that built the tool. These instructions shape every response: the personality, the format, the caution level, the tone. You learned that you are always operating within someone else's design decisions.

Now you are going to take back some of that power.

Most major AI tools now offer some version of "custom instructions" or "personal system prompts" -- a space where you can write persistent instructions that apply to every conversation. This is not a minor feature. This is you writing standing orders for the kitchen before every meal. It is one of the most under-utilized capabilities in modern AI tools, and understanding the hidden layers gives you a dramatic advantage in writing effective ones.

## How Custom Instructions Work (The Architecture View)

When you write custom instructions, your text is typically prepended to (or merged with) the company's system prompt. This means your instructions become part of the context the model reads before it processes your first message.

Remember the math from Chapter 5: in a typical conversation, your message might be 50 words. The system prompt might be 5,000 words. Your custom instructions sit between the two, adding perhaps 200-500 words to the context. Those 200-500 words influence every response in every conversation, because the model's attention mechanism processes them alongside every message you send.

This is enormously powerful. A well-written custom instruction functions like a permanent upgrade to every AI interaction. A poorly written one -- or an empty one -- means you are leaving a powerful lever untouched.

## The Three Layers of Personal System Prompts

Think of your custom instructions as having three layers, each serving a different purpose:

**Layer 1: Who You Are (Context the model always needs)**
This is persistent context about you -- your background, role, expertise level, and situation. Instead of repeating this in every conversation, you encode it once.

Example:
"I am a product manager at a mid-sized SaaS company. I manage a team of 6. My audience for most written work is senior leadership (VP and C-level). I have a technical background but my current role is strategic, not hands-on coding."

**Why this works:** Every response the model generates is now informed by your professional context. When you ask for help writing an email, the model knows your organizational level. When you ask for analysis, it knows your audience. When you ask for advice, it knows your role. This eliminates the need to provide this context in every single conversation.

**Layer 2: How You Want Responses (Style and format preferences)**
This is your preferred interaction style -- how you want the model to communicate with you.

Example:
"Be direct and concise. I prefer bullet points over paragraphs for actionable content. Skip preamble and caveats -- get to the substance immediately. When I ask a question, start with the answer, then provide context if needed. Do not repeat my question back to me. If you are uncertain about something, say so briefly rather than hedging for three sentences."

**Why this works:** These instructions address the model's default behaviors that annoy you. Every user has pet peeves about AI responses -- too wordy, too cautious, too formal, too many disclaimers. Your custom instructions can eliminate these friction points permanently. The model's generation is steered by these instructions before it starts responding to any specific message.

**Layer 3: What You Value (Quality standards and priorities)**
This is your intent stack -- telling the model how to resolve the tradeoffs it faces in every response.

Example:
"I value: accuracy over speed, honesty over diplomacy, specific examples over general principles, actionable recommendations over comprehensive overviews. When I ask for analysis, assume I want the 'so what' -- not just the findings, but what they mean for my decisions. When I ask for writing help, preserve my voice -- improve my drafts rather than rewriting them in your style."

**Why this works:** As Chapter 15 explained, the model is constantly managing competing priorities. Your custom instructions tell it how to resolve those tradeoffs in a way that matches your preferences. Without them, the model uses its default RLHF-trained tradeoffs, which are designed for the average user -- and you are not the average user.

> **"This Is Why..."**
> This is why custom instructions feel like unlocking a different AI. You are not changing the model. You are changing the persistent context that shapes every interaction. It is the same chef, but with your standing orders instead of (or in addition to) the default ones. The personality shift can be dramatic -- and it compounds across every conversation.

## Writing Your Personal System Prompt: A Step-by-Step Guide

**Step 1: Identify your top three frustrations with AI responses.**
What annoys you most? Too wordy? Too cautious? Too generic? Starts with unnecessary preamble? Gives you theory when you want actionable advice? Writes in a tone that does not match yours? These frustrations become your "do not do" instructions.

**Step 2: Identify the context you always provide.**
What do you find yourself typing at the beginning of every conversation? Your role, your expertise level, your audience, your situation? This repeated context belongs in your custom instructions.

**Step 3: Identify your quality standard.**
What makes a response "good" for you? Concise and actionable? Thorough and nuanced? Creative and unexpected? Precise and data-driven? Your quality standard becomes your value layer.

**Step 4: Write a first draft.**
Combine the three layers into a single instruction set. Keep it under 500 words -- longer is not better. The model's attention mechanism gives diminishing weight to very long instructions, and concise instructions are more reliably followed.

**Step 5: Test and refine.**
Use your custom instructions for a week across a variety of tasks. Notice what improves and what still needs work. Refine the instructions based on actual results, not theory.

## A Complete Example

Let us write custom instructions for our career changer -- someone who has transitioned from accounting to UX design and now uses AI regularly in their new role:

---

**About me:**
I am a UX designer who transitioned from accounting. I bring strong analytical skills, data literacy, and structured thinking from my accounting background. I currently work at a mid-sized tech company designing B2B products. My team has 4 designers and 3 researchers.

**My audience:**
Most of my written work is for either (1) my design team, who are fluent in UX terminology, or (2) product managers and engineers, who are smart but not design experts. When I do not specify, assume the audience is product managers.

**How I want responses:**
- Be direct. Skip the "Great question!" preamble.
- When I ask for UX advice, ground it in research and principles, not just best practices. Tell me *why*, not just *what*.
- I learn through concrete examples. Always include at least one specific example.
- If I ask for help with a design rationale or stakeholder communication, lean on data and evidence-based arguments -- my accounting background means I am more credible when I lead with numbers.
- Bullet points for actionable items. Prose for conceptual explanations.

**Quality standards:**
- Specificity over generality. "Use a card-based layout with 16px padding and a 4-column grid" is better than "create a clean, organized layout."
- Honesty over agreement. If my design approach has a flaw, tell me. I would rather fix it now than have it fail in user testing.
- When reviewing my work, be constructive but do not soften genuine problems. I can handle direct feedback.
- When I ask for alternatives, give me three: one safe, one interesting, one unexpected.

---

This is 250 words. It will apply to every conversation. Every time this user asks for UX advice, design feedback, stakeholder communication help, or creative exploration, the model's responses will be shaped by these standing orders. The difference between using AI with these instructions and without them is enormous -- and it compounds over hundreds of interactions.

> **"Try This Now"**
> Write your personal system prompt right now. Use the three-layer framework (Who You Are, How You Want Responses, What You Value) and keep it under 500 words. Apply it to your AI tool of choice and use it for a week. At the end of the week, evaluate: Which instructions worked well? Which had no noticeable effect? Refine and repeat. This is a living document -- treat it as v1.0, not the final version.

## Advanced System Prompt Techniques

Once you have the basics working, these advanced techniques can further improve your results:

**Technique 1: Conditional instructions.**
"When I ask about design decisions, always consider accessibility implications. When I ask for writing help, prioritize my voice over polish. When I ask for data analysis, always include confidence levels."

These conditional instructions activate only when relevant, preventing the model from applying inappropriate instructions to unrelated tasks.

**Technique 2: Anti-patterns.**
"Never start a response with 'Absolutely!' or 'Great question!' Never use the phrase 'in today's fast-paced world.' Never give me a disclaimer about AI limitations unless I specifically ask about reliability."

Anti-patterns are surprisingly effective because they target the model's highest-probability default tokens -- the generic phrases it falls back on most often. Blocking these forces the model into more authentic, specific language.

**Technique 3: Meta-instructions.**
"If my question is ambiguous, ask one clarifying question before responding rather than guessing. If I seem frustrated, acknowledge it briefly and then focus on being maximally helpful. If I give you positive feedback, remember what worked so you can replicate it."

Meta-instructions teach the model how to interact with you, not just how to respond to your content. They shape the relationship dynamic.

> **"Behind The Curtain"**
> Custom instructions are not universally followed with the same weight. The model's attention mechanism processes them alongside the much longer company system prompt. In cases of conflict -- your instruction says "be direct" but the company system prompt says "be thorough and nuanced" -- the company prompt often wins because it has more tokens and context. This is why testing and refinement matter. You may need to phrase your instructions more emphatically or specifically to override strong defaults.

## The Power of Project-Specific Instructions

Beyond personal system prompts, many AI tools now support project-specific or conversation-specific instructions. This is where you can set context for a particular type of work:

**For a specific project:**
"This conversation is about the checkout redesign project for our B2B platform. Key stakeholders: VP of Product (data-driven, skeptical of big changes), Engineering Lead (pragmatic, wants feasible solutions), Customer Success (advocates for ease of use). Our constraint is shipping within 6 weeks."

**For a recurring meeting type:**
"I will paste notes from our weekly design critique. Always structure the summary as: Key Feedback (organized by screen/feature), Design Decisions Made, Follow-up Tasks, Unresolved Debates."

**For a learning track:**
"I am working through a self-directed curriculum in UX research methods. My current knowledge level: intermediate. Challenge me appropriately. Track what I have learned in previous sessions in this conversation."

These project-specific instructions combine with your personal system prompt, creating a layered context that is both personal (your style, your standards) and situational (this specific project, this specific goal).

## The Hierarchy of Influence

Understanding how your various instructions combine helps you write more effective ones:

1. **Company system prompt** (most influence -- you cannot change it, but you can work with it)
2. **Your personal system prompt** (second most -- applies to every conversation)
3. **Project-specific instructions** (applies to a particular conversation or project)
4. **Your individual messages** (most specific, applies to a single exchange)

When these layers align, the model's behavior is powerfully focused. When they conflict, higher layers tend to win. Your strategy: write personal and project instructions that complement rather than contradict the company system prompt, and use individual messages to fine-tune specific responses.

---

Custom instructions are the bridge between understanding the hidden layers and embedding that understanding into your daily workflow. You are no longer just ordering from the menu -- you are talking to the chef before the restaurant opens, shaping every dish that will come out of the kitchen. In the final lesson, we bring everything together with the mindset that makes all of this work: the human-AI collaboration mindset.
