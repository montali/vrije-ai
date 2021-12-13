# Actor-Critic RL

We usually want to see how our objective function changes when we move the parameter $\theta$.

$\nabla_{\theta} J(\theta)=\mathbb{E}_{\tau \sim \pi_{\theta}}\left[\sum_{t=0}^{T} R_{t}(\tau) \nabla_{\theta} \log \pi_{\theta}\left(a_{t} \mid s_{t}\right)\right]$

We generate a trajectory, and along that trajectory we compute the **total return that we get from that point onwards multiplied by the gradient**.

Imagine you had a single trajectory (instead of averaging over all the possible): in that case, the gradient would be approximated by the single value you get with the expression along that path. If you look at this, and check the rewards along that path, that is just the sum of the rewards that you get following that actions, all the way up to the final position. That is a single sample estimate of the **Q-value**! You start in $s_t$ and apply action $a_t$, that would be the Q value!

We could actually just aswell plug in the Q value. When we look at the gradient, which by definition was equal to $\mathbb{E}_{\tau \sim \pi_{\theta}}\left[\sum_{t=0}^{T} R_{t}(\tau) \nabla_{\theta} \log \pi_{\theta}\left(a_{t} \mid s_{t}\right)\right]$, we can substitute it with $=\mathbb{E}_{\tau \sim \pi_{\theta}}\left[\sum_{t=0}^{T} q_{\pi_{\theta}}\left(s_{t}, a_{t}\right) \nabla_{\theta} \log \pi_{\theta}\left(a_{t} \mid s_{t}\right)\right]$. This is an expectation/mean over all the paths that can be generated using the policy $\pi_\theta$. If you would take $n$ trajectories, you would start somewhere in this $i$ trajectory, and keep doing that until you're absorbed. So, the aforementioned thing, sampled $N$ times, would just be $\nabla_{\theta} J(\theta) \approx \frac{1}{N} \sum_{i=1}^{N}\left[\sum_{t=0}^{T} R_{t}\left(\tau_{i}\right) \nabla_{\theta} \log \pi_{\theta}\left(a_{i, t} \mid s_{i, t}\right)\right]$, i.e. the average of the trajectories. 

So, what does the gradient policy theorem tell us? Remember that when you're talking about gradients (i.e. something that indicates how a function is increasing). Imagine that we fix the state and action, and image that our policy is parametrized by some $\theta$ that is 2-dimensional (you need 2 values to specify to get the policy). You take the gradient and multiply by the Q-value: this tells us the direction that will increase the probability of picking the action having a high q-value. If the q-value was negative, it would point to the **reverse direction of the gradient**, making it less probable than before. 

Remember that with the log being a monotone function, we can use it without altering the shape of the probabilities. The gradient will then point in the same direction!

We have a problem: the value of $q(s,a)$ is not very informative. What we need is some sort of baseline: that's where the advantage comes in. It gives you the relative advantage of an action compared to other actions in that state. 

To change the policy gradient to incorporate the advantage, we look at the Q-value with respect to the actual state value: if an action is bettert than the average, it will go in that direction! Suppose that all the q values were negative (as it may be a bad state): if you kept the form $\mathbb{E}_{\tau \sim \pi_{\theta}}\left[\sum_{t=0}^{T} q_{\pi_{\theta}}\left(s_{t}, a_{t}\right) \nabla_{\theta} \log \pi_{\theta}\left(a_{t} \mid s_{t}\right)\right]$, you would always move away from all actions, but if one is slightly better than the others (while still being negative), we need to move towards that! This leads us to the following:
$$
\nabla_{\theta} J(\theta) \propto \mathbb{E}_{\tau}\left[\sum_{t=0}^{T} \nabla_{\theta} \log \pi_{\theta}\left(a_{t} \mid s_{t}\right)\left(q_{\pi_{\theta}}\left(s_{t}, a_{t}\right)-v_{\pi_{\theta}}\left(s_{t}\right)\right)\right]
$$
The $\propto$ symbol means *proportional to*.

Now, how do we estimate the advantage? Typically, we have 2 neural networks: one that estimates the policy, and one that estimates the advantage. The network parameters are therefore $\theta$ and $w$, i.e. the things we need to learn. Once learned, they give us the function that approximates either the value function or the policy. What's the strategy to actually compute these v,q functions? We don't want to estimate them indipendently, as they're linked through the Bellman equation. A simple way is just estimating the $v$ function, then computing $q$ using the Bellman equations. 

The rewards are unbiased, while the estimate of $v$ is obviously biased: it is an estimate, not a real value! The q-estimate is therefore a combination of unbiased and biased. The reason we're playing with these is that both have pros and cons. The actual returns are unbiased but have high variability (every time you do something, you get a new path, and with a probabilistic policy that path will be very different).

A simple example illustrates this difference: imagine you had a sample of numbers taken uniformly between 0 and some $\theta$. Let's say you are waiting for your tram to arrive, and you have to estimate how many trams are in Amsterdam. Based on the trams you see before yours, you should estimate the $\theta$. We have two ways of approaching this:

- We know that $\theta$ is going to be at least as big as the largest number
- We would know that the average of what we see will be around the right result

In many cases it's better to have low variance and a correct result, instead of an averagely correct result but with high variance. Regulating the parameter $n$ in the n-step returns accounts for this bias/unbiased mixture.

Remember that when we talked about game theory we discussed the discount factor: across different games, the discount factor could be considered as the *probability of continuing the game*. With probability $\gamma$ you will continue, and with $1-\gamma$ you stop. This means that the average is the sum of the possible outcomes, times the probability that the length will be until that time. The probability that the length will be $k$ means that you take $k$ steps and then you stop (that is $1-\gamma$). The expected time until termination is just the , which we obtain shifting $1-\gamma$ and $\gamma$ out of the summation. IF you focus on that thing, it looks like $\sum k \gamma ^{k-1}$, which from high school we know is the $\gamma$ derivative of $\sum \gamma ^k$.

We compute this, and we get that on average you will have a path of size $\frac{\gamma}{1-\gamma}$.

Why is that important? That gives us an idea of how far rewards make a difference: if $\gamma$ is really small (say 0.1), the powers of that decreases very rapidly, and after a few steps the contribution doesn't really matter anymore.

Suppose you had a state space in which you started in the middle, you could have a high number of steps, and if you start the trajectory on the right and the gamma is almost zero, the effective length we can use to estimate is not that long. By the time you hit the reward (absorbing state), the discount factor will be too high for it ot make a difference. A small gamma would be counterproductive, while if gamma is close to one you would feel the influence of rewards almost everywhere. 

[This article is dope](https://towardsdatascience.com/understanding-actor-critic-methods-931b97b6df3f)
