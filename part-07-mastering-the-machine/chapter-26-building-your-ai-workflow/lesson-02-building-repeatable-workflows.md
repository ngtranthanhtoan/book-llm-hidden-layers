# Lesson 2: Building Repeatable Workflows

## From One Good Meal to a Restaurant That Runs Itself

There is a world of difference between a chef who can occasionally produce a brilliant dish and a kitchen that consistently produces excellent food, night after night, for every table. The brilliant dish is talent. The consistent kitchen is a *system* -- standardized preparation, clear station assignments, tested recipes, quality checks, and a workflow that turns individual excellence into repeatable results.

Your AI use should follow the same trajectory. If you are still approaching every AI interaction as a blank slate -- opening a chat, thinking about what to type, crafting a prompt from scratch, evaluating the output -- you are the chef reinventing the dish every night. It works, but it is exhausting and inconsistent.

Repeatable workflows change the game. They turn your best AI interactions into templates you can execute in minutes, with consistent quality, every time. This lesson shows you how to build them.

## The Anatomy of a Repeatable AI Workflow

A good workflow has five components:

**1. Trigger -- What kicks it off?**
A workflow starts with a recurring situation: a weekly report is due, a meeting needs notes organized, a new project requires a research brief, an email needs a thoughtful response. The trigger is the moment you recognize: "I have done this before, and I will do it again."

**2. Template -- What is the standard prompt?**
This is your refined prompt -- the one that includes Role, Context, Task, Constraints, Format, and possibly Examples from Chapter 23. You have tested it. You know it produces good results. You save it somewhere accessible. The next time the trigger fires, you do not start from scratch -- you start from the template.

**3. Customization Points -- What changes each time?**
Even in a repeatable workflow, something changes: the specific meeting, the particular document, the individual email. Your template should have clear placeholders -- [INSERT MEETING NOTES HERE], [RECIPIENT NAME AND RELATIONSHIP], [SPECIFIC TOPIC] -- that you fill in each time. Everything else stays constant.

**4. Quality Check -- How do you verify the output?**
Every workflow should include a defined quality check. For some workflows, that is a quick read-through. For others, it is running the output through the Challenge-and-Improve Loop from Chapter 23. For high-stakes workflows, it might include a specific verification checklist. The quality check is part of the workflow, not an afterthought.

**5. Iteration Log -- How does the workflow improve?**
The best workflows evolve. When you notice the AI consistently makes a certain kind of error or produces a suboptimal output, you update the template. When you discover a new instruction that improves results, you add it. Over time, your workflows get better -- not because the AI improves, but because your templates incorporate accumulated learning.

## Building Your First Workflow: A Step-by-Step Process

Let us build a workflow together, using a task that most professionals face regularly: turning meeting notes into a clear summary with action items.

**Step 1: Do it manually once.**
Open an AI chat and craft the best prompt you can for meeting notes summarization. Include Role, Context, Task, Constraints, and Format. Experiment until you get a result that meets your quality standard.

Let us say you arrive at:

"You are an executive assistant who produces clear, actionable meeting summaries. Your summaries are known for being concise and for capturing decisions and commitments accurately.

I will provide raw meeting notes. Transform them into a structured summary with these sections:
1. Meeting Overview (date, attendees, purpose -- 2 sentences max)
2. Key Decisions (bullet list, each with who decided and any conditions)
3. Action Items (task, owner, deadline if mentioned, priority if inferable)
4. Open Questions (issues raised but not resolved)
5. Context for Next Meeting (what should be on the next agenda)

Rules:
- If something is ambiguous, mark it [CLARIFY]
- If a deadline is implied but not stated, mark it [DEADLINE TBD]
- Do not infer decisions that were not explicitly made
- Keep the entire summary under 400 words

Meeting notes:
[NOTES]"

**Step 2: Test with three different inputs.**
Run this template against three different sets of meeting notes -- ideally ones that represent the range of meetings you typically attend (a project update, a brainstorming session, a decision-making meeting). Evaluate each output. Identify where the template works well and where it needs adjustment.

Perhaps you discover that the model sometimes infers action items that were actually just ideas mentioned in passing. You add a constraint: "Only include action items where someone clearly committed to doing something. Ideas and suggestions go under 'Open Questions' unless explicitly assigned."

**Step 3: Save the refined template.**
Store the template somewhere you can access it quickly. Options include:
- A note in your note-taking app
- A custom instruction or saved prompt in your AI tool (many now support this)
- A text expansion tool that inserts the template with a keyboard shortcut
- A simple document on your desktop

The key is *accessibility*. A template you have to search for is a template you will not use.

**Step 4: Define the quality check.**
For meeting notes, your quality check might be: "Scan the action items. Does each one have an owner? Cross-reference with the raw notes -- did the summary miss any decisions? Does anything marked [CLARIFY] actually have a clear answer in the notes?"

**Step 5: Use it consistently and refine.**
Every time you use the workflow, notice what works and what does not. After a month, review and update the template with your accumulated improvements. This refinement cycle is what transforms a good template into an excellent workflow.

> **"Pro Tip"**
> The biggest barrier to using workflows is the initial time investment in creating them. Here is the shortcut: the next time you have a good AI interaction -- one where the output was exactly what you needed -- immediately save the prompt as a template. Add placeholders for the parts that would change next time. You just created a workflow from a success, with almost no extra effort.

## Workflow Examples Across Common Tasks

Here are five ready-to-adapt workflow skeletons for the most common professional tasks:

**Workflow 1: Email Response**
Trigger: Received an email that requires a thoughtful response
Template: Role (my communication style) + Context (relationship, situation) + Task (respond to this email) + Constraints (tone, length, what to include/avoid) + Format (email) + [paste the email]
Quality check: Does it match my voice? Is the tone right for this relationship? Did it address all points raised?
Typical time: 2 minutes

**Workflow 2: Weekly Status Report**
Trigger: Friday afternoon
Template: Role (project manager summarizing for leadership) + Context (project name, current phase, audience) + Task (create weekly status update) + Constraints (length, focus areas) + Format (specific report template) + [paste this week's notes/updates]
Quality check: Are all key updates included? Is the tone appropriate for the audience? Are any risks understated?
Typical time: 5 minutes

**Workflow 3: Document Review**
Trigger: Receive a document that needs feedback
Template: Role (critical reviewer with specific expertise) + Context (document type, purpose, audience) + Task (review and provide structured feedback) + Constraints (focus areas, feedback format) + Format (tracked-changes style output) + [paste document]
Quality check: Is the feedback specific and actionable? Does it miss any major issues? Is the tone constructive?
Typical time: 5-10 minutes depending on document length

**Workflow 4: Brainstorming Session**
Trigger: Need ideas for a project, campaign, or solution
Template: Role (creative strategist in relevant domain) + Context (the problem, constraints, audience) + Task (generate ideas using the three-tier structure from Chapter 24) + Constraints (number of ideas, practicality requirements) + Format (conventional/creative/wild tiers)
Quality check: Are there at least two ideas I had not considered? Can I combine any for stronger approaches?
Typical time: 3 minutes

**Workflow 5: Learning Session**
Trigger: Need to understand a new concept or skill
Template: Role (adaptive tutor in relevant domain) + Context (my background, what I already know) + Task (teach this concept using analogies from my field) + Constraints (level of depth, learning style) + Format (explanation then comprehension check)
Quality check: Can I explain this concept to someone else in my own words?
Typical time: 10-20 minutes depending on complexity

## The Workflow Library

Over time, you accumulate workflows for every recurring task. This collection becomes your personal **workflow library** -- a curated set of AI interaction patterns that you can execute quickly and consistently.

Organize your library by:
- **Frequency** (daily, weekly, monthly, as-needed)
- **Domain** (writing, analysis, research, admin, learning)
- **Effort level** (quick -- under 2 minutes, standard -- 5-10 minutes, deep -- 20+ minutes)

A well-organized workflow library is worth more than any "ultimate prompt guide" you will find online -- because it is built from your specific needs, tested against your specific standards, and refined through your specific experience.

> **"Behind The Curtain"**
> Professional prompt engineers at companies building AI products use exactly this approach. They do not improvise prompts for each interaction. They maintain libraries of tested, versioned prompt templates that have been refined through hundreds of iterations. The difference between their results and a casual user's results is not talent or secret knowledge -- it is systematic refinement of repeatable workflows. You are now doing the same thing.

## Connecting Workflows: The Compound Effect

The real power of workflows emerges when you connect them. One workflow's output becomes another workflow's input:

**Research workflow** produces a briefing --> **Analysis workflow** evaluates the findings --> **Writing workflow** produces a report --> **Editing workflow** polishes the report --> **Email workflow** sends it to stakeholders.

Each step takes a few minutes. The total pipeline might take 20 minutes. Without workflows, the same sequence would take hours. And because each workflow is tested and refined, the quality is consistent.

This is the compound effect: individual workflows save time, but connected workflows transform your capacity. You are not just doing things faster -- you are doing things that were previously not worth the time investment. A research briefing that would take three hours (and therefore never gets done) now takes fifteen minutes (and becomes a regular habit).

> **"Try This Now"**
> Identify the one task you do most frequently with AI. It might be writing emails, summarizing content, brainstorming, or research. Build a complete workflow for it using the five-component framework above. Use it for the next two weeks, refining the template each time. After two weeks, measure: How much faster is the workflow compared to starting from scratch? How consistent is the output quality? You will likely find that the workflow is at least twice as fast and noticeably more consistent.

---

Repeatable workflows turn occasional AI competence into daily productivity. But there is one more powerful tool for consistency: creating your own system prompts and custom instructions. That is the subject of the next lesson -- where you stop being shaped by someone else's invisible instructions and start writing your own.
