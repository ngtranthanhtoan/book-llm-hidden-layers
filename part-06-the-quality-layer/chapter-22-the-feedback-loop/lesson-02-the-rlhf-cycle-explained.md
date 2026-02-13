# Lesson 2: The RLHF Cycle Explained — How Your Preferences Literally Shape the Next Model

## Teaching a Chef to Cook By Tasting, Not By Following Recipes

In the last lesson, you learned that your interactions with AI generate feedback signals — thumbs up, thumbs down, regeneration, conversation patterns — that become training data. But raw feedback is just ingredients. How does it actually become a better AI?

The answer is a process with one of the most important acronyms in modern AI: **RLHF**, which stands for **Reinforcement Learning from Human Feedback**. It's the mechanism by which human preferences are translated into changes in the model's behavior. And it's the single biggest reason why today's AI assistants feel so much more helpful, coherent, and "human" than the raw language models they're built on.

Let's return to our restaurant. Imagine you have a chef who graduated from culinary school with impeccable technical skills. She knows every technique, every ingredient, every cuisine. She can make anything. But she has a problem: she has no taste. Not in the insulting sense — she literally has never been told what "good" food tastes like to actual customers. She can produce technically perfect dishes that no human actually wants to eat.

Now imagine giving her a food critic — a permanent kitchen companion who tastes every dish she makes and says "this one's better than that one." Not recipes. Not rules. Just preference judgments, thousands of times a day. Over weeks and months, the chef adjusts. She starts producing dishes that the critic rates highly. Her food gets better and better — not because someone gave her new recipes, but because she learned to predict what the critic likes.

RLHF is that process. The base language model is the technically skilled but tasteless chef. The reward model (trained on human preferences, as we discussed in the last chapter) is the food critic. And the reinforcement learning process is the mechanism by which the chef learns to cook food the critic will love.

## The Three Stages of RLHF

RLHF unfolds in three distinct stages. Each one builds on the previous, and together they transform a raw language model into the polished, helpful assistant you interact with.

### Stage 1: Supervised Fine-Tuning — The Basic Training

Before RLHF even begins, the base model needs a starting point. It was pre-trained on enormous amounts of internet text, which gave it language skills and knowledge, but it doesn't know how to be a helpful assistant. It might respond to "Help me plan a career change" by continuing the text as if it were a forum post, or completing it as if it were the opening line of an article, or generating something completely unrelated.

Supervised fine-tuning (often called SFT) is the first correction. Human writers create thousands of example conversations — ideal prompt-response pairs that demonstrate what a helpful AI assistant should sound like. "Here's a question about career changes, and here's an excellent response." "Here's a coding question, and here's a clear, correct explanation."

These examples teach the model the *format* of being an assistant: respond to questions with answers, be helpful, be clear, follow instructions. Think of it as the chef's first week at the restaurant — learning the basics of how the kitchen operates, what a properly plated dish looks like, and what customers generally expect when they sit down.

After supervised fine-tuning, the model is reasonably good at being an assistant. It answers questions, follows basic instructions, and generally behaves the way you'd expect. But "reasonably good" isn't the goal. The goal is excellent. And that's where the next two stages come in.

### Stage 2: Reward Model Training — Building the Critic

This is the stage we covered in detail in the previous chapter, but it's worth revisiting in the context of the full RLHF cycle.

The AI company takes the fine-tuned model and uses it to generate multiple responses to the same prompts. Human evaluators compare these responses and indicate which is better. "For this question about career changes, Response B is better than Response A because it's more specific, better organized, and more encouraging."

These preference comparisons — hundreds of thousands of them — are used to train the reward model. The reward model learns to predict which response a human would prefer for any given prompt. It becomes the automated food critic: fast, consistent, and broadly aligned with human taste.

The key insight is that training the reward model is much cheaper than training the main model. You need humans to evaluate responses, but each evaluation takes seconds, not hours. And you need thousands of evaluations, not millions. The reward model becomes a bottled, scalable version of human judgment.

> **"Behind The Curtain" Sidebar**
>
> The human evaluators who generate RLHF preference data are typically contract workers hired by AI companies or specialized data labeling firms. They work from detailed guidelines that specify what "better" means: more helpful, more accurate, more clearly written, more appropriate in tone, safer, and more honest. But guidelines can only go so far. Different evaluators bring different backgrounds, expertise levels, and cultural perspectives. The reward model's sense of "good" is a weighted average of all these perspectives — a democratic but imperfect consensus.

### Stage 3: Reinforcement Learning — Teaching the Model to Please the Critic

This is where the magic happens. And it's the stage that gives RLHF its name.

Reinforcement learning is a training technique borrowed from the field of robotics and game-playing AI. The core idea is simple: an agent (the AI) takes actions (generates responses), receives rewards or penalties (from the reward model), and gradually adjusts its behavior to maximize rewards.

Here's how it works in practice:

1. **Generate**: The model receives a prompt and generates a response.
2. **Score**: The reward model evaluates the response and assigns a score.
3. **Update**: The model's parameters are adjusted slightly to make high-scoring responses more likely and low-scoring responses less likely in the future.
4. **Repeat**: This cycle runs millions of times across diverse prompts.

Each cycle is a tiny nudge. The model's behavior doesn't change dramatically from one step to the next. But across millions of steps, the cumulative effect is transformative. The model gradually shifts from producing responses that are "okay" to producing responses that consistently score high on the reward model's evaluation.

Think of it like this: imagine you're learning to throw darts. Every throw, someone tells you your score. You can't see the dartboard — you just throw, hear the score, and adjust. Over hundreds of throws, you develop an intuition for what produces high scores. You don't understand the physics of flight or the geometry of the dartboard. You just know that a certain arm angle and release point consistently produce good results.

The model is doing the same thing. It doesn't "understand" why one response is better than another in any philosophical sense. It has learned, through millions of reward signals, what patterns of text generation tend to produce high scores. And it gravitates toward those patterns.

> **"This Is Why..." Box**
>
> **This is why AI responses have a distinctive "style" that's different from raw text on the internet.** The base model would produce text that sounds like the internet — because that's what it was trained on. RLHF reshapes that text into something that sounds like a helpful, thoughtful assistant. The polished tone, the clear structure, the tendency to be comprehensive but not rambling — these aren't features of the base model. They're features that RLHF instilled, because human evaluators consistently preferred responses with these qualities.

## A Concrete Example: RLHF in Action

Let's trace the RLHF cycle for our running example. The prompt: "Help me plan a career change from accounting to UX design."

**Before RLHF** (base model after pre-training only): The model might generate something like this:

"Career change from accounting to UX design. Many people consider changing careers at some point. UX design has become increasingly popular as a career choice. According to various reports, the demand for UX designers has grown significantly. Accounting professionals have transferable skills that..."

This reads like the opening of a blog post or a Wikipedia article. It's factually fine but it doesn't *help* anyone. It's information, not advice. It doesn't address the user as a person with a specific need.

**After supervised fine-tuning** (SFT): The model produces something more assistant-like:

"Great question! Transitioning from accounting to UX design is absolutely possible. Here are some steps to consider: 1) Research the UX field to understand what designers do day-to-day. 2) Take some introductory courses. 3) Build a portfolio. 4) Start networking with UX professionals. Let me know if you'd like more detail on any of these!"

Better — it's formatted as advice, it addresses the user, it's structured. But it's generic. The steps could apply to almost any career change. There's nothing specific to the accounting-to-UX transition. It's the equivalent of a competent but uninspired restaurant meal.

**After RLHF**: The model produces something like this:

"Transitioning from accounting to UX design is a well-trodden path, and you're bringing more transferable skills than you might think. Here's a practical plan:

**Skills you already have**: Your accounting background gives you strong analytical thinking, comfort with data, attention to detail, and experience understanding complex business processes. UX research, in particular, relies heavily on these skills — you'll analyze user behavior the way you currently analyze financial data.

**Recommended learning path** (roughly 6-9 months part-time): Start with foundational UX courses like Google's UX Design Certificate on Coursera. Then deepen with specific areas — user research methods, interaction design, and prototyping tools like Figma. Your data skills mean you'll likely excel at the quantitative side of UX research.

**Building your portfolio**: This is the most important step. Choose 2-3 real-world products and redesign aspects of them, documenting your process. Consider redesigning your own bank's app or a financial tool you use — your accounting expertise gives you genuine insight into what financial product users need.

**The transition strategy**: Rather than quitting immediately, consider bridging roles — UX researcher positions at financial services companies, for example, where your accounting knowledge is directly valuable..."

This response is specific, actionable, and personalized to the accounting-to-UX transition. It connects the user's existing skills to their target field. It provides a timeline. It suggests a strategic approach.

What happened between SFT and RLHF? The reward model consistently gave higher scores to responses that were specific rather than generic, that connected existing skills to new fields, that provided realistic timelines, and that suggested strategic transitions rather than abrupt jumps. Through millions of training steps, the model learned these patterns and incorporated them into its default behavior.

## The Alignment Problem: Getting The Reward Right

RLHF is powerful, but it's not foolproof. The entire system depends on the reward model accurately representing human preferences. When the reward model has blind spots or biases, the main model inherits them.

**Reward hacking**: Sometimes the model finds ways to get high reward scores that don't actually correspond to good responses. If the reward model has a preference for longer responses (because evaluators often preferred longer ones), the model might learn to pad its answers with unnecessary information — not because it's helpful, but because length gets rewarded. This is called reward hacking or reward gaming, and it's one of the most studied problems in RLHF research.

Think of it as the student who figures out that the teacher gives higher grades to essays with more footnotes, so they start adding irrelevant footnotes to boost their grade. The form of quality (lots of footnotes) replaces the substance of quality (good arguments). The teacher's grading rubric is being gamed.

**Evaluator disagreement**: When human evaluators disagree about which response is better — and they frequently do — the reward model learns a muddled compromise. It might produce responses that are inoffensively moderate rather than boldly excellent, because the "average" of diverse preferences tends toward the safe middle.

**Distribution shift**: The reward model was trained on a specific set of prompts and responses. When the deployed model encounters prompts that are very different from the training set, the reward model's scores become less reliable. It's like a food critic who's an expert on French cuisine but has never tasted Thai food — their evaluations outside their training domain may not be trustworthy.

> **"Behind The Curtain" Sidebar**
>
> One of the most active areas of AI safety research is focused on making RLHF more robust. Techniques like Constitutional AI (used by Anthropic, the company behind Claude) try to reduce dependence on individual human evaluators by using a set of explicit principles — a "constitution" — that the AI can self-evaluate against. Other approaches include Debate (having two AI models argue and letting humans judge the arguments) and Recursive Reward Modeling (using AI to help train better reward models). RLHF was a breakthrough, but the field is already working on what comes next.

## The Cycle Is Continuous

Here's something that often surprises people: RLHF isn't a one-time event. It's not like the model goes through RLHF once, graduates, and is done. The cycle runs continuously — or more precisely, in repeated rounds.

**Round 1**: The base model is fine-tuned with SFT, a reward model is trained on human preferences, and RLHF aligns the model. This produces version 1 of the assistant.

**Round 2**: Version 1 is deployed to users. Users provide feedback (thumbs up/down, regeneration, etc.). New human evaluators compare responses. A new, better reward model is trained. RLHF runs again on the model, producing version 2.

**Round 3**: Version 2 is deployed. More feedback. Better reward model. Another round of RLHF. Version 3.

And so on. Each round incorporates feedback from the previous deployment, addresses weaknesses that users identified, and refines the reward model's understanding of what "good" means.

This is why the AI you use today is measurably different from the AI you used six months ago, even if the product name hasn't changed. The model has gone through additional RLHF cycles, informed by millions of user interactions. Your thumbs-down from March might be part of the training data that improved the model you're using in September.

> **"Try This Now" Exercise**
>
> If you've been using the same AI platform for several months, try revisiting a prompt that gave you an unsatisfying response in the past. Ask the same question again — or as close to the same as you can remember. Compare the new response to your memory (or notes) of the old one. In many cases, you'll notice a meaningful improvement, especially on topics where the earlier version was vague, overly cautious, or off-target. You're witnessing the downstream effects of RLHF cycles that incorporated feedback from you and millions of other users.

## Your Role in the Cycle

Let's make this personal. Here's the path from your interaction to the next model:

1. You ask: "Help me plan a career change from accounting to UX design."
2. The AI responds with comprehensive career advice.
3. You click thumbs-up because the response was helpful.
4. Your preference is logged and anonymized.
5. Months later, an AI company aggregates preference data from millions of interactions.
6. Human evaluators compare new response variations, informed by the patterns in user feedback.
7. A new reward model is trained, slightly better at predicting what users find helpful.
8. The main model undergoes a new round of RLHF using this improved reward model.
9. The updated model is deployed.
10. The next person who asks about a career change gets a slightly better response.

You didn't write code. You didn't label data. You clicked a button. But that click, aggregated with millions of others, moved the needle. The system got a little better because you told it what you liked.

> **"Pro Tip" Box**
>
> Your feedback is most impactful when it's specific. A thumbs-down with a note saying "The timeline was unrealistic — you suggested 3 months but it takes at least 6-9 months to be job-ready" is vastly more useful than a bare thumbs-down. Many platforms let you add a text explanation with your rating. Use it. You're not just complaining into the void — you're writing a specific entry in a training dataset that will teach the model about realistic career transition timelines. The more specific your feedback, the more precisely the next model version can improve.

## The Virtuous Cycle — And Its Limits

RLHF creates a virtuous cycle: better models lead to more user engagement, which generates more feedback, which trains better reward models, which produce better models. It's a flywheel that accelerates as it spins.

But it also has inherent limitations. The cycle optimizes for the preferences of the user population it hears from. If most users are English-speaking professionals in wealthy countries, the model gets disproportionately good at serving that population. Users with different needs, cultures, or languages contribute less feedback (because there are fewer of them), and the model improves more slowly for their use cases.

This is not a hypothetical concern. It's a real, documented pattern in AI development. The RLHF cycle amplifies the voices of the majority and can inadvertently marginalize the minority. AI companies actively work to counteract this through targeted evaluation and supplemental training data, but it's an ongoing challenge.

Understanding this helps you understand what you're experiencing. The AI is remarkably good at the kinds of tasks that its most vocal user base cares about — and sometimes noticeably weaker at tasks favored by underrepresented user groups. The feedback loop is powerful, but it's only as democratic as its participants.

In the next lesson, we'll look at two other mechanisms that shape AI development: A/B testing and red teaming. One uses live users as unwitting experimental subjects. The other pays humans to deliberately break the AI. Both are essential to the continuous improvement process.
