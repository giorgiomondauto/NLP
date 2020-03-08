## Transformer Architecture

### Introduction
Transformers are a type of Neural Network Architecture and they were developed to solve the problem of neural machine translation: any task that transforms an input sequence to an output sequence (e.g. speech recognition, text - to - speech transformation, etc.)

For models to perform neural machine translation, it is necessary to have some sort of memory. 
For example let’s say that we are translating the following sentence to another language (French):
“The Transformers” are a Japanese  band. The band was formed in 1968, during the height of Japanese music history”
In this example, the word “the band” in the second sentence refers to the band “The Transformers” introduced in the first sentence. When you read about the band in the second sentence, you know that it is referencing to the “The Transformers” band. This is really important for translation because there are so many cases in which words in some sentences refer to words in previous sentences.

For translating sentences like that, a model has to be able to capture those connections. 
Recurrent Neural Networks (RNNs) and Convolutional Neural Networks (CNNs) have been used to deal with this problem because of their properties. 

### Recurrent Neural Networks
Recurrent Neural Networks involve loops within the network allowing information to persist. Each word in a text represent an input for the network,
and each network passes the information of the previous words to the next network	that can use and process that information.

##### The problem of long-term dependencies
Consider a language model that is trying to predict the next word based on the previous ones. If we are trying to predict the next word of the sentence “the clouds in the (sky)”, we don’t need further context because
 it is pretty obvious that the next word is going to be sky.

But there are cases where we need more context. For example, let’s say that you are trying to predict the last word of the text: 
“I grew up in France. I speak fluent (-)”. Recent information (I speak fluent) suggests that the next word is probably a language,
but if we want to narrow down which language, we need context of France, which is in the previous sentence. We need a language model that is able to capture those dependencies/connections.

RNNs become very ineffective when the gap between the relevant information and the point where it is needed become very large. 
Because since the information is passed at each step, the longer the chain is the more probable the information is lost along the chain.

In theory, RNNs could learn this long-term dependencies. In practice, they don’t seem to learn them. LSTM, a special type of RNN, tries to solve this kind of problem

Let’s suppose we have an agenda full of appointments. What we usually do is to prioritise the appointments we think are more important and cancel the others. 
A Neural Network should do the same when looks at an input text and needs to decide which words should focus on.
Unfortunately, RNNs don’t do that : whenever it adds new information, it transforms existing information completely by applying a function. The entire information is modified, 
and there is no consideration of what is important and what is not.

This problem is overcome by Long short term memory LSTM.

### Long-Short Term Memory (LSTM)
LSTMs make small modifications to the information by multiplications and additions. With LSTMs, the information flows through a mechanism known as cell states. 
In this way, LSTMs can selectively remember or forget things that are important and not so important.

Each cell takes as inputs x_t 
- A word in the case of a sentence to sentence translation
- The previous cell state
- Output of the previous cell. It manipulates these inputs and based on them, it generates a new cell state, and an output
With a cell state, the information in a sentence that is important for translating a word may be passed from one word to another, when translating.

The problem with LSTMs
The same problem that happens to RNNs generally, happen with LSTMs, i.e. when sentences are too long LSTMs still don’t do too well. 
The reason for that is that the probability of keeping the context from a word that is far away from the current word being processed decreases exponentially with the distance from it.
That means that when sentences are long, the model often forgets the content of distant positions in the sequence.

One big problem of LSTMs and RNNs is: Distance between positions is linear


Reference including images/diagrams: https://towardsdatascience.com/transformers-141e32e69591
Word embedding - word2vec: https://medium.com/deeper-learning/glossary-of-deep-learning-word-embedding-f90c3cec34ca
