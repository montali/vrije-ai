# Automation, control and stress/workload

When things go wrong, we often have several things that happened together. For example, for a self driving accident we should have a distracted driver, a distracted pedestrian, strange conditions of the road...

This is why we use the **swiss cheese model**: *holes* in different levels are covered by other layers!

We already talked about another different application in which automation could be interesting: **radiology**. After the introduction of deep learning and CV, there have already been projects that outperform radiologists. 

First of all, we should ask why are tasks automated? Automation could outperform the human in terms of time and error avoidance. Then, which tasks could we automate? **Dull, Dirty and Dangerous** tasks. For example, *applying for a passport*, or *check an unexploded bomb*.

A lot of systems are working at the **information acquisition, selection, filtering level**. The next one is **data integration**: for example, *self driving* integrates lots of data from different sensors. Automation can also take form of **advisory systems**, for example collision prevention. Finally, **control and execution**, in which robots are included.

In terms of self driving, we have a different scale for the levels:

- Level 0: automated systems issue warning and momentarily intervene
- Level 1: hands on
- Level 2: hands off
- Level 3: eyes off
- Level 4: mind off
- Level 5: steering wheel optional

In order to trust the automated system we need to figure out when it is reliable and when it is not. What could be the causes of unreliability? First, **errors**, but even other reasons: usage outside of the operating range, wrong settings, logic not understood by the user... The level of automation has to be correct for the level of the user. 

Basically, the system could be pretty good while the interaction could still not be.

 After talking about these, we should talk about **trust**, i.e. **percieved reliability**. As there might be problems with the interface, we could have a low percieved reliability: this is critical for the acceptance of automated systems. This is the first thing to worry about when designing automated systems. You can have two possibilities: either the user **mistrusts** the system, either **overtrusts**. The first happens when the user fails to understand the system or its limitations. If you don't understand the system, you'll be inefficient and slow. You'll also occur in errors, as you're not taking warnings seriously. 

**Overtrust** happens when actual reliability is difficult to judge: you're following the system too much, and you don't actually have a clear picture of the actual reliability. You think the system is more reliable than it actually is, and this can have serious consequences: there will be more misses, as you're not paying attention, you detect failures slowly, and have poor situational awareness. 

A good automated system should have a less *rich* communication (compare natural speech to voice assistants, the latter need simple commands), preserve job satisfaction (self driving cars ain't fun!), should have a training adapted to the level of automation, and should be tuned to the task.

## How do we actually automate something?

We already talked about **task and function analysis**: these tell us what the task components are, and what the needed functions are. If you do that, you get a list of the tasks which you can allocate to human and system. This is a big challenge: we have to combine human and system tasks.

Humans are very good at detection of noise and at perceiving unexpected things. We need to know what the humans are good for: for example, generalization is a task in which we outperform the machine.

There are a few important things to consider to have **human-centered automation**: it's important to keep the human informed, trained and in the loop. We'll have to select appropriate stage and levels, using flexible, adaptive automation.

## Control

How do we select **responses** and **actions**? 

### Decision complexity

We already talked about it in **Decision Making**: making decisions could be difficult, especially when lots of options are available. People find it hard to make decisions: this is called the **paradox of choice**, as people get nervous when they have many options. 

Reaction time can be related to the logarithm of the number of **choices** (*stimuli*). `a` and `b` are constants, with `a` being the intercept and `b` the slope, depending on the task and the individual. 

Note that sometimes fewer alternatives are not faster: let's say I had morse code or a keyboard. Would I be faster using morse code (having 2 choices) or the keyboard (having 26 choices)? The answer is pretty obvious. Information transfer is greater with fewer decisions!

That's different, for example, when designing a website: you want the user to choose between a low number of choices, maybe multiple times. Users don't like to have a lot of choices, but the user may also get frustrated to the depth of the decision tree. There's always a **balance** to find.

Another thing is **response expectancy**: we have an expetatino about how the system is going to work, and we want to preserve that. For example, we like to have the same direction within stimula and response: we move the steering wheel right, the car goes right. In psychology there's a famous effect, **Simon effect**: you have to respond to a dot, appearing either on left or right, and you can respond either with your left or right hand. You will be way faster with the hand on the side of the dot.

Another thing to mention is **speed-accuracy tradeoff**: when we try to make things quicker, we become less accurate. However, in many cases speed and accuracy are positively correlated: for example, we are more focused in high-stress situations. 

Position control devices are multiple: it's important to know how to design these. You have to think about **Fitts' law**: it quantifies the difficulty of a movement and the time it requires. The relationship between the ratio of the distance and the target size is logarithmic. We can take the `a` case having distance 4 and width of target 1, the task difficulty would be 3. Having `a` and `b` as constants, we can get the **movement time**. 

An important concept is that of **gain**: defined as the ratio between delta of output and delta of input. This is the rate about how much you move, and how much the object is moved. In touch screens, this ratio is 1!

Position control devices represent a big thing today: mouse and touchscreen are technologies used every dy.

**Voice Input Devices** are a big thing too: hands and eyes are free, and there's a large number of possibilities. We might expect, in the future, to have brain-computer interfaces!

Talking about closed-loop control, there are different types of tracking: we talked about the mouse (0-order, as it directly changes the position), then you have a 1st order changing the **speed**(gas pedal, joystick), and 2nd order controlling acceleration (e.g. a spacecraft).

To differenciate from open-loop control, we also have open-loop control: the operator does not correct basing on the error, so he doesn't need to continuously look at the instruments.

