# Standard assignment - Q&A

We need to define a **controller** for ourself (they put one for us, which is a neural network `demo_controller`, having sensory inputs). In each NN you have weights, which we'll have to **optimize**. All of these weights, together, make our genome. We'll have a population of genomes.

## Plots

The first plot is a **line plot** showing the progress of our evolution (across generations). What we'll want to use are the **average** and **maximum** fitness values. 

To create the population of means, we need to do the evolution multiple times (5), then average the fitness of each individual over the different experiments. Having the population of the means, we can use it to calculate the mean of them and create the plot. We can do the same for the maximums, getting the maximum for each individual over the 5 experiments, then calculating the **mean of maximums**.

We then have to compare these things for each enemy.

For the second plot, we'll have to draw a **box plot**. Having results for each generation and each run, we need to calculate the best value of each run (run 1, generation 1), then select the best one for each population (runs*generations populations). Then you need to select one best for each run, and test each of them 5 times. You have one configuration for each NN, you put it into your NN and test it 5 times. Then you'll have the result for the best neural network for each run. You then calculate the mean of these 5 test results.



## Python3

To use Python3 instead of Python2.7, you just want to replace line 81 in file `evoman/tmx.py` with

```python
for c in list(tag):
```

removing the `getchildren()` call.

