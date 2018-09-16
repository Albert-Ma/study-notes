# From Linear Models to Multi-layer Perceptrons

date@2018/9/15


author@mxy

# LIMITATIONS OF LINEAR MODELS: THE XOR PROBLEM

The linear models we have talked in previous chapters is severely restricted cause that it cannot present XOR function.

That's the basic problem that linear models sometimes not work for most real applications which the dataset is non-linear.

# NON-LINEAR INPUT TRANSFORMATIONS

So how should we do when data is not linearly separable. Does it separable if data is in a high dimension.

For example, *mapping* data into 2 dimension maybe find a space which can separate 2 class's data.
$$ y = f(x) = \phi{(x)}W +b $$

In the XOR example the transformed data has the same dimensions as the original one, but often in order to make the data
linearly separable one needs to map it to a space with a much higher dimension.

But the function $\phi$ need to manually define which is dependent on the particular dataset, and requires a lot of 
human intuition.

## KERNEL METHODS

Kernelized Support Vectors Machines and Kernel method approach this problem(linearly inseparable) by defining a set of 
generic mappings, each of them mapping the data into very high dimensional – and sometimes even infinite – spaces, and 
then performing linear classification in the transformed space. Working in very high dimensional spaces significantly 
increase the probability of finding a suitable linear separator.

A downside of the approach is that the application of the kernel trick makes the classification procedure for SVMs 
dependent linearly on the size of the training set, making it prohibitive for use in setups with reasonably large 
training sets. Another downside of high dimensional spaces is that they increase the risk of overfitting.

## TRAINABLE MAPPING FUNCTIONS

Another different approach is to define a trainable non-linear mapping function and train it in conjunction with the linear
classifier. The mapping function also considered as "representation" of the dataset.

For example, the mapping function can take the form of a parameterized linear model, followed by a non-linear activation 
function g that is applied to each of the output dimensions.$$ y= \phi{(x)}W +b $$ $$ \phi{(x)} = g(xW^{'}+b^{'}) $$

This entie expression can learn both the representation function and the linear classifier on top of it at the same time.

This is the main idea behind deep learning and neural networks. In fact, equation  describes a very common neural network
architecture called a multi-layer perceptron(MLP).