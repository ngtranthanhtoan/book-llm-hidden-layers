# Lesson 3: Multi-Step Tool Chains

## When One Tool Isn't Enough

In the previous lesson, we watched the AI call a single tool and weave the results into its response. That's the basic unit of tool use. But the real power — and the real complexity — emerges when tools chain together. When the output of one tool becomes the input for another, and that result feeds into yet another, you get multi-step tool chains: sequences of coordinated actions that can accomplish tasks no single tool call could handle.

This is where AI stops being just a conversational partner and starts becoming something more like an assistant who can actually do research, analysis, and work on your behalf.

## The Investigative Reporter Analogy

Think of a veteran investigative reporter working on a story. She doesn't just do one thing. She follows a chain of investigation:

1. She searches public records for a company's filing. (Search tool)
2. She reads through the filing and identifies a key executive's name. (Document reading)
3. She searches for that executive's other business affiliations. (Another search)
4. She finds a connection to a second company and pulls its financial records. (Database query)
5. She compiles all her findings into a summary with key connections highlighted. (Synthesis and writing)

Each step depends on the results of the previous step. She couldn't have searched for the executive's name without first reading the filing. She couldn't have found the second company without the executive's name. The chain is sequential and logical, with each link building on the last.

Multi-step tool chains work exactly the same way. The AI plays the role of the reporter — deciding what to investigate next based on what it just discovered, calling the appropriate tool, interpreting the results, and deciding the next step.

## Anatomy of a Multi-Step Chain

Let's trace a realistic multi-step tool chain for our career change scenario. You ask:

"Research the UX design job market in Austin, Texas. Find the top three companies hiring, their salary ranges, and what skills they're looking for. Then create a comparison table."

Watch how the AI might handle this:

**Step 1: Initial search.**
- Tool call: Web search for "UX designer jobs Austin Texas 2025"
- Results: A mix of job listing sites, articles about the Austin tech scene, and company career pages.
- AI assessment: "I have general information, but I need specific company data."

**Step 2: Targeted company research.**
- Tool call: Web search for "top companies hiring UX designers Austin Texas"
- Results: Lists mentioning companies like Dell, Indeed, Oracle, and several startups.
- AI assessment: "I now have company names. Let me get specific salary data."

**Step 3: Salary research.**
- Tool call: Web search for "UX designer salary Dell Austin 2025"
- Tool call: Web search for "UX designer salary Indeed Austin 2025"
- Tool call: Web search for "UX designer salary Oracle Austin 2025"
- Results: Salary ranges from Glassdoor, LinkedIn, and other sources.
- AI assessment: "I have salary data. Now I need skills requirements."

**Step 4: Skills research.**
- Tool call: Web search for "UX designer job requirements Dell Indeed Oracle 2025"
- Results: Common skill requirements from recent job postings.
- AI assessment: "I have all the data I need to build the comparison."

**Step 5: Synthesis and table creation.**
- No tool needed — the AI uses its generation capabilities to organize all the gathered data into a structured comparison table.
- Alternatively, the AI might call a code execution tool to create a formatted table or even a downloadable spreadsheet.

The final response includes a well-organized comparison table with specific companies, salary ranges, required skills, and perhaps even links to current job postings. This response would have been impossible with a single tool call. It required a chain of five steps, each informed by the previous results.

> **"Behind The Curtain" Sidebar**
>
> Multi-step tool chains reveal something fascinating about the AI's planning capabilities. At Step 1, the model didn't necessarily know it would need Steps 2 through 5. It discovered the need for each subsequent step by evaluating the results of the current step. "I searched for UX jobs in Austin and got general results. To answer the user's specific question, I need company-specific data. So my next step should be..." This is real-time planning, not a pre-computed plan. The model is making decisions about what to do next at each stage, adapting its approach based on what it finds. It's the investigative reporter deciding her next move based on what the last phone call revealed.

## The Chain Dependencies

One of the critical challenges in multi-step tool chains is managing dependencies — understanding which steps must be sequential and which can be parallel.

**Sequential dependencies:** Step B requires the output of Step A. "Search for UX designer salary at Dell" (Step 3) can't happen until "Find top hiring companies" (Step 2) has identified Dell as a target. These must happen in order.

**Parallel opportunities:** Steps that don't depend on each other can happen simultaneously. Once the model knows it needs salary data for Dell, Indeed, and Oracle, those three searches can happen in parallel — none depends on the others' results.

**Conditional branches:** Sometimes the next step depends on what the previous step found. If the search for Dell's UX salaries returns no useful results, the model might decide to substitute a different company instead of pressing forward with incomplete data. The chain adapts to the reality of what each step produces.

Efficient orchestration of these dependencies — running parallel steps in parallel, sequential steps in sequence, and adapting to conditional results — is a significant engineering challenge. The better the orchestration, the faster and more reliable the multi-step chain.

> **"This Is Why..." Box**
>
> **This is why some AI-assisted research tasks take noticeably longer than others.** A question that requires a single web search might add one or two seconds to the response time. But a complex research request that triggers a five-step tool chain — with each step dependent on the previous one — can take twenty to thirty seconds or more. Each step involves: the model deciding what to do, formulating a tool call, waiting for the tool to execute, receiving results, interpreting them, and deciding the next action. If you've ever watched an AI "thinking" for an extended period during a research task, it's likely executing a multi-step chain behind the scenes.

## When Chains Break

Multi-step tool chains introduce multiple points of failure, and understanding these helps you work with AI more effectively.

**Link failure:** Any single tool call in the chain can fail. A web search might return no relevant results. A code execution might hit an error. An API call might time out. When a link breaks, the entire chain must adapt — either retrying the failed step, finding an alternative approach, or gracefully handling the missing information.

**Cascade errors:** A subtle error in an early step can cascade through the rest of the chain. If Step 2's search returns an incorrect company name (perhaps a company that's no longer in Austin), every subsequent step based on that name will produce irrelevant results. The model may not catch this error because the results look plausible — they're just about the wrong thing.

**Context overflow:** Each tool call adds results to the context, and multi-step chains can rapidly fill the context window. By Step 5, the model might be carrying the results of four previous searches, its own previous generation, the system prompt, and the conversation history. If this exceeds the context window, earlier results might be truncated or lost, leading to an incomplete or inconsistent final response.

**Decision fatigue:** At each step, the model must decide what to do next. Over many steps, the quality of these decisions can degrade. The model might make a great decision at Step 1 but a mediocre one at Step 4, simply because the accumulated context is complex and the decision space is large. This is analogous to a human researcher getting tired after hours of investigation and making poorer choices about what to follow up on.

> **"Pro Tip" Box**
>
> For complex research tasks that you know will require multi-step chains, consider breaking the task into explicit stages yourself rather than relying on the AI to manage the entire chain autonomously. Instead of one complex prompt, use a sequence of messages:
>
> Message 1: "Search for the top companies hiring UX designers in Austin, Texas."
> (Review the results. Confirm they're relevant.)
>
> Message 2: "Great. Now find the salary ranges for UX designers at [specific companies from the results]."
> (Review the salary data. Check for accuracy.)
>
> Message 3: "Now compile this into a comparison table with these columns: Company, Salary Range, Key Skills, and Why This Company."
>
> By breaking the chain into human-supervised stages, you catch errors early, ensure each link is solid before moving to the next, and prevent cascade failures. You're acting as the quality control layer in the chain.

## Tool Chains in Code Execution

Multi-step chains become especially powerful when code execution is involved. Consider this request:

"Download the last 12 months of stock price data for Apple, calculate the monthly returns, and create a chart showing the trend."

The tool chain might look like:

**Step 1:** Code execution to fetch stock data from a financial API.
**Step 2:** Code execution to calculate monthly returns from the raw data.
**Step 3:** Code execution to generate a visualization chart.
**Step 4:** Text generation to interpret the chart and provide analysis.

Each code execution step produces data that feeds into the next. The model writes Python (or another language), runs it, examines the output, writes the next piece of code, runs that, and continues until the task is complete.

What makes this powerful is that the model isn't just predicting what the answer should look like — it's computing the actual answer. The monthly return percentages are calculated precisely, not estimated from patterns. The chart shows real data plotted accurately. The analysis is grounded in computed facts, not generated plausibilities.

> **"Try This Now" Exercise**
>
> Ask the AI to do something that naturally requires multiple steps:
>
> "Find three recent articles about the future of UX design, summarize each one in two sentences, and then identify the common theme across all three."
>
> Watch the process carefully. The AI needs to: (1) search for articles, (2) read or retrieve content from each article, (3) summarize each one, and (4) synthesize a common theme. That's a multi-step chain.
>
> Now ask yourself: did the AI actually read the full articles, or did it summarize from search snippets? Did it find genuinely recent articles, or did it fall back on older content? Did the "common theme" feel like a genuine synthesis or a generic observation? These questions train you to evaluate multi-step tool chain outputs critically.

## The Compounding Value of Chains

Despite the risks and complexities, multi-step tool chains produce something genuinely valuable: responses grounded in actual, current, computed reality.

A single tool call gives you one piece of external data. But a chain of tool calls gives you a synthesized analysis built on multiple pieces of external data. The difference is like asking a financial advisor "What's Apple's stock price?" versus asking "Analyze Apple's performance over the past year, compare it to the tech sector average, and tell me whether it's overvalued relative to its growth rate."

The first question needs one data point. The second needs a chain of data retrieval, computation, comparison, and analysis. And the second answer is dramatically more valuable.

For our running example, a single-search response might tell you "UX designers earn about $100,000." A multi-step chain response can tell you "UX designers in Austin specifically earn $95,000 to $115,000, which is 15% above the national average; the three fastest-growing companies in the Austin UX market are X, Y, and Z; and based on current job postings, the most in-demand skill combination is user research plus Figma proficiency." That's the difference between a factoid and actionable intelligence.

## The Human-AI Partnership in Chains

Here's a practical philosophy for working with multi-step tool chains: think of yourself as the project manager and the AI as the researcher.

A good project manager doesn't micromanage every step, but she also doesn't disappear entirely. She sets clear objectives, reviews intermediate results, course-corrects when needed, and evaluates the final output.

Similarly, for important research tasks:
- Set a clear, specific objective in your initial prompt.
- Review intermediate results when the AI shares them (or ask the AI to share them).
- Redirect if the chain is going off-track: "That's not quite what I meant. Focus on startups, not large corporations."
- Evaluate the final output critically, especially for specific claims that came from tool results.

This partnership model gives you the best of both worlds: the AI's ability to execute multi-step research rapidly, and your ability to ensure the research is actually relevant and accurate.

The next lesson takes this concept to its logical extreme: what happens when tool chains become so complex and autonomous that the AI is essentially managing an entire workflow by itself — the world of AI agents.
