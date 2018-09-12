# Learning basics and Linear models

@date 2018/9/7

@author hcy

## 1. Supervised learning and parameterized functions

What is supervised machine learning?  Rather than designing an algorithm to perform a task, we design an algorithm whose input is a set of labeled examples, and its output is a function that receives an instance and produces the desired label.

As searching over the set of all possible programs (or all possible functions) is a very hard (and rather ill-defined) problem, we often restrict ourselves to search over specific families of functions. Such families of functions are called *hypothesis classes*.

The hypothesis class also determines what can and cannot be represented by the learner. One common hypothesis class is that of high-dimensional linear function:
$$
f(x)=x.W+b
$$
As we will see in the coming chapters, the hypothesis class of linear functions is rather restricted, it is limited to *linear relations*.Howerver, while restricted, linear models have several desired properties: they are **easy** and **effcient** to train, they often result in **convex optimization** objectives, the trained models are somewhat **interpretable**, and they are often very effective in practice.

## 2. Train, test and validation sets

Our main concern is the ability of f() to generalize well to unseen examples.

***Leave-one out***

One solution is to perform *leave-one-out* *cross-validation*:  train $k$ functions $f_{1:k}$, each time leaving out a different input example $x_i$, and evaluating the resulting function $f_i()$ on its ability to predict $x_i$.

***Held-out set***

A more effcient solution in terms of computation time is to split the training set into two subsets, say in a 80%/20% split, train a model on the larger subset (the training set), and test its accuracy on the smaller subset (the held-out set). 

In general it is better to shuffle the examples prior to splitting them, to ensure a balanced distribution of examples between the training and held-out sets. However, sometimes a random split is not a good option. So it is better to make it as similar as possible to how trained model will be used in practice.

***A three way split***

The accepted methodology is to use a three-way split of the data into train, validation and test sets. All the experiments, tweaks, error analysis and model selection should be performed based on the validation set. It is important to keep the test set as pristine as possible, running as few experiments as possible on it.

## 3. Linear models

### Binary classification

$$
\hat y=sign(f(x)) = sign(\bold x.\bold w + b)
$$

The output $f(x)$ is in the range $[-\infty, +\infty]$, and we  map it to one of two classes $\{-1, +1\}$ using the *sign* function.

***Feature Representations***

We need to select some useful features for the classification task. After deciding on a set of features, we create a feature extraction function that maps a real world object to a vector of measurable quantities which can be used as inputs to our models.

A central part in the design of linear models, it the design of the feature function (so called *feature engineering*). One of the promises of deep learning is that it vastly simplifies the feature-engineering process by allowing the model designer to specify a small set of core, basic, or “natural” features, and letting the trainable neural-network architecture combine them into more meaningful higher-level features, or representations. 

### Log-Linear binary classification

$$
\hat y = \delta(f(\bold x))=\frac 1 {1+e^{-{(\bold x.\bold w+b)}}}
$$

We may be interested also in the confidence of the decision, or the probability that the classifier assigns to the class. So map the output  into range [0, 1] using a sigmoid $\theta(x) = \frac 1 {1  + e^{-x}}$.
$$
P(\hat y=1|\bold x)=\delta(f(\bold x)) \\
P(\hat y=0|\bold x)=1 - \delta(f(\bold x))
$$

### Muti-class classification

We should assign an example to one of the k different classes. A possible solution is to consider k weight vectors and biases, one for each class, and predict the class resulting in the highest score:

The six sets of parameters $w$ can be arranged as a matrix $\bold W$ and a vector $\bold b$:
$$
\hat y = f(x) = x.\bold W+\bold b \\
prediction = argmax_i \hat y_{[i]}
$$

### Log-linear multiclass classification

In the multiclass case, we transformed the linear prediction into a probability estimate by passing it through the *softmax* function:
$$
softmax(\bold x)_{[i]}=\frac {e^{\bold x_{[i]}}} {\sum_j e^{\bold x_{[j]}}}
$$

$$
\hat y=softmax(\bold x\bold W + \bold b)
$$

The softmax transformation forces the values in $\hat y$ to be positive and sum to 1, making them interpretable as a probability distribution.

## 4. Representations

In the linear case, the representations are interpretable, in the sense that we can assign a meaningful interpretation to each dimension in the representation vector.

Deep learning models often learn a cascade of representations of the input that build on top of each other, in order to best model the problem at hand, and these representations are often not interpretable. However, they are still very useful for making predictions. Moreover, at the input and the output, we get representations that correspond to particular aspects of the input (i.e. a vector representation for each letter-bigram) or the output (i.e. a vector representation of each of the output classes).

## 5. One-hot and dense vector representations

xxxxxxxxxxxxxxxxx

## 6. Training as optimization

We introduce the notion of a *loss function* $L(\hat y, y)$, assigns a numerical score to a predicted output $\hat y$ given the true expected output $y$. The parameters of the learned function (the matrix $\bold W$ and the biases vector $\bold b$) are then set in order to minimize the loss $L$ over the trainning examples. 
$$
\hat \Theta = argmin_{\Theta}L(\Theta) = argmin_{\Theta}\frac 1 n \sum_{i=1}^nL(f(x_i;\Theta), y_i)
$$

The equation attempts to minimize the loss at all costs, which may result in *overfitting* the training data. To counter that, we use a function $R$ which is called *regularization term*. By adding $R$ to the objective, the optimization problem needs to balance between low loss and low complexity.
$$
\hat \Theta = argmin_{\Theta}\frac 1 n \sum_{i=1}^nL(f(x_i;\Theta), y_i) + \lambda R(\Theta)
$$

## 7. Loss functions

什么是Loss function, 引用wiki的解释：The loss function quantifies the amount by which the prediction deviates from the actual values. 通常而言，损失函数由损失项 (loss term) 和正则项 (regularization term)组成。

- 对于回归问题，有平方损失*square loss*
- 对于分类问题，有*hinge loss*(for soft margin SVM), *log loss*(for logistic regression)
  - 其中对于hinge loss，又可以细分为*hinge loss* (简称 L1 loss) 和*squared hinge loss* (简称 L2 loss)

### Hinge (binary)

$$
L_{hinge(binary)}(y, \hat y) = max(0, 1-y.\hat y)
$$

xxxxxxxxxxxxxxxxxx

## 8. Regularization

see "regularization.md"

## 9. Gradient based optimization

*stochastic gradient descent(SGD)*

xxxxxxxxxxxxxxxxxx
