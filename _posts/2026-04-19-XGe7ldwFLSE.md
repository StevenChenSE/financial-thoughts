---
layout: post
title: "M5 Max MacBook Pro Review: Desktop-Level Performance Finally Achieved"
date: 2026-04-19
category: technology
excerpt: "Apple's M5 Max MacBook Pro has arrived, and after spending quality time with this machine, I can confidently say it represents a pivotal moment in laptop computing. This isn't just an incremental upgr..."
word_count: 1444
video_url: "XGe7ldwFLSE"
transcription_time: 0.0s
model: "unknown"
---

## A New Era of Laptop Computing

Apple's M5 Max MacBook Pro has arrived, and after spending quality time with this machine, I can confidently say it represents a pivotal moment in laptop computing. This isn't just an incremental upgrade—it's a leap that finally brings desktop-level performance to a portable form factor.

I've been using the M5 Max as my primary machine, replacing my M4 Max MacBook Pro. Apple's claims about this chip are ambitious: a new GPU architecture with neural accelerators in every GPU core, over four times the peak GPU compute for AI compared to the previous generation, and up to 614 GB per second of memory bandwidth. These are eye-popping numbers. But the real question is: how much of that translates into real-world performance?

This review dives deep into the benchmarks and workloads that matter most—software development and local AI. While I'll be covering the M5 Pro, M5 Air, and the new Mac Studio in future videos, today focuses on the flagship M5 Max and how it compares to both the M4 Max and the M3 Ultra Mac Studio.

## CPU Performance: Single-Core Dominance

As a software developer, single-core performance matters for general system responsiveness and JavaScript-heavy applications. Apple has been absurdly good in this department for years, and the M5 Max pushes that lead even further.

Using Speedometer 3.1, which provides a quick read on browser and JavaScript responsiveness—mapping well to the day-to-day snappiness I actually feel—the M5 Max delivers the highest score I've ever recorded: **60.5**.

For context, the previous generation scores break down as:

- **M5 Max**: 60.5
- **M4 Max**: 56.7
- **M3 Max**: 49.6

That's a meaningful jump that translates directly into a noticeably snappier experience when browsing, editing code, or running responsive web applications.

## Multi-Core Performance: The Core Count Revolution

Single-core performance is only part of the story. Multi-core performance affects IDE responsiveness, code compilation, and heavier parallel workloads. This is where the architectural changes in the M5 Max become particularly interesting.

For testing, I use Mandelbrot, a real algorithm implemented in Python named after mathematician Benoît Mandelbrot. It's available on the benchmarks game website if you want to run comparisons yourself. I love it because it absolutely hammers all the cores.

Running with the recommended 16,000 flag, the results tell a compelling story:

- **M4 Max** (16 cores: 12 performance, 4 efficiency): 14.6–15 seconds
- **M5 Max** (18 cores: 6 super, 12 performance): 11.6–11.8 seconds
- **M3 Ultra** (32 cores): 8.5–8.6 seconds

The M5 Max delivers roughly a 20% improvement in multi-core tasks. That's substantial, but what's more interesting is the architectural change: the M5 Max has **no efficiency cores**. Instead, they're now called "super cores" (renamed from the previous performance designation), and the new performance cores are distinct from the old efficiency cores.

This explains the naming change—Apple couldn't continue calling them efficiency cores when they're now genuinely powerful processing units. The six super cores combined with twelve performance cores give this machine serious parallel processing capability.

What strikes me most is that the M5 Max comes surprisingly close to the M3 Ultra in multi-core tasks, despite having 14 fewer cores. The M3 Ultra remains the champion at 8.5 seconds, but the gap is narrower than the core count suggests.

## Storage Speed: A Massive Leap Forward

The M5 Max introduces what Apple calls new Gen 5 drives, and the speed improvements are dramatic. Testing sequential read and write speeds:

| Machine | Read Speed | Write Speed |
|---------|------------|-------------|
| **M5 Max** | 13,647 MB/s | 16,320 MB/s |
| M4 Max | 7,300 MB/s | 8,200 MB/s |
| M3 Ultra | 7,300 MB/s | 8,200 MB/s |

The M5 Max achieves roughly **twice the read and write speeds** of its predecessors. This matters enormously for local LLMs—large models must be loaded from disk first, and faster storage accelerates startup, caching, and large file transfers.

Random read/write performance also improved:

- **M5 Max**: 59 MB/s read, 45 MB/s write
- M4 Max: 49 MB/s read, 35 MB/s write
- M3 Ultra: 51 MB/s read, 40 MB/s write

While the gains aren't doubled here, they're still meaningful—about 20% faster random operations that benefit compilation and file system operations.

## Memory Bandwidth: A Critical Metric for AI

Memory bandwidth is crucial for local AI workloads, particularly during token generation. Apple's claimed memory bandwidth figures are impressive on paper, but I wanted to see how they translate to real sustained performance.

Using the Stream benchmark (a well-established memory bandwidth test available on GitHub), the results reveal something interesting:

| Machine | Stream Triad Performance |
|---------|-------------------------|
| **M5 Max** | 351,000 MB/s |
| M3 Ultra | 337,000 MB/s |
| M4 Max | 319,000 MB/s |

The M5 Max achieves 351,000 MB/s—about 13% higher than the M4 Max and roughly 4% higher than the M3 Ultra. However, these numbers come in lower than Apple's advertised figures because the Stream benchmark measures sustained memory throughput via the CPU, not peak system performance. Apple quotes peak numbers combining CPU and GPU memory access.

Notably, the M5 Max tops this chart, which raises an important question: does this mean token generation will be faster?

## Local AI Performance: The Real Story

For local LLM deployment, three factors matter most: storage speed, prompt processing (PP), and token generation (TG). Prompt processing—the first stage of inference—leans more on raw compute power and runs primarily on the GPU. Token generation, the second half of what LLMs produce, is more sensitive to memory bandwidth.

Testing with LM Studio, I ran Qwen 3.5 (35 billion active parameters, 3 billion expert parameters) with a 50,000-token context window. Here's what I found:

| Machine | Time to First Token | Tokens/Second |
|---------|---------------------|---------------|
| M4 Max | 1.58 seconds | 79.1 |
| **M5 Max** | 1.58 seconds | 88.49 |
| M3 Ultra | Much faster | 69 |

Interestingly, the M5 Max and M4 Max tie on time to first token, but the M5 Max generates tokens about 12% faster (88.49 vs 79.1 tokens/second). The M3 Ultra surprises with a much faster time to first token but lower overall generation speed.

Moving to a larger model, GPTOSS 12B (120 billion parameters, approximately 60 GB on disk), with the same 50,000-token context and a software architecture design prompt:

| Machine | Tokens/Second |
|---------|---------------|
| M4 Max | 61 |
| **M5 Max** | 65 |
| M3 Ultra | 82 |

The M5 Max edges out the M4 Max with 65 tokens/second versus 61, but the M3 Ultra's 32 cores still dominate at 82 tokens/second. During testing, the M3 Ultra pushed GPU usage to 100% while the M4 Max and M5 Max hovered around 75–79%. Power consumption was telling: both laptops used about 130 watts (with occasional spikes to 154W on the M5 Max), while the M3 Ultra drew a staggering 240 watts.

## The Neural Accelerator Revolution

Here's where things get really interesting. To test prompt processing speed specifically—how fast the model ingests and processes the input prompt—I used a freshly compiled version of Llama CPP running Llama Bench on Gemma 34B (Q4 quantized GGUF version).

The results were **stunning**:

| Machine | Prompt Processing (tokens/sec) |
|---------|-------------------------------|
| M4 Max | 1,855 |
| M3 Ultra | 2,959 |
| **M5 Max** | 4,468 |

The M5 Max achieves **4,468 tokens per second** for prompt processing—nearly 2.4 times faster than the M4 Max and significantly faster than even the M3 Ultra's 2,959 tokens/second.

This is where Apple's neural accelerators in every GPU core prove their worth. The company wasn't exaggerating when they claimed over four times the peak GPU compute for AI. The prompt processing improvements are real, substantial, and transformative for anyone working with large context windows or long documents.

## The M5 Ultra Question

The M5 Max beating the M3 Ultra in prompt processing speed raises an exciting possibility: what might the M5 Ultra deliver? If the M5 Max already surpasses the desktop M3 Ultra in this critical metric, the upcoming Mac Studio with M5 Ultra could be something truly special.

For now, the M5 Max MacBook Pro represents the best laptop Apple has ever made for AI workloads and software development. It won't replace the M3 Ultra Mac Studio for sheer multi-core throughput or massive model capacity (the M3 Ultra still supports 512GB of unified memory versus the M5 Max's 128GB ceiling), but for portable desktop-level performance, this machine is in a league of its own.

The question isn't whether the M5 Max is impressive—it's whether you can afford to wait for the M5 Ultra.