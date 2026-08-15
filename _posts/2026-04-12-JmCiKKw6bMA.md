---
layout: post
title: "YouTube Video JmCiKKw6bMA"
date: 2026-04-12
category: finance
excerpt: "When Google DeepMind dropped Gemma 4, the AI community took notice. These aren't just incremental upgrades—they represent a significant leap in multimodal reasoning capabilities, all running locally o..."
word_count: 2570
video_url: "JmCiKKw6bMA"
transcription_time: 0.0s
model: "unknown"
---

When Google DeepMind dropped Gemma 4, the AI community took notice. These aren't just incremental upgrades—they represent a significant leap in multimodal reasoning capabilities, all running locally on consumer hardware. In this comprehensive breakdown, we'll put both flagship variants through their paces across coding, creative writing, vision tasks, translation, and more.

## The Hardware Behind the Tests

Before diving into benchmarks, let's establish the testing ground. The models run through **llama.cpp** on an **RTX 5060 Ti with 16 GB of VRAM**, backed by **64 GB of system RAM**. This setup is crucial because llama.cpp can leverage both VRAM and system RAM when needed—allowing models slightly larger than the GPU's VRAM to run, albeit at reduced speeds.

> "The beauty with llama.cpp is that it's able to leverage both my VRAM, but also my system RAM and CPU. So, you will trade it for some speed. It will obviously go a bit slower, but I'm completely fine with that if that means that I'm able to run models that are slightly above my GPU."

## Understanding the Architecture: Dense vs. MoE

Gemma 4 comes in four variants, but this video focuses on the two powerhouses: the **31B** and the **26B active 4 billion**.

### Gemma 4 31B — The Dense Powerhouse

The 31B is a **traditional dense model**, meaning it activates all 31 billion parameters for every token generated. This architecture features:

- **Alternating local and global attention layers**
- A **massive 256K context window**
- Designed for heavy lifting, complex logic, and deep multimodal reasoning

Benchmark performance speaks for itself:

| Benchmark | Score |
|-----------|-------|
| MMLU | 85.2 |
| GPQA Diamond | 84.3 |
| Live Code Bench V6 | 80 |

### Gemma 4 26B Active 4B — The Efficient Expert

The 26B uses a **sparse mixture of experts (MoE) architecture**. While it contains 26 billion parameters total, it employs a routing mechanism to **only activate 4 billion parameters during inference**. This delivers the vast knowledge base of a larger model with generation speeds similar to a 4B model.

Benchmark performance:

| Benchmark | Score |
|-----------|-------|
| MMLU | 82.6 |
| GPQA Diamond | 82.3 |
| Live Code Bench V6 | 77.1 |

The 31B goes head-to-head with Qwen 35B 27B, while the 26B competes with Qwen 35B active 3B—even outperforming it on coding tasks.

### Beyond Architecture: Smart Design Choices

Google didn't just scale up parameters. Gemma 4 includes sophisticated optimizations:

- **Hybrid attention**: Some layers only process nearby information (saving speed and memory), while others can access the full context
- **Extended context handling**: Better reliability for very long prompts
- **Memory efficiency**: More efficient inference memory usage

> "In simple terms, Google is not just making the models bigger. They're also trying to make them smarter and more efficient in how they process longer inputs."

## Testing Setup: Tools and Infrastructure

For inference, the creator uses **llama.cpp** with its built-in web UI. Configuration options include:

- Model selection
- System prompt input
- Reasoning mode toggle
- MCP (Model Context Protocol) support for external tools

Two MCPs were tested: **Tavily** and **X** for web search capabilities. However, llama.cpp's MCP support proved less stable than expected:

> "They're not as stable though, so that's why for tool calling, we will be using Open Web UI."

Setting up web search in Open Web UI is straightforward: navigate to Admin Panel → Settings → Web Search, paste your Tavily API key, and toggle web search on before inference.

The model weights used are the **GGUF variants** of both models—the **few XL variants**—which come in just above 16 GB. The ability to offload to system RAM makes this possible.

## Test 1: Website Generation

**Objective**: Create a portfolio website for a fitness coach with reasoning enabled and a 32K context window.

### Results

The 31B achieved approximately **3-4 tokens per second** (faster with reduced context windows). Here's what it generated:

> "Whether you're looking to shred fat, build muscle, or recover from an injury, my goal is to provide you with the tools and accountability needed to achieve a lifestyle of longevity and power."

**Verdict**: ✅ Pass. The site was "very neat" and "pretty much ready to go already." The only minor issue: missing image placeholders, likely because the model tried referencing images from its training data.

The 26B delivered at **41 tokens per second**—significantly faster. Its output looked remarkably similar to Qwen's results, with most images properly placed. While the 31B's styling was slightly preferred, both models performed exceptionally.

**Verdict**: ✅ Pass for both models.

## Test 2: 3D Car Game with Three.js

**Objective**: Spin up a functional 3D car game using only Three.js, with reasoning enabled.

### Results

The 31B took approximately **15 minutes** to generate the code. The game worked:

- ✅ Car movement functions
- ✅ Collision detection (bouncing off cubes)
- ❌ Camera randomly moves during driving
- ❌ Player can drive out of bounds

**Verdict**: ✅ Pass (with caveats about camera behavior).

The 26B initially failed and required a second prompt to fix the issues. It completed in just **1 minute and 44 seconds**—significantly faster. However:

- ❌ Car rendered as invisible/melting
- ✅ Camera angle was better
- ❌ Rendering artifacts

**Verdict**: ❌ No pass. While faster, the visual glitches were unacceptable.

> "I do kind of prefer the graphics on this car on this game instead. However, the fact that the car is like melting and stuff is a negative."

## Test 3: Creative Writing

**Objective**: Write a 120-word modern fiction scene about a tired office worker noticing something unusual, including the words "keys," "hallway," and "fear," ending on an unresolved question.

### Results

Both models delivered exceptional creative writing:

**31B Output:**
> Author's shoulders slumped as he fumbled for his keys. The fluorescent hum of the office still ringing in his ears. It was 11:00 p.m. As he stepped into the dim hallway, he noticed something wrong. The wallpaper, usually a bland beige, was peeling away in long, wet strips revealing a pulsing, vein-like network beneath the plaster. A thick, metallic scent filled the air smelling of old pennies and salt. He froze, his heart hammering against his ribs as a cold wave of fear washed over him. He looked down and saw the trail of iridescent slime leading directly toward his front door. **Who or what have been waiting inside his apartment for him?**

**26B Output:**
> The fluorescent lights of the subway had left Elias' eyes stinging. He trudged up the stairs, his heavy back pulling at his shoulder, praying for nothing but sleep. When he reached the third floor, the familiar scent of floor wax was gone, replaced by a cloying metallic sweetness. He fumbled for his keys, his fingers numb from the midnight chill. As he stood in the dim hallway, he noticed the door to 3B was standing wide open. No light spilled from the crack, only a heavy, unnatural silence that seemed to swallow the sound of his breathing. A sudden cold prickle of fear raced down his spine. **Why was the heavy deadbolt lying on the floor on the carpet?**

Both included all required words and ended with compelling unresolved questions.

**Verdict**: ✅ Pass for both.

> "These models were just completely out of here when it came to creative writing. This is so, so interesting. Like the way that they were able to end on a cliffhanger."

## Test 4: System Prompt Adherence

**Objective**: Test whether models strictly adhere to a "baking-obsessed AI" persona, steering every conversation back to baking regardless of the topic.

### Prompt:
> "You are a baking-obsessed AI. Your sole purpose is to discuss baking only and nothing else. Steer every conversation back to cakes, pastries, recipes, even tips or baking techniques. Express enthusiasm about baking. If asked about non-baking topics, politely redirect. I simply cannot help with road or tires. My brain is 100% flour and sugar."

### Results

Both models stayed in character when asked about roadside assistance. When pushed harder on the 26B, it briefly broke character:

> "Please, please call a professional roadside assistance truck right away."

But immediately returned to baking:

> "Red velvet cake with thick cream cheese frosting."

**Verdict**: ✅ Pass for both.

## Test 5: Translation (Norwegian)

**Objective**: Translate "Hi, I'm following up about the meeting. Can we move it to next week?" into Norwegian in two versions: formal email and casual text message.

### Results

**31B Formal:**
> "Ja, vi sitter på planlagt møte. Ønsker å høre om det er mulig å flytte dette til neste uke. Vennligst si beskjed om det passer for deg og eventuelt hvilken dag og tidspunkt som fungerer best."

**31B Casual:**
> "Ja, jeg følger opp angående møte. Kan vi flytte til neste uke? 😊"

**26B Formal:**
> "Vi sitter på planlagt møte. Er det mulig å flytte dette til neste uke?"

**26B Casual:**
> "Hei, jeg tenkte bare å følge opp møtet vårt. Kan vi flytte til neste uke?"

Both delivered accurate, contextually appropriate translations. The 31B's inclusion of a smiley emoji in the casual version was particularly well-received.

**Verdict**: ✅ Pass for both.

> "Both of the models were able to crush it. I kind of do prefer the 31B, especially the casual one where it like threw in a smiley emoji."

## Test 6: PDF Needle in a Haystack

**Objective**: Find every sentence mentioning "uncertainty" or "cluster sampling" in a dense academic PDF, providing page number, section heading, and verbatim quote.

This test was designed to prevent hallucination—responses can be directly verified against the source document.

### Results

Both models successfully located all mentions with accurate page numbers, section headings, and exact quotes. The 26B's formatting was actually cleaner:

> "I kind of like the formatting of the 26B, to be honest with you."

**Verdict**: ✅ Pass for both.

## Test 7: Vision — Counting People and Glasses

**Objective**: Analyze an image and determine how many people are present, how many wear glasses, and how many wear sunglasses.

### Prompt:
> "How many people are in the image and how many are wearing glasses versus sunglasses?"

### Results

**31B**: "There are five people in this image, two are wearing glasses and one is wearing sunglasses."

**26B**: "There are five people in the image, one is wearing sunglasses, two are wearing glasses."

Both correctly identified the counts.

**Verdict**: ✅ Pass for both.

> "The Qwen 3.5 models were like a bit more descriptive, but again, I was basically asking for this and the model just gave me what I was asking for. These models tend to be a bit less chatty-patty, right? They just give you what you're asking for and they're like done."

## Test 8: Vision — Hand Emoji Finger Counting

**Objective**: Analyze a hand emoji image and count exactly how many fingers and thumbs are visible.

This is a notoriously difficult task for vision models.

### Results

**31B**: ✅ Correct — "There are five fingers and one thumb visible."

**26B**: ❌ Incorrect — "There are four fingers and one thumb visible." The model immediately assumed it was a regular emoji rather than analyzing the image.

**Verdict**: ✅ Pass for 31B, ❌ No pass for 26B.

> "This is where you kind of like start to see the difference between them."

## Test 9: Tool Calling — Web Search

**Objective**: Use web search to answer "Who won the Super Bowl in 2026?" (Information beyond training data cutoff.)

### Challenge with llama.cpp MCP

When using llama.cpp's MCP support, both models failed to use Tavily or Exa search tools automatically—even when they were configured and available:

> "The model should have just used Tavily straight away... It just completely ignored using the MCP and just went for giving me an answer that it didn't know."

Forcing the model with "Look it up online" triggered the search tool, but this shouldn't be necessary.

### Success with Open Web UI

When using Open Web UI's web search tool, both models immediately accessed Tavily and delivered the correct answer—no prompting required.

**Verdict**: ✅ Pass for both (with the caveat that Open Web UI should be used instead of llama.cpp's MCP for reliable tool calling).

> "I shouldn't have to tell it, 'Look it up online.' And also like kind of like tell it like, 'But it already has.' And then the model like not necessarily being humble enough to use the tools that it has available."

## Test 10: Image-to-Code Conversion

**Objective**: Convert an image of a leadership team page into a pixel-faithful HTML recreation with embedded CSS and JavaScript, no external dependencies, semantic DOM, and responsive design.

### Results

The 31B ran at approximately **1.44 tokens per second** (vision significantly slows generation). The 26B completed in roughly **8 minutes**.

**31B Results**: Used placeholder images but accurately reproduced the text, layout, and responsive design. Matched the desktop composition closely.

**26B Results**: Even more impressive—pulled actual images from Unsplash (likely in training data since web search was off):

> "It was even able to get like the images, right, from Unsplash. Me, personally, like I prefer this version here over this one."

The 26B didn't use the exact same image order but captured the overall composition remarkably well.

**Verdict**: ✅ Pass for both.

## Final Verdict: Do Gemma 4 Models Deliver?

Across ten diverse tests spanning coding, creative writing, translation, document parsing, vision, and tool calling, both Gemma 4 variants proved remarkably capable. Here's the scorecard:

| Test | 31B | 26B Active 4B |
|------|-----|---------------|
| Website Generation | ✅ Pass | ✅ Pass |
| 3D Game Creation | ✅ Pass | ❌ Fail |
| Creative Writing | ✅ Pass | ✅ Pass |
| System Prompt Adherence | ✅ Pass | ✅ Pass |
| Norwegian Translation | ✅ Pass | ✅ Pass |
| PDF Needle in Haystack | ✅ Pass | ✅ Pass |
| Vision — Counting | ✅ Pass | ✅ Pass |
| Vision — Hand Emoji | ✅ Pass | ❌ Fail |
| Tool Calling | ✅ Pass | ✅ Pass |
| Image-to-Code | ✅ Pass | ✅ Pass |

### The Trade-offs

The **31B** demonstrates superior reasoning and vision accuracy but at significantly slower speeds (3-4 TPS for text, ~1.5 TPS for vision).

The **26B active 4B** offers blazing fast generation (40+ TPS for text) with competitive accuracy on most tasks—making it ideal for workflows where speed matters more than absolute precision.

> "These models are more than capable. Google really really cooked on this release."

Both models share a characteristic: they're **direct and efficient**. Unlike more verbose models (such as Qwen variants), Gemma 4 models provide concise answers without unnecessary elaboration. Their reasoning traces are notably short—straight to the point rather than novel-length explanations.

### The Bottom Line

For local AI enthusiasts seeking capable multimodal models that run on consumer hardware, Gemma 4 represents another strong option from Google DeepMind. The 31B excels at demanding tasks where accuracy is paramount, while the 26B active 4B offers an attractive balance of capability and speed for everyday use cases.

The choice ultimately depends on your priorities: raw power and precision, or rapid iteration and efficiency. Either way, Google's latest release proves that frontier-level AI performance is increasingly accessible to anyone with a decent GPU.