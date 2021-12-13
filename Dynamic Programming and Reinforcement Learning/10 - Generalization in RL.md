# Generalization in RL

This will finally motivate Deep Learning in RL. We'll first broadly discuss generalization and applications, then dig into supervised/reinforcement learning. 

RL is about an agent taking actions in an environment, to achieve goals. The state is modified and the agent receives an observation and a reward. This is a generic setting as the transitions can be stochastic. Observation may not provide **full knowledge** about the underlying state! You can think of a maze, seen in FPV: you don't know the whole maze, just what you see.

Another thing that makes the RL problem complex is that the experience you get might be constrained: you may be using an emulator, or limited data.

For instance, deep RL is able to play ATARI games, just by looking at the pixels. Other applications are famous, like Go, poker, real time strategy games.

In real world scenarios it's often difficult to let an agent interact freely:

- The agent may not be able to interact with the true environment. What you can do is try to instead learn in a simulation, and use the policy that you have learned in simulation in the real world. You are though faced with the **reality gap**: in that case, the policy might not transfer well to the real world. 

- In another setting, you may have access to limited data;

We can do two things when applying RL to the real world:

- Build a **simulator** that is as accurate as possible: the better the simulator, the better the agent. If it's close enough, we can transfer the policy to the real world
- Improve the **generalisation** through the learning algorithm

## Generalization

Generalization can be defined as the capacity to achieve good performance in an environment where limited data has been gathered, or, in another definition, the capacity to obtain good performance in a related environment (meaning, related to the one you're training in): you can train the agent in one given *simulation*, and hope that the policy will transfer well to the real world. 

To formalize this, we will first discuss supervised learning then look at the RL setting. 

### Generalisation from limited data in supervised learning

In supervised learning, we're mapping from a dataset (number of points having labels and features) into a **predictive model** $f(x|D_{LS})$, trying to predict the label given some features. 

You get the datapoints, and you want to understand the dependence between $X$ and $y$. You only have a limited number of these datapoints!

Because you only have limited data, you need generalisation!

Taking a look at slide 14, you see two potential predictive models: one is overfitting too much, while the other has too much bias. In the bottom left, we're using a linear approximator, but the underlying distribution looks non-linear! On the top-right, the loss is very low on the training samples, but it probably won't be useful. 

Another way to visualize these is taking a new datapoint, and try to predict the label. You take one new input, and look at the predictive model, given the limited dataset of learning samples, then look at the predictions. 

The function $f(x)$ is a random variable itself, as the dataset is a random variable. This means that the average error is also a random variable. We can therefore write the **expected value** of this average error RV! This is equal to the expectation over the input state (every new sample that you get into the sample space). When you look at the $L2$ loss function, you can decompose it as $\underset{D_{L S}}{\mathbb{E}} \underset{Y \mid X}{\mathbb{E}}\left(Y-f\left(X \mid D_{L S}\right)\right)^{2}=\sigma^{2}(x)+\operatorname{bias}^{2}(x)$, directly having the bias-variance decomposition (which you get by looking at the expectations). You could also split the **variance** term into the *internal variance* (when there is some noise in the labels themselves, anyway, meaning there's a part of the loss you'll never be able to eliminate) and *parametric variance* (if you have an infinite amount of data, it will go to 0).

$\operatorname{bias}^{2}(x) \triangleq\left(\mathbb{E}_{Y \mid x}(Y)-\mathbb{E}_{D_{L S}} f\left(x \mid D_{L S}\right)\right)^{2}$

$\sigma^{2}(x) \triangleq \underbrace{\mathbb{E}_{Y \mid x}\left(Y-\mathbb{E}_{Y \mid x}(Y)\right)^{2}}_{\text {Internal variance }}+\underbrace{\mathbb{E}_{D_{L S}}\left(f\left(x \mid D_{L S}\right)-\mathbb{E}_{D_{L S}} f\left(x \mid D_{L S}\right)\right)^{2}}_{\text {Parametric variance }=\text { overfitting }}$

In the context of an L2 loss function (case of a regression algorithm), you can rewrite the sum as above. Basically, that's what we described earlier.

If you have an overfitting model, you'll have a very high parametric variance.

## Generalization in RL

As already said, there's no bias-variance decomposition when we're not using the $L_2$ loss. We do not want to have something that is too complex, but at the same time we want a sufficiently rich learning algorithm. Therefore, the idea of bias-overfitting is pretty similar. We have a dataset $D$ considered as a RV drawn from a distribution dataset $D \sim \mathcal{D}$ and we're interested in a policy $\pi_D$. (Ger uses $\alpha$ for policies!)

The goal of RL, in this MDP case (offline algorithm based on a finite dataset), is to go from the dataset into a policy. Then, you can estimate how good the policy is by looking at the maximisation (in expectation) of the difference you obtain by looking at the suboptimality of our $\pi_D$ compared to the optimal $\pi^*$. The latter doesn't have to be known, but for formalization we'll now assume that we know the expected return from it. 

You can decompose this error into two different terms, by introducing $\pi_{D\infty}$, corresponding to the $D$ we obtain with an infinite amount of data. By subtracting and adding the same term, we'll be able to obtain the same decomposition. Note that the asymptotic bias is not depending on the $D$ anymore, so it can be put out of the expectation. This decomposition is now similar to the previous, with a term being the bias and a term being the overfitting. If we have an infinite amount of datapoints, the overfitting will go to zero, and if you have an infinitely *rich* algorithm, we'll take the bias to zero. 

If you have more data, you reduce the risk of overfitting, and if you raise the policy class you reduce the asymptotic bias. You don't always lose/win (as in the image) at the same time, but in many contexts this happens.

We can optimize these errors in many ways.

### Abstract representation

With your algorithm, you can take into consideration spurious correlation without wanting it. We may try to remove all the features that discriminate states with very different roles in the dynamics

### Modifying the objective

We could *introduce a bias in the objective function*: we could first modify the reward. For example (in a maze) an instant reward the closer we are to the destinatino might sound nice, and it will lead to bias.

We could even tune the discount factor.

### Playing with the learning algorithm

We could design the algorithm to be as generic as possible. An important element is using *function approximators*. You could use a **representation of the value fucntion**, you could **directly learn a policy**, or you can **use a model of the environment in conjunction with planning**.

In all these cases, you can **use a function approximator for the value**.

The approximator will characterize how the features will be treated into higher levels of abstraction: it could be used for feature selection, for instance. 

