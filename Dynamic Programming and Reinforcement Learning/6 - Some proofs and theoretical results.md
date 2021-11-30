# Some proofs and theoretical results

These theorem won't be asked to be reproduced in the exam, but may be applicable in the answers.

Let's talk more about **policies**: they are not allowed to **anticipate**, i.e. know what's going to happen (unless the game is deterministic). They can depend on **all previous states** or also **randomise**, instead of taking one action you flip a coin. Does having a memory on previous states increase the rewards? We may say no, as the state transition only depends on the current state, not the others. 

We assume here a **finite-horizon**, and we call a policy **memoryless** (Markovian, as in Markov Chains) if the action, given the full history (of state/actions up until now), only depends on the current state (there's no memory, just current state):

$P\left(A_{t}=a \mid X_{1}=x_{1}, A_{1}=a_{1}, X_{2}=x_{2}, A_{2}=a_{2}, \ldots, X_{t}=x_{t}\right)=P\left(A_{t}=a \mid X_{t}=x_{t}\right)$

Something similar for transitions: the new state only depends on the current state and current action (we call this the Markov Property). 

$P\left(X_{t+1}=x \mid X_{1}=x_{1}, A_{1}=a_{1}, \ldots, X_{t}=x_{t}, A_{t}=a_{t}\right)=P\left(X_{t+1}=x \mid X_{t}=x_{t}, A_{t}=a_{t}\right)$

Because of this, we start with the Markov Property: if we know that this holds, we can construct (for every policy) a new policy having the same **marginal distributions** (it's important to realize that these are different from joint distributions!).

What is important in practice is assuming you have transition probability in the standard form we've already seen $P\left(X_{t+1}=x \mid X_{t}=x_{t}, A_{t}=a_{t}\right)=p\left(x \mid x_{t}, a_{t}\right)$.

In practice, when you encounter a certain problem, you have to be sure that the Markov Property is satisfied.

If I take a given point in time, what is the probability that I take action 0 or 1? It's always a half for both. Looking at marginal distributions (I look at one time unit), they are the same, but if you look at the joint distributions they are different. In expectations, if the marginal distributions are the same, the sum of expected rewards is just a sum over time units, as expectation of $x+y$ is the expectation of $x$ plus the expectation of $y$. Things are different if you're only interested in the expectation: the expected total reward (still looking at finite horizon) is the same, but if you look at more sensitive criteria you can get different things. 

If you have a time-dependent policy $\alpha$ (having memory), you create a memory-less policy $\alpha'$ inductively (for each timestep) which has the same marginal distribution. $P$ is probability, $p$ are transition probabilities. 

We saw that for every policy there's a Markovian policy with the same reward (it can still randomize, but if you randomize in your policy it's like combining different deterministic policies in one policy)

We've been using Bellman's principle optimality: if you have an horizon from 1 to t, and you look from $t$ to $T$, then as part of the optimal policy you can use the actions that are optimal from the next time on. *The actions that are optimal from today on, then the optimal policy from tomorrow will be part of the optimal policy from tomorrow.*

To prove this, suppose that $\alpha^*$ is an optimal policy for tomorrow, and I want to construct an optimal policy for today. Let's assume our theorem doesnt hold: I can't construct a policy that takes my actions for today, having those for tomorrow. We have the optimal policy $\alpha'$, we assume that $\alpha^*$ is not the right thing to do from tomorrow on (today I'm using $\alpha'$ and at some point I will do something that doesn't accord with $\alpha^*$). We say there is a moment $s$ in which the policies are different. From $s$ on, doing $\alpha'$ fives me a higher reward than $\alpha^*$. That doesn't work as we said that $\alpha^*$ was optimal, but we now proved that there's a better policy.

## Discounting

Assume our action and state spaces are finite, and assume we're maximising the reward over $x,a$. $M$ is the largest value in absolute terms of the rewards, and it always exists as the two spaces are finite. 

The first thing to realize is that if you're doing **discounting**, the expected reward at any point in time is **always less than $M$**. Things are always bounded!

The other thing is *what is the discounted reward*? We exchange total and expectation, and notice that we have an expectation (which is complex as it contains all the $X_t$s ), and because things are finite it works. 

## Bellman equation

We're now going to show that the Bellman equation converges. We've seen the Poisson equation, saying that if you look at the fixed policy and the discount value (the solution of the equation is $V_\alpha$). We showed that when you have actions, Poisson's equation is a linear system (just matrix multiplication) which you can solve (or use recursion), while Bellman has **maximisation** in it to look for an **optimal policy**.

The question now is: *can we show that both have a unique solution*? If you want to formally show that, you need more notation. We're looking at two operators (which work on a vector field, i.e. you know that a function maps from a multidimensional domain into a 1-dimensional space, while now we have vectors as output!) $J, J_\alpha$, mapping value functions into new value functions. The operators are just the equations: the $J$ operator is the maximum, while $J_\alpha$ is just the *Poisson operator*. The equation can be rewritten as $J_\alpha V = r_\alpha + \beta P_\alpha V$.

We have some properties to state: if you have $V$ and $V_\alpha$ and apply $J$ (with or without $\alpha$), then it preserves the ordering. If you have an increasing function, it will still be. This is called an *increasing vector field* or *monotone*. Of course this is vector ordering, and it holds for all the components. The second thing is that it's a contraction: it gets smaller, i.e. if you apply this mapping to $V$ and $V'$ and you look at the difference between the two, then the difference gets smaller. The points somehow get closer to each other. It doesn't matter where you start, you always end up close!

Suppose $V \leq V^{\prime}$, we want to prove something about $J_\alpha V$ using the definition. We copy the definition, and we'd like it to be smaller than $V'$ as defined before: $r_{\alpha}+\beta P_{\alpha} V \leq r_{\alpha}+\beta P_{\alpha} V^{\prime}=J_{\alpha} V^{\prime}$. Remember $P_\alpha$ is the transition matrix, which is a vector consisting of convex combinations of the Ps. You have two vectors that are ordered and you take a combination, you know the ordering is preserved!

We now know that for a given policy ($\alpha^*$) applied to $V'$, which might be the optimal or not. We though know it's $\le$ than the best one. 

Bellman equation says *I want to find a V that satisfies this equation*. 

## Policy iteration

We have a policy alpha, we solve the poisson equation, we get $V_\alpha^\beta$ that is the solution to the Poisson, you apply the policy and look for the maximiser. The $V_\alpha^\beta$ is the solution, and you look for the maximising action. You repeat with the new policy. The idea of the theorem is that if you have a certain $V$ (the solution of the Poisson equation) and you find a policy that for that $V$ does better, than not doing it once but doing it always is better. If you apply it always, that's an improved policy with respect to that one! If you know that you can improve with an $\alpha$, you know that it's a one step improvement and you should do it all the time. 

To prove that, we use the *monotonicity* we derived earlier. In policy iteration you only improve one step, but it kinda holds for the others too! You do one thing better, then you do the whole thing, and you conclude you should do that all the time!

Note that these are vector, when we write $>$ for a vector we mean at least one component is $>$ and the others are $\ge$.

We assume that $J_\alpha V > V$, we derive that $J_\alpha V \ge V$ (obviously), and if you do that again you know by monotonicity that you can apply $J_\alpha$ again: $J_{\alpha}^{2} V \geq J_{\alpha} V$.

We repeat this at infinite $t$, as it always is $\ge$: $V_{\alpha}^{\beta}=\lim _{t \rightarrow \infty} J_{\alpha}^{t} V \geq J_{\alpha} V>V$

We see that the value function gets better, because the number of policy is limited we know that this is finite.

## Discount factor close to 1

We talked about this, we now want to connect this to the average reward case. The first thing we show is that if you vary the discount factor and it gets close to 1, from a certain $\beta$ on (which we call $\beta^*$) the **policy doesn't change anymore**! There's a point in time at which the policy doesn't change anymore. Suppose there's no such $\beta^*$, meaning that the policies change infinitely often. Even as you converge to $\beta\rightarrow 1$. The number of deterministic policies is finite (as we have a Markovian Policy with finite states). There must be two policies $\alpha, \alpha'$ that change infinitely often as you approach 1. Taking a look at the value functions, which are systems of equations containing a $\beta$ too, which if you solve return you a rational function in $\beta$, or a **quotient** of polynomials. That means that the difference between two rational functions is still a rational function, and we know that any rational function has a finite number of zeroes. 

For any problem you consider there's a different $\beta^*$ after which there's just a single, last, optimal policy, which is called the **Blackwell Optimal Policy**. What is interesting is that this policy is also average optimal (i.e. if you get a discount factor close to 1, meaning it's very slow, the future rewards still have a pretty high value). Why is that the case? How can you do averages in discounting? We talked about limiting and time-average, and that time-average exists more often. This long-run average is also called the Cesarian limit (or if you do the limit through the discounting it's called Abelian limit). 