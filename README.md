# Self-Driving Car Simulation with Reinforcement Learning

This repository contains a self-driving car simulation implemented in Python using the Kivy framework. The self-driving car is equipped with a Deep Q Network (DQN) for learning and decision-making in its environment.

The self-driving car simulation involves a car navigating through a 2D map with the goal of reaching specified targets. The car is equipped with sensors to detect the environment, and a DQN is used for decision-making. Users can interactively draw on the map to simulate regions with sand, affecting the car's behavior.

- `ai.py`: Defines the Deep Q Network (DQN) and related components for reinforcement learning.
- `map.py`: Main script for the Kivy-based self-driving car simulation.
- `images`: Directory containing images used in the simulation.

Before running, make sure you have the following also installed 
```python
conda install -c peterjc123 pytorch-cpu

conda install kivy -c conda-forge
```
Run using the command 
```python 
python map.py
```

## Features

- Interactive Map Drawing: Users can interactively draw on the map, simulating regions with sand that affect the self-driving car's behavior.
- Target Navigation: The self-driving car navigates through a 2D map, aiming to reach specified targets.
- Deep Q Network (DQN): The car's decision-making is facilitated by a DQN, a type of reinforcement learning algorithm.
- Save and Load Functionality: Users can save the current state of the AI model and load the last saved state.

## Deep Q Network (DQN)
The self-driving car simulation incorporates a Deep Q Network (DQN) for decision-making. DQN is a type of reinforcement learning algorithm that enables the car to learn an optimal policy for navigating the environment. Here's a breakdown of the key aspects of the DQN implementation:

### Neural Network Architecture (Network class in ai.py)

- Input: The neural network takes a state vector as input, representing the current state of the environment. The state vector includes information such as sensor readings, orientation, and the presence of obstacles (sand) in the vicinity.

- Architecture: 
    - The neural network consists of three fully connected layers (fc1, fc2, fc3).
    - The first layer (fc1) has 30 neurons and applies a rectified linear unit (ReLU) activation function.
    - The second layer (fc2) has 100 neurons with a ReLU activation.
    - The final layer (fc3) produces the Q-values for each possible action (3 actions in this case).
- Output: The output of the neural network is a set of Q-values corresponding to each possible action. The action with the highest Q-value is selected as the agent's next move.

### Experience Replay (ReplayMemory class in ai.py)
- The DQN incorporates Experience Replay to enhance learning efficiency.
- The ReplayMemory class manages a replay memory buffer that stores experiences (state, action, reward, next state) during the agent's interactions with the environment.
- During training, random batches of experiences are sampled from the replay memory, breaking temporal correlations and improving the stability of the learning process.


### Training (Dqn class in ai.py)

- Learning Algorithm:
    - The DQN employs the Q-learning algorithm to update the Q-values based on the Bellman equation, aiming to minimize the temporal difference error.
    - The loss is calculated using the smooth L1 loss function.
- Exploration-Exploitation:
    - The agent selects actions using an epsilon-greedy strategy, balancing exploration (random actions) and exploitation (choosing the action with the highest Q-value).
- Reward Scheme:
    - Rewards and penalties are assigned based on the agent's interactions with the environment. Positive rewards are given for reaching targets, and negative rewards are assigned for collisions or deviations.

## Targets
The self-driving car simulation features three distinct targets that the car must navigate to. These targets are defined as follows:

#### Target A1:
Coordinates: (583, 710) aka Point 1. This is the initial target where the car begins its journey.

#### Target A2:
Coordinates: (628, 237) aka Point 2. After reaching Target A1, the car switches its target to A2.

#### Target A3:
Coordinates: (826, 262) aka Point 3. After reaching Target A2, the car switches its target to A3.

The rotation of targets introduces a dynamic aspect to the navigation task, requiring the car to adapt its behavior based on the current target. The switching of targets allows for continuous learning and exploration of the environment.

By navigating towards these targets and learning from its experiences, the self-driving car aims to optimize its policy for effective and efficient navigation in the simulated environment.

Video simulation of the program can be found [here](https://www.youtube.com/watch?v=gXsBGyxNsag) in youtube.