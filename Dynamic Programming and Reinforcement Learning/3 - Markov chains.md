# Markov chains

## Introduction

We are now travelling towards the **infinite horizon**!

In past example, we were talking about **total reward** in a given amount of timesteps $\mathcal{T}=\{0, \ldots, T\}$

We can still talk about **total rewards**, but in the infinite horizon we have **infinite timesteps**!

There are two possibilities for these: infinite horizon with **average reward**, or infinite horizon with **discounted reward**. Note that in the first, the reward you get at the beginning tends to disappear in the long run. Both are good candidates for, for example, inventory management. 

We could even talk about *continuous time* $\mathcal{T}^{\prime}=[0, \infty)$, still being usable with discounted or average reward.

This chapter will be about **Markov chains**, which will serve as background for long-run average rewards. 

## Markov Chains

We have **infinite time**, states being $|x|<\infty$ with $X_t$ state at time $t$, no actions/rewards, and transitions without actions: $p(y \mid x)=P\left(X_{t+1}=y \mid X_{t}=x\right)$.

We have some initial distribution, over the states with $\pi_0$ being the initial distribution (probability of state at $X_0$ being $x$ is $\pi_0(x)$).

What is the distribution at a given $t$? We'll need a forward recursion to do that. The probability at time $q$ that we're in state $y$ is the sum over all the possible states at time 0, and the transition probability that we go from $x$ to $y$. I look at where I am right now, then I check for all the initial states what the probability of being there is, and the probability from there to transition to the state I'm interested in. You can work this out using **Bayes' law**.

You can then of course repeat this in exactly the same way. $\pi_t$ can always be obtained from $\pi_{t-1}$. When you look at this, you can see that this looks like some entry of a matrix multiplication. This is true: $$\pi_{t+1}^{\top}=\pi_{t}^{\top} P$$ with the $P$ matrix being defined as $P_{x y}=p(y \mid x)$.

If you take an example and look to find the distribution at $t=4$, we try to check the timesteps from 0:

- We know that as $\pi_0$ is $1,0,0$, of course we are in state 1 at the beginning;
- Therefore, at time $1$ we surely are in state $2$, so $0,1,0$
- And so on...

0,1/2,1/2 is the answer.

**Simulation** is a good alternative: we simulate many times, and take the frequencies. 

### Properties

We call something a **path** in a Markov Chain if you have a chain of states for which all the transitions have a positive probabilities, i.e. a series of states that have a non-zero probability of happening. 

A MC is **communicating** if from any state I can reach any other state and back: there's a path between any  two given states, we don't know how long. We'll assume this to be true. We also assume the MC to be **aperiodic**, i.e. the gcd of lengths of all paths from a state to itself is 1. If you have a path of length 2 and one of length 3, the gcd is 1. But if all the paths have even length, then the GCD is 2 and we call it **periodic**.

To get the *time-average* distribution, you sum the distribution up to $t$ and then average. You can simply look at the limiting distribution to understand.

Then you have the **stationary distribution**: you have a distribution and you look at one step further, then you stay in the **same distribution**. 

Finally, a **theorem**: for aperiodic & communicating MCs, the time-average, limiting and stationary distributions **exist**, are **the same**, **unique** and **independent of $\pi_0$**.

## Markov decision chains

Now, for every state we have similar balance. We have the summation over the action for a certain state y, and this should be interpreted as the probability of being in state $y$: you sum over the actions (probability of being in state $x$ and choosing action $a$). These are the **balance equations**. We then want to maximize the **total expected reward**, which is very similar to the markov reward chains, but now we sum over all the states and actions. This is now an optimization problem with a linear objective. Applying it to the example, we add action 2 from state 3. Looking back at the previous slide, we sum over x and as, summing the reward times the state/action. 

### Policy iteration

We have a policy $\alpha$, we define transition probabilities ($P_{\alpha}(x, y)=p(y \mid x, \alpha(x))$) and rewards ($r_{\alpha}(x)=r(x, \alpha(x))$. We solve the Poisson equation we have previously seen for this fixed policy, then we check whether we can improve the policy: we look for another policy, state by state, looking for a higher value of $r_{\alpha^{\prime}}+P_{\alpha^{\prime}} V_{\alpha}$. We terminate when we have found the optimal policy. Be careful: if you have two policies having the exact same $V,\phi$ you may alternate between these infinitely. 

## Bellman equation

We saw, on the previous slide, in the policy iteration, that this policy improvement step terminates if you have an optimal policy. Apparently, the maximizer is the optimal policy as long as $V$ is the optimal one. This holds for the optimal policy: $r_{\alpha_{*}}+P_{\alpha_{*}} V_{\alpha_{*}}=\max _{\alpha^{\prime}}\left\{r_{\alpha^{\prime}}+P_{\alpha^{\prime}} V_{\alpha_{*}}\right\}$. We also know that the following holds for every policy: $V_{\alpha_{*}}+\phi_{\alpha_{*}}=r_{\alpha_{*}}+P_{\alpha_{*}} V_{\alpha_{*}}$. We can combine these! $V+\phi=\max _{\alpha}\left\{r_{\alpha}+P_{\alpha} V\right\}$ which looks like the Poisson, with a maximisation. This is the **Bellman equation!** (in vector notation)

There's nothing linear in here: there's a maximisation. 

Note that $e$ is the unit vector, not Euler's number.

