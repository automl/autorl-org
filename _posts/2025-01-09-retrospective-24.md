---
title: "2024 in AutoRL"
categories:
  - Blog
tags:
  - Review
  - 2024
---

TL;DR: From integrating RL with VLMs and LLMs to hyperparameter tuning, environment design, and generalization, 2024 was packed with innovation. 
We’ve highlighted top advancements in AutoRL and included a selection of our own projects at the end. 
Dive in to explore the cutting-edge in RL from the past year!

### Making Reinforcement Learning Work Out of the Box: A 2024 Overview 

2024 was a big year for RL in general and AutoRL specifically. 
Here we collect some of our highlights from last year.

#### AutoML for RL

AutoML for RL remains a key focus area. [Normalization and Effective Learning Rates in RL](https://arxiv.org/abs/2407.01800) by Lyle et al. introduces Normalize-and-Project, maintaining consistent learning rates in dynamic environments, particularly useful for long-term training. 
For hyperparameter tuning, [Generalized PBT](https://arxiv.org/abs/2404.08233) by Bai et al. refines Population-Based Training with pairwise learning to better balance exploration and exploitation, making RL algorithms more robust. 
Meanwhile, [Adaptive Q-Network](https://arxiv.org/abs/2405.16195) by Vincent et al. tackles on-the-fly hyperparameter tuning within RL training for improved real-world applicability. 
In [EVA: Explained Variance Adaptation](https://arxiv.org/abs/2410.07170) Paischer et al. optimize initialization strategies to speed up convergence in fine-tuning and improve performance across multiple domains.

Additional work has further examined the performance and consistency of RL hyperparameters in [Small Batch Deep Reinforcement Learning](https://arxiv.org/abs/2310.03882) and [On the Consistency of Hyper-parameter Selection in Value-based Deep Reinforcement Learning](https://arxiv.org/abs/2406.17523), both by Obando-Ceron et al.
Showing that this remains an open challenge limiting the applicability of RL algorithms.

A central challenge in RL is evaluating agent performance and selecting suitable algorithms. 
[Estimating Agent Skill in Continuous Action Domains](https://www.jair.org/index.php/jair/article/view/15326) by Archibald et al. introduces a Bayesian framework to separate decision-making and execution skills for robust, fine-grained assessments. 
Complementing this, the tool presented in [How to Choose a Reinforcement-Learning Algorithm](https://arxiv.org/abs/2407.20917) by Bongratz et al. simplifies algorithm selection by providing an interactive guide that aligns methods with task requirements, further reducing barriers for practitioners. 
Of course the final step would be to do this automatically. 
Just in case you’re still looking for research inspiration!

<div style="text-align: center;">
  <img src="/assets/images/blog_2024_retro/image6.png" width="600" />
</div>
<div style="text-align: left; margin-top: 5px;">
Figure: Partial screenshot of the RL-Picker tool to select an RL agent for your use-case
</div>
<br>


Improving generalization and efficiency in experience replay is another central theme.
[Investigating the Interplay of Prioritized Replay and Generalization](https://arxiv.org/abs/2407.09702) by Panahi et al. reveals trade-offs in prioritized sampling and proposes mitigations for instability, while [Averaging n-step Returns Reduces Variance in RL](https://arxiv.org/abs/2402.03903) by Daley et al. introduces compound returns that enhance sample efficiency without sacrificing performance.


#### Environment Design

<div style="text-align: center;">
  <img src="/assets/images/blog_2024_retro/image9.png" width="600" />
</div>
<div style="text-align: center;">
  <img src="/assets/images/blog_2024_retro/image2.png" width="600" />
</div>
<div style="text-align: left; margin-top: 5px;">
Figures: Genie generates interactive environments and its high-level architecture
</div>
<br>

Environment design and model-based methods are also undergoing rapid transformation. 
[Genie](https://arxiv.org/abs/2402.15391) by Bruce et al. and [Genie 2](https://deepmind.google/discover/blog/genie-2-a-large-scale-foundation-world-model/) by Parker-Holder et al. propose generative models that create interactive environments from unlabelled videos, enabling agents to learn diverse behaviors. 
Bridging pretraining and deployment, [PreLAR](https://www.ecva.net/papers/eccv_2024/papers_ECCV/papers/03363.pdf) by Zhang et al. introduces action-conditioned pretraining for world models, improving sample efficiency. 
Meanwhile, [DrEureka](https://eureka-research.github.io/dr-eureka/) by Ma et al. harnesses LLMs to automate sim-to-real transfer, [Action Abstractions for Amortized Sampling](https://arxiv.org/abs/2410.15184) by Boussif et al. enhances exploration by abstracting high-level actions, [Causality-Guided Self-Adaptive Representations](https://arxiv.org/abs/2407.20651) Yang et al. adapts to unseen dynamics via causal learning, and [CurricuLLM](https://arxiv.org/abs/2409.18382) by Ryu et al. uses LLMs to design task curricula, accelerating the learning of complex robot skills.

Reward engineering and the offline RL front continue to see impactful innovations. 
[Reward Centering](https://arxiv.org/abs/2405.09999) by Naik et al. stabilizes training by normalizing reward distributions, enhancing consistency across tasks. 
[Image-Based Dataset Representations for Predicting Learning Performance](https://openreview.net/forum?id=AKU4h6BPG7) by Mateos-Meleri et al. leverages convolutional models to predict policy outcomes and guide dataset optimization.

LLMs and VLMs are exciting tools for reward design and policy learning. [GenRL](https://github.com/SforAiDl/genrl) aligns VLMs with world models, enabling tasks to be specified through vision and language prompts, improving multi-task generalization. 
Similarly, [Real-World Offline RL from Vision-Language Model Feedback](https://arxiv.org/abs/2411.05273) by Venkataraman et al. automates reward labeling from suboptimal datasets, and [Online Intrinsic Rewards from LLM Feedback](https://arxiv.org/abs/2410.23022) by Zheng et al. synthesizes dense natural-language-based intrinsic rewards.

<div style="text-align: center;">
  <img src="/assets/images/blog_2024_retro/image3.png" width="600" />
</div>
<div style="text-align: left; margin-top: 5px;">
Figure: GenRL aligns learnt latent models such as DreamerV3 with VLM embeddings to generate rewards for zero-shot generalisation
</div>
<br>

Beyond reward design, LLMs and VLMs reshape how RL agents interact with their environments. 
[ROCKET-1](https://arxiv.org/abs/2410.17856) by Cai et al. employs visual-temporal context prompting to enhance spatial reasoning in open-world tasks, while [LLaRA](https://arxiv.org/abs/2312.02445) by Liao et al. uses conversation-style data augmentation to enrich vision-language policy learning for more sophisticated robotic behaviors. 
In [Adaptive Planning with Generative Models under Uncertainty](https://arxiv.org/abs/2408.01510) Jutras-Dubé et al. reduce replanning frequency without compromising performance, making generative models more practical.

#### Robotics

The field of AutoRL has made strides in robotics as well. [Online Foundation Model Selection in Robotics](https://arxiv.org/abs/2402.08570) by Li et al. balances cost and performance between open-source and closed-source models, while [Learning Robot Soccer from Egocentric Vision](https://arxiv.org/abs/2405.02425) by Tirumala et al. demonstrates an end-to-end approach for multi-agent policies trained purely from on-board vision, expanding RL’s applicability to complex robotic tasks without privileged information.

Major strides have been made towards developing methods that can work on – TODO

#### Benchmarks and Frameworks

Benchmarks and frameworks are critical for driving the field forward. [Kinetix](https://github.com/FLAIROx/Kinetix) by Matthews et al. introduces a procedurally generated physics-based task space for pretraining generalist RL agents, demonstrating the viability of large-scale pretraining. 
[BALROG](https://github.com/balrog-ai/BALROG) by Paglieri et al. provides a comprehensive benchmark to evaluate LLM and VLM decision-making in dynamic environments, while [VisualAgentBench](https://github.com/THUDM/VisualAgentBench/) by Liu et al. focuses on testing multimodal agents in diverse, real-world-inspired scenarios. 
Lastly, frameworks like [AutoRL X](https://github.com/lorifranke/autorlx) by Franke et al. bring RL to the web with a dynamic interface for visualizing and managing RL workflows, improving accessibility and collaboration. 
These benchmarks push the boundaries of evaluation and provide clear goals for future research.

<div style="text-align: center;">
  <img src="/assets/images/blog_2024_retro/image5.png" width="600" />
</div>
<div style="text-align: left; margin-top: 5px;">
Figure: Kinetix generates hardware-accelerated physics-based JAX environments to achieve very fast simulation
</div>
<br>

#### First AutoRL Workshop

A particular highlight of the year was, of course, the first AutoRL workshop at ICML. 
It hosted a diverse set of great work (see all papers [here](https://autorlworkshop.github.io/)), headed by our three best paper award winners [Can Learned Optimization Make Reinforcement Learning Less Difficult?](https://arxiv.org/abs/2407.07082) by Goldie et al., [BOFormer: Learning to Solve Multi-Objective Bayesian Optimization via Non-Markovian RL](https://icml.cc/virtual/2024/35850) by Hung et al. and [Self-Exploring Language Models: Active Preference Elicitation for Online Alignment](https://arxiv.org/abs/2405.19332) by Zhang et al.. 
Furthermore, we had great invited talks by Chelsea Finn, Roberta Raileanu, Pierluca D’Oro, Michael Dennis and Pablo Samuel Castro on everything from RL for robotics, in-context RL, AI-assisted agent design, learning interactive environments and the ALE as a benchmark for AutoRL. 
The videos are publicly available on [the ICML workshop
page](https://icml.cc/virtual/2024/workshop/29960).


#### Our Work

<div style="text-align: center;">
  <img src="/assets/images/blog_2024_retro/image7.png" width="600" />
</div>
<div style="text-align: center;">
  <img src="/assets/images/blog_2024_retro/image1.png" width="600" />
</div>
<div style="text-align: left; margin-top: 5px;">
Figures: ARLBench makes AutoRL evaluation easier with a unified architecture, JAX implementations and representative subsets of environments
</div>
<br>

Of course, AutoRL.org itself has not been idle. Our own work this year includes [HPO-RL-Bench](https://openreview.net/forum?id=MlB61zPAeR) by Shala et al. and [ARLBench](https://arxiv.org/abs/2409.18827) by Becktepe et al., two benchmarks for hyperparameter optimization based on tabular performance data and rapid execution respectively. 
Combined, they make benchmarking HPO for RL less computationally expensive. 
Dierkes et al. show the benefits of joint optimization for these critical components in [Combining Automated Optimisation of Hyperparameters and Reward Shape](https://arxiv.org/abs/2406.18293). 
Works like [Contextual World Models](https://arxiv.org/abs/2403.10967) by Prasanna et al. and [Inferring Behavior-Specific Context Improves ZeroShot Generalization in Reinforcement Learning](https://arxiv.org/abs/2404.09521) by Camaret et al. expand our understanding of generalization and how context can improve it. 
[One-shot World Models Using a Transformer Trained on a Synthetic Prior](https://arxiv.org/abs/2409.14084) by Ferreira et al. shows that prior-fitted networks can be used as in-context world models while [Hierarchical Transformers are Efficient Meta-Reinforcement Learners](https://arxiv.org/abs/2402.06402) Shala et al. use in-context learning to adapt to unseen tasks. 
[Towards Enhancing Predictive Representations using Relational Structure in Reinforcement Learning](https://openreview.net/pdf/04dcbd32d123cd5986ede053708d78cd83aa34d6.pdf) by Mohan and Lindauer improve representation learning methods in RL by incorporating relational inductive biases in self-predictive RL.

<div style="text-align: center;">
  <img src="/assets/images/blog_2024_retro/image8.png" width="600" />
</div>
<div style="text-align: left; margin-top: 5px;">
Figure: Our contextual extension to DreamerV3 allows better generalization to OOD contexts including extrapolation and counterfactuals. The figure compares naively concatenating context to our contextual RSSM.
</div>
<br>

Overall, this has been a very successful year on many fronts: our understanding of how to train RL algorithms increased, integration of foundation models particularly for environment design has made incredible progress and AutoRL is moving forwards both in terms of methods and benchmarking. We’re excited to see what 2025 will bring!
