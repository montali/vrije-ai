# Bayes dynamic programming

Imagine we had to choose between 2 medications. We're in a *learning setting*, and we're looking at methods having no underlying states. You can only pick one, and know the outcome after a few weeks. What we're interested in, having the outcomes as only information (0101 for example has 2 people cured). 

## Stateless bandits

Suppose you're pulling an arm, getting rewards $r_1,...,r_t$ up until time $t$, being realizations of some random variable $R_i$. Trying to estimate $Q$, we can consider it as $Q_t = (r_1+...+r_t)/t$.

If you assume certain things about $R_i$, i.e. that they are indipendently identically distributed (the rs have the same distribution and the realizations are independent). 

Basing on the Q values, we have to make decisions. We can use a **greedy policy** (always take the highest Q, but if we start with the wrong one we'll always pick it), an $\epsilon$-greedy, or a **greedy with optimistic initial values**.

## UCB

With CI being the confidence interval (statistical index), we want to use something like the upper confidence bound. We don't know the variance $\sigma$, so we use something that gets smaller as $t$ gets bigger. Don't dive into the statistics: just remember that the value gets closer and closer to the Q values, and the more you select an arm the $N_t(a)$ (number of plays for arm $a$), the smaller your confidence interval is, and the less likely you are to explore. 

We can now see the arms as stateless bandits, assuming we're not observing the states (or the state space is too big). We initialize the Q values at $2,2,2$ (some prior knowledge, as 2 is an upper bound to our reward). Then we have a matrix `r` with time and the different arms in it (3000 time units for 3 arms). `N` is the number of times we played an arm, and if I select arm `a` I enter the $Q$ value with the $\gamma_t$ recursion. 

Now, suppose you have a new medication, and no knowledge on the success probability (but no punishing rewards). What should you choose? 

