# Lesson 3: Few-Shot Prompting -- Showing What You Want

## The Apprentice Principle

Imagine you are training a new employee. You could spend twenty minutes explaining in precise, abstract terms exactly how you want your weekly status reports formatted -- the tone, the level of detail, which metrics to include, how to handle bad news, the length of each section. Or you could hand them two examples of excellent status reports and say, "Like this."

Which approach gets you a better result faster?

The second one. Almost always. And it works for the same reason with AI.

This technique is called **few-shot prompting** -- providing one or more examples of the output you want within your prompt. The "shots" are the examples. "Zero-shot" means no examples (just instructions). "One-shot" means one example. "Few-shot" means two to five examples. And understanding *why* it works, now that you have X-ray vision into the model's processing, will make you exceptionally good at it.

## Why Examples Are Magic (The Hidden Layer Explanation)

The reason few-shot prompting works so powerfully connects directly to the model's core mechanism: next-token prediction based on context.

When you provide an example in your prompt, that example becomes part of the context the model uses to predict every subsequent token. The model's attention mechanism identifies the patterns in your example -- the structure, the vocabulary, the level of detail, the transformations applied, the tone -- and generates output that follows those same patterns.

Think of it this way. If the model's context contains this:

```
Input: cloudy skies, 65 degrees
Output: Grab a light jacket. Might drizzle, but you'll be fine for a walk.

Input: heavy rain, 45 degrees
Output: Stay inside with a book if you can. If you must go out, full rain gear.

Input: clear skies, 82 degrees
Output:
```

The model does not need any instruction about what to do. The pattern is self-evident from the examples: take weather conditions and generate a casual, practical recommendation. The model will generate something like "Sunscreen, hat, and a cold drink. Perfect day to be outside." It matched the tone, the format, the length, and the purpose -- all learned from the examples alone.

This is far more efficient than trying to describe the same output style in words: "Generate a casual weather recommendation that is two sentences long, practical in nature, conversational in tone, and addresses both what to wear and what activity suits the weather." That description is longer than the examples, and the model is more likely to drift from it.

> **"Behind The Curtain"**
> Few-shot prompting works because the model treats the examples as the most recent and most relevant patterns in its context. The attention mechanism gives high weight to patterns that appear in the current prompt -- even higher than patterns from the trillions of training tokens. In a sense, your examples temporarily "reprogram" the model's output distribution for the duration of this interaction. This is why a single good example can be more influential than a paragraph of instructions.

## Zero-Shot vs. One-Shot vs. Few-Shot

Let us see the difference with a practical task: translating accounting skills into UX-relevant descriptions for a resume.

**Zero-shot (no examples, just instructions):**
"Translate the following accounting skills into UX-relevant descriptions for a resume. Make them sound relevant to UX design roles. Skills: budget forecasting, stakeholder presentations, compliance documentation, data reconciliation."

**Result:** The model will produce something reasonable, but the format, level of detail, and transformation style are entirely up to its default patterns. You might get single sentences, you might get paragraphs, you might get bullet points. The tone might be formal resume-speak or conversational.

**One-shot (one example):**
"Translate accounting skills into UX-relevant descriptions. Here is an example:

Accounting: Financial data analysis and reporting
UX version: Quantitative Research & Data-Driven Design | Analyzed complex datasets of 10,000+ transactions to identify user behavior patterns. Translated quantitative findings into visual narratives for executive stakeholders, a skill directly applicable to presenting UX research findings and metrics.

Now translate these:
- Budget forecasting and planning
- Stakeholder presentations
- Compliance documentation
- Data reconciliation"

**Result:** The model now has a concrete template. It knows the output should include a bold UX-framed title, a specific achievement with numbers, and an explicit bridge to UX relevance. Every translation will follow this pattern.

**Few-shot (multiple examples):**
"Translate accounting skills into UX-relevant descriptions. Here are two examples:

Accounting: Financial data analysis and reporting
UX version: Quantitative Research & Data-Driven Design | Analyzed complex datasets of 10,000+ transactions to identify user behavior patterns. Translated quantitative findings into visual narratives for executive stakeholders.

Accounting: Client relationship management and advisory
UX version: Stakeholder Management & User Advocacy | Managed relationships with 30+ corporate clients, translating their complex financial needs into clear, actionable recommendations. Expert at balancing competing stakeholder priorities -- the core challenge of UX design.

Now translate these:
- Budget forecasting and planning
- Compliance documentation
- Data reconciliation
- Process improvement and automation"

**Result:** With two examples, the model has an even more robust pattern. It sees that the transformation involves: (1) reframing the skill name in UX terminology, (2) citing specific numbers or scale, (3) making an explicit connection to UX work, and (4) maintaining a confident, achievement-oriented tone. The consistency across four translations will be higher than with one example.

> **"This Is Why..."**
> This is why the AI sometimes formats its response in a way you did not expect. Without examples, the model defaults to whatever format was most common in its training data for similar tasks. With examples, you override that default and impose your own format. If you have ever received a response that was technically correct but structured wrong, examples are the fix.

## The Art of Choosing Good Examples

Not all examples are equally effective. Here is what makes a few-shot example work well.

**1. The example should be representative, not exceptional.**
Choose an example that represents the typical case, not the most unusual one. If most of your accounting skills map neatly to UX, do not use the one weird edge case as your example. The model will try to match the difficulty and transformation style of your example.

**2. The example should show the transformation, not just the output.**
The power of few-shot prompting comes from the model seeing both the input *and* the output. When it sees the mapping from input to output, it learns the transformation logic -- not just what good output looks like, but how to get from A to B.

**3. The example should match the complexity of the real task.**
If your real inputs are complex, your example should be complex too. If you show a simple example but then give the model a complex input, it might oversimplify. Match the difficulty level.

**4. Two or three examples are usually the sweet spot.**
One example establishes a pattern. Two examples confirm it and add nuance. Three examples give the model very high confidence in the pattern. Beyond three, you get diminishing returns and start consuming context window space that could be used for other ingredients.

**5. Diverse examples teach flexibility.**
If you give three examples that are all identical in structure, the model learns a rigid template. If your three examples show slight variations -- different lengths, different emphasis, different edge cases -- the model learns a more flexible pattern. Choose examples that collectively cover the range of what you want.

> **"Pro Tip"**
> If you find yourself spending a lot of time writing instructions and still getting inconsistent output, stop writing instructions and write one good example instead. The cognitive effort is similar, but examples communicate format, tone, structure, level of detail, and transformation logic simultaneously -- things that are extremely tedious to describe in words but immediately obvious from a sample.

## Advanced Few-Shot Techniques

Once you understand the basic principle, you can use few-shot prompting in more sophisticated ways.

**Technique 1: Positive and Negative Examples**

Show the model both what you want *and* what you do not want.

"Rewrite these meeting notes into a clear summary.

GOOD example:
Meeting notes: 'talked about Q3 numbers, Sarah mentioned the dip in retention, we need to fix onboarding, John will look into it'
Summary: The team reviewed Q3 performance and identified customer retention as a key concern. Sarah highlighted a retention dip, attributing it to onboarding issues. Action item: John will investigate and propose onboarding improvements.

BAD example (do NOT do this):
Summary: The team had a meeting about Q3. They discussed retention. John will fix onboarding.

The bad example is too vague, lacks attribution, and converts an investigation task into a definitive assignment. Aim for the style of the GOOD example."

Negative examples are powerful because they activate the model's constraint-tracking mechanisms. The model actively avoids patterns it has been shown as undesirable.

**Technique 2: Chain-of-Thought Examples**

Instead of just showing input and output, show the reasoning process in between.

"Evaluate whether this business idea is viable.

Example:
Idea: A subscription box for exotic spices, targeting home cooks who want to explore global cuisines.
Thinking: The target market (home cooks interested in global food) is growing -- cooking shows, food blogs, and social media have driven interest. Subscription box fatigue is real, but spices are consumable (not another candle or sock), so there is genuine repeat need. The economics: spices have high margins, shipping is cheap (lightweight), and sourcing is straightforward. Main risk: differentiation -- several spice subscription services already exist. This would need a strong content angle (recipes, cultural context, video tutorials) to stand out.
Verdict: Viable with differentiation. Focus on the educational and cultural storytelling angle rather than just the product.

Now evaluate:
Idea: An AI-powered personal finance app that automatically categorizes expenses and suggests budget adjustments based on spending patterns."

The chain-of-thought example does not just show the model what the output looks like -- it shows the model *how to think about the problem*. The model will mirror the reasoning structure: identify the market, evaluate the economics, assess differentiation, identify risks, and deliver a verdict.

**Technique 3: Progressive Examples**

Use examples that build on each other, showing increasing complexity.

This works well when you want the model to handle a range of inputs, from simple to complex. By showing a simple example first and a more complex one second, you teach the model how to scale its response to match the input's complexity.

## Few-Shot Prompting for Our Running Example

Let us apply this to the career change scenario, using few-shot prompting to create an interview preparation tool.

"I want to practice answering UX interview questions. For each question, give me:
1. Why the interviewer is asking (what they are really evaluating)
2. A framework for structuring my answer
3. A sample answer that leverages my accounting background

Example:

Question: Walk me through your design process.
Why they are asking: They want to see that you have a structured approach and can articulate your thinking, not just show pretty deliverables. They are also checking if you understand that design is iterative.
Framework: Start with understanding the problem (research), move to defining the problem (synthesis), then explore solutions (ideation), build something testable (prototyping), and learn from real feedback (testing). Emphasize iteration.
Sample answer leveraging accounting: 'My process mirrors the audit methodology I used for eight years: first, understand the full picture before jumping to conclusions. In accounting, we call it the planning phase -- scoping the engagement, understanding the business, identifying risk areas. In UX, I start with user research and stakeholder interviews for the same reason: you cannot solve a problem you do not fully understand. Then I define the problem clearly -- in accounting, this was the audit finding; in UX, it is the problem statement. From there, I explore solutions through ideation and prototyping, test them with users, and iterate. The discipline of verifying assumptions before drawing conclusions? That is not something I had to learn for UX -- I brought it with me from eight years of audit work.'

Now give me the same three-part breakdown for these questions:
1. Tell me about a time you used data to inform a design decision.
2. How do you handle disagreements with stakeholders?
3. Why are you transitioning from accounting to UX design?"

This prompt uses one detailed example to establish a precise pattern -- three components, a specific level of depth, and a clear requirement to bridge the accounting background. The model will follow this pattern for all three subsequent questions.

> **"Try This Now"**
> Pick a task you do regularly -- writing emails, creating summaries, analyzing data, generating ideas. Take one output you created recently that you are proud of. Use it as a one-shot example in your next prompt. Notice how the AI's output immediately matches the quality, tone, and structure of your example. You have just taught the model your personal standard without writing a single line of instruction.

## When Not to Use Few-Shot Prompting

Few-shot prompting is powerful, but it is not always the right tool.

**Do not use examples when you want genuine creativity.** If you are brainstorming and want surprising, unexpected ideas, examples will anchor the model to the patterns you showed. You will get variations on your examples rather than genuinely novel approaches. For creative tasks, sometimes zero-shot with a clear task statement produces more interesting results.

**Do not use examples when they will consume too much context.** If your examples are very long (say, 500 words each) and you need to provide three of them, you have just used 1,500 words of context space on examples alone. For models with smaller context windows, this might not leave enough room for the actual task. Be strategic about example length.

**Do not use examples that are not representative.** A misleading example is worse than no example. If your example shows an edge case, the model will treat the edge case as the norm. If your example has a mistake, the model might replicate the mistake.

## The Power of Showing Over Telling

Here is the deepest insight about few-shot prompting, now that you understand the hidden layers: *the model is fundamentally a pattern-matching and pattern-continuing engine.* Its entire architecture -- the attention mechanism, the layer-by-layer processing, the autoregressive generation -- is optimized for identifying patterns in context and extending them.

When you write instructions, you are asking the model to *interpret* your instructions and then *generate* matching output. That is two steps, and things can go wrong at either step.

When you provide an example, you are giving the model a pattern to *continue directly*. That is one step. The pattern is right there in the context, and the model's entire architecture is designed to do exactly this -- see a pattern and extend it.

This is why a mediocre example often outperforms an excellent description. You are playing to the model's fundamental strength.

---

You now understand the anatomy of a prompt and the power of examples. But the most skilled AI users know something else: that the best results rarely come from a single prompt, no matter how well crafted. In the final lesson of this chapter, we will explore the iterative approach -- treating AI as a conversation, not a search engine.
