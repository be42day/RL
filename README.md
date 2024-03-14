# RL

## A formal definition
*Reinforcement learning is a framework for solving control tasks (also called decision problems) by building agents that learn from the environment by interacting with it through trial and error and receiving rewards (positive or negative) as unique feedback.*

## The RL Process
To understand the RL process, let’s imagine an agent learning to play a game:
<br/><br/>
<img src="drawing.jpg" alt="drawing" width="200"/>
- Our Agent receives state **S0** from the Environment — we receive the first frame of our game (Environment).
- Based on that state **S0**, the Agent takes action **A0** — our Agent will move to the right.
- The environment goes to a new state **S1** — new frame.
- The environment gives some reward **R1** to the Agent — we’re not dead (Positive Reward +1).

**This RL loop outputs a sequence of state, action, reward and next state.**
