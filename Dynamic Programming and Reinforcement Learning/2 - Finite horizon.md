# Finite horizon

Getting back to our *deterministic shortest path example*, we can now define our value function $v_t(x)$ as the **minimal distance** from $x$ to $s$ in maximal $t$ steps. The **state** is represented by the *crossings* in the road network, and the **action** is just the next node to visit. The **costs** are the *distances* $d(x,y)$.

In the **inventory example**, we define the value functino as the **minimal total costs from $t$ to $T$.** This is done recursively as: 
$$
v_t(x) = \min _{a \geq d_{t} \times}\left\{h x+K \mid\{a>0\}+V_{t+1}\left(x-d_{t}+a\right)\right\}
$$
for all $t=T-1,T-2,...$ and simply $v_T(x) = hx$.

Note that in the example the demand is always set at $2$. 

## General formulation

- **Action**: we have an action depending on the state or the time, and if you take all the actions together at a different point in time you get a **policy**. 

- **Rewards** $r_t(x,a)$ are **immediate** when action $a$ is taken in $x$ at time $t$.
- **Transitions** we have a **transition function** $\Gamma$ that tells us the state we obtain by taking an action $x_{t+1}=\Gamma\left(x_{t}, a_{t}\right)$
  - Note that it's essential that the new state only depends on the current state, not anything more

## Dynamic programming - optimality

We are in a deterministic, finite horizon setting, also knwon as *Bellman's principle of optimality*: what is optimal from $t+1$ is part of the optimal policy from $t$ on!

If you think about the number of possible ways in which you can go from one timestep to the next, you're exponentially increasing the number of paths. 

### Disambiguation

Bellman coined the term DP, as a counterpart to Dantzig's *Linear Programming* (which is a field in optimization). They used *Programming* and not optimization because it sounds too mathematical.

In CS, this term is used for *any method that can be solved recursively by solving subproblems*. **In this course**, we'll just mean solving **dynamic decision problems**. 

## Knapsack problem

We have a finite amount of capacity, we have to choose which items to take without exceeding the weight. Every item has a certain weight and revenue, and we want to take the ones that maximize our revenue while staying in the capacity limit.

- **Description**: N items, weight $w_n$ and value $v_n$ with total weight limit $W$
- **Objective**: maximize total value

We can solve this with linear programming:
$$
\max \sum_{n=1}^{N} a_{n} v_{n} \textrm{ subject to }\sum_{n=1}^{N} a_{n} w_{n} \leq W\textrm{ and }a_{n} \in\{0,1\}
$$
but even with DP, deciding at every point in time whether to take an item or not, stating the remaining weight: $\mathrm{T}=\mathrm{N}, \chi=\{0, \ldots, \mathrm{W}\}, \mathcal{A}_{\mathrm{tx}}=\{0\}$ if $x < w_t$ and $\{0,1\}$, otherwise $r_{t}(x, 0)=0, r_{t}(x, 1)=v_{t}, \Gamma_{t}(x, 0)=x, \Gamma_{t}(x, 1)=x-w_{t}$.

## Stochastic problem

Now, the time is the same but **our states are random**: we take an action without knowing the outcome deterministically. RV are used to make the transition random.

- **Time**: $\mathrm{t} \in \mathcal{T}=\{1, \ldots, \mathrm{T}\}$
- **States**: $x \in X$ is the state space, $X_t$ is a RV representing the state at $t$
- **Actions**: we have the action space, $A_t$ is the action at $t$. The difference is that we cannot predict what we'll do in x time steps
  - Note that the action is a RV because $X_t$ is a RV
- **Transition**: these are now probabilities that you go to $y$ given that you are in state $x$ and take action $a$ $p_t(y|x,a)$
- **Objective**: $\max _{\alpha} E \sum_{t=1}^{\top} r_{t}\left(X_{t}, A_{t}\right)$ i.e. we maximize the expected total reward

A short reminder first: the expected outcome is the sum of the outcomes multiplied by the probability of them happening. For example, for a die it is $1 \times \frac{1}{6} + 2 \times \frac{1}{6}+3 \times \frac{1}{6}+4 \times \frac{1}{6}+5\times \frac{1}{6}+6 \times \frac{1}{6} = 3.5$

We maximize the **expected reward** now, getting: $V_{t}(x)=\max _{a}\left\{r_{t}(x, a)+\Sigma_{y} p_{t}(y \mid x, a) V_{t+1}(y)\right\}$, where the second component is the expected value of the next state.

## Revenue management

This is a problem introduced by airline looking for *dynamic pricing* strategies. The problem is *how many seats to offer in different booking classes and when to close them?*

Let's start by a simple example: we have 2 customers but one seat only, who arrive one-by-one, who pay 100 and 150. What are the consecutive prices? We should probably use 150/150: if we had different pricing, the first one would buy it at 100 and the seat would be gone. 

Taking the thing further, we now have two timesteps, each one with a probability $0.4$ of a customer willing to pay 150, and one willing to pay 100. We would now probably choose 150 first, then 100 in the second one, to be assured that at last someone will get the spot. 

We have $n$ possible prices $f_1<...<f_n$.

Every customer has a willingness-to-pay. In $T$ short time periods, we have at most 1 request per period, and the probability of requests depends on class and time: $\lambda_t(i)$.

If there's no capacity left, we have $x=0$ and therefore $\mathcal{A}_{0}=\{0\}, \mathrm{p}_{t}(0 \mid 0,0)=1, \mathrm{r}_{\mathrm{t}}(0,0)=0$

If there's capacity, we have $\mathcal{A}_{0}=\{0\}, \mathrm{p}_{t}(0 \mid 0,0)=1, \mathrm{r}_{\mathrm{t}}(0,0)=0$

We offer a certain price $a$, then we sum the probability from 1 to $a$, with a direct reward being the revenue we're getting, but going to state $x-1$ as we **sold one ticket of our capacity**, and we sum the probability that no one arrives (and the state stays the same, as the capacity is the same):

$V_{t}(x)=\max _{a=1, \ldots, n}\left\{\sum_{i=1}^{a} \lambda_{t}(i)\left(f_{a}+V_{t+1}(x-1)\right)+\left(1-\sum_{i=1}^{a} \lambda_{t}(i)\right) V_{t+1}(x)\right\}$

Sometimes price fluctuate. How do we avoid prices going down?

