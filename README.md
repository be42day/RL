# RL

## A formal definition
*Reinforcement learning is a framework for solving control tasks (also called decision problems) by building agents that learn from the environment by interacting with it through trial and error and receiving rewards (positive or negative) as unique feedback.*
<br/><br/>

## The RL Process
To understand the RL process, let’s imagine an agent learning to play a game:
<br/><br/>
<img src="images/RL_process_game.jpg" alt="RL_process" width="500"/>
- Our Agent receives state **S0** from the Environment — we receive the first frame of our game (Environment).
- Based on that state **S0**, the Agent takes action **A0** — our Agent will move to the right.
- The environment goes to a new state **S1** — new frame.
- The environment gives some reward **R1** to the Agent — we’re not dead (Positive Reward +1).

**This RL loop outputs a sequence of state, action, reward and next state.**
<br/><br/>

### Observations/States Space
Observations/States are the information our agent gets from the environment. In the case of a video game, it can be a frame (a screenshot). In the case of the trading agent, it can be the value of a certain stock, etc.
<br/><br/>
<img src="images/obs_space_recap.jpg" alt="obs_space_recap" width="500"/>
<br/><br/>

### Action Space
The Action space is the set of all possible actions in an environment.
<br/><br/>
<img src="images/action_space.jpg" alt="action_space" width="500"/>
<br/><br/>

### Rewards and the discounting
The reward is fundamental in RL because it’s the only feedback for the agent. Thanks to it, our agent knows if the action taken was good or not.

**The agent’s goal is to maximize its cumulative reward, called the expected return.**

That’s why in Reinforcement Learning, to have the best behaviour, we aim to <ins>learn to take actions</ins> that maximize the expected cumulative reward.

To discount the rewards, we proceed like this:

- We define a discount rate called gamma. It must be between 0 and 1.
- Most of the time between 0.95 and 0.99.
- The larger the gamma, the smaller the discount. This means our agent cares more about the long-term reward.
- On the other hand, the smaller the gamma, the bigger the discount. This means our agent cares more about the short-term reward (the nearest cheese).

Our discounted expected cumulative reward is:
<br/><br/>
<img src="images/rewards_4.jpg" alt="rewards" width="500"/>
<br/><br/>

### Type of tasks
A task is an instance of a Reinforcement Learning problem. We can have two types of tasks: episodic and continuing.
<br/><br/>
<img src="images/tasks.jpg" alt="tasks" width="500"/>
<br/><br/>

### The Exploration/Exploitation trade-off
<img src="images/expexpltradeoff.jpg" alt="expexpltradeoff" width="500"/>
<br/><br/>

## Solving RL problems
How do we solve the RL problem?

In other words, how do we build an RL agent that can select the actions that maximize its expected cumulative reward?

### The Policy π: the agent’s brain
This Policy is the function we want to learn, our goal is to find the optimal policy π*, the policy that maximizes expected return when the agent acts according to it.
We find this π* through training.

There are two approaches to train our agent to find this optimal policy π*:

1. (Directly) Policy-Based Methods
   In Policy-Based methods, we learn a policy function directly.
   
   This function will define a mapping from each state to the best corresponding action. Alternatively, it could define a probability     distribution over the set of possible actions at that state.
   We have two types of policies:
   - Deterministic: a policy in a given state will always return the same action.
     
      <img src="images/policy_4.jpg" alt="policy-based" width="300"/>

   - Stochastic: outputs a probability distribution over actions.
     
      <img src="images/policy-based.png" alt="policy-based" width="300"/>
3. (Indirectly) Value-Based Methods
   In value-based methods, instead of learning a policy function, we learn a value function that maps a state to the expected value of being at that state.

   The value of a state is the expected discounted return the agent can get if it starts in that state, and then acts according to our policy.

   “Act according to our policy” just means that our policy is “going to the state with the highest value”.

   <img src="images/value_1.jpg" alt="value-based" width="350"/></br>
   
   <img src="images/value_2.jpg" alt="value-based" width="350"/>

Most of the time, in value-based methods, you’ll use an *Epsilon-Greedy Policy* that handles the exploration/exploitation trade-off.
<br/><br/>

## Q-Learning (value-based)
### Value-based methods
We have two types of value-based functions:

<img src="images/two-types.jpg" alt="value-based" width="500"/>

We see that the difference is:

- For the **state-value** function, we calculate the value of a state **St**
- For the **action-value** function, we calculate the value of the state-action pair **(St , At)**, hence the value of taking that action at that state.

However, the problem is that to calculate EACH value of a state or a state-action pair, we need to sum all the rewards an agent can get if it starts at that state.

This can be a computationally expensive process, and that’s where the **Bellman equation** comes in to help us.
<br/><br/>

### The Bellman Equation: simplify our value estimation
The idea of the Bellman equation is that instead of calculating each value as the sum of the expected return, which is a long process, we calculate the value as the sum of immediate reward + the discounted value of the state that follows.

<img src="images/bellman6.jpg" alt="bellman" width="500"/>
<br/><br/>

### Monte Carlo vs Temporal Difference Learning
There are two types of methods to update the value function: Monte Carlo and Temporal Difference Learning

- Monte Carlo: learning at the end of the episode
  
  <img src="images/MC-4p.jpg" alt="montecarlo" width="500"/>
  <img src="images/MC-5p.jpg" alt="montecarlo" width="500"/>

- Temporal Difference Learning: learning at each step
  
  <img src="images/TD-2p.jpg" alt="temporaldifference" width="500"/>
  <img src="images/TD-3p.jpg" alt="temporaldifference" width="500"/>

Formulas:

<img src="images/Summary.jpg" alt="summary" width="500"/>

**bootstrapping**

In general, *bootstrapping* in RL means that you update a value based on some estimates and not on some exact values. E.g. In TD(0), the return starting from state *s* is estimated (bootstrapped) by *Rt+1+γV(St+1)* while in MC we use the exact return *Gt*.

### What is Q-Learning?
Q-Learning is an <ins>off-policy</ins> <ins>value-based</ins> method that uses a <ins>TD</ins> approach to train its <ins>action-value</ins> function

<img src="images/Q-function-2.jpg" alt="Q-Learning" width="500"/>

**Algorithm:**

<img src="images/Q-learning-2.jpg" alt="Q-Learning" width="500"/>

<img src="images/Q_Learning_Process_134331efc1.jpg" alt="Q-Learning"/>

**Greedy strategy:**

This strategy always chooses the action that is expected to lead to the highest reward, based on the current knowledge of the environment.

**Epsilon-greedy strategy:**

The epsilon-greedy strategy is a policy that handles the exploration/exploitation trade-off. At the beginning of the training, the probability of doing exploration will be huge since ɛ is very high, so most of the time, we’ll explore. But as the training goes on, and consequently our Q-table gets better and better in its estimations, we progressively reduce the epsilon value since we will need less and less exploration and more exploitation.

<img src="images/Q-learning-4.jpg" alt="Q-Learning" width="500"/>

**Off-policy vs On-policy:**

It's about the sameness between the action choosing in *"training time"* and the action choosing when *"using the model"*.

<img src="images/off-on-4.jpg" alt="off-on-policy.jpg" width="500"/>


