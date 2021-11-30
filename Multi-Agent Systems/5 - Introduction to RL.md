# Introduction to RL

We're now trying to introduce a framework for single-agent RL. 

**Reinforcement Learning** means learning by interaction (trial and error). It's a natural way to learn complex skills! For example, suppose you're trying to learn to play a song on the piano by ear. You have possible actions, choosing the keys, immediate rewards (correct key) and cumulative reward (whole song, which is our **ultimate goal**). The problems become more difficult when the reward is only delivered at the end! 

Cooking is another example. 

There is no **oracle**: it is not a supervised learning, you get some reward but it's a very unspecified one (you don't know whether it's an optimal reward, minimal...). Secondly, you only get data on the action and states that you actually take. The **sparsity of feedback** is another problem: in many problems, you don't get a significant reward until you actually get to the final state (for example, in a game you only know if you won at the end). There is a sort of positive feedback between the policy that you're using and the reward you're getting! It's not a random indipendent set of inputs, as what you do has an effect on the rewards. 

## Formalization

When you've fot an agent interacting with an environment, what you care about are the states, the actions you take, and the transition that happen when you take an action. These could be deterministic or not. When you do that, you get an immediate reward, depending on the starting state, the action took, and the state you end up in. The **policy** $\pi$ specifies which action to take for each state. The goal is finding an **optimal policy**. An optimal policy describes the action for each state that will lead to the best final reward. 

## Markov Decision Processes

This is a mathematical formalism capturing the essence of RL. MDP has states, actions, transitions, rewards and also a discount. When you do an action you transition to a next state, getting a reward. MDP is a 5-tuple:

- States
- Actions $a \in A(s)$: for every state $s$ there's a set of actions that are possible
- Reward function: depends on the state you started, the action you took and the state you end up in. The expected value of the rewards given the states and actions $r\left(s, a, s^{\prime}\right)=E\left[R \mid s, a, s^{\prime}\right]$
- Transition probabilities $p\left(s^{\prime} \mid s, a\right)$: tells you if you're in a state, and take an action, where you could go
- A discount factor: tells you the horizon, if gamma is small the rewards are immediate, while if it's close to 1 we're interested in the future $0 \leftarrow \gamma \rightarrow 1$

If you have deterministic transitions, you know for sure the state you end up in knowing state and action. 

### Transition

 $p\left(s^{\prime} \mid s, a\right):=P\left(S_{t+1}=s^{\prime} \mid S_{t}=s, A_{t}=a\right)$, the probability that in state $s$ with actino $a$ you end up in $s'$.

### Rewards

The reward that you get while transitioning to a new state. Formally, it's the expected value of the reward that you get $$r\left(s, a, s^{\prime}\right):=E\left(R_{t+1}\mid S_{t}=s, A_{t}=a, S_{t+1}=s^{\prime}\right)$$ given status and action.

### Markov Property

Given that you know the current state, what you need to know to know about the next state is just the current. You don't need anything else. Formally, $P\left(S_{t+1}, R_{t+1} \mid s_{t}, a_{t}, r_{t}, s_{t-1}, a_{t-1}, \ldots, r_{1}, s_{0}, a_{0}\right)=P\left(S_{t+1}, R_{t+1} \mid s_{t}, a_{t}\right)$, i.e. it doesn't help you to know the whole history of previous states/actions. 

That is quite restrictive, but it's okay: it simplifies the mathematics, but it is always possible to enlarge the state space to capture any information you need. Suppose you need the position of a particle, you need the speed too. In order to have the speed, you should have at least 2 positions, $t$ and $t-1$. You can though define a new *superstate* capturing these two states. 

### Policies

If we're looking at **stochastic policies**, we determine that in a particular state we could take an action with a given probability, while for **deterministic policies** we link a state to an action.

### Return and rewards

If you look at concrete examples, most of them will have a concrete reward. It's nicer to have an infiinite horizon though, but you can always look at episodic tasks that when finished just loop in a final state. Note that the cumulative reward depends on the starting state and the policy you're applying.  You have a recursion saying that the total reward at time $t$ is the immediate reward that you get plus the reward you get from then on, discounted by some factor: $G_{t}=R_{t+1}+\gamma G_{t+1}$. 

### Value Functions

Once you have an MDP and a policy, you can start thinking about **value functions**. Given a policy and an initial state, the value of that state under this policy is the **expectation** you have of the total reward when you start in that space and apply that policy. You're in a certain state, you know what you do in each state. If you do $n$ experiments and average them, you get this expectation. We also use this idea of **state-action-value function**: what is the final reward on average when you use a policy $\pi$ start in state $s$, take an action $a$ and **from then on**, use a policy $\pi$. Note that in $q$, the **first action** is taken independently of the policy, while for $v$ the policy dictates every action along the path. 

If you start in a given state, do the rollout, you will pick actions with 20,50,30% probabilities. If you would do the state-action function, you would always choose that $a$, while with $v$ you use the policy (which is non-deterministic so differs in experiments). 

What you see is that the value function is like a weighted mean of $q$ by the policy probabilities: $v_{\pi}(s)=\sum_{a} \pi(a \mid s) q_{\pi}(s, a)$, basically the expected value using the policy.

**The value in a state is a weighted average of the state-action value function, weighted by the policy.** 

## Bellman equations

As said before, the **Bellman equations** will provide us with some sort of internal consistency for the value function. We're saying that there is a relationship between the state value and the state-action value.

If we have a look at the state-action value, what we're doing is saying *this is the expected value of the total reward when I know I start in $s$ and tkae $a$*. The only remaining question is *if I take that action, where do I end up? We have the probabilities $p\left(s^{\prime} \mid s, a\right)$*. Let's assume I end up in $s'$, which will happen with this probability. If we recursively do this, using the fact that the total reward is the sum of the immediate + the global discounted reward, we can just push the expectation through the equation and use the Markov property: if I know I'm in state $s_1$, I don't need to know the history anymore! If I do that, I can just rename $G_1$ to $G_0$, and that's just the definition of the value function!

Linking everything together, the state-action value is a sum weighted by the transition probability of the instant reward and the expected value after this.



Looking at the graph, you're in state and you have commited to take action $a$. Once you do that, you will transition to a new state with certain probability. If you're in $s$, the policy tells you you have a probability $\pi(a|s)$ of picking an action. We know we have committed to an action, and we have a probability of ending up in a given state with that action. The new value is just the sum of the possible transitions to the new state, and when we do that we end up in a new state $s'$  which has a discounted value $\left.\gamma \boldsymbol{v}_{\pi(} \boldsymbol{s}^{\prime}\right)$.

What the Bellman equation does is combining these, substituting $q(s,a)$ with its expanded version. We're saying *to know what a value is in state $s$, we sum over all the possible actions we can take with their probability, and check the rewards for the possible states we'll reach*. 

The Bellman equation for the state and value function is this, then: $v_{\pi}(s)=\sum_{a} \pi(a \mid s) \sum_{s^{\prime}} p\left(s^{\prime} \mid s, a\right)\left[r\left(s, a, s^{\prime}\right)+\gamma v_{\pi}\left(s^{\prime}\right)\right]$. If you rewrite it by interchanging the summation, we get:

$v_{\pi}(s)=\gamma \sum_{s^{\prime}} \underbrace{\left(\sum_{a} \pi(a \mid s) p\left(s^{\prime} \mid s, a\right)\right)}_{P\left(s, s^{\prime}\right)} v_{\pi}\left(s^{\prime}\right)$
$+\sum_{a} \underbrace{\left(\sum_{s^{\prime}} p\left(s^{\prime} \mid s, a\right) r\left(s, a, s^{\prime}\right)\right)}_{R(s, a)} \pi(a \mid s)$

If you look at this, you see that when you sum over $a$ the variable $a$ disappears, so this $P(s,s')$ can be thought as of *what's the probability, under the policy, that you move from $s$ to $s'$?* You could think of this as subscripted by $\pi:P_\pi$. If you look at the second, it's the expected value of the reward if you're in state $s$ and take action $a$. If you're in $s$ and take $a$ you might still end up in different states, and get different rewards. This $R(s,a)$ tells you what the immediate reward should be with that action in that state. You then multiply that out with the **probability that you will take that action** (basing on the policy), so that now only depends on $s$. This is the expected immediate reward that you will get in state $s$. Suppose you have $n$ states and write them as a vector, you say that $v_\pi(s)$is equal to $\gamma$ multiplied by the probabilities by the values, plus the immediate reward. 

Formally, you can use $(I-\gamma P) \mathbf{v}=\mathbf{r}$ to solve $v$, as you know all the others. Notice that $v$ is just the identity matrix times $v$. Remember that $\frac{1}{1-x} = 1 + x +x^2+...$. This works for matrices too: the total value (long-term) is $r$ plus $P_r$ (you take one step, you get additional reward), then $P_r^2$ (you take two steps, you get additional reward) and so on. $\mathbf{v}=(I-\gamma P)^{-1} \mathbf{r}=\left(I+\gamma P+\gamma^{2} P^{2}+\ldots\right) \mathbf{r}$

This tells you that there is a way of solving the value function. 

The value functions have internal consistency requirements, which are captured by the Bellman equations.

Looking at a simple MDP, consisting of 5 states (2 of which are absorbing, they end the game). We specify the policy with the red arrows: in state 1, we go with probability 1/4 to the left, 3/4 to the right. We assume transitions are deterministic: when we decide an action, it happens. The only probability is in the policy. When you do that, the rewards are written down in green: from 1 to A you get 0 reward, while travelling in-between you spend rewards. In B, you get 20: you wanna get there as quickly as possible. 

In order to turn an episodic path into an infinite one, you just stay in the same state and no longer get any reward. That means that the ER in absorbing states is 0.

If you want to solve the value function $\mathbf{v}_{\pi}=\gamma P_{\pi} \mathbf{v}_{\pi}+\mathbf{r}_{\pi}$, you can formally (we added the pis in the pedices as all of these depend on the policy) invert it. This is not that nice, though: it's better to do it **iteratively** $\mathbf{v}^{k+1}=\gamma P \mathbf{v}^{k}+\mathbf{r}$ until convergence.

The optimal value function is simply:  in a given state, what is the policy that maximizes $v_\pi$? This is the same for the Q-function. 

If you look at slide 77, the lines correspond to different actions. You want to take the maximum of them!

We now can get to the optimal state-action value function $q^{*}(s, a)=\sum_{s^{\prime}} p\left(s^{\prime} \mid s, a\right)\left[r\left(s, a, s^{\prime}\right)+\gamma v^{*}\left(s^{\prime}\right)\right]$.

### Model-based vs model free

In the first, you assuem that the MDP is known: you solve the Bellman optimality equations and solve them. If you have no explicit model, you have to explore in order to gather information that will help you in solving the equations. You're initally just doing random search, but the Bellman equations allow you to propagate values back up.2 

There are two problems depending on what you want to compute: if you're given a policy, and want to compute the value of each state, that is called *prediction*. The other is **optimal control**: you're not given a policy, and you want to find the best one. We can distinguish between cases in which we know the transitions, and those in which we don't (model-free). 

# Finding the optimal policy

In model-free, you have no prior knowledge about transition/rewards: the only way is experience, i.e. the agent is in the environment. We can talk about 4-tuples for experience: we're in a state, we pick an action, we get a reward and we go to a new state. Over time, the agent is keeping a database of these 4-tuples and he uses these to learn. There's two ways, **direct** and **indirect**. The latter tries to compute state values and improve the policy using greedification. 

In RL, we have an environment (which we don't really know) and we want to obtain the policy. Value function, for a given policy, compute a state's value. We can then use the bellman equations to actually learn states: whenever you have experience, you're learning something about states too! Experience will be therefore fed into the algorithms to learn information about the states. 

When we're doing policy improvement, we apply iteration steps to improve it through the values: you're increasing the value functions, as in every state, in the next iteration, you pick the optimal one. Because of the Bellman equations, we know that that is a weighted average of the q values. Your v values are improving for every iteration step.

In model-free approaches, we've looked at the V function. Now we'll shift to the Q: if you use model-based, you can actually compute the Q values through the V function (as you know V and what the actions lead to). In model-free, you don't know that: we need the Q values rather than the V values. Another thing we have to keep in mind is **looking at all the state-action pairs**: at some point, we have to make sure that we keep on exploring. Policy iteration is a combination of evaluation and optimisation. You take any estimate of the Q function (think of it as a table, in which you have the Q for the possible states/possible actions pairs). 

For a given policy, there's an actual q value corresponding to that. Our Q matrix is therefore going to converge to that after some experience! After some time, our Q matrix will be consistent with our policy's $q_\pi$. Then, you greedify and get the new policy! When we do exploration, we're going to use an epsilon-greedy version. We're not interested in having the Q matrix perfectly converge with the $q_\pi$, as we just need an approximation. What we call policy iteration is a variation of this: you pick a policy, get a Q matrix, then *project down and greedify*.

## Monte Carlo

Monte Carlo methods introduce an idea of sampling to get approximations. When you have a function and want to compute the man under a distribution, you can either compute the integral, or sample and average (MC). When you look at this, something seems wrong: you'd expect to see $p$ also in sample points, but in the integral you're just weighing the function by the probability, while in the sampling the probability *reappears in the sampling*!

You've fot a starting state, and you use the policy to generate an action. Along that path, you get rewards. 

If you want to compute Q, there's only one difference: you can pick your action, and then apply the policy. 

I can then use this to compute the V value, making sure that the actions were according to the policy. To simplify that, I can just weigh the values by the policy!

Imagine you're starting in a certain state, you generate a path, and it looks like the loop in slide 19. On the way out, it returns to that state. You could now have two experience records, you could argue that you have two estimates: you cannot average them out, as they're dependent, in fact the red path has the green path as subpath. They're not independent. When they're independent, you get a better and better approximation, but if they are it doesn't happen!

If you have a policy right now that excludes most actions, you have to make sure that exploration still happens. Possible solutions to that are, for example *exploring starts* (in which you always have a possibility of picking a state for every state) or soft policies like $\epsilon$-greedy.

What you'll also see is that the idea of *backup diagram* helps us in MCTS: we visualize that when we're in a certain state and take an action. Information about a children state gives us information about the parent too.

You can use Monte Carlo for policy evaluation together with epsilon greedy for policy improvement.

The Monte Carlo method uses complete sample returns in episodic tasks: you go down the tree to the terminal state, and use that value to estimate up the tree. 

The thing is that it uses direct sampling rather than the Bellman equations. This is the difference with the next topic.

Under the condition of GLIE. Infinite exploration means that all of the state actions are explored infinitely often: it doesn't mean that we visit them all the same number of times, as the intervals between visits can be different. It just means that the visits never completely stop. Then, we know that the policy converges to a greedy policy while going towards the end. 

This is one example of algorithm in which you sample, you keep track of how many times you visit a certain state, update the Q value through $Q\left(S_{t}, A_{t}\right) \leftarrow Q\left(S_{t}, A_{t}\right)+\frac{1}{N\left(S_{t}, A_{t}\right)}\left(G_{t}-Q\left(S_{t}, A_{t}\right)\right)$ and then just reduce the exploring over time ($\epsilon$ is getting smaller over time), with an $\epsilon$-greedy policy. We can prove that this converges to the optimal action-value function. 

## Temporal Differencing

The Bellman equation links value functions in neighbour states. Temporal differencing uses the **Bellman equation to propagate values**! Imagine you have two states, having actual value function $v(s)$ and $v(s')$. At some point, we estimated $\hat{v}(s)$ and $\hat{v}(s')$. We take an action and observe the reward, as at time $t+1$ we have two estimates, being $\hat{v}(s)$ and $r + \hat{v}(s)$. The difference between these two is the temporal difference! As we now have two estimates, we average them using a learning rate (convex combination, i.e. any combination of the form $\alpha x+ \beta y$ for $x$ and $y$, just a weighted average). If $\alpha=0$, the new estimate is equal to the old, the learning is zero. If $\alpha=1$, we just look at the reward and forget past information. In Monte Carlo, we had an estimate for the value, rolled down and computed the cumulative reward $G$ being the new estimate for the value in $s$. The new estimate was the old estimate plus alpha times the difference between the new value and the old. 

Now, in TD the update rule is the same expect for the fact that we're not waiting for the final state, we just take one step and then back up. 

Temporal differencing is said to be *bootstrapping*, as it uses *estimates*. In MC, we had unbiased estimates of the value as we traveled the whole tree down to the leaves, while here the value we get is an estimate itself. We're not sure that the value we have is the actual value, and we're computing new ones basing on past estimates. 

An interesting graphical visualization of this is the following: imagine you're in a state and have certain actions, what DP is doing is considering the whole red area. In Monte Carlo, the agent doesn't know the whole tree, just a path. It then averages the paths. What TD is doing is *impatient Monte Carlo*, using an estimate to update other estimates.

- DP requires a model, you need probs and rewards
- MC doesn't exploit bellman equations
- TD takes the best of both worlds, as you don't have a model and you use Bellman

## SARSA vs Q-learning

In Q-learning, we're trying to short-circuit SARSA: we're not trying to do the iteration part to evaluate a policy, rather just trying to find the optimal one. 

SARSA is just a TD that tells us what's happening. If in a state you take an action, you get a reward and transition to another state. What we do is using the exact same formula we used for TD, but apply it to $q$: the new estimate is the old estimate plus alpha times the learning rate by the Temporal difference. 

We have the same methodology, at every timestep we evaluate the policy with SARSA, trying to improve our Q estimate which should converge converge to the actual $q_\pi$. At some point, you do greedyfication which should be thought as *jumping* to the next policy in the triangle graph. You go up (evaluation), then jump to the new policy. Every policy you get, is an improvement. 

SARSA is the first model-free genuine RL algorithm. SARSA actually converges to the optimal action-value function, under the GLIE condition, and over time you reduce the exploration phase until you get to the greedy policy. The learning rate has to be set according to two conditions: 
$$
\sum_{t=1}^{\infty} \alpha_{t}=\infty\\
\sum_{t=1}^{\infty} \alpha_{t}^{2}<\infty
$$
$\frac{1}{t}$ is a learning rate that satisfies these conditions. 

Q-0learning is not trying to find the particular Q-value for a policy, just the optimal one. What happens for $q^*$, is that since we know from Bellman $q^{*}(s, a)=\sum_{s^{\prime}} p\left(s^{\prime} \mid s, a\right)\left[r\left(s, a, s^{\prime}\right)+\max _{a^{\prime}} q^{*}\left(s^{\prime}, a^{\prime}\right)\right]$. If you take just one sample, you can forget about the probabilities of going to different directions, and you can just update $q^*$ using this sample expression: $q^{*}(s, a) \leftarrow(1-\alpha) q^{*}(s, a)+\alpha\left(r\left(s, a, s^{\prime}\right)+\max _{a^{\prime}} q^{*}\left(s^{\prime}, a^{\prime}\right)\right)$. *I thought that the best action was this, I've taken one step, and now my new estimate is this and I combine them to get a new estimate.*

It's similar to SARSA, but we're looking at $q^*$.

The backup diagram starts from S,A, applies the action, gets the reward, moves to a new state, and you look around for the action that gives the best Q value. When does this converge? When $\left(R+\gamma \max _{a^{\prime}} Q\left(S^{\prime}, a^{\prime}\right)-Q(S, A)\right)$, i.e. the error is zero, meaning that the $Q$ has converged to an optimal value. As we're actually computing $q^*$ from scratch, there's no greedyfication needed. 

SARSA is said on policy, and Q-learning off: the first is using the policy to actually generate new states and actions for which you're trying to get the Q value. There is no difference between the policy you use for behaviour and the one you're trying to estimate. Q-learning is off-policy, as you're actually using two different policies: you're trying to estimate the optimal $q^*$, but you're using another one to move around. You're not always picking the greedy action, you may explore more!

On-policy is sample-inefficient: whenever you change the policy, you should create new experiences! 

