# Appendix A: Complete Glossary

Every technical term used in this book, defined in plain English. When a term refers to a concept explored in depth in a specific chapter, the chapter number is noted in parentheses.

---

## A

**A/B testing** — A method where a company shows different versions of an AI system to different users at the same time, then measures which version performs better, so that the user you are talking to today might literally be a different model version than the user sitting next to you. (Ch. 7, 22)

**Activation** — The numerical signal that a single "neuron" inside a neural network produces after processing its inputs, analogous to how strongly a nerve cell fires in a biological brain.

**Agent (AI agent)** — An AI system that can autonomously plan, use tools, and take multi-step actions in the real world rather than just generating text in a chat window. (Ch. 20, 25)

**Alignment** — The ongoing effort to make AI systems behave in ways that match human values and intentions, rather than pursuing goals that are technically correct but practically harmful or unhelpful. (Ch. 17, 22)

**Annotation** — The process where human workers label training data with useful information, such as marking whether a response is helpful, harmful, accurate, or well-written, so the AI can learn from those judgments.

**API (Application Programming Interface)** — A standardized way for software to communicate with an AI model, allowing developers to send prompts and receive responses without using a chat interface. (Ch. 7)

**Attention** — The mechanism inside a Transformer that lets every word in your message look at every other word to determine which ones are most relevant to its meaning, like diplomats at a round table each assessing how relevant every other diplomat is to their own role. (Ch. 9, 10)

**Attention head** — A single "perspective" within the attention mechanism that focuses on one particular type of relationship between words, such as grammar, meaning, or pronoun references. (Ch. 9, 10)

**Autoregressive generation** — The process by which an AI produces its response one token at a time, where each new token is chosen based on everything that came before it, including the original prompt and every token generated so far. (Ch. 18)

## B

**Base model** — The raw language model as it exists after pre-training but before any fine-tuning, alignment, or safety work, like a chef who has read every cookbook but has never been told what kind of restaurant she works in. (Ch. 1, 22)

**Batch processing** — Running multiple AI requests through the system at the same time to make efficient use of hardware, which is one reason response times can vary.

**Beam search** — A generation strategy where the AI explores several possible response paths simultaneously and picks the one that scores highest overall, rather than committing to one path token by token. (Ch. 19)

**Benchmark** — A standardized test used to measure how well an AI model performs on specific tasks like reasoning, coding, math, or general knowledge, similar to standardized tests for students.

**Bias (in AI)** — Systematic tendencies in an AI's responses that reflect imbalances or prejudices present in the training data, such as associating certain professions more strongly with one gender.

**Bias (in neural networks)** — A small numerical adjustment added inside the model's calculations that helps it fit patterns more accurately, unrelated to social bias.

## C

**CBRN detection** — A classifier that screens messages for content related to chemical, biological, radiological, or nuclear threats, one of the safety filters that runs before the main AI model processes your message. (Ch. 6)

**Chain-of-thought (CoT)** — A reasoning technique where the AI works through a problem step by step, writing out its logic as it goes, which dramatically improves accuracy on complex tasks compared to jumping directly to an answer. (Ch. 12)

**Classifier** — A small, specialized AI model trained to make a specific judgment about text, such as whether it is toxic, whether it contains personal information, or what language it is written in, operating like a security guard at the entrance checking IDs before the main event begins. (Ch. 6, 21)

**Completion** — The text that an AI model generates in response to a prompt, so named because the model is literally "completing" the sequence of text that you started.

**Confidence calibration** — How well an AI's expressed certainty matches its actual accuracy, meaning a well-calibrated model says "I'm 80% sure" about things it gets right roughly 80% of the time. (Ch. 14)

**Constitutional AI** — A training approach where the AI is given a set of written principles (a "constitution") and trained to evaluate its own outputs against those principles, rather than relying solely on human feedback for every judgment.

**Context window** — The maximum amount of text an AI can "see" at one time, including the system prompt, conversation history, and your current message, like the size of the chef's counter — once it is full, older ingredients get pushed off the edge. (Ch. 8)

**Coreference resolution** — The ability to figure out that "she," "the CEO," and "Dr. Martinez" all refer to the same person within a passage, one of the specific tasks that attention heads specialize in. (Ch. 10)

**CSAM detection** — A classifier specifically trained to identify child sexual abuse material, one of the most critical safety filters in the input classification pipeline. (Ch. 6)

## D

**Data poisoning** — A type of attack where malicious data is deliberately inserted into an AI's training set to manipulate its behavior in specific ways.

**Decoding strategy** — The method used to select which token to generate next from the probability distribution, including approaches like greedy decoding, beam search, and various sampling techniques. (Ch. 19)

**Decoder** — The part of a Transformer architecture that generates output tokens one at a time, which is the component used in most modern chat-based LLMs.

**Dimensionality** — The number of independent numerical values used to represent a single token in the model's internal space, with modern LLMs using thousands of dimensions to capture the full richness of a word's meaning. (Ch. 3)

## E

**Embedding** — A representation of a word or token as a list of numbers that encodes its meaning as a location in a vast mathematical space, where words with similar meanings occupy nearby positions, like placing every concept in human language onto a map where distance equals difference in meaning. (Ch. 3)

**Emergent properties** — Capabilities that appear in large AI models that were never explicitly programmed, arising from the sheer scale of training, such as the ability to reason about ethics or translate between languages when the model was only trained to predict the next token. (Ch. 1, 2)

**Encoder** — The part of a Transformer architecture that reads and processes input text, creating rich internal representations of meaning.

**Epoch** — One complete pass through the entire training dataset during the training process, with most models requiring multiple epochs to learn effectively.

**Extended thinking** — An advanced form of chain-of-thought reasoning where the AI uses a hidden scratchpad to reason extensively about a problem before producing its visible response, like a student using scratch paper before writing a clean final answer. (Ch. 12)

## F

**Feed-forward network** — A processing step within each Transformer layer that refines the information after the attention mechanism has established word-to-word relationships, like a second round of analysis after the diplomatic conference. (Ch. 11)

**Few-shot prompting** — A technique where you include a few examples of the desired input-output pattern in your prompt, so the AI can learn the pattern and apply it to your actual request. (Ch. 23, 24)

**Fine-tuning** — The process of taking a pre-trained model and training it further on a smaller, specialized dataset to improve its performance on specific tasks, like a general-purpose chef doing a week-long intensive course in Japanese cuisine. (Ch. 22, 25)

## G

**GPU (Graphics Processing Unit)** — The specialized computer chip that makes modern AI possible, originally designed for rendering video game graphics but ideal for the massively parallel mathematical operations that Transformers require.

**Gradient descent** — The core method by which an AI model learns during training, making tiny adjustments to billions of parameters to get incrementally better at predicting the next token, like tuning a billion tiny knobs simultaneously.

**Grounding** — Connecting an AI's responses to verifiable external sources of information, such as search results or uploaded documents, to reduce hallucination. (Ch. 8, 20)

## H

**Hallucination** — When an AI generates information that sounds confident and fluent but is factually incorrect, fabricated, or has no basis in reality, occurring because the model is completing patterns rather than looking up verified facts. (Ch. 4)

**Hidden layers** — The processing layers inside a neural network between the input and output, where the actual "thinking" happens, and also the central metaphor of this book: the many invisible processes between your message and the AI's response.

**Human feedback** — Judgments provided by human evaluators about the quality, helpfulness, and safety of AI responses, used to train reward models and improve the system through RLHF. (Ch. 22)

## I

**Inference** — The process of running a trained AI model to generate a response to a new prompt, as opposed to "training," which is how the model learned in the first place, analogous to the difference between studying for an exam and taking the exam.

**Input classifier** — Any of the specialized small models that screen your message before the main LLM processes it, checking for safety issues, detecting intent, and sometimes injecting hidden warnings into the system prompt. (Ch. 6)

**Intent classification** — The process by which the system determines what type of task you are asking for, such as whether your message is a question, a creative writing request, a coding task, or a conversation, in order to handle it appropriately. (Ch. 6, 13)

**Intent resolution** — The deeper process by which the AI figures out what you actually want, considering not just your literal words but also implied meaning, emotional context, and the type of interaction you expect. (Ch. 13)

**Intent stack** — The multiple simultaneous goals the AI is managing while generating a response, including task execution, user satisfaction, quality standards, safety constraints, format expectations, relationship management, and implicit knowledge application. (Ch. 15)

## J

**Jailbreak** — An attempt to trick an AI into bypassing its safety guidelines, typically through clever prompt engineering that disguises a prohibited request as something that appears benign. (Ch. 6, 17)

## K

**Key (in attention)** — One of the three vectors each token generates in the attention mechanism, representing "what information I have to offer," which other tokens compare against their Queries to determine relevance. (Ch. 9)

**Knowledge cutoff** — The date after which the AI has no training data, meaning it cannot reliably answer questions about events that occurred after that date without access to external tools like web search. (Ch. 5, 20)

**KV cache** — A technical optimization that stores previously computed Key and Value pairs during generation so they do not need to be recalculated for every new token, which is why the first token in a response takes longer to appear than subsequent tokens.

## L

**Latency** — The time delay between when you send a message and when you start seeing the AI's response, which includes time for classifiers, routing, model processing, and output filtering. (Ch. 7, 21)

**Layer (Transformer layer)** — One "floor" in the multi-story building of a Transformer model, containing an attention mechanism and a feed-forward network, with modern models stacking 80 or more of these layers on top of each other. (Ch. 11)

**Load balancing** — The process of distributing incoming AI requests across multiple servers to prevent any single server from being overwhelmed, one reason response times can vary throughout the day. (Ch. 7)

**LLM (Large Language Model)** — A massive neural network trained on enormous amounts of text to predict the next token, which at sufficient scale develops emergent abilities that make it capable of conversation, reasoning, writing, coding, and more. (Ch. 1)

**LoRA (Low-Rank Adaptation)** — An efficient fine-tuning technique that adjusts only a small fraction of a model's parameters rather than retraining the entire model, making customization faster and cheaper.

**Loss function** — The mathematical formula that tells the model how wrong its predictions are during training, which the training process tries to minimize, like a scoreboard showing how far the chef's dishes are from perfect.

## M

**Model routing** — The system that decides which AI model should handle your request, since many AI products use smaller, faster models for simple questions and larger, more capable models for complex ones. (Ch. 7)

**Multi-head attention** — The use of many attention heads running in parallel within a single Transformer layer, each one focusing on a different type of relationship between words, like having dozens of specialists simultaneously analyzing the same text from different angles. (Ch. 9, 10)

**Multimodal** — Describes an AI system that can process and generate multiple types of content, not just text, but also images, audio, video, or code. (Ch. 25)

## N

**Neural network** — A computing system loosely inspired by the structure of the human brain, made up of layers of interconnected nodes that process information, and the foundation upon which all modern LLMs are built.

**Next-token prediction** — The fundamental task that an LLM is trained to perform: given a sequence of tokens, predict which token is most likely to come next, which at massive scale produces seemingly intelligent behavior. (Ch. 1, 2)

**Nucleus sampling** — See "Top-p sampling."

## O

**Output classifier** — A specialized model that scans the AI's generated response before you see it, checking for toxicity, personal information leakage, copyright violations, and policy compliance. (Ch. 21)

**Output filter** — The collection of systems that evaluate, and potentially block or modify, the AI's response after it has been generated but before it is shown to you. (Ch. 21)

**Overfitting** — When a model memorizes its training data too closely instead of learning general patterns, causing it to perform well on familiar examples but poorly on new ones, like a student who memorizes answers to practice tests but cannot handle new questions.

## P

**Parameter** — A single adjustable number inside the AI model, one of billions of tiny "preference knobs" that collectively determine how the model responds to any input, calibrated during training by exposure to enormous amounts of text. (Ch. 1)

**PII detection** — A classifier that identifies personally identifiable information such as names, phone numbers, email addresses, or social security numbers, to prevent the AI from leaking or mishandling private data. (Ch. 6, 21)

**Policy reasoning** — The internal deliberation process where the AI evaluates whether a request is safe, appropriate, and within its guidelines, weighing helpfulness against potential harm before deciding how to respond. (Ch. 17)

**Positional encoding** — A technique that gives the Transformer information about the order of words in a sentence, since the attention mechanism processes all words simultaneously and would otherwise have no way of knowing that "the dog bit the man" differs from "the man bit the dog." (Ch. 9)

**Pre-training** — The initial, massive training phase where a model learns from trillions of tokens of text by predicting the next token over and over, absorbing the patterns, structures, and knowledge embedded in human language. (Ch. 1, 2)

**Probability distribution** — The ranked list of all possible next tokens along with their likelihood scores that the model produces at each step of generation, from which the actual next token is sampled. (Ch. 2, 19)

**Prompt** — Everything the user types or submits to the AI, which becomes part of the context that influences the generated response.

**Prompt engineering** — The practice of carefully crafting prompts to guide the AI toward better, more useful responses, informed by understanding how the model processes and generates text. (Ch. 23, 24)

**Prompt injection** — An attack technique where malicious instructions are hidden within seemingly normal text, attempting to override the system prompt or hijack the AI's behavior. (Ch. 6)

## Q

**Quantization** — A technique for reducing the memory and computational requirements of a model by representing its parameters with fewer digits of precision, trading a small amount of accuracy for significant gains in speed and efficiency.

**Query (in attention)** — One of the three vectors each token generates in the attention mechanism, representing "what am I looking for," which gets compared against every other token's Key to determine where to focus attention. (Ch. 9)

## R

**RAG (Retrieval-Augmented Generation)** — A system where the AI first searches through a collection of documents to find relevant information, then includes that information in its context when generating a response, allowing it to answer questions about specific documents or current information it was not trained on. (Ch. 8)

**Rate limiting** — Restricting how many requests a user or application can send to an AI system within a given time period, used to manage server load and prevent abuse. (Ch. 7)

**Red teaming** — The practice of having humans deliberately try to make an AI system produce harmful, incorrect, or policy-violating outputs, in order to discover and fix vulnerabilities before they affect real users. (Ch. 22)

**Reinforcement Learning from Human Feedback (RLHF)** — A training technique where human evaluators rate AI responses, and those ratings are used to train the model to produce responses that humans prefer, which is how raw language models are transformed into helpful, safe assistants. (Ch. 15, 22)

**Residual stream** — The main information highway running through all layers of a Transformer, where each layer adds its contribution to the running total of understanding rather than replacing what came before, like a river that gains tributaries without losing its original water. (Ch. 11)

**Reward model** — A separate AI model trained to predict how a human evaluator would rate a given response, used to automatically score outputs during training and sometimes during inference to select the best response. (Ch. 21, 22)

**Role prompting** — A prompting technique where you ask the AI to adopt a specific persona or expertise, such as "act as a senior UX designer," which activates relevant patterns from the training data and shifts the generation toward that domain's language and knowledge. (Ch. 23)

## S

**Safety classifier** — Any classifier in the input or output pipeline specifically designed to prevent harmful content, including detectors for toxicity, self-harm, weapons, CSAM, and other dangerous material. (Ch. 6, 21)

**Sampling** — The process of randomly selecting the next token from the probability distribution rather than always picking the most likely one, which introduces the variation that makes AI responses creative and non-repetitive. (Ch. 19)

**Scaling laws** — The observed pattern that AI model performance improves predictably as you increase model size, training data, and computing power, which has driven the industry's race to build ever-larger models.

**Self-attention** — The specific type of attention used in Transformers where each token in a sequence attends to every other token in the same sequence, including itself, to build context-aware representations. (Ch. 9)

**Self-consistency** — A technique where the AI generates multiple reasoning paths for the same problem and selects the answer that appears most frequently across those paths, improving reliability on reasoning tasks. (Ch. 14)

**Semantic space** — The vast multi-dimensional space where word meanings are represented as positions, so that words with similar meanings are close together and relationships between words can be expressed as directions and distances. (Ch. 3)

**Softmax** — The mathematical function that converts raw attention scores into probabilities that add up to one, ensuring that the model's attention is distributed as proportional weights across all the words it is looking at.

**System prompt** — The set of instructions, written by the AI product's creators, that is invisibly loaded at the beginning of every conversation, defining the AI's persona, capabilities, rules, formatting preferences, and behavioral boundaries before you type a single word. (Ch. 5)

## T

**Task decomposition** — The process by which the AI internally breaks a complex request into smaller sub-tasks, figures out the right order to address them, and works through them systematically. (Ch. 16)

**Temperature** — A setting that controls how "creative" or "random" the AI's token selection is, where low temperature produces predictable, focused responses and high temperature produces more varied, surprising, and sometimes chaotic responses. (Ch. 5, 19)

**Token** — The basic unit of text that an AI works with, typically a word, part of a word, or a punctuation mark, since the AI does not see full words or sentences but rather these smaller pieces. (Ch. 2)

**Tokenization** — The process of chopping text into tokens before the AI can process it, which explains why the AI sometimes handles word boundaries, unusual words, or non-English text in unexpected ways. (Ch. 2)

**Tokenizer** — The specific algorithm and vocabulary that determines how text is divided into tokens, with different AI models using different tokenizers that can split the same text differently. (Ch. 2)

**Tool use** — The ability of an AI to invoke external tools such as web search, code execution, file reading, or API calls during the generation process, allowing it to go beyond what it learned during training. (Ch. 20)

**Top-k sampling** — A generation method that limits the pool of candidate tokens to only the top k most likely options before sampling, which prevents extremely unlikely tokens from being selected while still allowing creativity. (Ch. 19)

**Top-p sampling (nucleus sampling)** — A generation method that limits the pool of candidate tokens to the smallest set whose combined probabilities exceed a threshold p, adaptively narrowing or widening the options based on how confident the model is. (Ch. 19)

**Training data** — The enormous collection of text that an AI model learns from during pre-training, typically comprising trillions of tokens sourced from books, websites, articles, code repositories, and other publicly available text. (Ch. 1)

**Transfer learning** — The principle that knowledge learned during pre-training on general text can be applied to specific tasks through fine-tuning, which is why a model trained on internet text can be adapted to excel at medical diagnosis or legal analysis.

**Transformer** — The neural network architecture, introduced in 2017, that processes all words in a message simultaneously using attention mechanisms rather than reading them one at a time, which became the foundation of virtually every modern large language model. (Ch. 9)

## U

**Unsupervised learning** — A type of training where the model learns patterns from data without being given explicit labels or answers, which is how pre-training works: the model simply learns to predict the next token from raw text.

## V

**Value (in attention)** — One of the three vectors each token generates in the attention mechanism, representing the actual information that will be contributed when another token's Query matches this token's Key strongly. (Ch. 9)

**Vector** — An ordered list of numbers that represents something in mathematical space, such as a word's meaning, a token's position, or a relationship between concepts, the fundamental unit of information inside a neural network.

**Vocabulary** — The fixed set of all tokens that an AI model can recognize and produce, typically around 100,000 pieces, which is the complete menu of building blocks from which all input and output text is assembled. (Ch. 2)

## W

**Weights** — The numerical values of a model's parameters that are learned during training, collectively encoding everything the model "knows" about language patterns, facts, and reasoning.

## Z

**Zero-shot prompting** — Asking an AI to perform a task without providing any examples, relying entirely on the model's pre-existing training to understand what you want, as opposed to few-shot prompting where you provide examples. (Ch. 23)

---

*This glossary covers the core terminology used throughout The Hidden Layers. For deeper exploration of any concept, refer to the chapter noted in parentheses after each definition.*
