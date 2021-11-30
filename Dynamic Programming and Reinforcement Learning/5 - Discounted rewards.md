# Discounted rewards

There are different reasons for our instant reward being more important than the future: one of the main is **interest**. If I have 100 euros and I put in my bank account, reward $x$ is now worth $x(1+\rho)^{t}$.

Using the discount factor $\beta = (1+\rho) ^{-1}$ and substituting $x$, we can prove that reward $1$ at $t$ is worth $(1+\rho)^{-t}$.

We're interested in calculating the value function of finite horizon $T$.

Why would we take discounting? In the long run we're all dead :) We have to be careful in choosing the discount factor: it's often close to 1. We also have another interpretation for discounting: having a total reward, but stopping wach time unit with probability $1-\beta$.

Suppose it's a probability of dying: we look at the total reward, but at every time unit there's a fixed probability of the game finishing. 

