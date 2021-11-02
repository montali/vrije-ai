# Evolutionary Robotics

We have to first explain the difference between **active and passive** entities. Passive things (like sunglasses) are things you could optimize, but exhibit no behaviour. On the other hand, when evolving robots you have **active objects**, having a **behaviour**.

When you look into this kind of evolution, it forms a specific a subtype of all Artificial Evolutionary Systems. There are a couple of differences:

- Individuals are **active/autonomous entities** making their own decisions, typically basing on sensory inputs or environment information
- They **operate in an environment**: this is a crucial difference, as individuals of the TSP (for example) are just points in a search space, while robots are embedded in space and time, being subject to physics laws
- **Evaluation and selection are based on what an agent does**, not what it is: we need tests for fitness evaluations, which then depend on many factors (for example the starting condition is a source of uncertainty). The space of behaviours is huge compared to the one of simpler problems, and it could just be an infinite number. The mate selection could even be defined without fitness functions, so open ended evolution is possible (same as in real life), meaning there's no task that you have to perform optimally, you just liberally reproduce as me in my exchange
- Usually, all offspring are made at the same time, while here **we may have an asynchronous reproduction**, as birth and death may be not sinchronized.

A robot is defined by a **sensory** component, a **controller** and **actuators**. Actuators interact with the **world**, changing it.

A **robot** is therefore a **combination of hardware and software**, embedded in a sensory-motor loop/stream. It always **operates in an environment**, exhibiting **behaviour**. Very often, a robot is made for some purpose/task, and it can be evaluated by this task.

The area of Evolutionary Robotics is not new, and it was used for the evolution of controllers. There are a couple of good definitions of the field:

- *Aims to apply evolutionary computation techniques to evolve the overall design, or controllers, or both, for real and simulated autonomous robots*
- *Useful both for investigating the design space of robotic applications and for testing scientific hypotheses of biological mechanisms and processes*
- *Robotics aim to continuously generate better behaviour for a given robot, while the long-term goal of Evolutionary Robotics is creating general robot-generating algorithms*

From a technical point of view, we know that programming a robot is very hard, as we're in a complex environment (the real world). The sensor-actuator mapping is not easy either, and the fitness can be unspecified or complex. The user/designer influence is very local, while target behaviour is **global** (a robot in an environment possibly containing other robots).

The majority of controllers are developed for some movement-related task.

To evolve a robot controller in a fixed body, we have two *brains*, being the controller code, and we could recombine these brains to get a *child brain*.

There are many possibilities for controllers, as neural networks, behaviour trees, rules, C++ programs, machine code. There are huge unknowns in this process, as the evolvability, the encoding, the variation operators...

Generally, a robot is specified by *sensors*, *actuators* (motors, LED-lights, IR-diodes, WiFi) and *controllers* (mapping sensor input to actuator output). 

The *Arena* could be defined by the *Floor* and the *Space*.

Finally, the *Task* has to be defined: it could be *movement-related*, *navigation-related*, *puck collection*...

The fitness function is definable as the quality of behaviour over an *evaluation period*, for example, in obstacle avoidance, we'll have a fitness considering forward speed, rotational speed, and collisions.

To evaluate fitness, we may both use simulations and real world experiments. 

We have to distinguish between two different stages in the robot design workflow: the first stage is the **design stage**, then we have the **deployment** and finally the robot can start the **operational stage**. Offline evolution takes place in the first, having a best controller installed on the robot and remaining fixated during operation, while online evolution happens during robot operation, and controllers are evolved and tested continuously and concurrently. The first option is more popular in literature.

### Off-line evolution

We can have **many generations** of **large populations**, conducting many runs, then deploying the best controller. If we use simulated evolution, we'll run into the **reality gap**, while real life evaluations have a longer runtime. In this approach, the emphasis is on optimizing the design.

### Online evolution

It's important to distinguish to types of entities: on one hand we have a **set of robots**, where one entity is one robot, while the **set of individuals** is composed of **controllers**. The connection can be defined in two ways: 

- One robot has one controller, the robot group size is the population size, and mutation happens inside robots while crossover happens between robots
- One robot has one population: one of these robots is used as an *island*, mutation and crossover takes place inside, and we *may have migration* between robots/islands

The evaluation is done in **real time and space.**

Online evolution is much more **natural**, as usually EAs are used for optimization and **not adaptation**. Online evolution is focused exactly on that. 

If we use real robots to evolve controllers, we have a *time problem*: evolving on physical systems take a long time. Using simulated environments leads to **reality gaps**: transferring a controller that was evolved in simulation usually fails because the behaviour is different from the simulated one. This difference is usually not good for us.

Let us revisit the difference between ER and EC:

- The fitness function is **always very noise** as it regards the real world
- The fitness function is also **very costly**: for robust behaviour we have to evolve and optimize a controller for different starting conditions
- The fitness function is very **complex** too, as there's a new element, *behaviour*. If you use an EA for optimization, you have genotype-phenotype-fitness, while in ER you have genotype-phenotype-behaviour-fitness
- The fitness function may be **implicit**: in a classic EA for optimization we always have a quality measure to maximize, converted to some fitness. In real life there's no such number, mating selection happens on difficult mechanisms.
- The fitness landscape has **no-go areas**: part of the search space contains *impossible robots* which may break down

Another consideration on the types of fitness functions can be done, distinguishing 3 dimensions:

- **Functional vs. Behavioural**: the first defines for example, *legs have to be synchronized*, while the latter could be *the robot can walk well*
- **Explicit vs. Implicit**: the first comes down to some *decomposition* of behaviour into some subbehaviour (that altogether are good enough) to achieve one whole fitness value
- **External vs. Internal**: in the first, an observer (camera) observes the robot and quantifies the behaviour, while in the latter the robot knows its goodness itself.

Generally, we prefer working on the WHAT and not the how, and autonomous above externally controlled. Putting this all together, ideally the fitness function should be internal, behavioural and implicit.

## Novelty search

The idea is quite strange: we ignore the goal, ignore the fitness and just mind the diversity of the behaviours we observe. This does not always lead to good behaviour, but it has been proved to be performing well.

For example, if we wanted to solve a maze, we could define the fitness as the distance to the target: this doesn't work good, and novelty search would apply well. Comparing NEAT and NEAT+novelty search for maze solving, the NEAT-only solution performs bad.

## MAP-elites

We create a map of the behaviour performance space, containing the intuitions of the robot. Behaviour characterization is define using N dimensions (being *objectives*), we transform the behaviour space into discrete bins according to a user-defined granularity level. We use some *discrete bins* to transform the behaviour space, obtaining N (number of behaviour characterisation, for example robot legs) by M (bins per dimension) controllers. We finally try to find the highest performing controller in the batch, drawing a behaviour-performance map to speed up the search. 

## Towards evolving real robots

Robots can be evolved in different ways: we can do it in simulation or real world, and evolve brain or body. Evolving the brain is what most scientists are concerned with, but evolving body AND brains in simulation is **non-existent** right now. This implies some technical opportunities, but on top of this, we have ethical, legal, societal issues: would we really want this?

Usually, the process of evolution takes space in simulation, and some of the robots can then be built in reality. Evolution is simulated, and some result is then physical. 

There's an underlying system architecture called the *Triangle of Life*, specifying a robotic life cycle. It starts with conception (creation of a genotype), which transitions to a phenotype during the *birth process*, finalizing in the *delivery* of the robot, followed by a *learning period*, optimizing its own controller for its own body. The brain is therefore adjusted to the body, as it happens in nature. After this learning period the robot can be tested, and if the brain matches the given body (robot passes some examination), we postulate the robot is an adult, and we can go make him go to the real world!

The triangle of life describes a generic architecture, while the EvoSphere defines a real world implementation of that. 

In an experiment by Brodbeck, we see robots generated by a few stacked blocks, with genotypes specifying the arrangement. All robots are then instantiated in the real world, and the fitness evaluation is done in the real world. This demonstrates an almost hands-free birth clinic. 

In a PoC of real world evolution robot morphologies, we can see more complex morphologies than the ones seen in Cambridge, having real reproduction. The reproduction is the hard part (robot reproduction requires that robot can have children), as selection is easy. All robots are built in the real world, and strictly speaking, there's no real evolution here. 

Of course they didn't stop with the robot baby project, and a big project started in 2018. They are combining the best of both worlds, using physical robots/birth clinic, and a digital evolutionary process in a simulated world, having the same genetic language. This allows cross-fertilization, having both virtual and physical parents!

Evolution was discovered (not invented) by Dariwn in the 19th century. He described it as a process that had already taken place in the Biosphere, in vivo. In the 20th century we invented the computer, allowing us to built virtual world and implement darwininian process in silico. Finally, in the 21st century there will be a transition from software to hardware.