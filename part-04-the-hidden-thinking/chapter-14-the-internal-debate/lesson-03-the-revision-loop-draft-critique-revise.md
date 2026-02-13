# Lesson 3: The Revision Loop — Draft, Critique, Revise

## The Sculptor's Method

Michelangelo reportedly said that he didn't create David — he simply removed everything that wasn't David from the block of marble. The sculpture was always there; his job was to reveal it through a process of chipping away, evaluating, adjusting, and refining.

The AI's response goes through a remarkably similar process. What you see in the chat window is the finished sculpture — polished, coherent, seemingly effortless. What you don't see is the chipping: the first draft that was too wordy, the second draft that missed a key point, the moment when the AI caught an error and corrected it, the restructuring that moved the most important insight from paragraph four to paragraph one.

This is the **revision loop** — the cyclical process of draft, critique, revise, and check that happens on the hidden scratchpad. It's one of the most powerful mechanisms in modern AI, and understanding it changes how you evaluate AI responses, how you ask for improvements, and how you collaborate with the AI to produce exceptional output.

---

## The Loop in Action

The revision loop isn't a single pass. It can cycle multiple times, each cycle tightening and improving the response. Let's trace through a complete example.

You ask:

*"Write an email to my manager explaining why I want to transition from my current accounting role to our company's UX team."*

### First Draft (on the scratchpad)

*"Dear [Manager's Name],*

*I am writing to express my interest in transitioning from my current role in the accounting department to the UX design team. Over the past several years, I have developed a strong interest in user experience design and believe my analytical skills would be a valuable addition to the team.*

*I have been taking online courses in UX design and have completed several projects in my spare time. I believe this transition would be mutually beneficial for both me and the company.*

*I would appreciate the opportunity to discuss this further at your convenience.*

*Best regards..."*

### First Critique

*"This draft is functional but weak. Problems:*
*1. It's generic — it could be sent by anyone about any role. There's nothing specific about this person's situation or this company's needs.*
*2. 'I believe my analytical skills would be a valuable addition' is vague. Which analytical skills? How specifically do they apply to UX?*
*3. 'Mutually beneficial' is cliche and unsubstantiated. How is it beneficial for the company?*
*4. The tone is too formal and stiff for an internal email to a direct manager. It reads like a cover letter, not a conversation starter.*
*5. There's no mention of how this transition would work practically — does the user want to shift roles immediately? Gradually? Through an internal transfer program?*
*6. It doesn't address the obvious concern the manager will have: who will handle the accounting work if this person leaves?"*

### Revised Draft

*"Hi [Manager's Name],*

*I wanted to bring something up that I've been thinking about for a while. Over the past year, I've been increasingly drawn to UX work — specifically how users interact with our products. I've noticed that my accounting mindset, particularly the way I analyze data patterns and test assumptions, actually aligns closely with how UX researchers work.*

*I've been building skills on my own time — I completed a UX research certification and redesigned the onboarding flow for [internal tool] as a side project (which I'd love to show you). I think there's a genuine opportunity here, both for my growth and for the team: our UX group could use someone who thinks in data and metrics, and I'd bring a perspective they don't currently have.*

*I know this raises practical questions about my current responsibilities, and I want to approach this thoughtfully. Would you be open to a 30-minute conversation about what a path forward might look like?*

*Thanks for considering this..."*

### Second Critique

*"Much better. More specific, more personal, better tone. Let me check:*
*1. Does it address the manager's likely concern about losing an accountant? Yes — 'I know this raises practical questions about my current responsibilities.'*
*2. Is the tone right for an internal email? Yes — conversational but professional.*
*3. Does it demonstrate competence without being arrogant? Yes — mentions certification and side project without overselling.*
*4. Does it make a clear ask? Yes — 30-minute conversation.*
*5. One issue: I referenced a 'UX research certification' but I don't know if the user actually has one. I should make this a template with placeholders rather than inventing credentials.*
*6. Another issue: 'redesigned the onboarding flow for [internal tool]' — I also don't know if they did this. Same problem.*
*Let me adjust to make these examples suggestive rather than assumed..."*

### Final Draft

The AI produces the polished version, with the invented credentials turned into suggestions like "mention any relevant courses, certifications, or side projects you've completed" or bracketed placeholders for the user to fill in.

---

## The Four Stages of the Loop

The revision loop follows a consistent pattern with four stages:

### Stage 1: Generate

The AI produces a first draft. This draft is driven by the strongest patterns in the training data — the most common way to approach this type of request. It's functional but rarely optimal, like a musician's first take in the recording studio.

The first draft tends to be:
- Generic (following common templates)
- Complete but unrefined
- Sometimes too long or too short
- Correct in broad strokes but imprecise in details

### Stage 2: Critique

The AI steps back and evaluates its own draft. This is where the self-consistency checking from Lesson 1 and the confidence calibration from Lesson 2 come into play. The critique asks:

- Is this accurate?
- Is this complete?
- Is this well-organized?
- Does it match the user's intent (all four layers)?
- Is the tone appropriate?
- Are there contradictions?
- Is anything unnecessarily vague?
- Am I assuming facts I don't know?

The critique is often surprisingly harsh. The AI doesn't soft-pedal its evaluation of its own work.

### Stage 3: Revise

Based on the critique, the AI modifies the draft. This might involve:
- Restructuring the order of information
- Adding missing elements
- Removing redundant or irrelevant content
- Increasing specificity
- Adjusting tone
- Correcting errors
- Improving flow and readability

### Stage 4: Check

After revision, the AI does a final verification: does the revised version actually address the critique's concerns? Are there new problems introduced by the revision? Is the response ready, or does it need another cycle?

If the check identifies remaining problems, the loop cycles again — critique, revise, check — until the response meets the AI's internal quality standards.

> **"Behind The Curtain"**
>
> The number of revision cycles varies significantly based on the complexity of the request and whether extended thinking is enabled. For simple requests, there might be zero revision cycles — the first draft is good enough. For complex creative or analytical tasks, the AI might go through three or four cycles. In extreme cases (highly constrained creative writing, complex technical analysis), the revision process can generate more scratchpad content than the final response itself. A 500-word response might have 3,000 words of drafts and critiques behind it.

---

## Why the First Draft Is Rarely the Best Draft

Understanding the revision loop explains a pattern that many AI users have noticed: the AI's first attempt at something isn't always great, but when you ask it to improve, the second version is dramatically better.

This isn't just because you gave additional instructions. It's because you activated an explicit revision cycle. When you say "That's good, but can you make it more specific?" or "Can you restructure this to lead with the strongest point?" you're doing the critique stage for the AI, giving it clear direction for the revision stage.

Here's the key insight: the AI's internal revision loop during extended thinking is good, but it's limited by what the AI can self-critique. The AI may not notice that the tone is wrong for your specific workplace, or that the structure doesn't match your manager's communication preferences, or that certain details are irrelevant to your situation. You notice these things because you have context the AI doesn't.

When you provide that critique, you're adding a human cycle to the revision loop — and human-AI revision cycles are more powerful than either human or AI revision alone.

> **"This Is Why..."**
>
> This is why the AI's second or third attempt at something is often dramatically better than the first. Each iteration adds another revision cycle, and each cycle is informed by your specific feedback. The AI isn't just "trying harder" — it's running the full critique-revise-check process with new information (your feedback) that it didn't have before. This is also why vague feedback like "make it better" produces smaller improvements than specific feedback like "the opening is too formal and the third paragraph is irrelevant."

---

## The Revision Loop and Different Task Types

The revision loop is more powerful for some tasks than others. Understanding which tasks benefit most helps you decide when to invest in iterative refinement.

### High Revision Value: Creative and Persuasive Writing

Writing tasks benefit enormously from revision because there are so many dimensions to optimize: clarity, tone, persuasiveness, structure, word choice, emotional resonance, and audience fit. Each revision cycle can improve a different dimension.

A first-draft cover letter might be structurally sound but tonally flat. After one critique-revise cycle focusing on tone, it might be engaging but too long. After another cycle focusing on conciseness, it might be tight and compelling.

### High Revision Value: Complex Analysis

Analytical tasks benefit from revision because the first draft often organizes information in the order it was retrieved rather than the order that's most useful for the reader. Revision restructures for impact, removes tangents, and strengthens the logical flow.

### Moderate Revision Value: Technical Content

Technical responses (how-to guides, explanations, code) have less room for subjective improvement but still benefit from revision that catches errors, improves clarity, and ensures completeness.

### Low Revision Value: Factual Retrieval

Questions with definitive answers don't benefit much from revision. "What year was the transistor invented?" gets the same answer in draft one as in draft five. The revision loop adds value when there are judgment calls to refine, not when there's a single correct answer.

> **"Pro Tip"**
>
> Use iterative revision strategically. For important creative or analytical output:
>
> **Round 1:** Get the initial response. Don't worry if it's not perfect.
>
> **Round 2:** Provide specific critique: "The structure is good, but the tone is too casual for my audience. The second section is the strongest — can you lead with that? Also, the statistics in paragraph three need citations or should be presented as estimates."
>
> **Round 3:** Fine-tune: "Almost perfect. Can you tighten the opening sentence and replace the generic closing with a specific call to action?"
>
> Three rounds of specific, targeted feedback will produce a result that's dramatically better than any single-shot prompt, no matter how detailed. You're leveraging the revision loop with human insight at each stage.

---

## Making the Internal Loop Visible

One of the most powerful techniques for getting better AI output is explicitly asking the AI to make its revision loop visible. Instead of happening on the hidden scratchpad, the revision process becomes part of the conversation — giving you the opportunity to intervene at each stage.

Here are three ways to do this:

### Technique 1: The Two-Step Draft

"First, give me a rough draft. Then critique it yourself, identifying three specific weaknesses. Then give me a revised version that addresses those weaknesses."

This forces the AI to show you its self-critique, which often surfaces problems you wouldn't have thought to address. You can then add your own critique to the second cycle.

### Technique 2: The Options Approach

"Give me three different approaches to this email. For each one, explain the strategy behind it and identify its strongest and weakest aspects. Then recommend which one I should use and why."

This is a variant of the revision loop where instead of revising a single draft, the AI generates multiple candidates and evaluates them comparatively. This often produces better results than sequential revision because the AI can combine the best elements from each approach.

### Technique 3: The Assumption Reveal

"Write this email, but before showing me the final version, list the five most important choices you made (tone, structure, emphasis, what to include, what to exclude) and why you made them."

This gives you insight into the decisions the AI made during the revision process, allowing you to redirect any choices that don't match your needs before seeing the final product.

> **"Try This Now"**
>
> Try the two-step draft technique with something you actually need. Ask the AI to:
>
> 1. Write a first draft of something (an email, a proposal, an explanation)
> 2. Critique its own draft, identifying three specific weaknesses
> 3. Produce a revised version addressing those weaknesses
>
> Read the self-critique carefully. You'll often find that the AI identifies problems you hadn't considered — issues of tone, missing context, structural weaknesses, or unstated assumptions. The revised version will almost certainly be stronger than the first draft, and you'll have a clear view into why.

---

## The Limits of Self-Revision

Before we move on, an important caveat: the AI's ability to revise its own work has limits.

**It can't fix what it can't see.** If the AI doesn't know that a fact is wrong, no amount of self-revision will correct it. Revision improves structure, tone, completeness, and internal consistency — but it can't verify external truth.

**It can over-revise.** Sometimes the AI's first draft captures a directness or energy that gets refined away through revision. Over-revision can produce text that's technically better but less compelling — like a song that's been produced to the point where it loses its raw feeling.

**It optimizes for its own standards, not necessarily yours.** The AI's internal critique evaluates the draft against what it learned about "good" writing from training data. But your specific needs might differ from those general standards. This is why your critique is so valuable — you provide the standard the AI can't access.

**Diminishing returns apply.** The first revision cycle produces the biggest improvement. Each subsequent cycle produces less improvement. By the fourth or fifth cycle, you're usually getting marginal gains that aren't worth the additional time and tokens.

The practical takeaway: the revision loop is one of the most powerful tools in your AI toolkit, but it works best when combined with your human judgment, your specific context, and your willingness to give targeted, specific feedback.

The AI can sculpt the marble, but you decide what the finished sculpture should look like.

In the next lesson, we'll explore one of the most surprising and practical aspects of the internal debate: what happens when you challenge the AI's answer. Why does "Are you sure?" sometimes produce a completely different — and sometimes better — response? The answer reveals something fundamental about how the AI's conviction works, and it gives you a powerful tool for extracting the AI's best thinking.
