# RL

## A formal definition
*Reinforcement learning is a framework for solving control tasks (also called decision problems) by building agents that learn from the environment by interacting with it through trial and error and receiving rewards (positive or negative) as unique feedback.*

## The RL Process
To understand the RL process, let’s imagine an agent learning to play a game:
<br/><br/>
<img src="images/RL_process_game.jpg" alt="RL_process" width="700"/>
- Our Agent receives state **S0** from the Environment — we receive the first frame of our game (Environment).
- Based on that state **S0**, the Agent takes action **A0** — our Agent will move to the right.
- The environment goes to a new state **S1** — new frame.
- The environment gives some reward **R1** to the Agent — we’re not dead (Positive Reward +1).

**This RL loop outputs a sequence of state, action, reward and next state.**

## Observations/States Space
Observations/States are the information our agent gets from the environment. In the case of a video game, it can be a frame (a screenshot). In the case of the trading agent, it can be the value of a certain stock, etc.
<br/><br/>
<img src="images/obs_space_recap.jpg" alt="obs_space_recap" width="700"/>

## Action Space
The Action space is the set of all possible actions in an environment.
<br/><br/>
<img src="images/action_space.jpg" alt="action_space" width="700"/>

## Rewards and the discounting
The reward is fundamental in RL because it’s the only feedback for the agent. Thanks to it, our agent knows if the action taken was good or not.

**The agent’s goal is to maximize its cumulative reward, called the expected return.**

That’s why in Reinforcement Learning, to have the best behaviour, we aim to <ins>learn to take actions</ins> that maximize the expected cumulative reward.

To discount the rewards, we proceed like this:

1. We define a discount rate called gamma. It must be between 0 and 1.
  - Most of the time between 0.95 and 0.99.
  - The larger the gamma, the smaller the discount. This means our agent cares more about the long-term reward.
  - On the other hand, the smaller the gamma, the bigger the discount. This means our agent cares more about the short-term reward (the nearest cheese).
2. Then, each reward will be discounted by gamma to the exponent of the time step. As the time step increases, the cat gets closer to us, so the future reward is less and less likely to happen.

Our discounted expected cumulative reward is:
<br/><br/>
<img src="images/rewards_4.jpg" alt="rewards" width="700"/>
