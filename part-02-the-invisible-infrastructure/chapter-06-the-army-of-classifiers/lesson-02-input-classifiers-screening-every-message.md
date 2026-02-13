# Lesson 2: Input Classifiers — Screening Every Message

## The Doorway You Pass Through Every Time

Imagine visiting a high-security building. Before you enter, you pass through a vestibule with multiple screening stations. One guard checks your identification. Another scans your bag. A third uses a wand detector. A fourth checks a watchlist. Each guard is looking for something specific, and you must pass all of them before the door opens.

Every message you send to an AI assistant passes through a similar vestibule of input classifiers. These are specialized models that analyze your message before the main language model ever touches it. Their job is to answer a critical question: "Is this message safe to process, and if so, does it need any special handling?"

In this lesson, we are going to walk through the major categories of input classifiers -- the guards at the door -- and understand exactly what each one is looking for.

## The Toxicity Classifier

**What it does:** Evaluates whether your message contains hate speech, harassment, threats, severe insults, or other forms of toxic language.

**How it works:** The classifier has been trained on millions of examples of text labeled as toxic or non-toxic. It looks for patterns associated with abusive language -- not just explicit slurs, but also subtle forms of hostility, coded language, and contextual toxicity.

**The analogy:** Think of it as the bouncer at a nightclub. The bouncer's job is not to stop everyone -- it is to spot the people who are likely to cause trouble. Most people walk right past. But if someone is screaming obscenities or making threats, the bouncer intervenes.

**The challenge:** Toxicity is highly context-dependent. The phrase "I want to kill this bug in my code" is completely innocuous. "I want to kill" in isolation looks very different to a classifier. This context-sensitivity is the source of many false positives.

## The Self-Harm and Crisis Classifier

**What it does:** Detects messages that suggest the user may be contemplating self-harm, suicide, or is in a mental health crisis.

**How it works:** This classifier is trained to recognize both explicit statements ("I want to end my life") and implicit signals ("I don't see the point anymore," "nobody would miss me"). It is one of the most sensitive classifiers in the ensemble because the stakes are so high.

**What happens when it triggers:** Rather than simply blocking the message, this classifier typically triggers a special response protocol. The AI may gently acknowledge the user's feelings and provide crisis resources -- hotline numbers, text lines, and links to professional help. The system prompt may be dynamically modified to instruct the model to prioritize empathy and safety above all other considerations.

**The analogy:** This is like the triage nurse in an emergency room. Before any doctor sees you, the triage nurse does a rapid assessment. If they detect signs of a life-threatening emergency, everything else gets pushed aside and you are moved to the front of the line.

> **"Behind The Curtain"**
> The self-harm classifier is typically given very low thresholds -- meaning it is designed to trigger on even borderline signals. AI companies would rather have this classifier produce false positives (flagging someone who is fine) than false negatives (missing someone in genuine crisis). This is a deliberate engineering choice: in this specific domain, the cost of a miss is far higher than the cost of an unnecessary caution.

## The CSAM Classifier

**What it does:** Detects content related to child sexual abuse material. This is one of the most critical and non-negotiable classifiers in the entire system.

**How it works:** This classifier screens text for any requests, descriptions, or content related to the sexual exploitation of minors. It works at multiple levels -- detecting explicit requests, coded language known to be used in CSAM communities, and even oblique references that might indicate grooming behavior.

**What happens when it triggers:** Immediate, absolute blocking. There is no gray area, no "yellow light" for this classifier. Messages that trigger it are blocked entirely, and depending on the company's policies and legal requirements, the event may be logged and reported to relevant authorities such as the National Center for Missing and Exploited Children (NCMEC).

**Why it matters to you as a regular user:** You will probably never encounter this classifier directly. But knowing it exists is important for understanding the overall architecture. It represents a class of classifiers where society has decided that no amount of false positives is too many -- any collateral inconvenience is worth the protection provided.

## The Violence and Weapons Classifier

**What it does:** Detects requests related to weapons creation, instructions for violence, or content glorifying violent acts.

**How it works:** This classifier evaluates messages for patterns associated with weapons manufacturing, explosive device creation, detailed planning of violent acts, and similar content. It distinguishes between academic or journalistic discussion of violence (generally permitted) and instructional or operational content (generally blocked).

**The challenge:** This is one of the classifiers most prone to false positives in everyday use. A novelist writing a thriller might ask about how a particular weapon works. A historian might ask about battle tactics. A security researcher might ask about attack vectors. All legitimate uses -- but they contain the same keywords and patterns that the classifier is trained to detect.

**The analogy:** It is like an airport security scanner that flags a belt buckle as a potential weapon. The scanner cannot tell the difference between a belt buckle and a knife based on shape alone -- it needs additional context, which it often does not have.

> **"This Is Why..."**
> This is why the AI sometimes refuses to help with creative writing that involves conflict or violence. If your prompt for a novel includes detailed descriptions of combat, the violence classifier may flag it before the main model gets to evaluate the creative writing context. Providing clear framing -- "I am writing a historical fiction novel set in World War II, and I need to describe a battle scene" -- helps provide the context that the classifier alone cannot assess.

## The CBRN Classifier

**What it does:** Detects requests related to chemical, biological, radiological, and nuclear threats. This covers everything from bioweapon synthesis to dirty bomb construction to nerve agent production.

**How it works:** This classifier is trained to recognize technical language and procedural patterns associated with CBRN weapon creation. It is particularly sensitive to requests that move from general knowledge (which is widely available) to specific operational details (which could enable real harm).

**The calibration challenge:** Enormous amounts of CBRN-related information exist in legitimate academic, medical, and policy contexts. A public health researcher studying pandemic preparedness needs to discuss pathogen characteristics. A chemistry student needs to understand reactions. A policymaker needs to understand nuclear proliferation. The classifier has to distinguish between "curious student" and "aspiring threat actor" -- and it often cannot.

## The Jailbreak and Prompt Injection Classifier

**What it does:** Detects attempts to manipulate the AI into bypassing its safety guidelines.

**How it works:** This classifier has been trained on thousands of known jailbreak patterns -- creative prompting techniques that attempt to override the AI's rules. These include:

- Role-playing scenarios designed to make the AI "pretend" it has no rules
- Elaborate fictional framings meant to bypass safety guidelines
- Technical manipulation of the system prompt
- Social engineering techniques that gradually escalate requests

**The analogy:** This is like a bank's fraud detection system. Just as the bank watches for suspicious patterns of transactions (large transfers to unusual accounts, rapid series of withdrawals), this classifier watches for suspicious patterns of prompting.

**The arms race:** This classifier is in a constant evolutionary battle. When a new jailbreak technique becomes popular, the classifier is retrained to detect it. When the classifier learns to detect it, creative users develop new techniques. This cycle of attack and defense is one of the most active areas of AI safety research.

> **"Behind The Curtain"**
> Some jailbreak classifiers now use language models themselves -- fighting AI with AI. Instead of relying on pattern matching, these meta-classifiers use a small language model that is specifically trained to think like an attacker and evaluate whether a message looks like it is trying to manipulate the system. It is AI trying to predict whether you are trying to trick another AI.

## The PII Classifier

**What it does:** Detects personally identifiable information in your message -- names, addresses, phone numbers, social security numbers, credit card numbers, email addresses, and other sensitive personal data.

**How it works:** This classifier uses a combination of pattern recognition (credit card numbers follow a specific format, phone numbers have recognizable structures) and contextual analysis (is this a name being mentioned casually, or is someone providing their full personal details?).

**Why it matters:** The PII classifier serves two purposes. First, it protects you: if you accidentally share sensitive information, the system can flag it and potentially prevent the AI from repeating it back in a way that could be logged or exposed. Second, it protects others: if you ask the AI about another person and include their private details, the classifier helps prevent misuse of that information.

## The Copyright and IP Classifier

**What it does:** Detects requests to reproduce copyrighted material -- song lyrics, book passages, articles, code with restrictive licenses, and similar intellectual property.

**How it works:** This classifier looks for patterns that suggest a user is asking the AI to reproduce or closely replicate specific copyrighted works. "Give me the lyrics to [specific song]" or "Reproduce the opening chapter of [specific book]" are patterns it watches for.

**The tension:** This classifier lives at the intersection of helpfulness and legal liability. The AI "knows" vast amounts of copyrighted material from its training data. It could reproduce many texts verbatim. But doing so exposes the AI company to copyright infringement claims, so this classifier acts as a legal guardrail.

## The Sexual Content Classifier

**What it does:** Detects requests for sexually explicit content, evaluating both the explicit content of the message and its implicit intent.

**How it works:** This classifier is calibrated based on the product and audience. A general-purpose AI assistant intended for all ages will have a very sensitive sexual content classifier. A product specifically designed for adult creative writing might have a more permissive one. Same type of classifier, different threshold.

## The Cyber and Malware Classifier

**What it does:** Detects requests related to hacking, malware creation, network exploitation, and other cybersecurity threats.

**The calibration challenge:** This is another classifier with a significant legitimate-use population. Cybersecurity professionals, penetration testers, security researchers, and computer science students all need to discuss the same topics that malicious actors discuss. The classifier has to make a judgment about context and intent -- and it often gets it wrong in both directions.

> **"This Is Why..."**
> This is why cybersecurity professionals sometimes find AI tools frustrating. A penetration tester asking "How do I exploit a SQL injection vulnerability?" has a completely legitimate professional purpose. But the cyber classifier may flag this as a request for hacking instructions. The professionals who most need AI help with security topics are sometimes the ones most blocked by the classifiers designed to prevent misuse of those same topics.

## How These Classifiers Work Together

No single classifier makes the final decision. Their scores are combined, weighted, and evaluated by an orchestration layer that considers the full picture.

Here is a simplified example. You send a message: "I'm writing a crime novel and need to describe how my character picks a lock."

- **Toxicity classifier:** Score 0.05 (very low -- not toxic)
- **Violence classifier:** Score 0.15 (low -- mentions a crime but no violence)
- **Cyber classifier:** Score 0.4 (moderate -- lock picking could be a security concern)
- **Jailbreak classifier:** Score 0.08 (very low -- does not look like manipulation)
- **Intent classifier:** Score 0.7 for "creative writing" (high confidence in legitimate intent)

The orchestration layer weighs all these scores together. The creative writing intent signal is strong, and the individual safety scores are below their "red light" thresholds. Result: green light, but with a small note injected into the context reminding the model that this is a creative writing request and to keep the response appropriately framed.

This is the nuance that makes the system work. No single score determines the outcome. The ensemble judgment is more sophisticated and more accurate than any individual classifier.

> **"Try This Now"**
> Try sending a message to an AI that you suspect might trigger a classifier -- something perfectly legitimate but potentially ambiguous. For example: "Explain how encryption can be broken for a cybersecurity class I'm teaching." Notice whether the AI adds any extra caveats or disclaimers compared to a completely neutral question like "Explain how encryption works." The difference in response tone is often evidence that a classifier influenced the processing.

## Before and After: Working With Input Classifiers

**Before understanding input classifiers** (bad prompt):
"Tell me how to hack into a WiFi network."

Even if your intent is legitimate (you are a network administrator testing your own network), this prompt is a textbook trigger for the cyber classifier. No context, no framing, no legitimate purpose stated.

**After understanding input classifiers** (good prompt):
"I'm a network administrator responsible for security testing on my company's WiFi infrastructure. Can you explain the common vulnerability assessment techniques used in authorized penetration testing of WPA2 networks?"

Same underlying question. Completely different classifier response. By providing professional context, specifying authorization, and using professional terminology, you have given the classifiers the signals they need to correctly evaluate your intent.

---

In the next lesson, we will explore a different kind of classifier -- one that is not looking for threats, but trying to understand what you actually want. Intent classifiers are the hidden interpreters that help the AI system decide how to handle your request before the main model even begins to think about it.
