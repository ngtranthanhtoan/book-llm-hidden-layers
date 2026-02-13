# Lesson 3: RLHF and Learned Tradeoff Preferences

## How the AI Learned to Compromise

In the last lesson, we explored the five great conflicts that the AI resolves with every response — accuracy vs. readability, completeness vs. brevity, helpfulness vs. safety, creativity vs. correctness, honesty vs. kindness. We saw that the AI doesn't flip a coin or follow a rigid rulebook. It has *preferences* — default positions on each dial that it gravitates toward unless you push it elsewhere.

But where did those preferences come from? The AI wasn't born with opinions about how honest to be or how much detail to include. Something taught it. And that something is one of the most important — and least understood — innovations in modern AI: Reinforcement Learning from Human Feedback, or RLHF.

This lesson is about how thousands of human judges, sitting at desks around the world, taught the AI which compromises humans prefer. It's a story that will fundamentally change how you understand why the AI behaves the way it does.

## The Taste Test That Shaped an AI

Imagine you're running a restaurant and you've hired a brilliant chef who has mastered every recipe in the world. The chef can cook anything. The problem is, the chef has no idea what customers actually *enjoy*. They can make a technically perfect dish, but they don't know whether customers prefer a bolder seasoning or a subtler one, a larger portion or a refined smaller plate, a traditional presentation or a modern one.

So you run thousands of taste tests. You serve two versions of the same dish to customers and ask: "Which one do you prefer?" Dish A is technically more complex but harder to eat. Dish B is simpler but more satisfying. You record the preference. Then you do it again. And again. Thousands of times, across every type of dish and every type of customer.

Over time, you build a detailed map of human preferences. Not rules — preferences. Tendencies. Patterns. The chef studies this map and gradually adjusts their cooking to align with what people actually want.

That is RLHF. And it is the reason the AI you talk to today feels helpful, conversational, and human-aligned rather than robotic, verbose, and oddly encyclopedic — which is exactly how early language models behaved before RLHF was applied.

## The Three Stages of Training

To understand RLHF, you need to understand that modern AI goes through three distinct training phases. Each one builds on the last, and each one gives the AI something different.

### Stage 1: Pre-training — Learning the Patterns of Language

This is what we covered in Part 1 of this book. The model reads trillions of words from the internet — books, articles, websites, conversations, code — and learns to predict what comes next. After this stage, the model is enormously capable. It knows facts, understands grammar, can write in many styles, and can reason about complex topics.

But it's also... odd. The pre-trained model doesn't know it's supposed to be helpful. It doesn't know it's in a conversation. It has no sense of what a "good" answer looks like versus a merely plausible one. If you ask it a question, it might answer, or it might continue the text as if it were a Wikipedia article, or it might generate something entirely random. It's a chef who has mastered every technique but doesn't know they're running a restaurant.

### Stage 2: Supervised Fine-tuning — Learning the Format of Helpfulness

In this stage, human trainers create thousands of example conversations: a human asks a question, and a human writes the ideal response. The model learns from these examples that it's supposed to be in a conversation, that it should be helpful, that it should answer questions rather than just continue text, and that its responses should have a certain structure and tone.

After this stage, the model feels much more like the AI assistants you're used to. It answers questions, follows instructions, and generally behaves like a helpful assistant. But its responses tend to be generic — safe, middle-of-the-road, one-size-fits-all. It hasn't yet developed *preferences* about how to handle the tradeoffs we discussed in the last lesson.

Think of this as the chef learning from a cookbook of "standard" dishes. They now know they're in a restaurant and should serve food when ordered. But they're cooking by the book, not with any refined sense of what people actually prefer.

### Stage 3: RLHF — Learning What Humans Actually Prefer

This is where the magic happens for our purpose. In this stage, the model generates multiple responses to the same prompt. Human raters — real people, hired and trained for this job — compare the responses and indicate which they prefer. Sometimes they rank multiple responses from best to worst. Sometimes they rate individual responses on specific dimensions: helpfulness, harmlessness, honesty.

These preferences are then used to train a "reward model" — a separate AI that learns to predict how highly a human would rate any given response. This reward model becomes the chef's internal compass for quality. The main model is then trained to generate responses that the reward model would score highly.

The result: the AI develops a finely calibrated sense of what humans want. Not just correct answers — satisfying answers. Not just safe answers — helpfully safe answers. Not just complete answers — appropriately complete answers.

> **"Behind The Curtain" Sidebar**
>
> The scale of RLHF is staggering. Training a single frontier model involves hundreds of thousands of human comparison judgments. These aren't casual opinions — raters follow detailed guidelines, sometimes dozens of pages long, specifying how to evaluate responses across multiple dimensions. Different AI companies have different guidelines, which is one reason their models behave differently on the same tradeoffs. The guidelines are, in effect, a company's philosophy about what "good" AI behavior looks like — written out as a specification that gets translated into mathematical training signals.

## How RLHF Shapes Each Conflict

Now let's connect RLHF directly to the five conflicts from the last lesson. In each case, human raters' preferences during RLHF training are what established the AI's default position on the dial.

### Accuracy vs. Readability

During RLHF, raters consistently preferred responses that were clear and accessible over responses that were technically precise but hard to follow. This doesn't mean they preferred inaccurate responses — they preferred responses that found the sweet spot of "accurate enough and clearly written."

When shown two responses to a medical question — one using dense clinical language and one explaining the same information in plain English — raters overwhelmingly chose the plain English version. The AI learned: readability matters more than most people would admit when asked in the abstract.

This is why AI responses tend to err toward accessibility. The RLHF training data said, again and again: "Humans prefer the clearer version."

### Completeness vs. Brevity

This one is fascinating because the preference shifted depending on the type of request. For quick factual questions ("What's the capital of France?"), raters strongly preferred brief responses. For complex questions ("How should I approach a career change?"), raters preferred more thorough responses — but with a ceiling. Responses that went beyond a certain length were rated lower even when all the additional information was relevant.

The AI learned a nuanced preference: be as brief as possible for simple requests, be thorough for complex ones, but never go longer than the user seems to want. This is why you get different response lengths for different types of questions without ever specifying how long you want the answer to be.

### Helpfulness vs. Safety

This is where RLHF gets most interesting — and most controversial. Raters were given detailed guidelines about what constituted "safe" versus "unsafe" responses. They were trained to penalize responses that provided genuinely dangerous information but also to penalize responses that refused harmless requests unnecessarily.

The result was a model that learned a nuanced threshold: help with everything that isn't genuinely dangerous, refuse what is, and handle the gray area with careful judgment. The specific position of that threshold varies by company — some train their models to be more cautious, others more permissive. This single training choice is responsible for a huge amount of the behavioral difference between different AI assistants.

> **"This Is Why..." Box**
>
> **This is why different AI assistants have noticeably different "personalities" even though they're based on similar technology.** Claude, ChatGPT, Gemini, and others all use variations of RLHF, but with different human raters, different rating guidelines, and different company philosophies about where to set the dials. When Claude feels "more cautious" or ChatGPT feels "more creative" or Gemini feels "more concise," you're experiencing the downstream effects of different RLHF training choices. The technology is similar; the human preferences baked in are not.

### Creativity vs. Correctness

Raters tended to reward creativity when it was warranted — brainstorming, creative writing, idea generation — but punished it when accuracy mattered. Speculative suggestions in a creative brainstorm were rated positively. The same speculative tone in a factual answer was rated negatively.

The AI learned to be context-sensitive about creativity: match the level of creative risk to the type of task. This is actually one of RLHF's great successes — the model developed a surprisingly good sense of when to be conventional and when to be inventive.

### Honesty vs. Kindness

This was the most complex preference for raters. Guidelines typically instructed them to prefer honest responses — but not brutally honest ones. The ideal was "respectful honesty" or "constructive candor." Raters penalized responses that were dishonestly flattering and responses that were unnecessarily harsh. They rewarded the middle ground: truthful, direct, but delivered with empathy.

The AI learned what you might call "diplomatic honesty" as its default — it tells you the truth but wraps it in considerate language. This is why the AI will tell you your business plan has weaknesses but won't call it "terrible," even if it is. The RLHF training data said: humans prefer truth delivered with care.

## The Raters Behind the Curtain

It's worth pausing to consider what this means. The AI's personality — its default level of caution, its tendency toward encouragement, its preference for structured responses, its diplomatic honesty — all of this was shaped by the preferences of a specific group of human raters.

Who are these raters? They're typically contractors, often with college educations, working for companies that specialize in data labeling. They come from diverse backgrounds but skew toward certain demographics. They follow training guidelines written by AI company employees. And their collective preferences become the AI's personality.

This raises profound questions. Whose preferences should be baked into an AI that billions of people use? Should the same defaults apply in every culture, every context, every use case? These are active debates in the AI community, and understanding RLHF helps you understand why the debates matter.

For our purposes as users, the practical implication is this: the AI's default behavior isn't neutral or universal. It reflects specific human preferences from a specific training process. When the AI's default position on a conflict dial doesn't match your preference, it's not because your preference is wrong — it's because the training data emphasized a different position.

> **"Behind The Curtain" Sidebar**
>
> A surprising finding from RLHF research: human raters exhibit systematic biases that get baked into the model. For example, raters tend to prefer longer responses, even when shorter ones are equally good — a phenomenon researchers call "verbosity bias." They prefer responses with confident language over ones that hedge appropriately. They prefer responses that include lists and formatting over equally good responses in plain paragraphs. The AI inherits all of these biases. This is why AI responses tend to be longer than necessary, more confident than warranted, and more heavily formatted than you asked for. These aren't bugs in the AI — they're reflections of human rater preferences.

## Beyond RLHF: Constitutional AI and Self-Training

RLHF isn't the only approach. Some companies, notably Anthropic (the maker of Claude), have developed an approach called Constitutional AI, where instead of relying entirely on human raters, they write a set of principles — a "constitution" — and have the AI evaluate its own responses against those principles.

Think of the difference this way. Traditional RLHF is like hiring taste-testers and letting their collective preferences guide the chef. Constitutional AI is more like giving the chef a detailed food philosophy document — "We believe in using fresh ingredients, balancing flavors, respecting dietary restrictions, and never compromising food safety" — and training the chef to evaluate their own dishes against those principles.

Both approaches work. Both produce models that handle tradeoffs well. But they produce subtly different results, because the principles in a constitution are explicit and consistent, while human rater preferences are implicit and variable. This is another reason different AI assistants "feel" different — they were trained to resolve conflicts using different methods.

## The Feedback Loop: How You Continue the Training

Here's something that brings this full circle: RLHF doesn't stop when the model is released. Every time you give a thumbs up or thumbs down to an AI response, every time you regenerate a response and pick the better version, every time you provide feedback — you're contributing to the next round of preference data.

Your reactions, aggregated with millions of other users' reactions, influence how future models resolve the five great conflicts. When enough users indicate that a particular default resolution isn't working — too cautious, too verbose, too diplomatic — the next model version adjusts.

You are, in a very real sense, one of the taste-testers in the ongoing restaurant feedback loop. Your preferences shape the AI that everyone uses.

> **"Try This Now" Exercise**
>
> The next time you use an AI and get a response that isn't quite right, instead of immediately reprompting, pause and diagnose. Ask yourself: "Which dial is in the wrong position? Is the AI being too cautious? Too verbose? Too diplomatic? Too creative? Too conservative?" Then, when you give feedback (thumbs up/down, regenerating the response, or adjusting your prompt), you're not just fixing this one interaction — you're casting a tiny vote about how the AI should handle this type of conflict in the future. Try deliberately using the feedback buttons more often, knowing that they influence training.

## What This Means for You

Understanding RLHF gives you three practical advantages:

**First**, you understand that the AI's defaults are preferences, not laws. When the AI resolves a conflict in a way you don't like, you can push back. The defaults are starting positions, not final answers.

**Second**, you understand that different AI products have different defaults because of different training choices. If one AI assistant frustrates you on a particular type of request, another might handle it better — not because of better technology, but because of different RLHF preferences.

**Third**, you understand that these defaults change over time. The AI you use today resolves tradeoffs differently than the version from six months ago, because new rounds of RLHF have updated its preferences. This is why tips and tricks from older AI guides sometimes stop working — the underlying preferences shifted.

The intent stack isn't fixed. It's learned, it's specific to each AI product, and it's constantly evolving. In the next lesson, we'll put all of this knowledge to work — learning how to explicitly steer the stack to get exactly the responses you want.
