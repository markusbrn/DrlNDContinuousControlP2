# 1. Introduction
This document describes the training of a robot arm with two joints that shall be able to track the motion of a moving target. For each time step the robot touches the target it receives a reward of +0.1.
To control the robot 4 continuous actions are computed which correspond to the joint torques of the robot and are scaled between +/-1 for joint max and min torque respectively. The state space consists of a total of 33 states (translational and angular position and velocity of the robot joints, etc).

The training task is considered solved when the robot is able to achieve an average score of +30 for 100 consecutive episodes. The project contains the following files with the following functions:

- Continuous_Control.ipynb: Jupyter Notebook to load the required python modules, perform the training process and display the results
- ddpg_agent.py: contains the classes Agent and ReplayBuffer. In the ReplayBuffer (state, action, reward, next_state)-tuples are recorded during robot operation and are stored to be used in the training process.
  The Agent class defines (among others) the functions to select the next action for the robot and to train the robot by applying the DDPG algorithm. This is explained in greater detail in the next section of this document.
- model.py: here the architecture of the actor and critic neural network(s) that are used for the DDPG algorithm are defined.
- checkpoint_actor/critic.pth: Snapshot of a trained networks for actor and critic. For inference only the actor network will be required.

# 2. Learning Algorithm
In this section the Learning Algorithm that is defined in ddpg_agent.py is described in greater detail. DDPG here stands for "Deep Deterministic Policy Gradient". The goal of the algorithm is 


# 3. Network Architecture
In correspondence to the state and output spaces the network has 37 inputs and 4 outputs. In between there are 2 fully connected layers - each with 64 neurons. Relu-functions are used at the output of each of the two fully connected layers.

# 4. Training Progress
To train the network a pool of training samples is built that consists of (state, action, reward, next_state, done)-tuples that are recorded during the training process. To avoid correlations between training samples, batches are sampled randomly from this training pool and are provided to the network.
The following hyperparameters are chosen for the training process:

- To implement the epsilon greedy exploration strategy an initial eps-parameter of 1 is selected. This gives a random exploration strategy at the start of the training process. This value is then multiplied with 0.995 after each episode and bounded from below at 0.01. This means that as the training proceeds the tendency goes towards chosing the action which is assumed to be optimal.
- The discount factor gamma is set to 0.99
- The learning rate for the network is 5e-4
- The parameters of the target network are updated every 4 episodes; the update is performed as a "soft update" where the old network parameters are weighted with 1e-3 and the new parameters are weighted with 0.999.

The training progress can be seen in the following figure:

![Image5](./images/image5.png)

Ultimately it took 479 episodes to train the network.

# 5. Ideas for Future Work
To enhance the training process it could be interesting to prefer training tuples that produce a significant training error. This strategy is known as Prioritized Experience Replay.

Another option is to use two sets of weights for the computation of the target value - one is used for the selection of the optimal action and the other is used to compute the expected Q-value with this action. For the computation of the expected Q-value the frozen weights theta- can be used. The goal of this strategy is to reduce the overestimation tendency of the target network in the case of random estimation errors [5] (which could e.g. be caused by the randomly initialized weights in the early stages of the network training process). This method is known as Double DQN.

# 6. References
[1], [2]: Reinforcement Learning Cheat Sheet (downloaded from https://github.com/udacity/deep-reinforcement-learning/blob/master/cheatsheet/cheatsheet.pdf)

[3]: Mnih V., et al: Human-level control through deep reinforcement learning; NATURE, vol. 508, p.529-533, 2015

[4]: downloaded from https://classroom.udacity.com/nanodegrees/nd893/parts/6b0c03a7-6667-4fcf-a9ed-dd41a2f76485/modules/4eeb16ab-5ac5-47bf-974d-12784e9730d7/lessons/a6829f14-5ef0-4b4a-83ed-234029c5cc60/concepts/22d7ab96-d6d2-4605-8cb6-2a8b5bd087f2

[5] v. Hasselt H., Guez A., Silver D.: Deep Reinforcement Learning with Double Q-Learning; arXiv:1509.06461v3 [cs.LG]; 8 Dec 2015