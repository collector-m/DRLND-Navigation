# Dependencies and Installation

## Dependencies

Since we're using the Udacity Workspace, I can only guess as to what
python packages you need. At the least you need

* Matplotlib
* Pytorch
* Python 3.4+
* Unity
* Numpy

## Installation

Install all packags into an anaconda environment, install Unity SDK.

## A note about Udacity Workspaces

It usually crashes when I come back to the terminal. Always.


# Implementation

## The Environment

Unity has an ML Agent framework of their own.

### Brains

Since we are using the Unity framework rather than the OpenAI Gym framework
we need to adapt what code we do have to use that env.

Environment information is composed of 'brains' that are used to act
as environmental agents, as opposed to our agent which does the thinking. Each brain has a name we can use.

```
brain_name = env.brain_names[0]
brain = env.brains[brain_name]
```

### Environment Info

From here we can get the `env_info`

```
env_info = env.reset(train_mode=True)[brain_name]
```

### Environment Action State & Size

From the brain we can get info about the number of actions we can do

```
action_size = brain.vector_action_space_size
state = env_info.vector_observations[0]
state_size = len(state) # the size of states available to us
```

## The Code

Since the purpose was to use the DQN network rather than a table based
function approximator, we should re-use the code we have from the DQN
lesson. I found the *model.py* and *dqn* code from that lesson and instead of importing it I just pasted it directly into the notebook.

Only the *dqn* function required change, namely information about the state.

### Agent

The agent is a canonical RL agent with methods for learn, act, and step.

Using EPS-greedy policy, the act function will make sure to avoid missing
out on learning opportunities.

Step also uses a replay buffer to keep a sample of random episodes framework for re-training.

Act is also where the magic happens. That's where the Qnetwork itself is
updated.

### dqn()

This is also re-used code from the QNetwork lesson. It's similar to the function we saw earlier in the lesson. For each episode and for each batch per episode, examine current state, act on that state, extract that reward and then step. If we've reached the terminal state, we're done.

Score is calculated by summing the rewards for all steps in the episode, and appended to a list.
