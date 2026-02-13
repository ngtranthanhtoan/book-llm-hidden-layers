# Lesson 1: Model Routing — Which Brain Answers Your Question

## The Hospital You Did Not Know You Were In

When you walk into a large hospital with a health complaint, you do not get to choose which doctor sees you. You walk in the door, describe your symptoms, and a triage system decides what happens next. A minor headache? You might see a nurse practitioner. A possible broken bone? You are sent to radiology and then an orthopedist. Chest pain? You are immediately routed to the emergency cardiac team. The triage system matches the severity and type of your problem to the appropriate level of medical expertise.

Every time you send a message to an AI assistant, something strikingly similar happens. Your message is evaluated, classified, and then routed to a specific model -- or sometimes one of several possible models. The brain that answers your question might not be the same brain that answered your last question. And the brain selected for a casual "What's the weather like in Paris?" might be entirely different from the one selected for "Help me plan a career change from accounting to UX design."

Welcome to the routing layer: the invisible traffic controller that decides which AI brain handles your request.

## Why Multiple Brains?

You might be wondering: "Doesn't ChatGPT just use GPT-4? Doesn't Claude just use... Claude?" The answer is more complicated than that. Most AI companies maintain a portfolio of models of different sizes and capabilities:

**Small models** are fast, cheap, and good at simple tasks. They might have a few billion parameters and can answer straightforward factual questions, perform basic translations, or handle simple formatting tasks. Think of them as the general practitioner: competent, efficient, great for routine matters.

**Medium models** are more capable but slower and more expensive. They handle moderate complexity: summarizing documents, writing professional emails, explaining concepts, having substantive conversations. Think of them as the specialist: more depth, more nuance, more time per patient.

**Large models** are the most powerful and the most expensive. They handle complex reasoning, creative tasks, nuanced analysis, and sophisticated problem-solving. They might have hundreds of billions of parameters and cost ten to a hundred times more per query than the small models. Think of them as the elite specialist: the surgeon, the diagnostician, the researcher -- called in for the cases that genuinely require their expertise.

The routing layer's job is to match each incoming request to the appropriate model. Send a simple question to the large model, and you are wasting expensive resources on something the small model could handle perfectly. Send a complex reasoning task to the small model, and the user gets a mediocre answer that damages their experience and trust.

> **"Behind The Curtain"**
> When you select "GPT-4" or "Claude Sonnet" in a consumer product, you might assume that every message goes to that exact model. In some cases, that is true. But many AI systems use additional routing logic beneath the hood. A "GPT-4" conversation might route simple follow-up questions to a smaller, faster model and reserve the full GPT-4 for the complex messages. The user experience feels seamless -- but different brains handled different parts of the conversation.

## How Routing Decisions Are Made

The routing layer uses several signals to decide where to send your message.

**Signal 1: Complexity estimation.** As we discussed in the Chapter 6 lesson on intent classifiers, a complexity classifier evaluates how difficult your request is. Simple requests get routed to smaller, faster models. Complex requests get routed to larger, more capable models. This classification is the primary driver of most routing decisions.

**Signal 2: Task type.** Different models may be optimized for different types of tasks. Some models are fine-tuned for code generation. Others excel at creative writing. Others are optimized for conversational interaction. The routing layer can match the task type to the model that handles it best.

**Signal 3: User tier.** This is the uncomfortable truth about AI routing: paying customers often get access to better models. A free-tier user might be routed to smaller, cheaper models more frequently. A premium subscriber might have priority access to the largest, most capable models. This is not always transparent -- the interface might look the same for both users, but the brain behind the screen can be different.

**Signal 4: System load.** If the most capable model is overloaded with requests, the routing layer might redirect your message to a different model to maintain acceptable response times. This is especially common during peak usage hours, when the demand for the best models exceeds capacity.

**Signal 5: Geographic and regulatory factors.** Some regions have specific data processing requirements. Your message might be routed to models deployed in specific data centers based on your location, legal jurisdiction, or the regulatory environment.

Let us trace our running example through the routing layer. You type: "Help me plan a career change from accounting to UX design."

The complexity classifier says: moderate to high. The task type is planning and advice-giving. Let us say you are a premium subscriber. The system is not currently overloaded. The routing decision: send this to the large model. This is a complex, nuanced request that benefits from sophisticated reasoning.

But if you had typed "What's the capital of France?" -- the complexity classifier says trivially simple, the task type is factual recall. Routing decision: the small, fast model can handle this perfectly. Why wait three seconds for the large model when the small model can answer correctly in half a second?

> **"This Is Why..."**
> This is why response speed sometimes varies dramatically for seemingly similar questions. You asked a complex question and it took five seconds. Your friend asked a different but seemingly similar question and got a response in one second. The difference might not be that one question was harder for the model to process -- it might be that the questions were routed to different models entirely. The fast response came from a small, quick model. The slow response came from a large, powerful model that needs more time to generate.

## The Seamless Handoff

One of the most impressive engineering feats of the routing layer is that you almost never notice it. The transition between models happens invisibly. The interface looks the same. The conversation flows continuously. There is no "please hold while we transfer you to a more capable model."

This seamlessness is achieved through careful design:

- All models in the portfolio are trained to follow the same system prompt format, so the personality and rules remain consistent across model switches
- The conversation history is formatted identically for all models, so context is preserved
- Output formatting standards are shared, so responses look similar regardless of which model generated them
- The response streaming mechanism (the effect of text appearing word by word) is consistent, masking differences in generation speed

The goal is that you should not be able to tell which model answered your question. In practice, attentive users sometimes can tell -- the large model produces more nuanced, more thoughtful responses, and the small model's responses sometimes feel a bit shallower or more formulaic. But the routing layer's design goal is invisibility.

## The Analogy: Air Traffic Control

Think of the routing layer as air traffic control for AI. Just as air traffic controllers manage dozens of aircraft -- directing each one to the appropriate runway, altitude, and flight path based on its size, destination, fuel level, and current conditions -- the routing layer manages hundreds of thousands of simultaneous requests, directing each one to the appropriate model based on complexity, task type, user tier, and system load.

And just as you, the airline passenger, never see the air traffic controller's decisions -- you just sit in your seat and arrive at your destination -- you never see the routing layer's decisions. You just type your message and receive a response. The routing happens entirely behind the scenes.

> **"Pro Tip"**
> If you suspect your request is being routed to a smaller, less capable model and you want the best possible response, try signaling complexity explicitly. "This is a complex question that requires careful reasoning" or "I need a thorough, detailed analysis" are not just instructions for the model -- they are signals to the routing layer that this request deserves the most capable model available. You are essentially telling the triage system: "This is not a headache. This is serious."

## The Multi-Model Conversation

In some systems, a single conversation might involve multiple models at different points. The opening greeting might come from a small model. A complex analysis in the middle might be handled by the large model. A follow-up clarification might go back to the small model. Each routing decision is made independently based on the current message.

This creates an interesting phenomenon: the "quality" of your AI conversation can fluctuate from message to message. One response feels incredibly insightful and nuanced. The next feels surprisingly shallow. It is not that the AI got tired or distracted -- it is that a different model handled each response.

Understanding this helps explain one of the most common user complaints: inconsistency. "The AI was brilliant when I asked it to analyze my business plan, but then gave a terrible answer when I asked a follow-up question." The follow-up might have been classified as simpler and routed to a smaller model -- one that did not have the same depth of reasoning as the model that handled the original analysis.

## Before and After: Working With the Routing Layer

**Before understanding model routing** (bad approach):
The user sends a complex, nuanced question in a terse, casual way: "Career advice?"

Two words. The routing layer sees this as simple and routes it to a small, fast model. The user receives a generic, shallow response and concludes that AI is not useful for career advice.

**After understanding model routing** (good approach):
"I need detailed, expert-level guidance on transitioning from a senior CPA role in public accounting to a UX design career. Please consider the following factors: my financial obligations, the skills gap, the market demand in Chicago, and a realistic 12-month timeline. I'd like you to analyze this from multiple angles and provide actionable recommendations."

The complexity signals are unmistakable. The routing layer sends this to the most capable model available. The user receives a thoughtful, comprehensive response that actually helps them plan their career change.

The difference was not just better prompting for the model. It was better signaling for the routing layer.

---

In the next lesson, we will look more closely at one of the routing layer's most important and most error-prone components: complexity estimation, and what happens when the system misjudges how hard your question really is.
