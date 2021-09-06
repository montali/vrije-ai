# Evolutionary computing - 1 intro

If evolution can create intelligence, we can say it is plausible that *artificial evolution can create artificial intelligence*. This leads us to a question: **can we really evolve intelligence?**

It's important to notice that **intelligence is a property related to behaviour**, i.e. the environment, the body, the brain. Indeed, to have intelligent behaviour we need body and brain, or **hardware and software**. In the 20th century, AI was concerned with **thinking**: just think about DeepBlue. This was the era of **digital AI**. Now, we have another type of AI: **embodied AI**. For example, football-playing robots (*RoboCup*) fall in this category.

The question will now become **can we evolve embodied intelligence**, directly leading to robots. The concept of robot spans lots of things: humanoids, autonomous vehicles, surgical robots, industrial robots...

This diversity of robot forms leads us to the search of optimal bodies and brains. For example, we could notice that 4-footed robots play football better. This makes us wonder if we **can copy something or someone**, i.e. who's the best designer? The answer is **evolution**! The idea is then converting the principles of natural evolution to artificial intelligence. It ain't difficult to see that problem solving in AI can be delated to natural evolution. For example, in the TSP problem, we can evolve a solution by simply making 3 decisions: **identifying the individuals** (candidate solutions, which may or not be optimal), **selection** (survival of the fittest), **reproduction** (if you have 2 parents, cross them over and create a third individual having features from both). Based on this, evolutionary computing has been applied to many tasks nowadays, delivering incredibly good solutions. 

Is evolutionary simulation always possible? We can run into a big problem, known as **reality gap**, i.e. the difference between the behaviour of simulations and the real behaviour. Simulatinos only have limited applicability. So, the question is not *can we evolve robots*, rather **can we evolve real robots?**

Selection is easy: the performance in tasks can be used as a fitness measure. The big question is about reproducibility. It only takes two ideas: look at nature and copy a trick: every living being has two levels of existence, i.e. a genotype and a phenotype. We can do the same for robots, where the first is the specs of the robot, and the second is that specific robot. We can then use a 3D printer to convert the phenotype into a genotype

The **triangle of life** consists of 3 concepts, starting from digital DNA entering morphogenesis (3D printer/human hands), then the robot is **delivered** (birth), starting **infancy** (learning process to understand how to move the body), and getting to **fertility** (only if the learning went well, otherwise it's removed). Finally, the **mature life** consists in survival, mating, learning, task execution...

We should also think about the ethical side: if we had a robot population reproducing in the wild, **would it be safe**?

We should add a **killer switch** that could stop the reproduction. We therefore need a centralised and externalised reproduction, arriving to the notion of an **evosphere**, having a production center, a learning center, an arena (representing the outside world) and **recycling**. The kill switch is the production center itself, if we turn it off, robots can't reproduce anymore. 

The Amsterdam experiment was groundbreaking as it was the first with a real population in which robots could co-exist and interact. The fitness was therefore evaluated in a shared environment, and the selection was done by the robots themselves (to use a natural analogy, in Cambridge the human chose, while in Ams the robots chose on their own). Finally, in Amsterdam the number of deaths/births was not fixed, so the population could grow or shrink. 

So far, the good news is that we're only at the start! What we also do is that we identify the steps that a user needs to go through to build such a system, first of all the decision of how the robots are made (the phenotype). After doing that, we have to determine which genotypes can exist, and how to convert them to phenotypes. In other words, we're creating the production center. Then, how they **reproduce** (mutation, crossover), the **target** (skill, task, fitness, reward), the **selection** (parent selection, survivor selection) and finally the **learning** (supervised, unsupervised.)

Now, how do we make sure that the robots are fit for the real environment? We have to observe that there's two selection mechanisms (parent and environmental), having two objectives. Another important question to be asked is *is the brain more important than the body? Which one is the most important?* It happens often that the body is more important than the brain.

Finally, the designer can choose between the Darwinian or the Lamarckian evolution model, with the second one apparently being a better choice.

The most succesful research in this field is titled *Autonomos Robot Evolution: Cradle to Grave*, featuring a robotic arm building robots (from the *Robot Bank* components).

Human assistance can intervene in selection and reproduction, and this distinuighses the **type of robot evolutionary system** (1,2,3,4).

In the near future it's quite likely that we'll have type 1 evosphere, in 5-15 years type 2 and 3, and in 15+ years fully autonomous type 4 robots.

Rather then directly engineering the robot, we're engineering a system that engineers the robot for us!

