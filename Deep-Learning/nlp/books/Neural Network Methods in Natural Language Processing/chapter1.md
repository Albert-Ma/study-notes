# Introduction

date@2018/9/5


author@mxy

## The challenges of natural language processing

Besides the challenges of dealing with ambiguous and variable inputs in a system with ill-defined and unspecified set of
rules, natural language exhibits an additional set of properties that make it even more challenging for computational 
approaches, including machine learning: it is *discrete*, *compositional*, and *sparse*.


### Language is symbolic and discrete

Characters and words are discrete, there is no inherent relation between two words or characters that can be inferred from
the symbol themselves, or from the individual letters they are made of.There is no simple operation that will allow us
to move from the word “red” to the word “pink” without using a large lookup table or a dictionary.


### Language is also compositional

The meaning of a document or a sentence is composed of the basic words, you cannot know it all if you just see one character
or one word.

### Data sparseness

The way in which words (discrete symbols) can be combined to form meanings is practically infinite. The number of possible
valid sentences is tremendous: we could never hope to enumerate all of them.

## Neural networks and deep learning
Deep learning is a new branch of machine learning inspired by the way computation works in the brain, which can be 
characterized as learning of parameterized differentiable mathematical functions.Maybe you can say that deep learning is
to learn a correct representation of the given data.

## Deep learning in nlp

 A major usage in nlp is the embedding layer which can transform discrete objects to continuous objects. It's part of the
 training process.
 
 There are two major kinds of neural networks: feed-forward networks and recurrent / recursive networks.
 
 
 Feed-forward networks can disregard the order of elements. Convolutional feed forward networks are specialized 
 architectures that excel at extracting local patterns in the data: they are fed arbitrarily-sized inputs, and are 
 capable of extracting meaningful local patterns that are sensitive to word order, regardless of where they appear in
  the input.These work very well for identifying indicative phrases or idioms of up to a fixed length in long sentences 
  or documents.
  
 Recurrent neural networks are specialized models for sequential data. They allow abandoning the markov assumption that
 was prevalent in natural language processing for decades, and designing models that can condition on entire
sentences, while taking word order into account when it is needed, and not suffering much from statistical estimation 
problems stemming from data sparsity.This capability leads to impressive gains in language-modeling, the task of
 predicting the probability of the next word in a sequence (or, equivalently, the probability of a sequence), which is 
 a cornerstone of many NLP applications.
 
 Neural network can accommodate the *structured* problems in nlp which required the production of complex output structures
 such as sequences or trees.
 
 
 ### Success stories
 
Convolutional and pooling architecture show promising results on many tasks, including *document classification*,
*short-text categorization*, *sentiment classification*, *relation type classification between entities*, *event detection*,
*paraphrase identification*, *semantic role labeling*, *question answering*, *predicting box-office revenues of movies based on
critic reviews*, *modeling text interestingness*, and *modeling the relation between character-sequences and part-of-speech tags*.


Recursive models were shown to produce state-of-the-art or near state-of-the-art results for *constituency and dependency parse re-ranking*, 
*discourse parsing*,*semantic relation classification*, *political ideology detection based on parse trees*, *sentiment 
classification*, *target-dependent sentiment classification* and *question answering*.


## Summary

Human are excel at creating, utilizing and understanding language, but not excel at describing language with regularities
and formal understanding. So neural networks especially deep neural networks can learn the representation of given data.
This is good and also bad.It's depend on data too much. 
 