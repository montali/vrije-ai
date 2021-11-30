# Bellman equation

We have already talked about the linear programming approach, which turns out to be computationally slow. We are going into a *computationally more attractive* method.

We want to find a *backward way* to compute the long-term average reward. 

We can now introduce the *small order of f* $o(f(t))$, being just the small-O and Big-O notation. 

Remember the Poisson equation $V_{t+1}(x)=r(x)+\sum_{y} p(y \mid x) V_{t}(y)$, for which we split it into the first timeunit and the reward, or we can even split it using $\pi_t$: $V_{t+1}(x)=V_{t}(x)+\sum_{y} \pi_{t}(y) r(y)=V_{t}(x)+\phi_{*}+o(1)$. We got this by splitting up the $t+1$ in the first $t$ and the last time unit, when $t$ goes to infinity (limited distribution), we get to $\phi^*$.

If we subtract $\phi^* _t$ from both sides (where its value is two times the long-run average reward). We get the same if we start in a stationary situation we get $\phi^*$ at every time unit. If you start at $\phi^*$ in a stationary distribution, you always have $\phi^*$. Then, we take the limit.

Therefore, to get the total difference between starting in $x$ or in stationarity, we can just get $V_{*}(x)=\lim _{t \rightarrow \infty}\left(V_{t}(x)-\phi_{*} t\right)$.

The vector $\phi^*$ tells you something about starting in x/starting in statinoarity. This is something we call transients (i.e. things that disappear aftern a given amount of time). 

If we subtract $\phi_* t$, we get the reward of starting from $x$ plus the value of the states we can reach from there. We call this the **Poisson equation**. We know that $\phi_*$ is **independent of the initial distribution**.

As equation $V+\phi e=r+P V$ has no unique solution, we have a problem of non-uniqueness. To avoid this problem of non-uniqueness, we impose $<\pi_{*}, V_{*}>=0$. Therefore, we take one state (0 or any reference state that we like) and we set its value to 0, obtaining a **unique solution** for $V+\phi e=r+P V$. This allows us to avoid having to determine $\pi_*$.

For an example, we can fill in the Poisson equation. To do it for state 1, we have $V(1)$ + $\phi$ = the reward + the V in state 2 (as it's the only possible state to reach). The same is done for 2: the reward is 1, the only possible next state is 3. Finally, for $V(3)$ we have reward 2. Now, we have a system which has a *surplus variable*: because of this, we set $V(1)=0$ as aforementioned. 