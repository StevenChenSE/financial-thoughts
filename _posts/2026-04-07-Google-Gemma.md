---
layout: post
title: "Google Gemma"
date: 2026-04-07
category: finance
excerpt: "Google has recently set the local LLM community abuzz with the release of **Gemma 4**, its most capable family of AI models to date. Built upon the advanced **Gemini 3 technology**, Gemma 4 is already..."
word_count: 943
video_url: "T6AvsQVSL74"
---

Google has recently set the local LLM community abuzz with the release of **Gemma 4**, its most capable family of AI models to date. Built upon the advanced **Gemini 3 technology**, Gemma 4 is already demonstrating impressive benchmarks, reportedly outperforming competitors up to 20 times larger. But beyond its technical prowess, one feature truly makes Gemma 4 stand out: its license.

## The Power of Open Source: Apache 2.0

In a move that has been widely celebrated, Google has released Gemma 4 under the **Apache 2.0 license**. This signifies a clear response to the open-source community's long-standing requests. The Apache 2.0 license is fully open and commercially permissive, granting users unparalleled freedom. As the speaker highlights, "That means you can do almost anything you want with this model. Full freedom, no lockin to corporations and complete control over your data and products." This level of flexibility is a significant advantage for developers and businesses alike, fostering innovation and ensuring data sovereignty.

## Integrating Gemma 4 into a Local Workflow

The primary goal for many, including our speaker, Nick (a software developer with over 20 years of experience), is to integrate Gemma 4 into their local development environment. Nick emphasizes that he doesn't view Gemma 4 as a replacement for paid models but rather as a **complement** for "less complex tasks or in situations where I don't want my data leaving my machine."

To get started, Nick utilizes **LM Studio**, a popular tool for running local LLMs. His setup strategy involves:

*   **MacBook (24 GB RAM, M4 Pro chip):** For smaller, more accessible versions of the model.
*   **Desktop (AMD Ryzen 7 CPU, 128 GB RAM, GeForce RTX 460Ti with 16 GB VRAM):** For larger variants, specifically those with 26 or 31 billion parameters.

He opted for a larger quantized version of the 7.5 billion parameter model on his MacBook, anticipating better output quality despite a minimal size difference.

## Key Features of the Gemma 4 Family

While the model was downloading, Google's key highlights for Gemma 4 were reviewed:

1.  **Agent-Based Workflows:** Designed with agents in mind, these models natively support function calling and can produce clean, structured JSON.
2.  **Multimodal Capabilities:** All versions are multimodal, capable of working with images and video. Smaller models (E2B and E4B) even boast native audio support, allowing them to understand speech directly.
3.  **Expansive Context Window:** The smaller versions offer a context window of **128,000 tokens**, while larger ones extend to **256,000 tokens**. This capacity should enable them to handle extensive codebases, a claim that warrants further testing.
4.  **Multilingual Support:** As a bonus, the models support a wide array of languages.

## Hands-On Testing: Performance and Capabilities

### MacBook Pro Test (7.5 Billion Parameters)

After downloading the 8-bit quantized version of the 7.5 billion parameter model, it was loaded into LM Studio. The model, despite its 7.5 billion parameters, showed **4 billion effective parameters** for better performance and utilized approximately **12 GB of memory** on the MacBook. The context window was set to its maximum of 128,000 tokens.

**Task 1: Python Function Generation**
A standard prompt was used: "Write a Python function to sort a list of dictionaries by two keys."
*   **Time Taken:** 49 seconds
*   **Average Speed:** ~31 tokens per second
*   **Latency:** ~4.5 seconds before starting to respond
*   **Verdict:** "Honestly, that's a pretty solid result" for a MacBook Pro with an M4 Pro chip.

**Task 2: Image Recognition**
An image of a desk with a keyboard, Kindle, mouse, and pen was uploaded.
*   **Identified:** Keyboard, mouse, Kindle. It also described the surface and lighting.
*   **Missed:** The pen.
*   **Verdict:** "The important thing is that it captured the overall scene and correctly identified most of the major objects."

### Desktop Test (26 Billion Parameters)

Next, the larger 26 billion parameter version of Gemma 4 was tested on the desktop machine.

**Desktop Specs:**
*   **CPU:** AMD Ryzen 7
*   **RAM:** 128 GB
*   **GPU:** GeForce RTX 460Ti with 16 GB VRAM

**Task: Python Function Generation (Same as MacBook Test)**
*   **Monitoring:** NVT top (GPU usage) and Htop (CPU/RAM usage) were used. It was observed that the full Gemma 4 model didn't fit entirely into the GPU memory, relying heavily on the CPU and system RAM.
*   **Time Taken:** 1 minute 3 seconds
*   **Average Speed:** ~12 tokens per second
*   **Verdict:** Slower than the smaller model, "almost three times slower," but acknowledged as not a "fair direct comparison" due to differing capabilities. This provided a clear understanding of its performance on the desktop setup, which often acts as a powerful server accessed via SSH.

### Advanced Challenge: Visualizing a Sorting Algorithm

Back on the MacBook, a more complex task was presented: visualizing a sorting algorithm by generating an HTML file. This task had been used in previous tests of models like Quen 3.5 and Quen Coder Next.

*   **System Load:** Similar to previous tests, almost all CPU cores were fully utilized, and video RAM was maxed out.
*   **Result:** The model successfully generated a functional and visually appealing HTML file that animated the sorting process, even incorporating a custom font and a real-time speed slider.
*   **Verdict:** "Overall, very solid."

## Conclusion: A Valuable Complement

After thorough testing, the verdict is clear: the Gemma 4 family of models is "really good." While not intended to replace paid models, they serve as an excellent **complement** for simpler tasks or scenarios demanding strict data privacy. The Apache 2.0 license, combined with their impressive capabilities and multimodal features, positions Gemma 4 as a significant contender in the local LLM landscape, offering developers unprecedented freedom and control. 
