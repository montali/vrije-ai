# RL - Model-free methods

Today we'll introduce **policy gradient methods** and **Deep Reinforcement Learning**.

## Policy gradient methods

Up until now, we had a policy, value functions (with a consistency check being the Bellman equations). Today, we're looking at an alternative in which we try to estimate the policy directly, without these detours through the value functions. The ingredients are 3: a **parametrised policy** $\pi_{\theta}(a \mid s)$ (a mapping/probability taking you from a state to an action). To make life easier, we look at parametrised versions, i.e. we're looking at a family of possible policies, and by tweaking the parameter you can move around. This is a restriction: the best might not be part of this family, but that's a risk we're willing to take. You can also think of this as an advantage: if you know something about the problem, you could encode this knowledge into the choice of the family of policies. Secondly, we need an **objective function** $J(\theta)$ to maximize, and an **update rule** that effectively does this maximisation, using the current state of the parameter and a learning rate of the gradient: $\theta_{\text {new }} \leftarrow \theta_{\text {old }}+\nabla_{\theta} J\left(\theta_{\text {old }}\right)$.

Imagine that your state space is actually the continuous space between $-1$ and $1$. Whenever you make a step, you get a negative reward, i.e. it costs energy to move around. When you get to the absorbing state, the rewards stop. Your total reward is going to be negative, so you'll want to move to one of the N points that are the closest to you. We're going to introduce a policy family looking like the red curve, i.e. the probability, when you're in X, of **going right**. What you see is that this is centered at $\theta$, and moving $\theta$ you're moving this point. When you're at the right of $\theta$, the probability of going right is almost 1. The total energy you spend is the length of your path. If you're at the left, the probability of going to the right is very low, so we'll go left. 

We want to maximise our total rewards along the path, so if there's a $\gamma$ discount factor we'll have a total reward equal to $R(\tau):=\sum_{t=1}^{T} \gamma^{t-1} r_{t}$. In the past we may have used $g$ for rewards, but $R$ is more used in literature. 

What we have in *abstract terms* is just a simplification of the notation: we have a function depending on the parameter $\theta$. We have a stochastic variable $X$ for which we want to find some function (the reward), $X$ is the path and $\phi$ is the reward. We know we generate the $X$ with a probability that depends on $\theta$. That's what we want to optimize. In order to find the optimum, we compute the derivative. You can then change the order of the operations, push the derivative inside the integral, then the first part doesn't depend on $\theta$. 

Looking at the policy gradient theorem, we're looking at an integral of some probability distribution by some function. Notice that the multiplication by probability is just the **expected value** of the function as long as we sample $X$ from the distribution!

Notice that maximums in the probability correspond to maximums in its log, as it's just rescaled. 

The gradient of the $g$ function is an expectation of the original function times the derivative of the log of the probability. This means that at a given $X$ position, how does $p$ or $log(p)$ change if $\theta$ increases? If you increase $\theta$ slightly by some positive number, how does it change? If we increase $\theta$, the probabilities decrease when we're at the left, increase when we're at the right. 

Looking at the graph, if we have the probability or its log, the shape is the same. Now, what did we learn, basically? We know that if we shift $\theta$, the probability shifts to the right. If now we have our $\phi$ function, we can have a look at the graph, and we're shifting the $\phi$ function ontil it's under the triangular shape. In that case, because of the simmetry, the negative and positive values are weighted equally, and **the gradient is going to 0**.

This means that the equation makes sense, and allows us to understand where to position our probability density!

The general result we obtained for the simplified notation can now be generalised: we were interested in a $\phi$ function which is the reward, the input is not a position but a trajectory, which is sampled from the policy. 

$\nabla_{\theta} J(\theta)=\nabla_{\theta} \mathbb{E}_{\tau \sim \pi_{\theta}}[R(\tau)]=\mathbb{E}_{\tau \sim \pi_{\theta}}\left[R(\tau) \nabla_{\theta} \log p(\tau \mid \theta)\right]$



### Re-explained after I understood shit

Let's say we have a trajectory $\tau$ which just tells us a *history* of an episode, meaning a series of transitions from states with actions and rewards. We know the reward over that trajectory is just the discounted sum of all the rewards we had. Considering we have a policy $\pi$ which is parametrized by $\theta$, our objective function to maximise should just represent the rewards we get using that policy: in other words, if we sampled one million trajectories from that policy and averaged them, that would represent our objective. This, in statistics, is just the **expectation** of $R(\tau)$ of a bunch of trajectories $\tau$ sampled using $\pi_\theta$.

We know, from probability theory, that this expectation is just the integral of the reward of a trajectory,. multiplied by the probability of sampling that trajectory:$J(\theta):=\mathbb{E}_{\tau \sim \pi_{\theta}}[R(\tau)]=\int R(\tau) p(\tau \mid \theta) d \tau$.

To maximise this, we can compute its derivative $\frac{d}{d\theta} g(\theta)$. We can push the derivative inside the integral, and since $R(\tau)$ doesn't depend on $\theta$, we push it further.

Taking a look at this integral, we can think of it as follows: we have our function $\phi(x)$ representing the reward, centered around a point and $0$ elsewhere. If we had 3 examples $\theta$, just representing where we centered the probability distribution, $\theta_1$ and $\theta_3$ would not get much, while $\theta_2$ would get a lot of reward: sampling from that probability distribution (taking an x with probability p), most $x$ would return a $\phi(x)\ge0$. This, ideally, means that we'd like to shift $\theta_1$ to the right and $\theta_3$ to the left.

Now, we can perform some transformations to make this nicer: having the $\frac{d}{d \theta} g(\theta)=\int \phi(x) \frac{d}{d \theta}(p(x \mid \theta)) d x$ formula, we can do a little trick: we multiply and divide by $p(x|\theta)$, obtaining $\frac{ \frac{d}{d \theta}(p(x \mid \theta))}{p(x|\theta)}$ in the middle. High school taught us that the derivative of the $log$ is $\frac{\frac{d}{dx} f(x)}{f(x)}$, so we swap that. Then, if we rename $\left[\frac{d}{d\theta} log(p(x|\theta))\right]$ as $s(x)$, we just have $\int s(x) p(x|\theta) dx$, which, as we said earlier, is just **the expectation of $s(x)$!**

So, we finally rewrite this as 
$$
\frac{d}{d \theta} E_{X \sim p_{\theta}}[\phi(X)]=\mathbb{E}_{X \sim p_{\theta}}\left[\phi(X) \frac{d}{d \theta}(\log p(X \mid \theta))\right]
$$
That's nice! Now, ideally, how do we interpret this? It is pretty straightforward: $\frac{d}{d \theta}(\log p(X \mid \theta))$ just tells us how the probability distribution is changing when we change $\theta$. In other words, if we fixed a random $X$ and shifted $\theta$ (which, for now, just represents the location around which the probability is centered) to the right, we would know that values on the left would decrease (arrows pointing down), while values on the right would increase (arrows pointing up). 

The turning point is now: if we multiply this gradient/derivative, which is telling us how the probability changes when we move $\theta$, by the rewards, it means that if our rewards are high in the negative zone of the gradient (the left), we'll move $\theta$ left, and the opposite for the positive zone! That's exactly what we want! When we'll reach the optimal point, this shifting quantity will reach 0, as the negative side and the positive side cancel each other (reward*-gradient is equal to the inverse of reward*+positivegradient).

Now, we just need a few last steps. If we wanted to consider the probability of a trajectory happening, it would just be the product of the probabilities of all the states/actions happening given the policy. Mathematically speaking, the probability of the trajectory happening (given the policy parametrized by $\theta$) is $\prod_{t\ge0} p(s_{t+1}|s_t, a_t)\pi_\theta(a_t|s_t)$. We then take the logarithm of this, obtaining a sum (log of product is the sum): $\log p(\tau|\theta)=\sum_{t\ge0}log(p(s_{t+1}|a_t,s_t)) + \log(\pi_\theta(a_t|s_t))$. Notice, though, how the first part does not depend on $\theta$. This means that when we take the partial derivative wrt $\theta$, it is considered as a constant and therefore disappears. Finally, we get that $\log(p(\tau|\theta)) = \log(\pi_\theta(a_t|s_t))$. **We can substitute this in the previous result, finally getting rid ofthat $p$**: 
$$
\grad_\theta J(\theta) = \grad \mathbb{E}_{\tau \sim \pi_\theta} [R(\tau)] = \mathbb{E}_{\tau\sim\pi_\theta} \left[\sum_{t\ge0}R_t(\tau) \grad_\theta log \pi_\theta(a_t|s_t)\right]
$$


## Deep Q-Networks

We've seen how to use value functions to derive policies, and how to write the policy directly. We can now try to move from standard RL to **Deep** RL. Why do we need it? The problem is that in simple examples, if the number of states/actions is limited, we can actually compute the value functions with deterministic experience. If the number of state/actions increases, the space becomes huge! There are lots of states, and only for a handful of them you have indication about the value. You therefore need some function approximation, based on the values you actually have,m to try and generalise the results!

We have so far used value functions as a *lookup table*, as every state had a value. That can't be done if the space is too big, so now we define a neural network (or another function approximator!) that gives us an approximation of the real value function!

We want to use a deep neural net and fit it to the value functions, using SGD. 

Imagine we would know what the actual value is in every state: we'd want our neural network mean-squared error to be minimized. How do we solve that? We look at the gradient and move the weights opposite to it, to minimize it. 

We're using *experience* to immediately estimate the optimal Q-value. In order to do that, we construct an approximation. We have a NN outputting the approximation $\hat{q}_{\theta}$ for $q^*$. This Q-learning is off-policy, and in every state we're comparing/backing up the maximum value. Two improvements can be made to this: one is the *experience replay memory* and the other is using a *target network*.

As we collect experience, 4-tuples defined as $\left\{s, a, r, s^{\prime}\right\}$, if you had a trajectory these experiences would be **highly correlated**. If we push all these experiences into a databse, then **sample batches** from the ERM when we filled up this buffer

Basically, what happens is the following:

- You initialize the weights
- Using any policy you want (like $\epsilon$-greedy), you roll-out these trajectories
- Once the ERM is sufficiently filled, you can start selecting batches
- When you have a batch, for all of the experiences in that batch you
  - Compute the target $y$ value, i.e. what you think the value should be: the sum of the reward you got, and the maximum reward you could get in the new state $s'$
  - You compare that to what you actually have in the $q$ estimation and compute the loss
  - Using the loss function, as you use $\theta$ (the network's weights), you can compute new values for $\theta$ to improve the network

### Target network

Note that the **target value we're computing to update the network** is **computed using the network itself**: $y_{i}=\left(r_{i}\right)+\gamma \max _{a_{i}^{\prime}} q_{\theta}\left(s_{i}^{\prime}, a_{i}^{\prime}\right)$.

This is clearly not a good idea! In the *target network approach*, we use an older version of $\theta$ in these computations (which can be said *lagged*) that only gets updated every $N$ iterations. 

If you take a look at the updated formula, we're now using some weight $w^-$ that is only updated once in a while:

$\mathcal{L}_{i}\left(w_{i}\right)=\mathbb{E}_{s, a, r, s^{\prime} \sim \mathcal{D}_{i}}\left[\left(r+\gamma \max _{a^{\prime}} Q\left(s^{\prime}, a^{\prime} ; w_{i}^{-}\right)-Q\left(s, a ; w_{i}\right)\right)^{2}\right]$

