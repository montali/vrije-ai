# Neuroevolution

We all know that a neural network is an abstraction of a natural brain. We have weights and biases that we are gonna use to get an output. The common learning method is **supervised learning**, in which you **do know the answers**. It may happen that we don't know the answers some times: an example of this is **control** applications, as playing a car videogame. There may be multiple ways of *driving well*.

In **neuroevolution**, instead of adjusting weight of a network through examples, we **evolve populations of networks**. What you can do is that then the performance of driving the car is your individual's fitness. We could have different approaches:

- Evolving the weights only, with fixed topology
- Evolving the topology too
- Evolving the activation functions too

Other applications may be rocket control, robot control, music creation, pictures... Prediction and classification problems are also possible.

### Pros and cons

You're now obviously avoiding **local optima** as you're maintaining **diversity**, you get more creative/intersting solutions, and you can use it for supervised/unsupervised learning tasks.

The negative points is that **explainability is low**, and it is **computationally expensive**.

## Simple neuroevolution

You're turning the problem into vector optimization, with a fully connected network topology.

## Advanced methods

There's no guarantee that a given topology is optimal. We can **evolve it too!**

### NEAT

NEAT is one of the most famous neuroevolution algorithms. Its main premises are the following:

- **Minimality**: it's expensive to optimize big networks, so we start from small ones and only enhance them if needed
- Protecting of innovation through **speciation**: this gives innovations a chance to show their potential

The population starts with **minimal topologies**, and complexity should be maintained if useful.

Talking about **reproduction**, we introduce the **competing conventions problem. ** This means we have more than one way to express a solution to a weight optimization problem with a NN. In other words, how do you know which gene you can combine with which during crossover? Having an *ignorant crossover*, we can miss information if we crossover in the wrong point. To solve this, NEAT uses **innovation numbers**. Our genome is consisting of two lists: one contains the node genes, while the second contains the connections. These have an ID, called *Innovation Number*. Using this innovation number it's possible to align two solutions and compare them to perform crossover. When we find two aligned genes we can inherit them randomly, while when we have disjoint (middle) or excess (end) genes, we take the one from the fittest parent. 

Mutation can add/remove nodes, add/remove a connection, and mutate a weight. Multiple things can happen in the same mutation. 

Innovations could be distruptive: a single extra node could make the NN behave very differently, while changing a weight is a very local change. Maybe, initially the node will cause fitness to degrade, but giving it time to optimize, this innovation could be very useful. Because of this immediate degrade in fitness, though, we have to be careful not to get rid of it quickly. This is done with **speciation**, so that **individuals within a species are similar**. Competition only happens among species members. 

Basically, a list of species is maintained (in the beginning there's no list), and each existing species is represented by a random genotype inside the species from the previous generation (each species has a representative). In each generation, genotypes are sequentially placed into species, and a given genotype in the current generation is placed in the first species in which it is compatible with the representative: when you create a new individual, you go through the list of species, and when you find a match you insert it there. The compatibility is measured according to a **compatibility distance**: you choose the very first species that has a distance lower than a threshold. If a genotype is not compatible with any species, you **create a new one**.

The compatibility distance is obtained by comparing the number of disjoint genes, the excess genes, the average weight differences (of the matching genes) and the number of genes of the largest genome. 
$$
\delta=\frac{c_{1} E}{N}+\frac{c_{2} D}{N}+c_{3} \bar{W}
$$
Then, we implement what's called **fitness sharing**: the fitness of individuals is reduced basing on the species size.

## Types of encoding and CPPNS

When talking about NEAT, we were concerned with a **direct encoding**, having one gene per *cell of the phenotype*. That could be a little bit too much! **Indirect encoding** is also known as generative, and it is based on the **reuse of structures**. Like this, we can obtain a highly compressed representation.

### CPPNS

**Compositional Pattern Producing Networks** is concerned with the second type of encoding. The idea is that it generates **objects**, having a smaller search space. This network represents a function of the problem given its geometry or context. We could use NEAT to evolve this, having activation functions that are also evolving. We are composing groups of functions related to each other, and this could create patterns. When we use the network, we **query** it by providing inputs about the geometry of the problem to the network, obtaining outputs. Let's say we had inputs X and Y and two output colros. We can use this network to colour a grid. 