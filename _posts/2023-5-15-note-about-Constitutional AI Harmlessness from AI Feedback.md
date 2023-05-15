---
layout: post
title: Paper Note - Anthropic Constitutional AI
---

Constitutional AI: Harmlessness from AI Feedback

paper source: [https://arxiv.org/abs/2212.08073](https://arxiv.org/abs/2212.08073)


# Thesis Summary

This method can perform data augmentation to **solve the variety problem that arises from human labeling**.

Using good/bad labels cannot teach humans what they truly want. In a previous paper [Bai et al., 2022], when encountering a harmful request response, humans may choose a much more harmless but helpless response due to their label preference (between A and B). This can lead to a limited response from the model, such as "I don't know".

The pipeline consists of the following steps:

1. Define a series of principles to limit the language model response.
2. Use chain-of-thought to revise the response by the language model itself.
3. Train the model using this data.
4. Finally, fine-tune the model using RLHF.

Humans only need to define a high-level goal and let the LM reach the goal by itself.

## Useful content

- **Important Points**
- **How (Method)**
- **Why (Why do this experiment and why use this method)**
- **Other / Problem Need to Solve**
