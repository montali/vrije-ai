# The origins

Knowing the historical context in which a scientific discipline was born is often useful. This is the case for Evolutionary Computing too.

**Charles Darwin** was one of the most important fathers, together with **Watson&Crick** (helix structure discovery), **Von Neumann** and **Turing**.

These people were responsible for the basics for EC.

Now, why would we need it? Remember the talk we had about evolution of intelligence: **if evolution can develop intelligence, then artificial evolution can develop artificial intelligence.** There's also another reason: EAs can be used as heuristic problem-solving methods.

Problem-solving is a **common topic** in mathematics, CS... There are two processes happening nowadays: the **complexity** of the problems is increasing, while the **available time** is decreasing!

We need algorithms that can work on a wide range of problems, with fast translation from problem to problem. We may look at nature: _is there a solution that we could copy?_ In fact, there is one: the natural problem-solver we have is **the brain**, but we are actually more interested in the **mechanism that created it**, evolution.

Interestingly, the idea of using evolution in problem-solving is very old: Turing proposed it in 1948!

In 1962, Bremermann proposed optimization through evolution and recombination. Rechenberg in 1964, Fogel, Owens and Walsh introduced **evolutionary programming** in 1965, and in 1975, Holland proposed **genetic algorithms**. Finally, in 1992 Koza proposed **genetic programming**.

There's EC conferences every year, the most famous being **EVOSTAR** and **GECCO**.

## Survival of the fittest

When talking about evolution, we know it's based on the **survival of the fittest**: the shortage of resources leads to selection. The fittest individuals have higher chance of reproducing. As already said, fitness in nature is a derived, secondary measure, while in EC the fitness is defined a priori and the reproductive chances are derived from that, not the inverse.

The second important pillar of Darwinian evolution is **creating diversity** (reproduction), the physical and behavioural differences that affect your phenotype, partly determined by inheritance, partly by the development (nature vs. nurture). Some phenotypic traits will be passed on to the next generation, so next generations will have new, better combinations.

_If you have variation, heritage and selection, you must have evolution_.

We have combinations of traits that are better adapted, increasing the development chances (individuals are more prone to be fit). Variations occur through random changes, fueling diversity, having effect on the population. **An individual never evolves: it's the population that does so.**

Artificial evolution could be beneficial to discover generalization about natural evolving systems.

## A deeper insight

We know that population can be represented by a number of **traits** (muscular mass, skin color, weight...) forming an _n-dimensional_ space, so we can construct a _n+1_-dimensional space, with height corresponding to fitness. Selection _pushes_ the population up in this landscape, but there's always random variations (a population could go down the hill). There may be local optimums too.

We have to consider that the information that's required to build a living organism is found in the DNA, and there's a dichotomy between the **genotype** (DNA) and the **phenotype** (the incarnation, the outside of the individual). They are clearly linked, and in nature the mapping is extremely complex. It could be that one gene affects several traits, or the inverse too. We assume, somehow, that small changes in the genotype lead to small changes in the phenotype. This means that the landscape is kind of continuous.

As for the rest of genetics, genes are structured and chromosomes are their unit. Often, there are two copies of the same chromosome (two halves complement themselves, if one is lost, the other reconstructs it). The complete genetic material in an individual's genotype is called **genome**. We nowadays know that 99.9% of human DNA is the same.

How do these chromosomes work? The most important application is **reproduction**: a human body cell contains 23 pairs of chromosomes, while the gametes (sperm/eggs) contain half. The **crossover** happens during fertilization, in which the chromosomes _align, duplicate and swap._

**Mutations** are really important: crossing over is never perfect, there's always replication errors that introduce variations. This is typically a good thing, but may not be (tumors?).

It's also interesting to know that there's deep coding systems behind life on earth: DNA is built from nucleotides (there's 4 of them), and most of the living being on earth share most of them.

Finally, we have to state a fact that is interesting for artificial evolution too: there's a several steps process from DNA to RNA to protein, and this process is **one way only!** You cannot get the genotype from the phenotype. If something happens to the individual in a given period of time, this change will not **be coded back to the DNA**. **Lamarckian evolution is therefore wrong!** This, though, does not mean that we cannot use it in Artificial Evolution.

## Summary

Evolutionary Computing had origin in the 60s and the 70s, with different names/dialects which have been merged under the **Evolutionary Computing** field. This is embedded in several sciences, like bio-inspired computing, computational intelligence, artificial intelligence...

Evolutionary computing **does not have to be biologically plausible!**
