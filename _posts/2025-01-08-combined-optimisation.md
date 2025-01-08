---
title: "Optimising Smarter: Joint Hyperparameter and Reward Shaping in Reinforcement Learning"
categories:
  - Blog
tags:
  - Paper
  - 2024
---

TL;DR: Jointly optimising hyperparameters and reward shapes in RL outperforms separate tuning, delivering better performance and stability, even in complex environments like Robosuite Wipe. No hand-tuning required.

### Optimising Smarter: Joint Hyperparameter and Reward Shaping in Reinforcement Learning

RL has achieved remarkable advancements, but one basic challenge remains ever-present: tuning hyperparameters and reward functions.
This is tedious yet critical and can determine the success or failure of an RL algorithm.
Traditionally, these two components are optimised independently, and in benchmark environments, reward functions are often left untuned altogether.
This raises the question: is the tuning of hyperparameters and reward shapes truly independent?

In our work, *Combining Automated Optimisation of Hyperparameters and Reward Shape*, we demonstrated that they actually are dependent.
Our findings show that hyperparameters and reward shapes are highly interdependent, and achieving optimal RL performance requires tuning both components together.
This challenges the conventional approaches and requires a more unified optimisation framework.

#### Interdependency between Hyperparameters and Reward Parameters

To better understand the interdependence of hyperparameters and reward shapes, we conducted experiments training the PPO algorithm on LunarLander.
Specifically, we performed an exhaustive grid search over various hyperparameter values and reward weights, analysing how each pair influenced training performance.

These findings are visualised in Figure 1, which shows the relationships between hyperparameters and reward weights.
For the distance weight, we observed a non-convex region of successful training parameters and that performance varies significantly across the full search space.
Velocity weights exhibited sharp boundaries between regions of success and failure, further showing the balance required for effective tuning.
While our analysis was limited to pairwise combinations, it is reasonable to expect even stronger dependencies in higher-dimensional parameter spaces.

<center>
  <img src="/assets/images/combined_optimisation/heatmap_matrix_rewmin.png" />
  <br>
  Figure 1: Landscapes depicting the average return on Gymnasium LunarLander for pairwise hyperand reward parameters over ten PPO trainings. 
  Lower values (lighter) correspond to faster landing time and, thus, better performance. The yellow lines mark the default values for each parameter. 
  The blue line denotes the best-performing hyperparameter value for each specific reward value. 
  The black dots mark the incumbent configurations found in the joint optimisation experiments
</center>
<br>

Hyperparameters and reward weights are therefore intricately linked, and their joint optimisation is important for achieving the best possible performance in RL applications.
Independent optimisation approaches fail to capture these interdependencies, leaving potential performance gains unexplored.

#### Joint Optimisation in Practice

Recognising these interdependencies, the next step was to design a practical optimisation approach.
Our goal was to examine a method that could seamlessly integrate with existing black-box hyperparameter optimisation workflows while jointly optimising reward shapes.

Figure 2 provides an overview of our optimisation loop. In this framework:
1. Both hyperparameters of the RL algorithm and weights of the reward shape are treated as part of a unified search space.
2. The optimisation algorithm evaluates configurations by training the RL agent and measuring its task performance.
3. Promising configurations are iteratively refined, enabling joint optimisation of both components.

<center>
  <img src="/assets/images/combined_optimisation_2024/optimisation_loop.png" />
  <br>
  Figure 2: Illustration of the two-level optimisation process. 
  Outer loop: hyper- and reward parameter optimisation; inner loop: RL training. 
  In each iteration, the parameter optimiser chooses parameters and receives their performance measured by $\mathcal{O}\_{\text{goal}}(\pi)$
</center>
<br>

We used the DEHB (Differential Evolution with Hyperband) algorithm for this purpose, a state-of-the-art multi-fidelity black-box optimiser.
However, the approach is general and can be easily applied to other black-box optimisation methods.

In our experiments, we compared the joint optimisation of hyperparameters and reward shapes (requiring no hand-tuning!) with two alternative approaches:

1. Optimising only the hyperparameters while using a competitive, pre-defined reward shape.
2. Optimising only the reward shape while keeping the hyperparameters fixed at competitive values.

In the paper, we used the PPO and SAC algorithms across four environments: LunarLander, Google Brax Ant, Google Brax Humanoid, and Robosuite Wipe.
Among these, Robosuite Wipe stands out as a complex, underexplored environment with a challenging reward structure, making it an excellent testbed for evaluating the generalisability of our approach.

We tested two optimisation strategies:

1. Single-objective optimisation, which focuses solely on maximising performance.
2. Multi-objective optimisation, which balances performance and stability by optimising the performance minus a policy’s standard deviation.

The SAC results, as summarised in Figure 3, demonstrated that joint optimisation consistently matched or outperformed the hand-tuned baselines.
In simpler environments like LunarLander and Ant, joint optimisation reliably recovered baseline performance without requiring any manual tuning.
In more challenging environments, such as Humanoid and Wipe, joint optimisation went a step further, yielding superior performance.
For instance, in the Wipe environment, the method achieved a reward score close to the theoretical maximum of 141, showing its ability to handle complex reward structures and extract maximum potential from the task.

<center>
  <img src="/assets/images/combined_optimisation_2024/performance.png" />
  <br>
  Figure 3: Boxplots for the SAC optimisation of the five median performances of each experiment’s optimisation runs.
</center>
<br>

The multi-objective optimisation further enhanced the utility of joint optimisation by improving the stability of the learned policies.
While maintaining a similar level of average performance, this approach significantly reduced the variance in performance across training runs in many cases.
Such consistency is crucial for real-world applications, where reliable policy behaviour can be as important as achieving peak performance.

#### Implications and Future Directions

Our findings have broad implications for RL research and applications:

1. **Unified Optimisation:** Hyperparameters and reward shapes should always be optimised jointly to account for their interdependencies.
2. **Practicality:** Our approach integrates easily into existing optimisation pipelines and scales effectively to new environments.
3. **Generalisability:** The method is robust across diverse benchmarks, including less-studied environments like Wipe, making it suitable for real-world applications.

Future research needs to extend this work by exploring more sophisticated reward function transformations and investigating the trade-off between performance and stability in RL training.

More information about this work and implementation details can be found in the paper's GitHub repository [here](https://github.com/ADA-research/combined_hpo_and_reward_shaping).
