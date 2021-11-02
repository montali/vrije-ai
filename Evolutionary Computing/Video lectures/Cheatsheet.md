# Lesson E - The origins

1948 Turing proposes genetical or evolutionary search

1962 Bremermann proposed optimization through evolution and recombination

1964 Rechenberg introduces Evolution Strategies

1965 Fogel, Owens, Walsh introduce Evolutionary Programming

1975 Holland introduces Genetic Algorithms

1985 first international conference

1990 furst internatiional conference in EU

1992 Koza introduces genetic programming

1993 first scientific EC journal

1997 EC research network evonet

2003 first  book

Individuals are units of selection, population is unit of evolution

# Lesson F - What is an evo alg

Selection op (only use fitness, indep from representation) => population level (pop is evolving, not ind), Variation op => individual level

gene vs allele = variable vs value

Parent selection usually stochastic, survivor selection often deterministic

CX is explorative, mutation exploitative

dimensionality $n^2$ size $2^{nn}$

# Lesson G - Representation and variation

## Binary

Mutation: mutation rate is the independent probability of changing each gene, normally between 1/popsize and 1/chromlength

n-point CX: choose n points, exchange alternatively. (n=1 has positional bias)

Uniform CX: flip a coin for each gene to choose, 2 children (inverted)

CX does not change the allele frequencies of the population.

## Integer

N-point and uniform CX work as before

Bit-flip mutation subst. by random resetting = with a prob. a new value for the gene is randomly chosen, could even make a "creep"

## Real valued

Can encode as bitstrings with chromosome length L (determining precision of solution): $\Gamma\left(a_{1}, \ldots, a_{L}\right)=x+\frac{y-x}{2^{L}-1} \cdot\left(\sum_{j=0}^{L-1} a_{L-j} \cdot 2^{j}\right) \in[x, y]$

### Mutation

Uniform mutation: draw new value randomly in [LB,UB]

non-uniform: e.g. Gaussian, 2/3 will be in $-\sigma,+\sigma$

Gaussian: $\begin{aligned}
&\sigma^{\prime}=\sigma \cdot \exp (\tau \cdot N(0,1)) \\
&x_{i}^{\prime}=x_{i}+\sigma^{\prime} \cdot N_{i}(0,1)
\end{aligned}$ with LR $\tau \propto 1 / \mathrm{n}^{1 / 2}$ and boundary rule $\sigma^{\prime}<\varepsilon_{0} \Rightarrow \sigma^{\prime}=\varepsilon_{0}$

Can become n $\sigma$s: $\begin{aligned}
&\sigma_{i}^{\prime}=\sigma_{i} \cdot \exp \left(\tau^{\prime} \cdot N(0,1)+\tau \cdot N_{i}(0,1)\right) \\
&x_{i}^{\prime}=x_{i}+\sigma_{i}^{\prime} \cdot N_{i}(0,1)
\end{aligned}$ where $\tau'$ is overall LR and $\tau$ is coordinate-wise LR $\tau^{\prime} \propto 1 /(2 \mathrm{n})^{1 / 2} \text { and } \tau \propto 1 /\left(2 \mathrm{n}^{1 / 2}\right)^{1 / 2}$. Note the difference in $N$ and $N_i$

Correlated mutation: add $k$ values $\alpha$ with $k=n \cdot(n-1) / 2$. Build covariance matrix as

- $\mathrm{c}_{\mathrm{ii}}=\sigma_{\mathrm{i}}^{2}$

- $\mathrm{c}_{\mathrm{ij}}=0 \text { if } \mathrm{i} \text { and } \mathrm{j} \text { are not correlated }$

- $$
  \mathrm{c}_{\mathrm{ij}}=1 / 2 \cdot\left(\sigma_{i}^{2}-\sigma_{\mathrm{j}}^{2}\right) \cdot \tan \left(2 \alpha_{\mathrm{ii}}\right) \text { if } \mathrm{i} \text { and } \mathrm{j} \text { are correlated }
  $$

- 

Then, we know the relation between covariance and angle to be $
\tan \left(2 \alpha_{i j}\right)=\frac{2 c_{i j}}{\sigma_{i}^{2}-\sigma_{j}^{2}}
$

So, $
\begin{aligned}
\sigma_{i}^{\prime} &=\sigma_{i} \cdot e^{\tau^{\prime} \cdot N(0,1)+\tau \cdot N_{i}(0,1)} \\
\alpha_{j}^{\prime} &=\alpha_{j}+\beta \cdot N_{j}(0,1) \\
\bar{x}^{\prime} &=\bar{x}+\bar{N}\left(\overline{0}, C^{\prime}\right)
\end{aligned}
$ with $\beta \approx 5°$

The object variables $x$ are now mutated by adding $\Delta x$ drawn from an n-dimensional normal distribution with covariance matrix $C'$ 

Note that uncorrelated mutation acts on a single gene, correlated mutation acts on the whole vector with a multidimensional Normal distribution.

### Recombination

Discrete: each allele comes from one of the parents with equal prob.

Intermediate: Averages parents, $
z_{i}=\alpha x_{i}+(1-\alpha) y_{i}
$ with $\alpha$ fixed, variable (time?) or random.

Single arithmetic: pick a single gene (once), apply intermediate CX

Simple arithmetic: pick a single gene and apply intermediate CX until the end

Whole arithmetic: apply intermediate CX on the whole vectors

Blend crossover: range for the new var $z_i$ is $[x_i-\alpha \cdot d_i, x_i+\alpha\cdot d_i]$. Basically, get a random $u \in [0,1]$, then $
\gamma=(1-2 \alpha) u-a
$ and $z_{i}=(1-\gamma) x_{i}+\gamma y_{i}$.

Multiparent: diagonal (back, il primo rimane uguale, n-1 punti CX con n figli) oppure average

## Permutation

Mutation parameter is now for the whole individual

### Mutation

Random swap; Insert mutation (pick two, put the second in front of 1st shifting others); Scramble (pick subset, randomly rearrange);Inversion mutation (pick subset, invert it)

### Crossover

Order 1: pick a subset from first, copy it, then copy what's missing from the 2nd (starting from subset point and %)

PMX: pick subset, copy it, try to go up from same subset to P1, put the element in the place where P1 is. When you finish the subset from P2, copy the rest from P2.

Cycle: Look for cycles (start first, go down, find same up), copy alternately

Edge recombination: List edges (% too), pick random current, delete it from edges, if there's a common edge pick that, otherwise element having shortest list, otherwise random

## Tree

 Appear in GP, defined by Terminal set and function set. 3 rules: T correct, F corrent if arity is ok and ts are correct, there is no other form.

Mutation: randomly replace subtree by random tree (two probs, p of mut and p of choosing point as Mutpoint)

Recombination: random exchange with same probabilities



# Lesson H- Fitness evaluation

Generational vs Steady state (generation gap, i.e. % rep < 1.0)



Windowing -> subtract the worst fitness from all the values

Sigma scaling: $f^{\prime}(i)=\max \left(f(i)-\left(\bar{f}-c \cdot \sigma_{f}\right), 0\right)$

Rank- based (ASC): $P_{\text {lin-rank }}(i)=\frac{(2-s)}{\mu}+\frac{2 i(s-1)}{\mu(\mu-1)}$, $P_{\text {exp-rank }}(i)=\frac{1-e^{-i}}{c}$

Takeover time in ES is $\tau^{*}=\frac{\ln \lambda}{\ln (\lambda / \mu)}$

EXP: Fitness sharing: $f^{\prime}(i)=\frac{f(i)}{\sum_{j=1}^{\mu} \operatorname{sh}(d(i, j))} \quad \operatorname{sh}(d)=\left\{\begin{array}{c}
1-d / \sigma \quad d \leq \sigma \\
0 \text { otherwise }
\end{array}\right.$ (more inds in high hills)

EXP: Crowding: $\mathrm{d}\left(\mathrm{p}_{1}, \mathrm{o}_{1}\right)+\mathrm{d}\left(\mathrm{p}_{2}, \mathrm{o}_{2}\right)<\mathrm{d}\left(\mathrm{p}_{1}, \mathrm{o}_{2}\right)+\mathrm{d}\left(\mathrm{p}_{2}, \mathrm{o}_{1}\right)$ (uniform spread in hills)

IMP: island model, cellular EA

Distances: fitness,geno,pheno, algo

# Lesson I - Parameter tuning

Fitness->Utility

Iterative: reduces number of tested vectors (REVAC,SPO, METAEA)

Multi-stage: reduces number of tests per vector (Racing) (selective testing=multistage vs complete=single stage)

# Lesson J - Parameter control

Deterministic: $\sigma(t)=1-0.9 \times \frac{t}{T}$

1/5 rule $\sigma(t)= \begin{cases}\sigma(t-n) / c & \text { if } p_{s}>0.2 \\ \sigma(t-n) \cdot c & \text { if } p_{s}<0.2 \\ \sigma(t-n) & \text { otherwise }\end{cases}$ every n steps with $p_s$ succ. muts

Self adaptive $\boldsymbol{\sigma}^{\prime}=\sigma \times e^{N(0, \sigma)}$

Constraints: $W(t)=(\mathrm{C} \times t)^{\alpha}$

$W(t+1)=\left\{\begin{array}{c}\beta \times W(t) \text { if last } \mathrm{k} \text { champions all feasible } \\ \gamma \times W(t) \text { if last } \mathrm{k} \text { champions all infeasible } \\ W(t) \text { otherwise }\end{array}\right.$

Relative vs absolute evidence (direction and magnitude fixed vs variable)

# Lesson K - Working

Design/Production/Publication/Application

Performance: Avg Evals to Solution, Success Rate, Mean Best Fitn.

Either fix the time or the quality

# L - Popular EAs

GA: bitstring, 1-point CX (with prob pc), bitflip mutation (indpb), FPS roulette wheel, Generational

ES: Real-valued, discrete/intermediary CX, gaussian mutation, uniform random, $(\mu, \lambda)$ or $(\mu+\lambda)$. HAS SELF-ADAPTIVE or 1/5th

EP: Real-valued, no CX, Gaussian mutation, Deterministic (one parent one offspring), probabilistic survivors. No predefined representation (so no predef. mutation). Usually has self-adaptive stepsize.

GP: trees, exchange subtrees,(OR) random change trees, FP (divided into 80%/20% for best/others), Generational. Can fully initialize trees ($d=D_{max}$) or grow method ($d\le D_{max}$). Commonly, half and half.

# M - newer EAs

Differential Evolution: pops are lists, 4 parents for one child. Mutation is done with differential (take two random inds, subtract them and multiply by scaling factor). CX is uniform random, with restriction (one random is always from first parent). DE/basechoice/numberofdiffs/CX (bin is uniform) $v_{i}=a_{i}+F \times\left(b_{i}-c_{i}\right)$

PSO: inds carry a perturbation vec that is updated with current v, vector from best past position individual, vector of best past position global

EDA: Select best, fit distribution over them, sample offspring from distribution

Model-assisted: use model for fitness evaluation in % of evals

LCS: tuple representing rules, 1-point over conditions/actions, binary resetting on c/a, FP with sharing, stochastic survivors. Michigan has rule=individual, pittsburg has ruleset=individual.

# N- Hybridisation

Simulated annealing: $\mathbb{P}_{c}(\operatorname{accept}(j))= \begin{cases}f(j) \leq f(i) & 1 \\ f(i) & <f(j) & e^{\frac{f(i)-f(j)}{c}}\end{cases}$

# O - MOP

Decision vs Objective space

Pareto optimal set vs pareto optimal front

# Constraint

Indirect: we can sum over constraints (+1 for each violated) or over variables/individuals (+1 if variable violates at least 1 constraint), or estimate the distance from correctness

Direct: eliminating, repairing, special MU/CX, decoding

# Evolutionary robotics

Active vs. passive entity (behaviour)

Async reproduction possible

Offline (evolve first, install best, can be simulated or real) vs. online evolution (can be one ind-one robot or one rob-one population, as islands).

Online evolution facilitates adaptation!

Reality gap!

Fitness: noisy, costly, complex (behaviour between pheno and fitness), implicit, no-go areas.

Fitness: functional vs. behavioural, explicit vs implicit, external vs internal.

Novelty search, map elites.

# Neuroevolution

Could be evolving weights only with fixed, fully connected topology.

NEAT: minimal and speciation. Innovation number to identify connections (genes), align genomes and perform crossover. Matches are random, disjoint and excess are from the fittest. Generate, put into species (compatibility distance) or create if none is found. Fitness sharing is applied, then eliminate worst. Species with higher fitness generate more offspring.

