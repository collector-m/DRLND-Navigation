# Algorithm

We used QNetworks with the following hyperparameters

      BUFFER_SIZE = int(1e5)  # replay buffer size
      BATCH_SIZE = 64         # minibatch size
      GAMMA = 0.99            # discount factor
      TAU = 1e-3              # for soft update of target parameters
      LR = 5e-4               # learning rate
      UPDATE_EVERY = 4        # how often to update the network

## QNetworks

The Qnetwork itself is a 3 layer fully connected, RELU neural network. The first layer is the size of our discrete state space and maps to the action states at the last layer.

The Qnetwork it self is the policy approximator of the RL Agent itself.

## Greedy Epsilon

To avoid missing out on rare but high reward states, we use greedy epsilon with a starting EPS of 1.0. For every step this degrades by .05 and will stop at 0.1.

## Replay Buffer

The agent uses a replay buffer to store samples of episodes. This prevents the loss of rare episodes from training. After a certain number of steps have elapsed (4 because of UPDATE_EVERY), then we are to sample and relearn.

# Results

IT seems as though we don't need more than 1000 episodes as that's where we stop learning anything new.

      Episode 100	Average Score: 1.00
      Episode 200	Average Score: 5.32
      Episode 300	Average Score: 6.99
      Episode 400	Average Score: 9.75
      Episode 500	Average Score: 12.39
      Episode 600	Average Score: 14.34
      Episode 700	Average Score: 14.65
      Episode 800	Average Score: 15.85
      Episode 900	Average Score: 15.53
      Episode 1000	Average Score: 15.29
      Episode 1100	Average Score: 15.27
      Episode 1200	Average Score: 15.62
      Episode 1300	Average Score: 15.96
      Episode 1400	Average Score: 15.55
      Episode 1500	Average Score: 16.20
      Episode 1600	Average Score: 16.11
      Episode 1700	Average Score: 15.88
      Episode 1800	Average Score: 15.73
      Episode 1900	Average Score: 15.89
      Episode 2000	Average Score: 15.61

# Improvement

Moving the saved weights from the save file (which CANNOT be retrieved from the workspace). we could then transfer the weights to an agent playing the game. If we can visualize what's going on with the agent right now, then we can perhaps see what's going on.
