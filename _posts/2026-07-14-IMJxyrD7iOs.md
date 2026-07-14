---
layout: post
title: "3 New PCs, One Giant AI Model… This Shouldn’t Work"
date: 2026-07-14
category: Finance
excerpt: "The dream of local AI development is becoming increasingly tangible. Mini PCs have evolved from novelties into serious development machines capable of running integrated development environments and l..."
word_count: 1078
video_url: "IMJxyrD7iOs"
original_title: "3 New PCs, One Giant AI Model… This Shouldn’t Work"
channel_name: "Alex Ziskind"
transcription_time: 0.0s
model: "unknown"
---
## Clustering Intel's Latest Mini PCs for Local AI Inference

The dream of local AI development is becoming increasingly tangible. Mini PCs have evolved from novelties into serious development machines capable of running integrated development environments and local AI models without incurring API costs. The latest contender is the ASUS NUC 16 Pro, featuring Intel's newest silicon. But what happens when you combine multiple units? This analysis explores clustering three NUC 16 Pros to run a 70 billion parameter AI model that exceeds the capacity of any single device, revealing critical insights into memory bandwidth, software maturity, and clustering strategies.

## Hardware Overview: The ASUS NUC 16 Pro

The ASUS NUC 16 Pro represents a significant step up in mini PC engineering, designed with redundancy and performance in mind. The unit tested features the Intel Core Ultra X7 358H processor, paired with 64GB of RAM and the new Arc B390 GPU. A key feature is the dedicated NPU (Neural Processing Unit), marketed as a separate AI engine. Connectivity includes Wi-Fi 7, Bluetooth 6, dual Thunderbolt 4 ports, dual Ethernet, and extensive I/O options. The chassis allows for easy access via a pull tab, facilitating upgrades. While the 32GB configuration starts around $1,700, the 64GB version commands a premium, positioning these units as high-end tools for developers.

## Single-Box Performance and the Memory Wall

Before clustering, understanding the limits of a single NUC is essential. Local Large Language Model (LLM) inference involves two distinct stages: prompt processing and token generation.

### GPU Acceleration vs. Memory Limits
Testing the Arc B390 GPU against the CPU revealed a clear divergence. Prompt processing speed doubled with the GPU enabled, jumping from approximately 1,000 to 2,200 tokens per second. However, token generation remained stagnant at roughly 46 tokens per second regardless of the engine used. This phenomenon is known as the **memory wall**. Because the GPU shares memory with the CPU, token generation is bottlenecked by memory bandwidth rather than compute power. The GPU's additional muscle cannot overcome the speed at which data moves through the RAM.

### NPU and Software Maturity
The dedicated NPU presents a different set of challenges. Popular inference tools like **Llama.cpp** currently lack support for the NPU, necessitating the use of Intel's **OpenVINO** toolkit. While OpenVINO could run small models on the NPU, larger models required manual rebuilding, as pre-built versions failed to load. This highlights a common issue with bleeding-edge hardware: the software stack often lags behind.

Comparative tests showed that for small models, the GPU remains the fastest engine, while the NPU outperforms the CPU but suffers from slow spin-up times. Notably, when comparing software on the GPU, **Llama.cpp** (using the Vulkan API) outperformed Intel's own OpenVINO by 2.5 times, achieving 34 tokens per second versus 14 tokens per second on the same hardware.

### Power Efficiency
Efficiency metrics favored the NPU in terms of raw power draw, consuming only 17 watts compared to 24 watts for the GPU and nearly 30 watts for the CPU. The NPU is also the coolest and quietest option. However, the GPU proved more efficient per token generated due to its higher speed, completing burst operations faster and using less total energy.

## Clustering Strategies: Size vs. Speed

With the single-box limits established, clustering three NUCs offers a path to greater capacity. However, the approach must align with the goal: handling larger models or increasing throughput.

### Splitting Models for Size
Clustering allows the distribution of a model across multiple machines, pooling their RAM. This was tested with **Qwen 3.6 35B**, a model that fits within a single machine's memory. When split across three NUCs via a 2.5 Gbps Ethernet switch, performance plummeted from 35 tokens per second on a single unit to just 17 tokens per second on the cluster. The overhead of network latency and message passing, combined with the memory wall, negated the benefits of added compute.

The true value of model splitting emerged with **Llama 3.3 70B**, a dense model requiring 75GB of memory. A single NUC with 64GB RAM cannot load this model. However, the three-machine cluster pools 192GB of RAM, successfully loading and running the model. The speed was modest at 1.4 tokens per second, but the model executed, proving that clustering enables access to models otherwise inaccessible.

### Network Upgrades and Bottlenecks
To address potential network bottlenecks, the cluster was reconfigured using a Thunderbolt triangle topology, providing 20 Gbps links between machines. Surprisingly, this yielded no performance improvement. The generation speed remained at 1.43 tokens per second. The bottleneck is not the network bandwidth but the memory access patterns and the sheer volume of tiny messages exchanged between nodes. A wider highway does not resolve a traffic jam caused by the destination's capacity.

### Replicating Models for Throughput
A different clustering strategy involves replicating the full model on every machine and load-balancing requests. This approach does not split the model but scales the ability to handle multiple concurrent queries. Testing this method showed linear scaling: a single machine handled roughly 196 tokens per second under load, while the three-machine cluster achieved nearly 500 tokens per second. This configuration is ideal for serving multiple users or high-throughput applications where the model fits within the RAM of a single node.

## Conclusion and Recommendations

The experiment with three Intel NUC 16 Pros yields clear lessons for AI developers and enthusiasts. The hardware is impressive, offering robust connectivity and strong integrated graphics, but the software ecosystem still has rough edges. Intel's OpenVINO showed compatibility issues, and open-source tools like Llama.cpp remain superior for GPU performance.

The "memory wall" dominates performance on these APUs, limiting token generation regardless of compute power. Clustering these machines is not a magic solution for speed when splitting models; network overhead and memory constraints often degrade performance. However, clustering is invaluable for two specific use cases:
1.  **Size:** Running massive models that exceed the RAM of a single machine.
2.  **Throughput:** Replicating models to serve high volumes of requests efficiently.

For models that fit within a single NUC, clustering for speed is counterproductive. In such scenarios, the hardware might be better utilized as a Proxmox server for virtual machines or other development tasks. As software stacks mature and technologies like RDMA become more accessible on consumer silicon, the potential for mini PC clusters may grow, but for now, users must carefully match their clustering strategy to their specific workload requirements.