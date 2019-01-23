# 1. Introduction
The goal of this project is to develop and test a (Policy Gradient) Reinforcement Learning Algorithm that is able to successfully control a robot while tracking a target in a simulation environment (UnityML).
For each step that the robot is touching the target object it receives a reward of +0.1.
To control the robot, four continuous actions are available which correspond to the torque commands that are sent to the robot joints. The torque output is scaled to +/-1 where +1 correspondes with maximum torque and -1 is negative max torque. The state space consists of 33 variables (translational and angular position and velocity of the robot joints,...).
The environment is considered solved when the robot achieves a reward of +30 over 100 consecutive episodes.

# 2. Installation
To install the project, the project repository has to be cloned with the command "git clone https://github.com/markusbrn/DrlNDContinuousControlP2.git". Next please set up your python environment correctly. You can find the instructions how to do so here (https://github.com/udacity/deep-reinforcement-learning#dependencies).
Finally you have to download the environment that is used to simulate the robot world. Please follow the links below (depending on the operating system you are using):

- Linux: https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Linux.zip
- Mac OSX: https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher.app.zip
- Windows (32-bit): https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Windows_x86.zip
- Windows (64-bit): https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Windows_x86_64.zip

The unzipped environment files have to be copied in the project repository folder.

# 3. Training and Testing the ML Agent
In order to train and test the agent please start and run the jupyter notebook file from the project repository.