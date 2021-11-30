We initialize $V_t = V_0=(0,0,0,0)$

You then put it in the Poisson system (removing the $\phi$!)

$V_{t+1}(1) = 1 + V_t(2) \rightarrow 1+0$

$V_{t+1}(2)=min\{2+V_t(3) , 4+V_t(1)\}$

$...$

Then you have $V_1=(1,2,3,4)$

You then iterate again with $V_1$ substituted with $V_t$:

The values keep increasing, and they will never converge like this. In the slides it says the $span(V_{t+1}-V_t)$ needs to be smaller than a given $\epsilon$. What's a span though? Remember it as *you take the maximum of $V_{t+1}-V_t$, then you subtract from it the minimum of $V_{t+1}-V_t$*. If you do enough iterations, all these values will converge. Usually you keep $\epsilon=0.01$
$$
max\{V_{t+1}-V_t\}-min\{V_{t+1}-V_t\} < \epsilon
$$
Notice that on the long run, $V_{t+1}-V_t$ converges to $\phi$!

In **policy iteration**, you fix the policy and you compute the values. You have $\phi$ here.
