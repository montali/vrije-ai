# Monte Carlo Tree Search

## MDP setting

RL is about an agent that can learn from experience. The agent can take actions, transitioning the environment from $x_t$ to $x_{t+1}$. In MDP setting, the agent receives the whole information about the environment.

One thing making this setting generic is that the transitions can be **stochastic**! You take an action, you have a probability distribution over the next states. An example MDP is a deterministic mini grid-world with 9 concrete states and 4 discrete actions. 

The MDP is defined as a 5-tuple $(\mathcal{X}, \mathcal{A}, T, R, \gamma)$:

- $\mathcal{X}$ is a finite set of state (might even be continuous)
- $\mathcal{A}$ is the action space
- $T$ is the transition function, given a state and an action will transition to a new state (it's conditional on the action)
- $R$ is the reward function
- $\gamma$ is the discount factor

We are trying to optimize the **expectation of discounted returns**. We have an expectation over the next timesteps in the trajectory, and the further we are in the trajectory, the more discounted it is. 

This is defined given action $x_t=x$ (where $x$ is given as input to the value function), and afterwards with policy $\pi$.

The optimal value function is the one providing the highest expected return, out of any policy in the policy space, and the optimal policy as the one providing the optimzed expected return. 

## Techniques to solve MDPs

A RL agent can use either of the following, or a combination. The first one is a **representation of a value function** providing a prediction of how good a state is. The second approach is a direct representation of the policy $\pi(x)$ (or $\pi(x,a)$ for stochastic policies). These two are called model-free, as they do not rely on the knowledge on the model. The third is **model-based**, requiring a model of the environment in conjunction with a planning algorithm.

## MTCS algorithms

The idea is that we first learn a model (or we are given it), then we use planning and from that we can act in the environment. These algorithms need a geneartive model for the environment: for a given state, and an action, you need a model that gives you the next state and the reward. The good thing about that is you do not need to know the full transition function, you just need the necessary transitions from the state $x$. Model-free techniques are stupid!

The idea is that you start from a given state, and estimate the expected return for the optimal policy $V ^*(x)$, which is equal to $Q^*(x,a)$ at the condition that $a=\pi^*$. You can see from the top of the tree, and building it for all the possible scenarios. 

The idea is that by exploring your tree, you want to build up the value function such that you'll be able to know the best action.

### Purely random MCTS

We will have an exploration policy that is **purely random**. The idea is that we start by building a search tree from the current state $x_t$. We'll start this loop until convergence, sample a trajectory, and update the estimates of the q-value functions using this formula: $Q(x, a)=\frac{\sum_{x^{\prime}}\left(r+\gamma \max _{a^{\prime} \in \mathcal{A}} Q\left(x^{\prime}, a^{\prime}\right)\right)}{n(x, a)}$.

You build the search tree by randomly exploring your possible actions. If you have 3 possible actions, you'll sample them with probability .33 each. 

You have one given state $x$ that is the input of your function, and if the node is a terminal node you return the heuristic value of the node, while if it is not, for each action $a$ you update the Q value using the aforementioned formula $Q(x, a)=\frac{\sum_{x^{\prime}}\left(r+\gamma \max_{a^{\prime} \in \mathcal{A}} \text { get\_Q\_values }\left(x^{\prime}, a^{\prime}\right)\right)}{n(x, a)}$. Note that $n(x,a)$ is the number of times you picked action $a$ in state $x$.

Suppose you have sampled 18 trajectories in a two-steps stochastic game with 2 possible actions. 

We start from the leaves and get the expected return. For example, with $1,0,1$, the ER is $2/3$. Then, if you want to look at the optimal ER for a state $x^{(1)}$, you get the maximum of the two. Once you have done these, you take them up. 

### MCTS in n-players

There's another player now, wanting to maximize his rewards (zero-sum game). The *maximin approach* can be used to maximize the rewards for a worst case scenario. We try to maximize our own expected return, **in the worst case scenario for the actions that the opponent does**. The only part that changes is the *maximin* scenario: there's not a maximization only now, as the opponent will try to maximize their rewards (minimizing yours). 

We know that this is a very good strategy for many games, and it converges to the optimal policy (as the number of trajectories tends to infinity).

**But**: generally, it needs a lot of trial and error. For instance, chess cannot be solved with random MCTS, as the state space is approximately $30^{85}$, as the size of the tree is $w^d$ with $w$ possible moves and $d$ depth.

If possible, we'd want to only explore the most promising state-action pairs. The second thing we can work on is trying to **cut the trees** at some depth, so that we don't expand the trajectory but just estimate the value function. 

A heuristic evaluator makes the thing affordable. You are not sure that you are getting the optimal policy, rather one that is good enough and saves a large amount of computation. 

In general, we are also interested to go further than heuristics and want to learn during the search. We'll reduce the breadth and depth of search using UCT and a deep learning function approximator.

### UCT

The idea is that you start with a selection mechanism, with which you only expand the actions that are of interest, build the trajectories only for these, and when you reach the leaf you estimate the return by **random rollout**. You want to already know how good this node is without expanding the root, you use the information you got to then inform the selection mechanism. 

In UCT we use a formula that favours taking actions that lead to a high reward: $\underbrace{\frac{w_{i}}{n_{i}}}_{\text {exploitation }}+\underbrace{c \sqrt{\frac{\ln N_{i}}{n_{i}}}}_{\text {exploration }}$.

We still want to explore the environment, with the second term decreasing when we take sufficiently often a given action in a given state. 

We have: 

- $w_{i}:=$ number of wins for the node considered after the $i$-th move
- $n_{i}:=$ number of simulations for the child node (i.e. action)
- $N_{i}:=$ total number of simulations for the parent node
- $c:=$ exploration parameter, in practice usually chosen empirically (in a specific theoretical setting equal to $\sqrt{2}$ )

If the action space is large, the breadth of search can still be huge. You still have to try all the actions at least a couple of times, as long as your $n_i$ is $0$, you are forced to explore the action. 

We could now make use of a learned heuristic of $X$: if you have two states that are similar in terms of *content* and *interestingness*, then the Q value should be close. If you have a function approximator that is able to approximate the value for a state, we could use this as heuristic. Instead of using random rollout, we could try some specific rollout policy that gives a better estimation of how good a state is.

You can use policy approximation to reduce breadth and depth, guiding the search. 

If you have access to a perfect generative model, the learned model will have some inaccuracies. 