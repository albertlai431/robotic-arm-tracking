## Agent

### DDPG Algorithm

The **DDPG (Deep Deterministic Policy Gradient)** algorithm is based on **Deep Q Learning**. Similarly to DQNs, it uses a replay buffer as well as fixed-Q targets for its networks to help the model converge. 

However, unlike Deep Q Learning, the DDPG algorithm is an actor-critic method. 

### Implementation

**Agent**
- Actor (policy) method and its fixed target
- Critic (baseilne) method and its fixed target
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
    - After UPDATE_EVERY iterations, sample batch of experiences from replay buffer and update both network (Agent learn method)
      - Update target network after a certain number of updates

### Hyperparameters
<!---
```python

```
--->      

### Deep Q-Network Architecture
#### Actor
1. **Fully Connected**: 33 → 128 (Input layer)
2. **Batchnorm** (Normalization)
3. **RELU** (Activation)
4. **Fully Connected**: 128 → 128 (Hidden layer)
5. **RELU** (Activation)
6. **Fully Connected**: 128 → 4 (Output layer)
7. **TanH** (Activation)

## Critic
1. **Fully Connected**: 33 → 128 (Input layer)
2. **Batchnorm** (Normalization)
3. **RELU** (Activation)
4. **Concatenation** 128 → 132 (Concatenating actions and state)
5. **Fully Connected**: 132 → 128 (Hidden layer)
6. **RELU** (Activation)
7. **Fully Connected**: 128 → 1 (Output layer)


## Plot of Rewards
<!---
![Plot of Rewards](/assets/training.png "Plot of Rewards")

_Environment solved in 391 episodes!	Average Score: 13.02_
--->


## Ideas for Future Work
<!---
To improve performance, multiple future steps could be taken. For one, further improvements like Double DQN, Prioritized Experience Replay and Duelling networks could be implemented. In addition, different architectures of the Deep-Q network would be explored to better model the environment. Finally, more experimentation could be done with the hyperparameters! 
--->