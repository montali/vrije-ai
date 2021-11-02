# Dynamic Programming and RL

### Assignments/Grading

The grading consists of two parts. There are 4 homework assignments (most of them are algorithms, some theoretical questions to answer, each counts 10%). You can do them in couples, but for every assigment you'll need to have a different partner. The exam counts for 60% (minimum is 5.0/10)

Lectures will take 2x2x45min. There are TA sessions scheduled on friday morning (2 different times, some on campus some online). Assignments are due 1-2 weeks later. They are published at week 1,2,4,6. 

There's also some overlap in the deadlines. Finally, written exam in week 8.

### Literature

All the content seen in class and in tutorial sessions are what's important for the exams. Optionally, you can read two books:

- Markov Decision Processes by Kallenberg
- 2nd edition of Reinforcmenet Learning by Sutton & Barto

## Introduction to the course

We can see a short map of a city, and we're going to talk about the **shortest path problem**: basically, what Dijkstra solved. We're in the red car and want to get on the motorway, and there are distances. 

TODO: insert map!

You have to make **multiple decisions**, maybe determined upfront but maybe not. Every time you reach an intersection, you need a decision. There are possible *states* (current location), a *time* (measured in terms of steps), and finally, we know the problem is *deterministic*: it is completely predictable, so the *optimal policy* can be computed in advance (**offline**). The algorithms we're going to discuss are **dynamic programming** algos, but other algorithms exist (Dijkstra), even though they are **not generic**.

Let's now look at the same grid, but now there are **traffic lights**: we're inserting non-determinism in our problem. Now, lengths are measured with a random variable: $2+D$ where $D$ is the RV, an unpredictable delay which is either 0 or 5: $P(D=0)=P(D=5)=0.5$.

Commonly, we use the **shortest expected path**. We have a **model for the randomness**: we can compute the optimal policy, as we know the model for the randomness. We cannot predict the exact time, but we can still provide the optimal policy **upfront**. We still call this **offline**.

The algorithm is still dynamic programming, but with expectations included in the right way, and usually the randomness is in transitions and not in the *rewards*.

Now we move on to a third situation: the durations are unknown, not even in distribution (*model-free*). They could be deterministic or random: we just don't know. If you're the first person traveling there, all the roads have the exact unknown duration, but they can be **learned**! By taking a road, its realization becomes known to **future drivers**. How do we include that in the criterion? We could have the first driver travel everywhere to explore, but that wouldn't be optimal. This becomes interesting when we **execute it multiple times**. We can talk about the exploration vs. exploitation tradeoff. We cannot simply use DP anymore: we need heuristics, maybe Q learning, or more mathematical ways like Bayesian DP.

## Key concepts

### Time

We're studying **sequential** dynamic decision making: for every time unit, you make a decision.

The current decision has **direct** (reward or costs) and future **consequences** (future **state**, with its direct rewards...).

### State

State is a concept that **links time periods**. It contains all knowledge needed to predict future behaviour (Markov property, i.e. adding more info does not increase reward). The state could be physical, or maybe just accumulated information. Some examples of state:

- Chess: position of all pieces
- Inventory: items at stock per product
- Autonomous driving: position + direction + speed

The state space is called $\mathcal{X}$.

### Rewards

We have 3 options: *finite rewards*, *long-run average* or *discounted*. Suppose our rewards are repetitive: 1,2,4,1,2,4,1,2,4, what would be the final reward for T=10?

- **Finite**: just sum them, obtaining 10*(1+2+4)
- **Long-run average**: average by time, $3.5*10$
- **Discounted**: with discount factor $\beta \in (0,1): 1+2\beta + 4 \beta ^2 + \beta ^3 \dots$