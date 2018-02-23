---
layout: post
title: Paper Summaries I - Theoretical Impediments to Machine Learning.
---
*This is the first of a series of paper summaries on Machine Learning*

*The original technical report by Judea Pearl can be found [here](http://web.cs.ucla.edu/~kaoru/theoretical-impediments.pdf).*

During the past two decades incredible developments have been made in
the field of machine learning. The usage of GPUs and very large sets of
data have allowed for the development of really complex systems that are
capable of classifying images in a broad range of classes with high accuracy
or detecting the objects (from animals to cars or people) present in these
images without specifying the number of objects. Outside of the image domain,
neural network based translators have shown incredible results. All of these
examples have shown the great potential of machine learning but there
are some problems that escape its capabilities.

Machine learning systems can’t be used to reason about questions that would
be fundamental in advanced AI systems. The field of causal inference
distinguishes a three-layer hierarchy of questions depending on their nature.
From bottom to top: observational (“What does X tell me about Y?”), interventional
(“What if I do X?”) and retrospective (“What if I had done X?”). Current
techniques would be restricted to responding questions that belong to the
first level with questions such as “What’s the most likely price of a stock
given its historic prices?”. Even though these questions can be really
interesting, they leave out two behaviors that characterize human nature:
reasoning about the effects that our actions can have and learning from past actions.

These limitations start with the lack of a formal representation for this
type of statements in model-blind techniques, such as neural networks.
Representations that model them can be found inside of the field of causal
inference. For the interventional layer we can model probabilities of the
type P(y | do(x), z), the probability of observing Y=y, if we set X=x and
consequently observe Z=z. In the case of the retrospective or counterfactual
layer, P(yx | x’, y’) models the probability of an event Y=y had we observed
X=x, given that was observed was X=x’ and Y=y’. Questions that belong to
the lower layers can be responded asking an equivalent question in an upper
layer but not the other way around.

The set of mathematical tools that allows modeling and reasoning about such
statements in both a graphical and algebraic way has been baptised as
“Structural Causal Models” by Judea Pearl and includes three main parts.
Firstly, graphical models can encode the causal assumptions in the knowledge
we have about the world. This is, we can write cause-effect relations
between variables and test their validity against the experimental data.
Counterfactuals and interventional logic make it possible to encode questions
belonging to level 2 and 3 of the hierarchy and have been introduced in the
graphical model framework. The third and final point are structural
equations, that provide a semantic bridge between the last two. 

With the increasing use of artificial intelligence techniques, the most
important question is shifting to whether the developed systems will be
able to reason about the world to modify its state or learn from past actions.
These questions can’t be responded by black-box models and will require of
higher-level logic and tools. SCM provide a solid mathematical base to
reason about these questions and will be of great importance when modeling
the future of AI systems.




