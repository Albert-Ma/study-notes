# Beam Search(集束搜索)

@author mxy

@date 2018/9/6

## Introduction

自然语言处理领域的机器翻译、文本摘要生成等生成词序列的任务中，解决问题的模型通常最后的输出是基于单词表上的概率分布，得到概率分布之后通常会需要解码器decoder
采样概率分布从而得到最有可能的单词序列。在nlp使用RNN循环神经网络时，可能会遇到这种情况，模型输出是文本，神经网络模型中的最后一层
的每个神经元对应输出词汇表中的每个单词，在通过softmax激活函数输出词汇表中的每个单词作为序列中的下一个单词的概率。

解码可能性最大的输出序列需要搜索所有可能的输出序列。 但是词汇量的大小通常是数万或数十万，甚至数百万个单词。 因此，搜索问题在输出序
列的长度上是指数级的，并且完全搜索是非常复杂的，是NP-complete问题。

既然是NP-complete问题，无法直接解决，可以通过一些启发式的方法来逼近最优解。最常用的方法是greedy search 和 beam search。

## Greedy Search

贪婪算法是最简单且效率最高，但是效果确不如beam search，仅仅是局部最优解。

在rnn输出最终的概率分布的时候，贪婪算法每次选择概率最大的那一个，直到遇到终止符则结束搜索。假设词表大小为5，a,b,c,d,e，概率分布如下表所示，
其中单词经过映射为Integer，列index代表单词，比如第0列代表a：

[0.1, 0.2, 0.3, 0.4, 0.5],  
[0.5, 0.4, 0.3, 0.2, 0.1],  
[0.1, 0.2, 0.3, 0.4, 0.5],  
[0.5, 0.4, 0.3, 0.2, 0.1],  
[0.1, 0.2, 0.3, 0.4, 0.5],

则最终贪婪算法的输出单词序列则是e,a,e,a,e

## Beam Search

集束搜索也是基于贪婪搜索，只不过是每次不是选择最大的那一个，而是选择size大小的几个，size通常由人工设定。

> The local beam search algorithm keeps track of k states rather than just one. It begins with k randomly generated states.
 At each step, all the successors of all k states are generated. If any one is a goal, the algorithm halts. Otherwise, it
 selects the k best successors from the complete list and repeats.  
 
 ——Pages 125-126, Artificial Intelligence: A Modern Approach (3rd Edition), 2009.


> In NMT, new sentences are translated by a simple beam search decoder that finds a translation that approximately 
maximizes the conditional probability of a trained NMT model. The beam search strategy generates the translation word by
 word from left-to-right while keeping a fixed number (beam) of active candidates at each time step. By increasing the
  beam size, the translation performance can increase at the expense of significantly reducing the decoder speed.
  
 ——— Beam Search Strategies for Neural Machine Translation, 2017.
 
 所以集束搜索是寻找使得条件概率最大的序列，从左到右，保持size大小的候选集，然后当前条件概率乘以下一个单词的概率分布，得到新的序列，选择size
 大小的最大条件概率的序列得到新的候选集，如此循环。用上个例子说明，假设beam size为2，则结果：
 
[0.1, 0.2, 0.3, 0.4, 0.5],  
[0.5, 0.4, 0.3, 0.2, 0.1],  
[0.1, 0.2, 0.3, 0.4, 0.5],  
[0.5, 0.4, 0.3, 0.2, 0.1],  
[0.1, 0.2, 0.3, 0.4, 0.5],

![Aaron Swartz](https://raw.githubusercontent.com/Albert-xy/study-notes/master/Deep-Learning/nlp/images/beam_search_result.png)


## Reference

1.[How to Implement a Beam Search Decoder for Natural Language Processing](https://machinelearningmastery.com/beam-search-decoder-natural-language-processing/)

2.[谁能解释下seq2seq中的beam search算法过程?](https://www.zhihu.com/question/54356960)