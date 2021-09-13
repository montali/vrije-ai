# Problems to be solved

We'll now discuss different perspective to categorize problems.

## Black box model

This approach distinguishes 3 different components:

- A **model** in the middle, that transforms input into outputs
- **Inputs**
- **Outputs**

We can distinguish different tasks for this approach:

- **Optimization**, in which we know the model and desired output, but not the inputs we need to get them. For example, timetables, TSP, 8-queens.
  - An example of this kind of problems: we have to create **timetables** for a university, having an enormously big search space. The goodness can be defined in multiple, conflicting ways;
  - A second example is the development of a **physical structure for satellites** to connect the body to the antenna. The problem is that vibrations can propagate in a way that it breaks the thing. The design has to be optimized to make it non susceptible to vibrations. A good design for these is not symmetrical, surprisingly.
- **Modelling**: here, the model is unknown. A popular example is **machine learning**, in which we know input and outputs but not the model. Note that these can be transformed into optimization problems.
  - An example is an application for banks that predicts the customers' payback of loans: it connects the data from the customer, and tries to make a prediction about how well the payback will go
- **Simulation**: here, we don't know the output. We know model and inputs, and we can give these to the model and check the output
  - For example, a weather forecast system, or evolutionary economics (artificial life), which uses models to simulate trade, economic competition
  - These can also be used for biologically inclined investigation, to test not-wanted mechanisms (incest?)

### Wind turbine example

In the **Wind turbine example** video, we see a guy optimizing the shape of a turbine blade through Evolutionary Algorithms, ultimately reaching a strange yet ultra efficient shape.

## Search problems

In this kind of problem, we work our way through the search space in a certain manner, trying to find a solution. It's interesting to consider the cardinality of the search space: it can get pretty big.

We first have to state the difference between **search problems** (a search entity defining the search space) and **problem-solvers** (which move through the search spaces).

## Optimization vs. constraint satisfaction

Another interesting comparison is the one between an **objective function** and a **constraint**: the first is based on a quantitative evaluation of a possible solution, as of to assign a number to a solution (to find the maximal or minimal one). A **constraint** is, on the other hand, a binary evaluation that delivers a boolean result that tells whether that constraint holds. For example, _"Is city A visited after city B?"_.

We can combine all these options getting different possibilities:

![optimisation-vs-constraint](./res/optimisation-vs-constraint.png)

In this context, we can consider the 8-queens problem as a **Constraint Satisfaction Problem**: there can be multiple solutions, none of which is optimal compared to the others.

## NP problems

This is heavily different from the others. We want to describe problems by their difficulty, i.e. how hard a problem is to solve. There are some notions to remember:

- **Problem size**: often expressed as the number of problem variables and their domain;
- **Running time**: the number of operations the algorithm takes to solve the problem **in the worst case**;
- **Problem reduction**: the possibility of transforming a problem into another one via a mapping.

Given these notions, we can classify problems into several classes:

- **Class P**: an algorithm can solve the problem in **polynomial time**
- **Class NP**: there's an exponential algorithm solving the problem, but the **verification** of a solution can be done in polynomial time
- **Class NP-hard**: a problem is NP-hard if any other NP problem can be reduced to this. Might be verifiable in non-polynomial time
- **Class NP-complete**: problem is in NP and any other NP problem can be reduced to this problem by a polytime algorithm (NP-hard)
