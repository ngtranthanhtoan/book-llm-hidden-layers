# Lesson 1: The Tool Use Decision Process

## When Memory Isn't Enough

For the past two chapters, we've focused on how the AI generates text from its own internal knowledge — that vast web of patterns learned during training. The autoregressive loop, the probability distributions, the temperature controls — all of this describes a model reaching into its own memory and constructing a response token by token.

But there are moments when memory isn't enough. When you ask "What's the weather in Tokyo right now?" the model knows what weather is, it knows what Tokyo is, it knows how to describe weather — but it has no idea what the weather is right now, because its training data stopped at some point in the past. When you ask "Run this code and tell me if it works," the model can predict what the code might do, but it can't actually execute it. When you ask "Search my company's database for last quarter's revenue," the model has never seen your company's database.

These moments require something beyond generation from memory. They require tools. And the decision to use a tool — when to use one, which one to use, and how to use it — is one of the most fascinating and consequential processes happening behind the scenes of modern AI.

## The Doctor's Decision

Think of the AI as a highly knowledgeable doctor. Most patient questions can be answered from medical training and experience. "What causes headaches?" "How does aspirin work?" "What should I eat to lower cholesterol?" The doctor draws on years of knowledge and delivers an informed answer.

But some questions require something beyond knowledge:

"What does my blood work actually show?" The doctor needs to order a lab test — that's a tool.

"Is this mole cancerous?" The doctor needs to run a biopsy — that's a tool.

"What medication am I currently taking?" The doctor needs to check your medical records — that's a tool.

The doctor's first decision, before every single answer, is: "Can I answer this from my knowledge, or do I need to use a diagnostic tool?"

This is exactly the decision the AI faces with every message you send.

## The Internal Assessment

When your message arrives, the model doesn't just start generating a response. Before — or more precisely, during the early stages of — generation, the model makes an assessment about tool necessity. This assessment considers several factors:

**Temporal relevance.** Does the question require current information? "Who is the president of France?" might be answerable from training data if the answer hasn't changed, but "What did the president of France say today?" clearly requires a real-time search. The model has learned to recognize temporal markers — "today," "right now," "this week," "latest" — as signals that its training data might be stale.

**Computational need.** Does the question require precise calculation? The model can do simple arithmetic in its head (though not always reliably), but complex computations — running code, processing data, doing statistics — benefit from actual code execution. "What's 15% of 847?" might be answered from internal computation. "Analyze this dataset of 10,000 entries and find the top correlations" definitely needs a tool.

**External data requirement.** Does the question reference specific documents, databases, websites, or files that the model hasn't seen? "Summarize the PDF I just uploaded" requires a document reading tool. "Check my calendar for next Tuesday" requires a calendar API.

**Action requirement.** Does the request ask the model to do something in the real world, not just say something? "Create a spreadsheet with these columns" requires a file creation tool. "Send this email" requires an email API. "Book a flight" would require a booking tool.

The model weighs all these factors and makes one of three decisions:

1. **No tools needed.** Answer from internal knowledge. This is the most common path for conversational AI.

2. **Tools needed, and I know which ones.** Initiate a tool call with specific parameters.

3. **Tools might help, but I'm not sure.** Generate a partial response and decide mid-stream whether to invoke a tool.

> **"This Is Why..." Box**
>
> **This is why the AI sometimes says "I'll search for that" and other times just answers directly.** The model has made an internal assessment of whether its training data is likely sufficient. For timeless facts ("What is photosynthesis?"), it generates from memory. For time-sensitive information ("What are today's stock prices?"), it recognizes that its training data is outdated and triggers a search tool. For ambiguous cases ("What's the current population of Tokyo?"), it might answer from training data with a caveat ("As of my last update...") or decide to search, depending on how the model was configured and how strongly the temporal signal registers.

## What Tools Are Available?

The AI doesn't have a fixed, universal set of tools. The available tools depend entirely on how the AI system was built and deployed. Think of it as the doctor's equipment — a family physician has a stethoscope, a blood pressure cuff, and can order basic lab work. A hospital physician has access to MRI machines, surgical suites, and specialized diagnostic equipment. Same medical training, very different toolkits.

Here are the most common tool categories in modern AI systems:

**Web search.** The AI can search the internet for current information, just like you'd use Google. This is the most widely available tool and the one most users have encountered. When the AI says "Let me search for that" and then provides results with citations, it's using a web search tool.

**Code execution.** The AI can write code and actually run it in a sandboxed environment. This is enormously powerful for data analysis, mathematical computations, creating visualizations, and testing logic. When the AI says "Let me write some code to calculate that" and then shows you results with precise numbers, it ran actual code rather than estimating from patterns.

**File operations.** The AI can read documents you've uploaded (PDFs, spreadsheets, images), create new files (documents, spreadsheets, presentations), and sometimes edit existing ones. This bridges the gap between conversation and deliverables.

**API calls.** In more advanced deployments, the AI can interact with external services — checking a database, querying a weather service, looking up flight prices, sending messages. Each API is a specific tool with defined inputs and outputs.

**Image generation.** Some AI systems can call a separate image-generation model to create pictures, diagrams, or charts based on your description.

**Memory and retrieval.** The AI might have tools to search through previous conversations, stored notes, or knowledge bases. This is what happens when the AI "remembers" something from a conversation weeks ago — it's not internal memory but a retrieval tool accessing stored data.

> **"Behind The Curtain" Sidebar**
>
> Here's what most users don't realize: the list of available tools is part of the system prompt (which we covered in Chapter 5). Before you type your first word, the AI has been told something like: "You have access to the following tools: web_search(query), code_execution(language, code), file_read(file_id)..." along with descriptions of what each tool does, when to use it, and what parameters it needs. The model then treats tool use as a special kind of token generation — instead of generating regular text tokens, it generates structured tokens that specify which tool to call and with what inputs. The tool descriptions in the system prompt are as important as any other instruction. If a tool is poorly described, the model might use it incorrectly or not use it when it should.

## The Decision Tree

Let's trace the tool-use decision process with a concrete example. You're in a conversation with an AI that has access to web search, code execution, and file creation. You type:

"Help me plan a career change from accounting to UX design. Include current salary data for both fields."

The model begins processing your request and encounters two sub-tasks:

**Sub-task 1: Career change planning.** The model assesses: "Do I need tools for career change advice?" No. This is a knowledge-based task. The model has extensive patterns for career advice, skill transfers, and professional development. It can generate this from memory.

**Sub-task 2: Current salary data.** The model assesses: "Do I need tools for salary data?" Probably yes. Salary data changes over time, varies by region, and the model's training data might be outdated. The word "current" is a strong temporal signal. The model decides to trigger a web search.

The model's generation might look something like this (simplified):

1. Begin generating career advice tokens from internal knowledge.
2. Reach the point where salary data needs to be inserted.
3. Generate a tool call: `web_search("average salary UX designer 2025")` and `web_search("average salary accountant 2025")`.
4. Pause generation and wait for search results.
5. Receive search results with specific numbers and sources.
6. Continue generating, now incorporating the actual salary data from the search results.

From your perspective, you see the response appearing, perhaps with a brief pause when the model is waiting for search results, followed by the rest of the response with specific, cited salary figures.

> **"Try This Now" Exercise**
>
> Test the tool-use decision process yourself. Ask these three questions in sequence and watch the AI's behavior:
>
> 1. "What are the three branches of the US government?" (No tools needed — timeless, well-known fact)
> 2. "What was the most popular movie at the box office last weekend?" (Tool needed — time-specific information)
> 3. "Calculate the compound interest on $10,000 at 5% annual rate over 15 years with monthly compounding." (Tool potentially needed — precise calculation)
>
> Notice the difference in how the AI behaves. The first question gets an immediate answer. The second might show a search indicator or take slightly longer. The third might involve the AI writing and executing code. You're watching the tool-use decision in real-time.

## When the Decision Goes Wrong

The tool-use decision isn't always correct, and understanding the failure modes helps you get better results.

**False positive: Using tools when it shouldn't.** Sometimes the model decides to search for information it could answer from memory, wasting time and potentially getting confused by conflicting search results. "What year was the Eiffel Tower built?" doesn't need a search, but a cautious model might search anyway, introducing unnecessary latency.

**False negative: Not using tools when it should.** Sometimes the model confidently answers from memory when it should have searched. This is more dangerous, because you might get outdated or incorrect information delivered with full confidence. "What is the current interest rate?" answered from training data could be significantly wrong if rates have changed since the training cutoff.

**Wrong tool selection.** The model might choose to search the web when it should execute code, or try to answer from memory when it should check an uploaded document. This usually results in a less useful response rather than a harmful one.

**Poor tool parameterization.** The model might use the right tool with the wrong inputs — searching for the wrong query, running code with a logic error, or reading the wrong section of a document.

> **"Pro Tip" Box**
>
> You can significantly influence the tool-use decision through your prompt. If you want the AI to use tools, include explicit signals: "Search the web for current data on..." or "Use code to calculate..." or "Check the document I uploaded for..." Conversely, if you don't want tools used (perhaps because you're testing what the model knows from memory), you can say: "Based on your training data, what do you know about..." These explicit signals override the model's internal assessment and ensure the right tools (or no tools) are used.

## The Tool-Use Decision and Our Running Example

Let's revisit our career change prompt with tools in mind.

**Without tools available:** "Help me plan a career change from accounting to UX design." The model generates entirely from memory. The advice is based on patterns from its training data — career guides, Reddit posts, professional development articles, job market analyses. The information is generally good but might be outdated or generic.

**With tools available:** The same prompt might trigger several tool decisions:
- Web search for current UX designer job market conditions
- Web search for current salary comparisons
- Possibly a search for specific UX bootcamps or certification programs with current pricing
- The rest answered from internal knowledge (transferable skills, portfolio advice, mindset guidance)

The tool-enhanced response is the same voice, the same structure, the same quality of advice — but with real, current data woven in. The career planning framework comes from the model's knowledge. The specifics come from tools.

This hybrid approach — knowledge for the timeless elements, tools for the time-specific ones — is how the most effective AI systems operate. And understanding where the boundary falls helps you understand what to trust implicitly and what to verify.

In the next lesson, we'll look at what happens after the model decides to use a tool — the orchestration loop that coordinates generation, tool calls, and result integration into one seamless response.
