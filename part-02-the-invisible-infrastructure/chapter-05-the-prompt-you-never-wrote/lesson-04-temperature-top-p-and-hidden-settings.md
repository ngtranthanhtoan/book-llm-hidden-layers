# Lesson 4: Temperature, Top-p, and Hidden Settings

## The Dials Behind the Curtain

Imagine you are watching a jazz musician perform. Some nights, she plays it straight -- precise renditions of classic standards, every note exactly where you expect it. Other nights, she is adventurous -- improvising wildly, taking unexpected detours, surprising you with combinations you have never heard before. Same musician, same instrument, same songs. But someone turned a dial, and the entire performance changed.

Language models have dials too. They are invisible to most users, set by the companies that deploy the AI, and they fundamentally alter the character of every response you receive. The most important of these dials is called **temperature** -- and once you understand it, you will never look at AI responses the same way again.

## Temperature: The Creativity Dial

Recall from Part 1 that a language model generates text by predicting the next token. At each step, the model calculates a probability for every possible next token in its vocabulary -- roughly 100,000 options. These probabilities create a landscape: some tokens are highly likely (tall peaks), and others are extremely unlikely (deep valleys).

Temperature controls how the model navigates this landscape.

**Low temperature (close to 0):** The model almost always picks the single highest-probability token. It walks along the ridgeline, always choosing the safest, most predictable path. The result is focused, consistent, and repetitive. Ask the same question twice with temperature near zero, and you will get nearly identical answers.

Think of it like ordering at a restaurant where the chef always makes their signature dish exactly the same way. Reliable. Predictable. Sometimes a little boring.

**High temperature (close to 1 or above):** The model becomes more willing to pick lower-probability tokens. It wanders off the ridgeline, exploring valleys and side trails. The result is more creative, more varied, and sometimes surprising. But it can also be incoherent, tangential, or nonsensical -- because some of those low-probability tokens were low-probability for good reason.

This is the chef on their wild night, throwing unexpected ingredients together. Sometimes genius. Sometimes a disaster.

**The sweet spot** for most AI applications is somewhere in the middle -- typically between 0.5 and 0.9. High enough to avoid robotic repetition, low enough to avoid creative chaos.

> **"Behind The Curtain"**
> Most consumer AI products set their temperature somewhere between 0.7 and 1.0, but users never see this setting and cannot change it in the standard interface. When you use the API directly (the programmer's way of accessing the same model), temperature is one of the first parameters you can adjust. This means developers building apps on top of these models have a level of control over AI behavior that regular users do not even know exists.

## A Concrete Example

Let us make this tangible. Suppose the model is generating a response to "Help me plan a career change from accounting to UX design" and has just written: "The first step in your career transition is to..."

At this point, the model calculates probabilities for the next word. The landscape might look roughly like this:

- "understand" -- 25% probability
- "assess" -- 18% probability
- "identify" -- 15% probability
- "research" -- 12% probability
- "evaluate" -- 8% probability
- "explore" -- 6% probability
- "recognize" -- 3% probability
- "embrace" -- 1.5% probability
- "demolish" -- 0.001% probability

At **low temperature**, the model picks "understand" almost every time. The response will be sensible but predictable.

At **medium temperature**, the model might pick "understand" most of the time but occasionally selects "research" or "explore" -- reasonable alternatives that add variety.

At **high temperature**, the model might occasionally pick "embrace" -- an unusual but potentially interesting choice. And in very rare cases at extreme temperatures, it might even pick "demolish" -- which makes no sense here and would lead the response off a cliff.

This is the fundamental tradeoff of temperature: variety versus reliability. And it is happening at every single token position, hundreds or thousands of times per response.

> **"This Is Why..."**
> This is why regenerating a response -- clicking that "retry" button -- sometimes gives you a completely different and sometimes better answer. Even at moderate temperatures, the probabilistic nature of token selection means the model can take a different path each time. You are not fixing anything by regenerating. You are rolling the dice again and sometimes getting a better outcome.

## Top-p: The Other Creativity Dial

Temperature has a sibling called **top-p** (also known as **nucleus sampling**), and it approaches the same problem from a different angle.

Instead of adjusting how "peaked" or "flat" the probability landscape is (which is what temperature does), top-p puts a ceiling on how many options the model considers.

Here is the analogy. Imagine you are at a buffet with 50 dishes. Temperature controls how adventurous your palate is. Top-p controls how many dishes you are even willing to look at.

With **top-p = 0.1**, the model only considers the smallest set of tokens whose combined probability adds up to 10%. If the top three tokens account for 10% of the probability, those are the only three options. Everything else is eliminated before the model even considers it.

With **top-p = 0.9**, the model considers the tokens whose combined probability adds up to 90% -- a much larger pool. More options, more variety, more potential for surprise.

In practice, temperature and top-p are often used together, each complementing the other. A common configuration might be temperature = 0.8 with top-p = 0.95, which creates a balance between creativity and coherence.

> **"Try This Now"**
> If you have access to an AI platform's API (like the OpenAI Playground, Anthropic's API console, or similar tools), try this experiment: send the exact same prompt three times at temperature 0.2, then three times at temperature 1.0. Notice how the low-temperature responses are almost identical to each other, while the high-temperature ones vary wildly. You are seeing the creativity dial in action.

## The Other Hidden Settings

Temperature and top-p are the most well-known hidden settings, but they are not the only ones. Several other parameters quietly shape every AI response you receive.

**Maximum tokens (response length limit).** This setting caps how long the response can be. If the maximum is set to 500 tokens (roughly 375 words), the model will stop generating at that point, even if it was mid-sentence or mid-thought. Some platforms set generous limits. Others restrict them to save costs, since longer responses cost more to generate.

> **"This Is Why..."**
> This is why some AI responses end abruptly or feel incomplete. The model did not decide to stop -- it hit a maximum token limit imposed by the platform. In some cases, the model is trying to say more but is simply not allowed to continue.

**Stop sequences.** These are specific strings of text that, if generated, cause the model to immediately stop. Some platforms use stop sequences to prevent the model from generating certain patterns -- for example, preventing it from simulating a multi-turn conversation by generating fake "User:" lines.

**Frequency penalty.** This setting discourages the model from repeating words it has already used. A higher frequency penalty means the model actively avoids repetition, which can make text more varied and natural-sounding but can also force the model into using unusual synonyms when the obvious word was actually the best choice.

**Presence penalty.** Similar to frequency penalty, but this one discourages the model from repeating topics or themes rather than specific words. A high presence penalty pushes the model to keep introducing new ideas rather than elaborating on ones it has already mentioned.

**Top-k.** Like top-p, this limits the pool of candidate tokens, but it works by setting a fixed number rather than a probability threshold. Top-k = 50 means the model only considers the 50 most probable tokens at each step, regardless of how much probability they collectively represent.

## The Invisible Tuning of Your Experience

Here is what makes these settings so consequential: they are set for you, not by you. When you use ChatGPT, Claude, Gemini, or any other consumer AI product, the company has chosen specific values for all of these parameters. Those choices reflect the company's priorities:

- A coding assistant might use lower temperature for more reliable, precise code generation
- A creative writing tool might use higher temperature for more imaginative prose
- A customer service bot might use low temperature with strict maximum token limits for fast, consistent answers
- A brainstorming assistant might use high temperature with high top-p for maximum idea diversity

These are not neutral choices. They embed a philosophy about what the AI experience should be. And they can change without notice. An AI company might adjust the temperature from 0.8 to 0.7 on a Tuesday afternoon, and millions of users would notice their AI feeling slightly "different" without being able to pinpoint why.

> **"Behind The Curtain"**
> Some AI companies dynamically adjust these settings based on the detected task type. Writing a formal business email? The system might quietly lower the temperature. Brainstorming creative ideas? It might nudge the temperature up. This means the same product can behave differently for different types of requests, and the user never knows a setting changed.

## The Interaction Between Settings and System Prompts

Temperature, top-p, and other generation settings interact with the system prompt in subtle ways. Consider a system prompt that says "be creative and surprising" paired with a low temperature setting. The system prompt is pushing toward creativity (through the content of the instructions), but the temperature is pushing toward predictability (through the mechanics of token selection). The result is a compromise -- responses that try to be creative in their structure and ideas but are expressed in fairly predictable language.

Conversely, a system prompt that says "be precise and factual" paired with high temperature might produce responses that are factually grounded in their content but occasionally express those facts in unexpected ways.

This is why prompt engineering alone -- even very good prompt engineering -- cannot fully control the AI's behavior. There are mechanical dials operating beneath the level of text instructions, and they have their own influence.

## The Practical Impact on You

So what does all of this mean for you as a user? Several things.

**First, accept variability as a feature, not a bug.** The AI is not supposed to give the exact same answer every time. The temperature setting deliberately introduces variation, and this is generally beneficial -- it prevents the AI from being a boring, repetitive machine.

**Second, use regeneration strategically.** When you get a response that is not quite right, regenerating it is not a sign of failure. You are taking another sample from a probability distribution. The next sample might be better. Or worse. But it will be different.

**Third, understand that "creativity" and "accuracy" are in tension.** The settings that make an AI more creative also make it less predictable and potentially less accurate. The settings that make it more reliable also make it more monotonous. There is no free lunch. When you want creative brainstorming, expect some duds mixed in with the gems. When you want precise factual answers, expect them to sound a bit formulaic.

**Fourth, know that you may have more control than you think.** If you use the API or advanced features of certain platforms, you can adjust these settings yourself. Even if you use only the standard interface, you can influence similar effects through your prompts: asking the AI to "be creative and surprising" functions as a soft temperature increase, while asking it to "be precise and stick to verified facts" functions as a soft temperature decrease.

> **"Pro Tip"**
> Match your prompt style to the hidden settings you want to simulate. For tasks requiring precision (factual research, technical explanations, data analysis), use language that signals "be precise": specific questions, constrained formats, requests for citations. For tasks requiring creativity (brainstorming, creative writing, exploring possibilities), use language that signals "be creative": open-ended questions, invitations to surprise you, requests for unusual perspectives. Your language acts as a soft dial, nudging the model in the direction you want.

## Before and After: Working With Hidden Settings

**Before understanding hidden settings** (bad prompt):
"Give me exactly the perfect answer for my career change plan."

This prompt sets up an impossible expectation. Due to temperature and probabilistic generation, there is no single "perfect" answer -- there is a distribution of possible good answers. The user will be disappointed when the response is good but not perfect, and they will not understand why regenerating gives a different result.

**After understanding hidden settings** (good prompt):
"Give me three different approaches to transitioning from accounting to UX design -- one conservative, one moderate, and one aggressive. I want to compare options."

This prompt works with the probabilistic nature of the model rather than against it. By asking for multiple approaches, you are essentially sampling the distribution within a single response. You get variety by design rather than by luck.

---

With an understanding of the invisible instructions, the hidden context, the pre-defined personality, and the mechanical dials that shape AI behavior, we are ready for the final lesson in this chapter -- a synthesis that reveals why the same underlying model can become radically different products depending on who is pulling the strings.
