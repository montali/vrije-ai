# Exercise1

$P(E|H) = \frac{P(E,X)}{P(X)} = \frac{P(H|E)P(E)}{p(H)} = \frac{P(H|E)P(E)}{P(X|Y=y_1)P(Y=y_1)+P(X)P(Y=y_2)} = \frac{2}{3}$

We have two coins, one being fair and one not (H/H). You can flip the coin, and you get a probability 0.5/0.5 or 1/0. You take as a prior that both have probability 0.5 of being in your hand.

### Question A

$p(H) = \frac{1}{4}+\frac{1}{2} = \frac{3}{4}$

$p(T) = \frac{1}{4}$

You can also represent visually starting from the belief of which coin it is (both 1/2), then wonder what happens when we have a tail (we know for sure it's the fair one), while if I get a head the probability becomes (1/3,2/3)

### Question B

What is the chance that we have a fair coin given some outcome? We can rewrite this as a more general form:
$$
\frac{P(X|Y=y_1)P(Y=y_1)}{P(X|Y=y_1)P(Y=y_1)+P(X)P(Y=y_2)} 
$$
With the coins being $y_1$ and $y_2$.

Having this formula, you can fill it using our beliefs which were calcualted in step A. At the start, the probability that we have a fair coin or an unfair coin is 1/2,1/2, but as we proceed further this probability changes. Remember that these probabilities are always just $p, 1-p$.

If we always get heads, we get $\frac{1}{2}, \frac{1}{3},\frac{1}{5}, \frac{1}{9}$ probability of having a fair coin, or generally speaking, $\frac{1}{2^n+1}$.

### Question C

What's the probability of ending up in the certainty case? First, the probability of getting $T$ is $\frac{1}{4}$: we have 0.5 probability of having a fair coin, and 0.5 of getting T from that. On the second run, the probability of getting the fair coin if we got $H$ in the first is $\frac{1}{2}*\frac{1}{3}$.

# Question 2

You have some Beta that tells you, if you have $k$ wings and $l$ losses, you have a Beta distribution with $Beta(k+1, l+1)$.

We start with 2 Bernoulli bandits (equally likely), both have been played once and arm1 gets to $Beta(0+1, 1+1)$ and arm2 gets $\Beta(1+1, 0+1)$.

Then, for *a* and *b* you calculate 1000 times the Beta distribution of arm 1 $Beta(1000,1,2)$ and 2 $Beta(1000,2,1)$ and I'm going to compare how many times arm1 is bigger than arm2. 

For *c* you can do the same trick as *a*.

# Question 2/2

When you are in state 1 you can get a small reward 2. You have a discount factor of 0.9 so there's probably a breaking point somewhere. To derive the Q values we have the standard formula $Q(x,a) = \sum_y p(x,a,y)(r(x,a,y)+\gamma \max_{a'}\{Q(y,a')\})$.

We have two states, initialize the Qs to zero, then iteratively update them. 