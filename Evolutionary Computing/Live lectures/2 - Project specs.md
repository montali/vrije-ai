Two tasks to solve, 1/10 and 18/10.

40% of the grade is first task, 60% is task 2.

**EvoMan**: fight an enemy, task is designing a controller that wins :)

- 8 kinds of enemies
- controller has to kill them all
- enemy will have static rules (no improvement for him)
- In the first task, we have to fight a single enemy
- In the second task, we fight them all (**generalist**)
- 20 sensors in the game
  - 16 distance from player to projectile (8 projectile tops, 2 coordinates each)
  - 2 distance from player to enemy (2 coordinates)
  - 2 for direction of agents
- 2 kinds of loop
  - iterations of the game
  - search of solution
- Params **you can't change**:
  - level = 2
  - contacthurt="player"
  - playermode="ai"
  - enemymode="static"
- Others you can change:
  - multiplemode -> difference between task 1 and 2, returns more enemies
  - speed -> related to pygame, increases speed of evolution
  - randomini -> random initialization for the enemy/player positions
  - sound -> turn this shit off bro
  - clockprecision -> pygame uses different kinds of *timing*, use *low* to avoid problems
  - timeexpire -> 3k, it's a time limit for the game (some of the games get stuck), default a good choice tho
- There's docs in `evoman1.0-doc.pdf` and you can find papers at `multi_evolution.pdf`
- Reporting research on Canvas (Extra folder) might be useful to get inspirations about reports

## Specialist agent

Design of 2 different EAs (completely separated!) using 3 or more enemies. Compare the two algorithms for the different enemies. 

## Generalist

Choose 2 groups of enemies and combat. There's a competition (and two ranks), winners get 1 point, silver get 0.6, bronze get 0.3.

The second rank is represented by the **gain**, a comparison of the energies of player/enemy:
$$
g = \sum_{i=1}^n p_i - \sum_{i=1}^n e_i
$$

## Report

Needs to be 3 page+1 for the cover (you can use one additional for the references), we have to use the GECCO template. 

- Introduction: try to make the goal and research **clear**, they need to see that we know what we're doing
- Methods: be brief.
- Results and discussions: discuss the results using some plots (why this part of plot is like this, why they're different...)
- Conclusions/Summary
- Literature: add everything you used.

## Rules

- Do not use the EA code that's available in the repo (but inspiration is allowed)
- You **can** use libraries like DEAP 
- You can use the default fitness function, but you're not required to do so!
- Do not make changes in the EVOMAN source code (they need comparable work)

## Plots

Two types of plot: 

- Max and average for the generations/fitness (fitness on Y, generations on Y)
- Comparison of two solutions (box plot) one box plot for solution
  - You have population for each solution
  - Select the best individual (there's randomness, so...)
  - Re-run the best individual

## Tips

- Box plot using the results of different *populations* (select the best solution for each of the 10 independent runs, then test it 5 times)
- Do not use the EA demos
- The cleanest example is `dummy_demo.py`
- Everything you need is in the manual
- Reduce the plot size!
- Test algorithms using small populations (avoid starting with 100 generations!)
- Consider the experiments' time!
- Might be interesting to normalize the input of the controller (found in the default)
- Enable experiment recovery using `load_state()` and `save_state()`
- Review the baseline papers! Look for *Julian Togelius*

