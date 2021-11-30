# Continuous time

An example of this is *admission control*, in which we admit customers to a queue. There's lots of applications for continuous time.

Arrivals often occur in what is called a Poisson process, and service according to an exponential distribution. For service times, we often assume an exponential distribution for mathematical convenience. The exponential distribution is always non-negative, and the probability that the duration is smaller than $t$ has this form: $1-\mathrm{e}^{-\mu t}$

You can derive that the expectation of this is just $1/\mu$.

This type of distribution is **memoryless!**

## Poisson process

We know that the time that passes between two arrivals is determined by an exponential distribution $X \sim \exp (\mu): X \geq 0, P(X \leq t)=1-\mathrm{e}^{-\mu t} \forall t \geq 0, E X=1 / \mu$, being memoryless. We would though like a way of expressing the number of arrivals we expect in a given interval of time. This is done by the **Poisson processes**, with probability of having $n$ arrivals in a time $t$ equal to: $N \sim \operatorname{Poisson}(\lambda) \Leftrightarrow P(N=n)=\frac{\lambda^{n}}{n !} \mathrm{e}^{-\lambda}, E N=\lambda$.

The bigger $\lambda$, the smaller the expectation, if the interarrivals have an exponential distribution then the horizon has a Poisson distribution. In expectation, the interarrival time is $1/\lambda$.

If $N$ is a Poisson distribution, the probability of N being equal to $n$ is $\frac{\lambda^{n}}{n !} \mathrm{e}^{-\lambda}$, and the expectation is just $\lambda$ (1 over the duration of the exponential). Also, if $N$ (the arrivals in a certain period) has a Poisson distribution, the process is a **Poisson process**. In a process, you look at the arrival time and you **count** the arrivals for every point in time. 

## Semi-Markov processes

We use the term *process* in continuous time, and *chain* for discrete time. We now have a Markov Chain in discrete time, (you can see it as something continuous but with exactly 1 between times). We introduce the **sojourn time**, being the time in which we stay in a state $s$, and we now do not know the number of timestamps in an interval of continuous time, or in other words, how many **jumps** we did.

We are interested in the long-time distribution, but taking into account that **I spent more time in some states than others!** To do so, we have to integrate over time. It's pretty easy to calculate this time-average distribution. For that, we can use the stationary distribution of the so-called *embedded chain* (just looking at jump times), so $\pi^*$ is the stationary distribution if you just look at jump times. 

$\nu_{*}(x)=\frac{\pi_{*}(x) \tau(x)}{\sum_{y \in \mathscr{X}} \pi_{*}(y) \tau(y)}$ (note that there's a typo in the slides)

Remember that $\tau$ is the expected value of the time that passes between arrivals, so this makes sense: we are just multiplying the probability of being in a state, by the time we expect the state to last. This quantity $\nu_{*}$ therefore just represents the time we spend in a state. If we multiply it with the rewards, we can get the long-time average reward. Note that the denominator is just the sum over all the states.

We basically divide the time we spent in $x$ by $N_n(x)$, i.e. the number of visits to $x$ in the first $n$ steps. 

Now, note that a *semi-Markov* process is not Markovian: as we're not performing jumps at every instant of time (it's continuous!), sometimes we need memory about previous time than the current. In other words, for arbitrary $t_{1}, \ldots, t_{n}, s:$
$P\left(X_{t_{n}+s}=x \mid X_{t_{1}}=x_{1}, \ldots, X_{t_{n}}=x_{t}\right) \neq P\left(X_{t_{n}+s}=x \mid X_{t_{n}}=x_{t}\right)$

If we though condition the $t_1,\dots,t_n$ to be **jump times**, this is a Markov chain.

## Exponentiality

Suppose you have two exponentials ($\lambda,$and$ \mu$), what is the probability that one rings earlier? The probability is $P(X<Y)=\frac{\lambda}{\lambda+\mu}$. Now, semi-markov processes have the memoryless property, and if they have exponential sojourn time we just call them markov processes and not *semi*. In a semimarkov process you have your toll, and a $p$ to move to a different state. You are in a state $x$ and $T$ exponential, and you move to state $y$ with probability $p(y|x)$. This is equivalent to having two clocks and moving to a new state when one of the two clocks goes off, wondering what's the probability. As before, on the right we had the sum of the two components on the right, while now we have the same duration (as they sum to one), with probability that we move from $x$ to $y$ which is $p(y|x)$. 

Note that as the probabilities over the states $y,z$ sum to 1, the sum of all of them is just $\lambda(x)$. This means that we can consider $T(x) \sim \exp (\lambda(x))$ just as the minimum between all the $\exp (\lambda(x) p(y \mid x))$ with $y$ changing = $\min_{y} \exp (\lambda(x) p(y \mid x))$. Basically, we can consider $T(y|x)$ as an alarm clock, and the first to ring determines the transition. We are just basically considering the first state that we can go to.

So, which type of models can you model with semi-Markov chains? 

## Rewards

The rewards for *keeping stock* (something you pay for keeping things at stock) are called *rate rewards*, which are continuous until jump, while lump rewards are at jump. The expected reward per unit of time is therefore $r^{r}(x)+r^{l}(x) / \tau(x)$. That is a crucial difference: the Poisson equation now has a $\tau(x)$ more! Note that if you have already calculated the $\phi$ through the stationary distribution, you can use it in the computation of the Poisson. 

## Semi-Markov Decision Processes

Having soujorn time $T(x,a)$ we want to add decisions: the time considers actions too now. We have rewards $r(x,a)$, but now the time you spent in a state depends on your action (and it must go to the right).

### Backward recursion

With the chain we just has, we stay 2 time units in 2, and 1 time unit in 1, which is the same as considering 1 time unit with probability 0.5 for 1. 