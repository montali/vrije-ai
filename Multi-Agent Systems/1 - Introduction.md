# Multi-Agent systems

Always send emails to the CWI email eric.pauwels@cwi.nl

We'll have 7 weeks of lectures (6 ECTS).

Monday's are lab sessions, thursdays and tuesday classes.

The homework can be made in groups of 3-4 people, if you fail 2 of them you get 0. The deadline is usually the next lab session. 

The first homework are pass/fail, while there's a **final individual assignment** (more substantial), reaching up to 4 points. The final exam counts 50% of the final grade.

There are several books:

- Shoham and Leyton-Brown, MultiAgent Systems, found online
- Sutton and Barto - Reinforcement Learning, found online
- William Spaniel: game theory 101 (YouTube)

The slides should suffice, but it may be interesting to read these.

There also are optional books, just for *personal improvement*.

## Intro to MAS

To introduce the matter, we first have to note that there are **five ongoing trends** within computing:

- **Ubiquity**: computing power is everywhere, you can connect to it
- **Interconnection**
- TODO

Computers are getting more intelligent, and as a consequence we delegate to them. We think about computers not as *signals*, rather similar to *humans*. What we're looking at are computer systems that can act on our behalf.

An **agent** is a computer system that is **situated in an environment** and is capable of **autonomous actions**, in order to meet its **objectives**. It has perception, a sort of *mental state*, and returns *actions*.

A MAS is one that consists in **multiple agents** interacting with **each other**, and the **environment**. Generally, the agents may have **different goals**. In order to be successful, they need to **cooperate**. 

The green dots are the agents, observing **part of the environment**. They have a *mental state*, i.e. what they've learned, and that determines how they're going to act. Initially, we'll look at non-cooperative agents. 

There are several motivations. First of all, **technological**: we're growing distributed, networked computer systems. Secondly, MAS are more **robust**: there's no single point of failure. They're scalable, flexible, and reusable. Applications vary: IoT, swarms of robots...

There's a second reason: they can be **seen as a model for interactivity in societies**, and they're useful in studying economics, social sciences and so on. 

A typical question may be *how can cooperation emerge in societies of self-interested agents*?

In a sense, MAS can be thought of as **distributed AI**, as usually AI concerns itself with processes which are *cognitive*, while distributed AI is more concerned with social interaction.

There can be **two approaches**: suppose we give the individual capabilities to agents, what sort of global behaviour emerges (bottom-up). The alternative is *suppose we search for specific global characteristic, what sort of guidelines/conventions should we impose to agents to obtain interesting global properties*?

MAS has inspirations from many fields, which is a strength but a weakness too: this is an analogy with AI itself.

## Agent Types

We can consider *5 categories* (but don't be too religious about these, they're changing) involved with the *level of autonomy*

### Simple Reflex Agents

Think of this as a *Roomba hoover*, meaning that it reacts to things with simple *if-then rules*.

### Model-Based Reflex Agent

This includes an actual model: the best Roombas build a model of your living room, interacting with it intelligently and complementing its model with the sensors' data. 

### Goal-based agent

The agent has a specific goal, and based on this it creates a **plan**. One example of this is the BDI model, in which you think of an agent having 4 different mental components: *belief* (what it knows about the environment), *desire* (the things it thinks of as possible goals, might be mutually exclusive), *intention* (corresponds to a *desire to which you have committed*, having allotted resources for that intention) and finally *planning action* (a sequence of actions to achieve intentions).

### Utility-based agents

This is seen in RL: before, all the goals had the same utility. They don't have the concept of *achieving something almost good as a goal*. Utility measures *how useful a result is*, through the use of a utility function. 

### Intelligent agents

These are capable of **flexible** and **autonomous actions**: they can be **proactive** (plan to the goal), **reactive** (react to things) and **social** (able to communicate).

## Environments

We can talk about **accessible** environments, in which the agent can **completely observe the whole environment** or **inaccessible**. Then, we can talk about **deterministic** vs **nondeterministic** environments: in the latter, we don't exactly know what happens in response to an action. We've got **static** and **dynamic environment**: in the first, the environment doesn't change **apart from the actions the agent takes**, while in the latter the environment changes without the agent doing anything. Finally, we can talk about **discrete** and **continuous**.

## Main topics

We'll start of with an intro to **game theory**: you have competing agents, trying to use their rationality to optimize their rewards. We can then talk about **exploration vs exploitation**: I have certain knowledge, do I use it or spend resources trying to explore it? Then, **Reinforcement Learning**, a single learning agent interacting with the environment and learning how to improve its utility. Finally, **Multi-Agent RL**, 

RL is different from supervised learning and unsupervised learning: we learn from **interaction**, but mostly from feedback on the final result. That is basically a big problem of RL: you get the total reward, you want to optimize this and not the incremental reward. 