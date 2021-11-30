# Bandits

Suppose we wanted to solve TicTacToe with backward recursion. If you model it, there are 9 positions. The possible states are $3^9$, some of which we will never reach: in any of the 9 fields you can either have $\empty,X,O$.

The reward can be $1$ or $-1$, if you win or lose respectively.

It is more logical to do a forward approach, building a tree and estimating the values of certain states. 

We've seen the discounted Bellman equation $V^{\beta}(x)=\max _{a}\left\{r(x, a)+\beta \sum_{y} p(y \mid x, a) V^{\beta}(y)\right\}$. We can now define the Q values, so we take what is inside the brackets as Q values for the actions. Therefore, pretty easily, $V^{\beta}(x)=\max _{a} Q^{\beta}(x, a)$. The value function is just a function of the state and the optimal action. You can also make recursion for the Q values. If you then substitute again $V$, you can simply obtain:

$Q^{\beta}(x, a)=r(x, a)+\beta \sum_{v} p(y \mid x, a) \max _{a^{\prime}} Q^{\beta}\left(y, a^{\prime}\right)$

Very easily, we've found recursion for the Q values!

Why shouldn't we always use the $V$s and not the $Q$s? If you already know the $r$ and $p$ (means, you're doing *planning* and not *learning*) and you're therefore able to compute the value function, this function gets 1 dimension more, and thus needs more memory! Your program gets more complicated!

## Planning

We know how to solve these small problems for which we know $r$ and $p$.

Both MCTS and Deep Reinforcement Learning are computationally demanding. Sometimes, you can use a structure to  **decompose the problem**. This is what happens with **bandits**.

When dealing with *learning problems*, for which $p$ and $r$ are unknown, we have methods to approximate our value function, for example **Q-learning**. 

## Bandits

The type of bandits we're talking about are **multi-armed bandits**. Slot machines are single-armed bandits, basically. Consider multiple slot machines as a multi-armed bandit!

What's important is that if you do not play an arm, you **have no information about an arm**. The exploration/exploitation tradeoff is crucial here. 

We have two approaches: you can think as every action/arm having its own state space, and it's a markov reward process: if you choose an arm, it transitions to another state. 

### Framework for model-based bandits

We consider $n$ parallel processes, of which we can only play 1 at a time. The transitions, if I'm in $X$ (multidmiensional vector with the state for every bandit), and I choose action $a$, I have to look at the transitions for this bandit $a$: $p_a(y_a|x_a)$. The state of that bandit changes, all the others don't/

We can look at the example in slide 8: we have 3 bandits, if I pull arm 1 I stay in the same state and get $1/10$ reward. IF we only pulled arm 1, we'd get a long-time reward of $2/10$: consider the discount factor $0.5$, we get $1/10 + 1/20 + 1/40$ which is basically $X+0.5X+0.25X+0.125X+...=2$.

## Gittins index

The goal is reducing the dimensionality by looking at an arm at a time. Simply calculating the value of every arm is not sufficient: that value tells us something about what happens if we keep pulling that, but we want something that is more *explorative*. How do we do that? The solution is playing the arm with the **highest Gittins index**:

$m_{i}\left(x_{0}\right)=\max _{T} \frac{E \sum_{t=0}^{T} \beta^{t} r_{i}\left(X_{t} \mid X_{0}=x_{0}\right)}{E \sum_{t=0}^{T} \beta^{t}}$

This is the Gittins index of arm $i$ in state $x_0$. There are two important steps: what we see on top is the discounted reward, and it looks pretty simple. It's the expected sum of rewards up to time $T$. However, note that the $T$ is capital: we divide it by the discounted time, up to T. Finally, we look at the best $T$ we can get: should we pull an arm 1 unit of time, 2 units of time, 3..?

$T$ is not an integer: it is a **random variable**! It's said *stopping time*, and it may depend on the state. Thinking at the example it makes sense: you want to pull the 3rd arm on the first unit, stop if you end up in state 2 but continue if you go to state 3.

$T$ can depend on the state, but it cannot anticipate it. 

You always calculate the Gittins index from a certain time on. 

Can we somehow rewrite this as an infinite horizon problem? We can add a restart option to arm, which takes us to the initial state. To formalize it, what is the Bellman equation? For $x_0$ (starting state, you always play it once), it is the standard expression $V\left(x_{0}\right)=r_{i}\left(x_{0}\right)+\beta \sum_{y} p\left(y \mid x_{0}\right) V(y)$.

The Gittins index of 2 in state 1 is 1: we get a reward of 1, and the summations cancel each other. The Gittins index for 1 is just $1/10$, as we get $1/10$ all the time. Therefore, the optimal action with states $1,2,1$ is $2$, as the Gittins index is the highest. 

