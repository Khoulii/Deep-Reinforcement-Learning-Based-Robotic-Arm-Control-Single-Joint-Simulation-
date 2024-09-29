# Deep-Reinforcement Learning Based Robotic Arm-Control: A Single Joint Simulation

## Problem Statement
The project focuses on controlling a robotic arm, particularly a one-degree-of-freedom joint, to perform the inverted pendulum swing-up task. The goal is to manipulate the joint effectively by applying torque to swing the pendulum into an upright position. This classic control problem involves learning a policy that allows the agent (robotic arm) to balance the pendulum, with continuous action and observation spaces, and rewards based on the angular position, velocity, and applied torque. Also I will attempt using a bottom-up approach based on Deep Q-Networks (DQN).

## Environment
The environment used for this task is "Pendulum-v1", sourced from OpenAI's Gymnasium framework. The simulation allows the agent to apply torque to swing the pendulum upright, with:
- Action space: Torque range from -2.0 to 2.0.
- Observation space: x-y coordinates (constrained between -1.0 and 1.0) and angular velocity (constrained between -8.0 and 8.0).
- Rewards: Based on angular position, velocity, and applied torque.
- Customizable acceleration of gravity (default: 10.0 m/s²).

##  Implementation
Using Python, a rule-based policy was developed to control the robotic arm in the inverted pendulum swing-up task. This policy targets angular velocity and selects actions by dividing the angular velocity range into intervals. The testing phase involved applying the rule-based policy over 100 episodes and accumulating episodic rewards for evaluation. Metrics included average test scores and a moving average to identify trends.
The DQN algorithm is implemented with a neural network designed with three fully connected layers, using experience replay to enhance learning stability. The training loop involves:
- Action selection using an epsilon-greedy strategy.
- Neural network updates based on mean squared error loss between predicted and actual actions.
- Epsilon decay to reduce exploration over time.

## Results
The simple rule based system revealed challenges in effectively controlling the robotic arm:
- Negative episodic rewards ranged from approximately -1315.9 to 1933.65.
- An average test reward score of -1624.35 indicated suboptimal performance.
- The episodic reward plot exhibited a fluctuating pattern, showing no clear improvement trend.
<p align="center">
  <img src="https://github.com/user-attachments/assets/466a8537-a24d-4778-8db0-9c55805f1b6a" width="400">
</p>

During testing over 500 episodes on the DQN algorithm, the following observations were made:
- Negative trend in average episode rewards, with a score of -1185.4.
- Stabilization around episodes 200 to 300, but the agent performed below average.
- The learning process was indicated by a downward trend in the loss per training step and a balanced exploration-exploitation trade-off.
<p align="center">
  <img src="https://github.com/user-attachments/assets/519a80e0-753d-49fe-85de-d17fa3da2f50" width="400">
  <img src="https://github.com/user-attachments/assets/ed0371b1-f830-4a1d-9786-62ea15bc2f19" width="400">
  <img src="https://github.com/user-attachments/assets/d02cb7f6-412d-40ab-ba91-b8bb9a8b4ea0" width="400">
</p>

The DDPG approach showed significant improvement:
- The agent's reward stabilized around 200 after 100 episodes.
- Average score of -156.3 demonstrated a huge improvement compared to both DQN and the rule-based agent.
- Decreasing actor and critic losses indicated improvements in action selection and value estimation.
<p align="center">
  <img src="https://github.com/user-attachments/assets/b2550808-f258-444f-bc88-73f03ce3f636" width="400">
  <img src="https://github.com/user-attachments/assets/f2272848-fc2d-405f-8248-b2522aa867d0" width="400">
  <img src="https://github.com/user-attachments/assets/a57389f0-bd66-4619-a441-f9b4dceb6d36" width="400">
</p>

The SAC approach yielded similar enhancements:
- The agent's reward stabilized around 200 after approximately 70 episodes.
- Average score of -213.2 showed significant improvement compared to previous methods.
- Stable alpha loss indicated a good balance between exploration and exploitation, with decreasing Q1 and Q2 losses demonstrating better accuracy in critic estimations.
<p align="center">
  <img src="https://github.com/user-attachments/assets/40c35512-6a5e-4a77-ae24-eaa6d2535863" width="400">
  <img src="https://github.com/user-attachments/assets/9aaa70b8-2766-4ee0-872e-feb23608c861" width="400">
  <img src="https://github.com/user-attachments/assets/78827898-44ed-470a-a009-6cf60812006" width="400">
</p>

## Conclusion
The refined intelligent system, utilizing both DDPG and SAC algorithms, successfully addressed the limitations of the initial top-down and bottom-up approaches. The improvements achieved through advanced algorithms and neural network architectures demonstrated the capability of effectively controlling the robotic arm in the challenging inverted pendulum swing-up task.
