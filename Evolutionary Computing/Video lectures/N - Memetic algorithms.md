# Memetic algorithms

In this lecture we'll explain what **hybridisation** is and why we should use it.

## Hybridisation: what and why

This is the **combination of an EA** with another **problem-solving heuristic**. We can use it to **improve the EA** boosting the search capabilities, or the inverse: boosting a heuristic with evolutionary tricks.

A famous book by _Michalewicz_ gave some insights on these. On the horizontal axis we see the problems, and the vertical axis shows the performance of any given method. A method has a curve; the pure EA shows good performance but it changes over different problems. A problem-tailored method only performs good in a specific one. But if you combine these both, you get high performances in more problems. These are **memetic algorithms**.

We all probably know what a **meme** is, but mostly we don't have the scientific notion. What is that, then? The **newest self-replicator on earth**, i.e. what is being imitated or copied from person to person.

Hybridisation could happen in different steps: it can be done during crossover, mutation or selection.

### Heuristics in initialization

What are the available approaches? We could, for instance, have a tournament amongst individuals to create the initial candidate population. We could also have a local search method and use this for initialization: we pick $n$ random points, and do some hill-climbing seeding the initial population with these.

You could also have some constructive heuristics, so that you don't have a blind random population.

A popular approach is using **an archive**: if you solved the problem in the past, you initialise the population with solutions that are already known. However, it's not always advantageous: the performance may drop at first if local optima on different landscapes do not coincide. The mean performance increases, but the best doesn't.

### Intelligent operators

It is sometimes possible to incorporate heuristics in crossover/mutation. For example, Merz's DPX operator for the TSP problem looks at common sub tours, decides to keep these and connect the remaining points in a smarter way using a heuristic neighbourhood search. If you think about local search, you could compare it to the reproduction operator that is common in EAs, and it's quite natural to perceive local search as _lifetime learning_. The idea is that the generation in EA are created by crossover and mutation, and once you have the individuals, everything you do to them can be considered as during their lifetime, before they reproduce and create offspring. For example, in Neural Network learning, we could learn the structure with EAs, then learn the weights with backpropagation. Local search can also be combined in another way: keeping it for the _endgame_, as EAs can find interesting areas of the search space but are slower in the search of that area. You switch on some intelligent search heuristic to speed up this last stage.

Graphs are a good representation of the search space when dealing with local search. The $neighbourhood(x)$ concept is useful in this, defined as the set of points that can be reached by a point $x$ with _one application of a move operator_.

Having this notion of neighbours, we can **connect two points** with an **edge of a graph**. Each point in the search space can be seen as a node, and an edge connects two of them. These edges may or may not be symmetrical, and they may have weights.

We can say that the **degree** of a graph is the maximum number of edges coming into/out of a single node, i.e. the **size of the biggest neighbourhood**. As for the pivot rules, this is very important: knowing when to stop is crucial. We could have completely random strategies, informed search... We could have a **greedy ascent**, stopping as soon as a fitter neighbour is found, or a **steepest ascent**, stopping after the whole set of neighbours is examined and choosing the best. As always, there's no general best answer to which is best.

Variations of local search methods can be distinguished by many features, an important one being **where the search happens**: in the genotype space or the phenotype space?

Another difference is **how many iterations of the local search are admissible**. You may want to be generous, or limiting.

A very interesting link between **local search** and **biology** is looking at it as **lifetime learning** (learning that happens during the lifetime of an individual), and two very opposing options are famous: the **Lamarckian** and **Baldwinian**. The first was a biologist who thought that traits acquired by an individual during its lifetime can be transmitted to its offspring. In an EA, this would replace an individual with its fittest neighbour. The latter (Baldwin) believed the opposite: traits cannot be transmitted, but fitness is. This makes the individual get its best neighbour's fitness. A lot of work has been done on this, and it's driven by the fact that **Lamarck was wrong**, and there's some evidence on that. However, in EA we are not constrained by biology: it doesn't matter whether the mechanism works or not.

Everything we said before assumed a single point search: a point in, a point out. We could though use these operators **inside the crossover**, having multiple points as input and multiple points as output.

Diversity becomes a very serious issue if you have local search, representing a quite strong push towards better points. This, though, means losing diversity! This requires some mechanisms to avoid that. For example, Merz's DPX crossover explictly generates individuals at same distance to each parent as they are apart. Another example is Simulated-Annealing acceptance criterion, where the temperature is inversely proportional to the population diversity.

### Simulated annealing

This could be considered a family member of the EA family, even though the metaphor is physical. Annealing is based on a _cooling_ metaphor, if it's done slowly the liquid has time to acquire the perfect structure minimizing the energy contained in the structure, while if it's cooling too quickly you'll have errors. The algorithmic equivalent is a search process, in which we are stepping from point to point to optimize a function f. Whether we accept a point depends on the following formula:

$$
\mathbb{P}_{c}(\operatorname{accept}(j))= \begin{cases}f(j) \leq f(i) & 1 \\ f(i)<f(j) & e^{\frac{f(i)-f(j)}{c}}\end{cases}
$$

We have a generic point $j$ that we want to replace to point $i$. The probability of doing so during the search is shown here: if the function is smaller or equal, we accept the new point. If the function is bigger, then we may accept it with a probability depending on the temperature. This is obviously for a minimization problem, and it means that we **accept worse solutions with a probability that is proportional to how much time has passed from the start of the search**.

We have a parameter $c$ that decides how likely we are to accept worse neighbours, i.e. how fast the _liquid cools down_.

The **Boltzmann selection operator** is a particular application of this: in early stages we have a population which is really **diverse**, while at late stages our population has converged:

$$
P(\text {accepting neighbour})=\left\{\begin{array}{cc}
1 & \Delta f>0 \\
e^{\frac{k \Delta f}{f_{\max }-f_{a v g}}} & \Delta f<0
\end{array}\right.
$$

Choosing operators is very important in a memetic algorithm: you normally have one single variation operator, while here you can also have a search operator or more of them. It is advisable to make the operator different from the mutation/crossover ones, otherwise it won't add value. The added value can be decided by the landscape, and if you change operator, the notion of neighbourhood/landscape changes and it may mean that a local optimum may be a slope now. This means that using a new operator might change how we're exploring the space. To implement that, operator selection can be learned and adapted on-line. We may have all the operators, then think about a mechanism that chooses the operator online/offline.

## Adaptive memetic algorithm

There are some considerations to choose these operators: you could build one, have multiple of them simultaneously, and **add a gene that indicates which search operator we use on the next step**.

Related to this, there's a question: is there any resemblance to the logic of self-adaptive mutation step-sizes? The answer is probably that we **have to first mutate the search operator**, then **search**.

## Summary

We've seen that **memetic algorithms** are **EAs which are hybridised with other heuristics**. This hybridisation offers the **best of both worlds**: blind evolution and problem-specific intelligence. You could use operators from literature. Memetic algorithms are popular in real world applications, and they have been shown to be faster and more accurate. These are the **state of the art** on many problems.
