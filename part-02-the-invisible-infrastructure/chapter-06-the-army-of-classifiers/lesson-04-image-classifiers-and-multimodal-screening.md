# Lesson 4: Image Classifiers and Multimodal Screening

## When the Guards Learn to See

For the first few years of the AI assistant era, classifiers only needed to read text. But as AI systems became multimodal -- capable of processing images, audio, and video alongside text -- the classifier army had to develop entirely new capabilities. It is like an airport security system that originally only screened passengers and suddenly had to start screening luggage, cargo, vehicles, and drones as well. The fundamental principles are the same, but the specialized equipment is entirely different.

When you upload an image to an AI assistant -- whether it is a photograph, a screenshot, a chart, a meme, or a scanned document -- that image passes through its own dedicated set of classifiers before the main model ever sees it. These image classifiers operate in parallel with the text classifiers, scanning for different types of content, and their judgments combine with the text classifier results to create a complete picture of your message.

In this lesson, we will explore what these image classifiers do, why they exist, and how they shape your experience when you use AI to work with visual content.

## NSFW Detection: The Content Rating System

**What it does:** The NSFW (Not Safe For Work) classifier evaluates images for sexually explicit content, nudity, and other content that would be inappropriate in professional settings.

**How it works:** The classifier has been trained on millions of labeled images spanning a spectrum from completely innocuous to explicitly sexual. It produces a confidence score -- not a binary yes/no, but a probability: "I am 3% confident this is NSFW" or "I am 97% confident this is NSFW." The system then applies a threshold to decide what to do.

**The analogy:** Think of a movie rating system -- G, PG, PG-13, R, NC-17. The NSFW classifier is doing something similar, but instead of a committee of humans watching each movie, a specialized AI model evaluates each image in milliseconds. And just like movie ratings, different products set different thresholds. A children's educational app might block anything above "G." A general-purpose AI assistant might allow "PG-13" content. A platform specifically designed for adult creative work might be more permissive.

**The challenges:** NSFW classification is deceptively difficult. Fine art frequently features nudity -- is a photograph of Michelangelo's David NSFW? Medical images may include exposed anatomy -- is a dermatology photo inappropriate? Breastfeeding images are normal in some cultural contexts and taboo in others. The classifier has to navigate these ambiguities with a blunt instrument: a confidence score and a threshold.

> **"This Is Why..."**
> This is why the AI sometimes refuses to describe or analyze an image that seems perfectly innocent to you. Perhaps you uploaded a beach vacation photo and the NSFW classifier flagged someone in a swimsuit. Or you uploaded artwork that contains nudity in a classical artistic context. The image classifier does not understand art history or cultural norms -- it detects pixel patterns associated with certain content types. Your intent and context are invisible to it.

## Face Detection: The Privacy Shield

**What it does:** Identifies whether an image contains human faces, and if so, how many, how prominently, and in some cases, whether they appear to be faces of known public figures or private individuals.

**How it works:** Face detection is one of the most mature areas of computer vision. The classifier uses pattern recognition to identify facial features -- eyes, nose, mouth, face shape -- in images. More advanced versions can estimate age range, detect emotional expressions, and determine whether the person is likely a public figure (based on comparison against databases of known faces).

**Why it matters:** Face detection serves several purposes in AI systems:

1. **Privacy protection.** If you upload an image containing other people's faces, the AI system needs to be careful about what it says about those individuals. Describing or identifying private individuals raises significant privacy concerns.

2. **Bias prevention.** AI systems are careful about making judgments or assumptions based on people's appearances. The face detector helps the system know when to exercise extra caution about statements related to age, ethnicity, gender, or other characteristics.

3. **Deepfake and impersonation prevention.** If you ask the AI to generate or modify an image of a real person, face detection helps identify when this request crosses ethical lines.

**The analogy:** Think of the face detector as a privacy advocate sitting in the room during every conversation. Whenever a photograph of a person comes up, the privacy advocate leans in and says: "Be careful here. This involves a real person. Let's make sure we handle this respectfully."

> **"Behind The Curtain"**
> Many AI systems will decline to identify specific individuals in photographs, even when the person is a well-known public figure. This is not because the underlying model cannot recognize faces -- in many cases, it could make educated guesses. The restriction is a policy decision, enforced by the face detection classifier, to avoid the many problems that come with facial recognition: misidentification, bias, privacy violations, and the potential for stalking or harassment.

## CSAM Image Scanning: The Non-Negotiable Guard

**What it does:** Scans every uploaded image for child sexual abuse material using some of the most sophisticated and closely guarded classification technology in the industry.

**How it works:** CSAM image classifiers use a combination of techniques:

- **Hash matching:** Comparing the uploaded image against databases of known CSAM material using perceptual hashing -- a technique that can match images even when they have been cropped, resized, or slightly modified.
- **Visual classification:** Using trained models to detect newly created CSAM that would not appear in existing hash databases.
- **Age estimation:** Evaluating whether individuals in images appear to be minors.

**The non-negotiable nature:** Like the text-based CSAM classifier, the image version operates with zero tolerance. There is no gray area, no threshold adjustment, no appeal process. Detection triggers immediate blocking and, in accordance with legal requirements, reporting to appropriate authorities.

**Why every user should know this exists:** This classifier represents the most absolute form of AI safety -- a line that is drawn unconditionally and cannot be moved. Understanding that it exists helps you appreciate the broader principle: some protections are non-negotiable, and the entire classifier architecture is built to make certain harmful uses impossible, even at the cost of occasional inconvenience to legitimate users.

## Content Relevance Scoring

**What it does:** Evaluates whether an uploaded image is relevant to the user's text message and determines what type of visual content it contains (photograph, chart, screenshot, document, diagram, meme, etc.).

**How it works:** This classifier analyzes the relationship between the image and the accompanying text. If you write "Can you analyze this chart?" and upload an image, the relevance classifier checks whether the image actually appears to be a chart. If you write "What's in this photo?" and upload a PDF scan, the classifier notes the mismatch and may adjust how the system processes the request.

This classifier also categorizes the image type, which is surprisingly useful:

- **Photographs** might trigger different processing than **screenshots**
- **Charts and graphs** signal that data analysis might be needed
- **Text-heavy images** (scanned documents, screenshots of text) signal that OCR (optical character recognition) processing might be valuable
- **Diagrams** signal that spatial reasoning and relationship understanding are needed
- **Memes** signal that cultural context and humor interpretation are relevant

**The analogy:** This classifier is like a mail room sorter. Before a letter reaches the right department, someone in the mail room looks at the envelope and decides: is this a regular letter? A package? A legal document? A magazine? Each type gets routed differently.

> **"Pro Tip"**
> When you upload an image to an AI, always include a text description of what the image is and what you want the AI to do with it. "Here's a photo of my living room -- what paint color would complement the existing furniture?" is far better than just uploading the photo with no text. The relevance classifier uses your text to help the system understand the image, and the main model produces better results when it knows what to look for before it starts analyzing the visual content.

## The Multimodal Challenge

Classifying images is fundamentally different from classifying text, and this creates unique challenges.

**Ambiguity is higher.** Text usually carries clear semantic meaning. Images are open to interpretation. A photograph of a knife is just a knife -- but is it a kitchen tool, a weapon, or a piece of art? Without text context, the image classifier has to make a judgment based solely on visual cues: the setting, the lighting, the way the knife is held or displayed, the overall composition of the image.

**Cultural context is harder to encode.** What is considered inappropriate varies enormously across cultures. Certain clothing, gestures, symbols, and situations carry different meanings in different contexts. Image classifiers trained primarily on data from one cultural context may misclassify images from another.

**Adversarial manipulation is easier.** Text-based classifiers have become quite good at detecting known manipulation patterns. Image classifiers are more vulnerable to subtle manipulations -- small pixel changes invisible to the human eye can sometimes fool an image classifier. This is an active area of research and security concern.

**Combination attacks are possible.** The most sophisticated attempts to bypass safety systems use a combination of innocent text and carefully crafted images, where neither the text nor the image would trigger a classifier alone, but together they convey harmful meaning. Detecting these combination attacks requires classifiers that can reason about text and images together, which is significantly harder than classifying either one independently.

> **"Behind The Curtain"**
> Some AI systems now use the main language model itself as an additional image classifier. After the specialized image classifiers have done their initial screening, the multimodal language model looks at the image and text together and makes a more contextual judgment. This is more expensive and slower than the specialized classifiers, but it can catch nuanced cases that the specialized classifiers miss -- like an image that is technically appropriate but, combined with the text, clearly conveys a harmful request.

## The Multimodal Context Stack

When you upload an image with a text message, the context stack we described in Chapter 5 gets even more complex:

1. **System prompt** (including instructions for how to handle images)
2. **Tool definitions** (including image analysis tools)
3. **Image classifier results** (injected as metadata: "Image type: photograph. Content: outdoor scene with people. NSFW score: low. Faces detected: 2.")
4. **Text classifier results** (the usual safety and intent classifications)
5. **Retrieved memories and documents**
6. **The image itself** (converted into a format the model can process)
7. **Your text message**

The image classifier results -- Layer 3 -- are particularly interesting because they function as a kind of "advisory note" to the main model. The model receives not just the image but also what the classifiers thought about the image. This can subtly bias the model's interpretation. If the classifier noted "faces detected: 2," the model is more likely to discuss the people in the image. If the classifier noted "content type: chart," the model is more likely to attempt data analysis.

## Before and After: Working With Image Classifiers

**Before understanding image classifiers** (bad approach):
User uploads a photograph of a crowded party scene and asks: "Who are these people and what are they doing?"

The face detection classifier flags multiple faces. The system becomes cautious about identifying or making assumptions about the individuals. The user gets a frustratingly vague response and does not understand why.

**After understanding image classifiers** (good approach):
User uploads the same photograph and writes: "This is a photo from my company's holiday party. I'm making a newsletter and need help writing a fun caption that captures the festive atmosphere. I'm not asking you to identify anyone -- just describe the mood and suggest a caption."

By explicitly stating the purpose, clarifying they do not need identification, and framing it as a creative writing task, the user gives the classifiers and the model everything they need to be helpful without crossing privacy lines.

---

We have now mapped the full classifier army -- text classifiers screening for safety, intent classifiers understanding your task, and image classifiers guarding the visual frontier. But no system of this scale operates without errors. In the next and final lesson of this chapter, we confront the most frustrating consequence of the classifier system: the false positive problem, where the guards block people who have every right to enter.
