# robotic-arm-tracking
Train an arm with two joints in the Unity Reacher environment to track a ball 🏀 with deep reinforcement learning 🤖 

Languages: Python 3.6 and Pytorch\
Environment: [Unity ML-Agents Toolkit](https://github.com/Unity-Technologies/ml-agents)

## The Environment

**Before Training:** *Reward: 0.0*
![Before Training ](/assets/before-training.gif "Before-training")
<!--- 
**After Training:** *Reward: +17.0*
![After Training ](/assets/after-training.gif "After-training")
-->

### Actions
Actions are in the form of a continuous vector space of size 4, corresponding to torque applicable to the two joints.

### States
The state of the environment has 33 dimensions, including position, velocity, angular velocity, and rotation of the arm.

### Rewards
The agent is given a reward of **+0.1** for every time step when the agent's hand is in the goal location, accumulated throughout the episode. The environment is _solved_ when the agent accumulates an reward of **+30** over 100 consecutive episodes.

## Installation (Windows 10 64-bit)
1. Install [Anaconda](https://docs.anaconda.com/anaconda/install/) if you don't have it already.
2. Open Anaconda Prompt/command line/terminal 
3. Create a new environment (named control-env): `conda create --name control-env python=3.6` 
4. Activate environment: `activate control-env`
5. Navigate to desired directory to download project file: `cd path/to/desired/directory`
6. Clone the repository: `git clone https://github.com/albertlai431/robotic-arm-tracking` 
7. Go to dependencies directory: `cd robotic-arm-tracking/python`
8. Install dependencies (may take a while): `pip install .`
9. Install pytorch 0.4.0 with conda: `conda install pytorch=0.4.0 -c pytorch`
10. Create kernel with environment: `python -m ipykernel install --user --name control-env --display-name "control-env"`

<!--- 
## How to Use
1. Launch jupyter-notebook and navigate to cloned repository directory
2. Open `train.ipynb` and run the code if you would like to train the agent 💪
3. Open `test.ipynb` and run the code if you would like to observe a fully trained agent! 😃
4. **Important:** Before running any code in either of the ipynb files, click **Kernel** on the top bar, **Change kernel > control-env**
5. Remember to deactivate the environment in the Anaconda Prompt/command line/terminal after you are done: `conda deactivate` 

## Potential Issues
- The folder `Banana_Windows_x86_64` may not always work; if you are getting a `UnityTimeOutException`, please go to [this link](https://github.com/udacity/deep-reinforcement-learning/tree/master/p1_navigation#Getting-Started) and replace `Banana_Windows_x86_64` with the correct folder for your system. You may also need to modify the `env` declaration. 
--->