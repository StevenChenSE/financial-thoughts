---
layout: post
title: "How ChatGPT Works: A Guide to Large Language Models"
date: 2026-03-29
category: technology
excerpt: "Large language models like ChatGPT can feel both magical and mysterious. You type anything into a text box, and words appear in response—but what exactly is happening behind the scenes? How is this to..."
word_count: 1053
video_url: "7xTGNNLPyMI"
---

Large language models like ChatGPT can feel both magical and mysterious. You type anything into a text box, and words appear in response—but what exactly is happening behind the scenes? How is this tool built, what are its strengths and limitations, and what are we really interacting with? This guide walks through the entire pipeline of how systems like ChatGPT are created, from raw internet data to the sophisticated neural networks that power them.

## Stage 1: Pre-training—Gathering the Raw Material

The journey begins with **pre-training**, and the first step is perhaps the most monumental: **downloading and processing the internet**.

Companies like OpenAI, Anthropic, and Google create massive, curated datasets from publicly available online text. A representative example is the **FineWeb dataset**, created by Hugging Face. This dataset, after extensive filtering, amounts to about **44 terabytes of disk space**—a surprisingly manageable volume that could nearly fit on a single modern hard drive.

### Where does all this text come from?
The primary source is **Common Crawl**, an organization that has been systematically scraping the web since 2007. As of 2024, Common Crawl has indexed **2.7 billion web pages**. However, this raw data is far from ready for training.

### The Filtering Pipeline
Turning raw web crawl data into a clean, usable dataset involves multiple stages:

1.  **URL Filtering:** Domains associated with malware, spam, adult content, or hate speech are blocked and removed.
2.  **Text Extraction:** Web pages are stored as raw HTML. Specialized processing strips away all the navigation, ads, and code, leaving only the core textual content.
3.  **Language Filtering:** A language classifier identifies the language of each page. For an English-focused dataset like FineWeb, only pages with more than 65% English content might be kept.
4.  **Deduplication & PII Removal:** Near-duplicate content is removed, and systems scan for **Personally Identifiable Information (PII)**—like addresses or Social Security numbers—to filter out those pages.

The result is a vast tapestry of clean text: millions of documents ranging from news articles about tornadoes to curious medical facts, all concatenated into one long sequence.

## From Text to Tokens: The Language of AI

Before this text can be fed to a neural network, it must be converted into a format it understands. Neural networks expect a **one-dimensional sequence of symbols** from a finite set, known as a **vocabulary**.

While you could treat individual bits (0s and 1s) as symbols, this creates impractically long sequences. A better approach is to group bits into bytes (256 possible symbols), but state-of-the-art models go further. They use algorithms like **Byte Pair Encoding (BPE)** to find the most common consecutive symbols and group them into new, single symbols.

This process, called **tokenization**, shrinks the sequence length in exchange for a larger vocabulary. **GPT-4 uses a vocabulary of 100,277 unique symbols, or "tokens."**

You can explore how this works using tools like the [**Tokenizer Playground**](https://platform.openai.com/tokenizer). For example, the phrase "hello world" tokenizes into two tokens: "hello" (ID 15339) and " world" (ID 1917). Capitalization, spaces, and punctuation all affect tokenization.

After tokenizing a dataset like FineWeb, you don't have 44 terabytes of text anymore—you have a **sequence of about 15 trillion tokens**, a numeric representation of the entire training corpus.

## The Core: Training the Neural Network

This is where the computational heavy lifting happens. The goal is to train a neural network to model the statistical relationships of how tokens follow one another in the sequence.

### The Learning Process
1.  **Sample a Context Window:** The training algorithm randomly samples a "window" of consecutive tokens from the massive sequence. In practice, this can be up to 8,000 tokens long, but for simplicity, imagine a window of four tokens.
2.  **Predict the Next Token:** This context window is fed into the neural network. The network's job is to predict the very next token in the sequence.
3.  **Compare and Adjust:** The network outputs a probability for every token in its 100,277-word vocabulary. Initially, these predictions are random. The training system knows the *actual* next token from the data. It then mathematically adjusts the network's internal parameters to **slightly increase the probability of the correct token** and decrease the probability of others.
4.  **Repeat, Everywhere:** This update doesn't happen for just one window. It happens simultaneously for billions of sampled windows across the entire dataset. Through countless iterations, the network's parameters are tuned until its predictions align with the statistical patterns of the training text.

### Inside the "Transformer" Network
The neural network architecture used by nearly all modern LLMs is called the **Transformer**. You can visualize a production-grade example [**here**](https://transformer-circuits.pub/).

*   **It's a Mathematical Function:** The Transformer is a fixed, stateless mathematical expression. It takes a sequence of token IDs as input and outputs a set of probabilities.
*   **It Has "Parameters":** The network's knowledge is encoded in its **parameters** (or weights)—numbers that are adjusted during training. A model might have billions or trillions of these. Think of them as knobs on a complex soundboard; training is the process of finding the right knob settings.
*   **Information Flows Through Layers:** The input tokens are first converted into numerical vectors ("embeddings"). These vectors then flow through a series of layers—including **attention blocks** and **multi-layer perceptrons**—where they are mixed and transformed via simple operations like multiplication and addition.
*   **Biological Metaphor (with Caution):** You can loosely think of the network's intermediate values as the firing rates of synthetic neurons. However, as the video notes, *"your biological neurons are very complex dynamical processes that have memory... there's no memory in this expression."* These are far simpler, stateless mathematical functions.

## What Have We Built?

By the end of this pre-training process, we have a neural network that is a **compressed, statistical model of the patterns in its training data**. It has learned a world model built from the relationships between words, concepts, and facts as they appear across a vast swath of human writing.

This foundation allows it to generate coherent text, answer questions, and mimic reasoning. However, it's crucial to remember its nature: it's an incredibly sophisticated pattern-matching engine, predicting what token is most statistically likely to come next based on its training. Understanding this pipeline demystifies the "magic" and provides a clearer mental model for engaging with these powerful, yet fundamentally statistical, tools.