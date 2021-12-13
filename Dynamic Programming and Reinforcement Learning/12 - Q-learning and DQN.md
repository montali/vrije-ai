# Q-learning and DQN

The expected return following a policy $\pi$ links a state to a scalar. IT is the expectation of the sum from 0 to infinity of the discounted rewards.

In the Q function, we still have the expected return, but we first take a given action $a$ and then we follow the policy $\pi$.
$$
V^{\pi}(x)=\mathbb{E}\left[\sum_{k=0}^{\infty} \gamma^{k} r_{t+k} \mid x_{t}=x, \pi\right]
$$

$$
Q^{\pi}(x, a)=\mathbb{E}\left[\sum_{k=0}^{\infty} \gamma^{k} r_{t+k} \mid x_{t}=x, a_{t}=a, \pi\right]
$$

$Q^*$ means we have the optimal policy, so the optimal policy is just defined as the argmax by $a$ of Q.

Now we can rewrite the $Q$ value function differently, leading to the Bellman operator, meaning we define the function recursively (i.e. as a function of itself):
$$
=\mathbb{E}\left[r_{t}+\gamma Q^{\pi}\left(x_{t+1}, a^{\prime} \sim \pi\right) \mid x_{t}=x, a_{t}=a, \pi\right]
$$
The expectation at time $t$ + the $Q$ at time $t+1$ where the action $a'$ is taken accordingly to policy $\pi$.

We can then specify $Q ^*$, i.e. the expectation of the immediate reward plus $\gamma$ by $Q^*$ with the action picked by the optimal policy $\pi^*$. Knowing that the optimal policy returns the action having the maximum $Q$, we can replace the notation:
$$
=\mathbb{E}\left[r_{t}+\max _{a^{\prime} \in \mathcal{A}} Q^{*}\left(x_{t+1}, a^{\prime}\right) \mid x_{t}=x, a_{t}=a, \pi^{*}\right]
$$
To obtain $Q^*$, we could solve the system of equations, or repeatedly apply Bellman iterations until we find the fixed point, or finally, **learn from trial and error** using the Bellman iterations in the RL context.

## Dynamic Programming

You can now rewrite the equation integrating a *Bellman operator* applied on $Q^*$ itself. The operator is defined as the sum over the $x'$ states on the transition functions (probability of going to a state given $x,a$) multiplied by the immediate reward  and the discounted long term discount. $K$ is any function going from a state action pair into a scalar. We could start initializing $K$ as we want, and then, by applying the bellman operator on this function $K$, you update the $K$ function and you will **converge to $Q^*$**. The bellman operator is applied onto the function $K$, being itself a function of a pair of state, action. 

### Chain problem

If you start from state 1 and you are very greedy, you will just keep on doing $b$ and get a small reward. Otherwise, if you're patient enough (with high discount), you will just accept having no reward at all for 4 steps, then get reward 1 at every timestep. 

If you start with initializing 0s everywhere, after one iteration you'll end up in table 1. Our function is just a lookup table: we initialize it with 0s, and apply the Bellman iteration iteratively.

Looking at the Bellman operator, first we initialize $K$ at 0 for every state-action pair. What will happen is that you will only get the immediate reward after the first iteration, as $K$ is 0 everywhere. Then, your $K$ value function will then contain $0.2$ showing the reward you just got. You then apply again the Bellman iteration, and this time $K$ is not 0 everywhere: you will get the immediate reward plus gamma and the maximum over the action for the next state. After enough iterations, you will converge to a fixed point. Note that $a$ in state 5 is 1(immediate) + discount*reward of doing the best thing in 5, which gives return 1 (same action). For state 4, it is 0.9 as a will take us to state 5, in which its best action rewards us 1.

There are some typos in the slides: $b$ in state 5 will yield 0.18.

## Q-learning

In DP, we were directly given the transition probabilities and the rewards. A more interesting setting is **learning from samples**: you do not need to know exactly the environment (in the form of transition and reward), but you just get some samples.

We initialize the Q value function arbitrarily (as we did with $K$). We are still working in discrete state/action space. 

Then, for each episode, we start in a given starting state (sometimes we choose it, sometimes it's just given by the environment). We do some trial/error in an episode: we choose a given action from the $Q$ value function (maybe using $\epsilon$ greedy), take it and observe the reward in the next state. From that, we can use the update rule:
$$
Q(x, a) \leftarrow Q(x, a)+\alpha\left[r+\gamma \max _{a^{\prime}} Q\left(x^{\prime}, a^{\prime}\right)-Q(x, a)\right]
$$
For a given $(x,a)$ we use our previous value plus a **learning rate** $\alpha$ of the reward + $\gamma$ by the maximum action in the next state. We want our updates to be close to 0 when we're converging, so we subtract the value we already have.

Given a finite MDP, this algorithm will converge to the optimal Q-function as long as two conditions are respected: the learning rate should be high enough such that if summed over infinite timesteps, it is infinite, but low enough to have a square at infinity that is lower than infinity. Secondly, the exploration policy has to be such that we cannot have a policy that is deterministic and will fail to explore some part of the environment: in the end we will have to explore **all actions in all states**.

This is nice, and with small tables it's iteratively working okay. But with continuous features we are desperate.

## Function approximation with deep learning

When you have a number of states that's too high (for example, continuous). For now, we'll consider a discrete action space.

The most important equations, with DL as function approximator, are the following. Instead of having a tabular function approximator, you introduce a function approximator depending on some parameter $\theta$, for example the weights/biases of the NN. Previously, $\theta$ was just the table. 

Then, those parameters will be updated with the following rule: $\theta:=\theta+\alpha \frac{d}{d \theta}\left(Q(x, a ; \theta)-Y_{k}^{Q}\right)^{2}$.

The goal is that at convergence, our Q value estimate will be equal to the target $Y_k^Q$.

The target is very close to the Bellman operator: given a state action pair, you get the reward and the discounted estimate.

This function approximator could be deep learning, but even whatever else (as long as you're able to calculate the derivative).

### Tweaks

Applying the aforementioned technology, we have no guarantee that we will converge. There are though still ways of making this better: the first one is using **a replay memory** and sampling **minibatches**. We therefore save experience, select a minibatch of information, and train on it.

The second idea is the **target network**: the Q value approximator that we use recursively to estimate the next state's Q, will only be updated every once in a while. 