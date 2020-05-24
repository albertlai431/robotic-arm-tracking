## Agent

### DDPG Algorithm

The **DDPG (Deep Deterministic Policy Gradient)** algorithm is based on **Deep Q Learning**. Similarly to DQNs, it uses a replay buffer as well as fixed-Q targets for its networks to help the model converge. Its actor also picks the best action deterministically, rather than stochastically like traditional policy methods. Where DDPG differs from Deep Q Learning is that it is able to generalize to continuous action spaces, something that Deep Q Learning is unable to do.

DDPG algorithm is a (self-proclaimed) actor-critic method. It has 4 networks; an actor network, a critic network, and fixed target networks for both of them. The actor network takes a state as input and outputs the believed best action deterministaically. The critic takes both the state and action as input and outputs the Q-value for that state-action pair. Similarly to DQNs, the loss is calculated between the predicted reward at the current state and of the next state, which is then used to backpropagate through both networks to allow them to learn. The soft update used to update the fixed networks is slightly different than that of Deep Q-learning, it updates only a small percentage of the fixed network at a time (0.1%) to allow the learning to be more stable. 

### Implementation

**Agent**
- Actor (policy) method and its fixed target
- Critic (baseline) method and its fixed target
- One replay buffer 
- Act method: uses the local actor network along with the noise function to output the next action
- Step method: store experience tuple in replay buffer, and learns UPDATE_EVERY
- Learn method: updates local actor and critic networks with gradient descent through loss.backward and optimizer.step, and soft updates the target  for both networks

**Training:**
- Loop over episodes:
  - Reset environment and observe initial state
  - Loop over time steps
    - Select action (Agent act method)
    - Execute selected action
    - Observe reward, next state, and done
    - Pass (state,action,reward,next_state, done) tuple to Agent (Agent step method)
      - Agent stores tuple in replay buffer
    - After UPDATE_EVERY iterations, sample batch of experiences from replay buffer and update both networks (Agent learn method) UPDATE_TIMES times
      - Update target networks after a certain number of updates

### Hyperparameters
```python
BUFFER_SIZE = int(1e6)  # replay buffer size
BATCH_SIZE = 128        # minibatch size
GAMMA = 0.99            # discount factor
TAU = 1e-3              # for soft update of target parameters
LR_ACTOR = 1e-4         # learning rate of the actor 
LR_CRITIC = 1e-3        # learning rate of the critic
WEIGHT_DECAY = 0        # L2 weight decay
UPDATE_EVERY = 20       # how often to update the network
UPDATE_TIMES = 20       # how many times to update the network
``` 

### Deep Q-Network Architecture
#### Actor
1. **Fully Connected**: 33 → 128 (Input layer)
2. **RELU** (Activation)
3. **Batchnorm** (Normalization)
4. **Fully Connected**: 128 → 128 (Hidden layer)
5. **RELU** (Activation)
6. **Fully Connected**: 128 → 4 (Output layer)
7. **Tanh** (Activation)

## Critic
1. **Fully Connected**: 33 → 128 (Input layer)
2. **RELU** (Activation)
3. **Batchnorm** (Normalization)
4. **Concatenation** 128 → 132 (Concatenating actions and state)
5. **Fully Connected**: 132 → 128 (Hidden layer)
6. **RELU** (Activation)
7. **Fully Connected**: 128 → 1 (Output layer)


## Plot of Rewards
![Plot of Rewards](/assets/plot.png "Plot of Rewards")

_Environment solved in 653 episodes!	Average Score: 30.05_


## Ideas for Future Work
To improve performance, other algorithms like PPO, D4PG, GAE and A3C could be implemented. As well, more experimentation could be done with hyperparameters, network layer sizes, and training epochs. Finally, the second environment with 20 agents could be experimented with to improved performance.  