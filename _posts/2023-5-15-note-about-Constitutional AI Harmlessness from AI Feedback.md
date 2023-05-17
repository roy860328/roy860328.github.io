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

Humans only need to define a high-level goal and let the LM reach the goal by itself..

![_config.yml]({{ site.baseurl }}/images/Constitutional_AI/Untitled.png)

![_config.yml]({{ site.baseurl }}/images/Constitutional_AI/Untitled%201.png)

## Useful content

- **Important Points**
    - Scaling Supervision
        - more efficient than collecting human feedback
    - **A Harmless but Non-Evasive (Still Helpful) Assistant**
        - the model was willing to engage with sensitive topics in a harmless, thoughtful manner rather than shut down the discussion
    - Simplicity and Transparency
        - Clarification of AI training objectives by principle
            - (1) by literally encoding the training goals in a simple list of natural language instructions or principles,
            - (2) by using chain-of-thought reasoning [Nye et al., 2021, Wei et al., 2022] to make AI decision making explicit during training,
            - (3) by training AI assistants that explain why they are declining to engage with harmful requests.
- **How (Method)**
    - A series of principles
    - Chain-of-Thought
    - RLHF
        - feedback model to generate comparisons data for PM
- **Why (Why do this experiment and why use this method)**
    - Experiment: Number of Revisions / Number of Revisions + Varying number of constitutional principles used
        - Figure 5 / Figure 6
    - Experiment: Remove Critiques
        - Figure 7
            - **better harmlessness scores for small models (10B)**
            - no noticeable different for large models
    - Experiment: RLHF
        - train a HH model using human feedback labels only for helpfulness
        - replace human feedback labels with model feedback labels for harmlessness
        - all the RL runs in this paper use the same set of training prompts
            - which consists of all the HF and model-generated prompts used for SL-CAI (Section 3.2)
                - plus additional model-generated prompts: 491,142 for red team and 474,300 for helpfulness
        - Results
            - We **didn’t see much benefit to using context distillation**
            - Figure 8 / Figure 9
                - RL-CAI improve Harmless but reduce Helpfulness.
                - **RL-CAI models can be over-trained**
- **Other / Problem Need to Solve**
    - 
- Q
    - These principles were chosen in a fairly ad hoc and iterative way for research purposes. In the future, we believe such principles should be redeveloped and refined by a larger set of stakeholders, and that they should also be adapted depending on the intended usage and location in which the model may be deployed. Since such a small number of bits of information are involved in these principles, it’s worth studying these bits carefully
    - Figure 8
        - Most of company don’t care about Harmless. Can data augmentation skills such as Chain-of-Thought and Principle be used in Helpfulness?
        
        ![_config.yml]({{ site.baseurl }}/images/Constitutional_AI/Untitled%202.png)
        
    - is that would be possible use latent space (z) as a goal like RL goal / Meta-learning / Mulite-task learning? z would be a principle embedding
    - soft preference labels better results than hard labels
        - [Kadavath et al., 2022].

