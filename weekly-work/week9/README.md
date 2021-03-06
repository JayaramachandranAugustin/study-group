# Session IX: Word Vectors, AI *x* Fashion, and U-Net

*Meeting date: March 6th, 2017*

This session marked the beginning of our coverage of Stanford's [CS224d](https://cs224d.stanford.edu/) course, which is taught by [Richard Socher](http://www.socher.org/) and focuses on Deep Learning applied to Natural Language Processing. 

In addition, we enjoyed fascinating technical talks from: 

1. **[Jessica Graves](https://sefleuria.tumblr.com/)**  on AI applications in the fashion industry, and 
2. **[Grant Beyleveld](https://grantbeyleveld.wordpress.com/)** on his implementation of the [U-Net](https://arxiv.org/abs/1505.04597) Convolutional Networks for object recognition in images (slides [here](https://github.com/the-deep-learners/study-group/blob/master/slides/2017-03-06__grant_beyleveld__u_net.pdf))

A summary blog post, replete with photos of the session, can be found [here](https://insights.untapt.com/deep-learning-study-group-ix-natural-language-processing-ai-in-fashion-and-u-net-1a4726037806). 


## Recommended Preparatory Work

The recommended preparatory work for Session IX was the first three lectures of CS224d, each of which is 75-80 minutes: 

1. the [course introduction](http://viewpure.com/Qy0oEkCZkBI?start=0&end=0)
1. [on Word Vectors](http://viewpure.com/aRqn8t1hLxs?start=0&end=0), and
1. [more on Word Vectors](http://viewpure.com/CP9bIt4IPVo?start=0&end=0)

## Summary


Topic highlights of the session included: 


#### From Lecture 1 (Course Intro, NLP, Deep NLP)

##### Recommended prerequisites

* proficiency in Python
* college-level calculus and linear algebra
* understanding of the fundamentals of probability and statistics
* knowledge of machine learning (i.e., equivalent of Stanford CS229), e.g.:
	* cost functions
	* simple derivatives
	* how to optimise with gradient descent
	
##### NLP Levels

1. phonetic/phonological analysis (if starting with speech) or OCR (optical character recognition)/tokenization (if starting with text)
2. morphological analysis
3. syntactic analysis
4. semantic interpretation
5. discourse processing

Phonetic/phonological analysis (in level 1), level 3, and level 4 are covered in this course.

##### NLP Applications

* simple:
	* spell checking
	* keyword search
	* finding synonyms
* moderate:
	* extracting information from websites, e.g.:
		* product price
		* dates
		* location
		* people or company names
	* classifying
	* school-grade reading level
	* sentiment of longer documents
* complex:
	* machine translation
	* spoken-dialog systems
	* answering of non-straightforward questions
	
##### Examples of NLP in Industry

* search
	* written
	* spoken
* digital advertising
* language translation
	* automated
	* assisted
* sentiment analysis
	* marketing
	* finance/trading
* speech recognition
* automation of customer support

##### Why NLP is Challenging

* the representation, learning, and use of linguistic, situational, world, or visual information is complex
* examples:
	* *she* in this example is dependent on the associated verb:
		* "Jane hit June and then *she* [fell / ran]."
	* the ambiguity of words: "I made her *duck*."
	
##### "Deep Learning"

* it is a subfield of *machine learning*
	* ML works well because of **human-designed** representations and input feature
		* e.g.: the features for *named entity recognition* (locations, organisation names, etc.; Finkel, 2010)
	* ML becomes a weight-optimisation problem to make the best final prediction
		* ~80% of time: describing the data with features a computer can understand requires domain-specific knowledge, typically Ph.D.-level talent
		* ~20% of time: optimising weights on features
* in contrast, *deep learning*: 
	* *representation learning* attempts to automatically learn useful features or representations
	* algorithms attempt to learn (multiple levels of) representation and an output
	* modelling directly on *raw* inputs (e.g., words)

##### The History and Etymology of "Deep Learning"

* CS224d focuses on various families of *artificial neural networks*
	* (A)NNs are the dominant model family inside deep learning
* is DL simply stacked logistic regression units? 
	* to an extent, however the end-to-end (e.g., text input-to-probability output) modelling principles distinguish it; there are connections to biological neuroscience in some cases
* CS224d does *not* take a historical approach, instead focusing on leading contemporary methods for NLP problems
	* the history of Deep Learning models (i.e., since the ~1960s) is well-covered by Jürgen Schmidhuber (2015) ["Deep Learning in Neural Networks: An Overview"](https://arxiv.org/abs/1404.7828)

##### Reasons for Exploring Deep Learning

* manually-designed features are often:
	* over-specified
	* incomplete
	* take a long time to design, validate
* in contrast, *learned features* are:
	* easy to adapt
	* fast to learn
* therefore, deep learning provides a framework for representing (e.g., linguistic, visual, world) information that is:
	* flexible
	* universal
	* learnable
* deep learning is useful for both:
	* *unsupervised learning* (e.g., with raw text alone)
	* *supervised learning* (e.g., with labelled data like positive or negative sentiment)

##### Deep Learning for Speech

* first large data set DL breakthrough happened in speech recognition
	* the University of Toronto's Dahl et al. (2012) ["Context-Dependent Pre-Trained Deep Neural Networks for Large-Vocabulary Speech Recognition"](http://ieeexplore.ieee.org/document/5740583/)
	
##### Deep Learning for Machine Vision

* until 2014, the bulk of deep-learning research groups focused on machine vision, which was the second application of DL after speech recognition
	* i.e., AlexNet (Krizhevsky et al., 2012, ["ImageNet Classification with Deep Convolutional Neural Networks"](https://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks))
	
##### Deep NLP = [Deep Learning] + NLP

* this approach combines the ideas and goals of NLP, then applies representation learning and deep learning methods to solve them
* in recent years, this approach has facilitated large strides across broad aspects of NLP, e.g.:
	* *levels*: 
		* speech
		* morphology
		* syntax
		* semantics
	* *applications*: 
		* machine translation
		* sentiment analysis
		* question answering
		
##### Representations at NLP Levels

###### Phonology

* traditional: phonemes
* DL: train model to predict phonemes (or words, directly) from sound features and represent them as *vectors*

###### Morphology

* traditional: morphemes (e.g.: "un-"(prefix), "-interest-"(stem), "-ed"(suffix))
* DL:
	* every morpheme is a vector
	* neural network combines two vectors into one vector
	* neural word vectors can be visualised in two-dimensional space
	* e.g., Thang, Socher & Manning, 2013, ["Better Word Representation with Recursive Neural Networks for Morphology"](https://nlp.stanford.edu/~lmthang/data/papers/conll13_morpho.pdf)

###### Syntax

* traditional: phrases, in discrete categories like NP or VP
* DL: 
	* every word and ever phrase is a vector
	* a neural network combines two vectors into one vector
	* e.g., [Socher, Lin, Ng & Manning, 2011](http://ai.stanford.edu/~ang/papers/icml11-ParsingWithRecursiveNeuralNetworks.pdf)
	
###### Semantics

* traditional: 
	* lambda calculus
		* carefully-engineered functions
		* takes specific other functions as inputs
		* no notion of similarity or fuzziness of language
* DL:
	* vectors represent every:
		* word
		* phrase
		* logical expression
	* again, neural network combines two vectors into one vector
	* e.g., [Bowman, Angeli, Potts & Manning, 2014](https://nlp.stanford.edu/pubs/snli_paper.pdf)

##### NLP Applications

###### Sentiment Analysis

* traditional: curated sentiment dictionaries combined with either:
	* bag-of-words representations (i.e., ignoring word order)
	* hand-designed engation features (this doesn't capture "everything")
* DL: one RNN model used simultaneously for:
	* morphology
	* syntax
	* logical semantics
	
###### Question Answering

* common: a lot of feature engineering to capture world and other knowledge, e.g., regular expressions ([Berant et al., 2014](http://www.aclweb.org/anthology/D/D14/D14-1159v2.pdf))
* DL: Can use same model as in **morphology** section above
	* stores in vectors:
		* morphology
		* syntax
		* logical semantics
		* sentiment
		
###### Machine Translation

* traditional:
	* many levels of translation have been tried in the past
	* were very large complex systems
* DL: vectors!

##### Metamind

* Socher's start-up
* acquired by Salesforce
* performs:
	* sentiment analysis	
	* named-entity recognition
	* part-of-speech tagging
	* answers synthetic questions (**whoa!**)
		* even if it requires multiple passes to understand meaning (**wow wow wow**)
	* machine translation
	* leverages ConvNet to label images


#### From Lecture 2 (Word Vectors)

##### Discrete Representations of Meaning

* traditional: 
	* use a taxonomy like WordNet that has:
		* hypernyms ("is-a") relationships and synonym sets
	* problems with this discrete reprentation:
		* great as a resource by misses nuances, e.g., of synonyms (these are not binary but gradual)
		* does not include new words
		* subjective
		* requires human time to create and to adapt
		* not straightforward to compute accuracy of word similarity
		* nearly all rule-based and statistical NLP work regards words as atomic symbols, creating massive one-hot representation vectors:
			* speech: 20k
			* PTB (Penn Treebank 3): 50k
			* big vocabulary: 500k
			* Google 1TB corpus: 13 million
		* with one-hot, similar words are not encoded differently from unrelated ones
		
##### Distributional Similarity-Based Representations

* "You shall know a word by the company it keeps" (JR Firth, 1957, 11)
* there is great value in representing a word by the means of its neighbours

###### Window-Based Co-Occurrence Matrix

* symmetric windows (left or right context is equivalent), with lengths of five to ten are common

###### Low Dimensional Vectors

* store *most* of the important information in:
	* **dense vector**: fixed, small number of dimensions
		* typically 25-100 dimensions
* dimensionality-reduction methods:
	1. **singular value decomposition** of co-occurrence matrix *X*
		* hacks to *X*:
			* function words (the, he, has) are too frequent
				* ...therefore, syntax has too much impact
				* solutions:
					* min(*X*, *t*), with *t*~100
					* ignore them all
			* ramped windows that count closer words more
			* Pearson correlations instead of counts, with negative values floor at zero
			* and more
		* problems with SVD:
			* computational cost scales quadratically for *n*-by-*m* matrix
				* impractical to fit millions of words or documents
			* challenging to incorporate new words or documents
			* the learning regime is different relative to DL models
	1. directly learn low-dimensional word vectors
		* an old idea
			* learn representations by backpropagating errors ([Rumelhart, Hinton & Williams, 1986](http://www.nature.com/nature/journal/v323/n6088/abs/323533a0.html))
			* a neural probabilistic language model ([Bengio et al., 2003](http://www.jmlr.org/papers/volume3/bengio03a/bengio03a.pdf))
			* NLP ("almost") from scratch ([Collobert & Weston, 2008](https://ronan.collobert.com/pub/matos/2008_nlp_icml.pdf))
			* **word2vec** ([Mikolov et al. 2013](https://papers.nips.cc/paper/5021-distributed-representations-of-words-and-phrases-and-their-compositionality.pdf))
				* recent
				* simpler
				* faster
				
##### Word2Vec

* predict surrounding words in a window of length *m* of every word in corpus
* *objective function*: maximise the log-probability of any context word given the current center word
* every word has *two* vectors
* essentially "dynamic logistic regression"
* analogies
	* linear relationships between vectors efficiently encode dimensions of similarity
	* analogies testing dimensions of similarity can be solved quite well by doing vector subtraction in the embedding space 
	* e.g.:
		* syntactically:
			* *x_apple - x_apples*  ~=  *x_car - x_cars*  ~=  *x_family - x_families*
		* semantically (i.e., for verb and adjective morphological forms; [SemEval-2012 Task 2](https://sites.google.com/site/semeval2012task2/)):
		* *x_shirt - x_clothing*  ~=  *x_chair - x_furniture* 
		* *x_king - x_man*  ~=  *x_queen - x_woman* 

##### Count-Based vs Direct Prediction

* Richard Socher's table summarises the traditional (count-based) and contemporary (DL) NLP approaches with respect to:
	* techniques
	* key papers
	* pros and cons

![Socher slide](https://github.com/the-deep-learners/study-group/blob/master/weekly-work/week9/02_pros_and_cons_of_counting_vs_w2v.png)


#### From Lecture 3 (More on Word Vectors)

##### Stochastic Gradient Descent

* with a large corpus (e.g., Google 1TB corpus):
	* you could have 40B tokens and windows
	* you would not have enough memory for a single update with gradient descent, or you'd have to wait a very long time
	* ergo, gradient descent is not an optimal solution for (probably) all neural nets
	* *stochastic* gradient descent:
		* the solution!
		* update model parameters after each window *t*
		
##### GloVe

* enables fast training *and* scales to huge corpora
* nevertheless has good performance even with a small corpus and/or small vectors

##### Two Sets of Vectors

* we have *U* and *V* from all vectors *u* and *v*
	* both capture similar co-occurrence information
	* best solution is to sum them, i.e., *X_final = U + V*
	* one of many hyperparameters explored in [Pennington, Socher, & Manning (2014)](https://nlp.stanford.edu/pubs/glove.pdf)
	
##### Evaluating the Quality of Word Vectors

* intrinsic:
	* evaluation on a specific/intermediate subtask
	* fast to compute
	* helps to understand that system
	* not clear if really helpful unless correlation to real task is established
* extrinsic:
	* evaluation on a *real* task
	* can take a long time to compute accuracy
	* doesn't clarify whether subsystem is the problem or its interaction with other subsystems
	* progress is made if replacing one subsystem with another improves accuracy
	* e.g., named-entity recognition
	* **extrinsic evaluations are the focus of CS224d**
	
##### Visualisations of GloVe Vectors

###### Gender

![gender](https://github.com/the-deep-learners/study-group/blob/master/weekly-work/week9/03_05_GloVe_visualizations_gender.png)

###### Corporate CEOs

![CEOs](https://github.com/the-deep-learners/study-group/blob/master/weekly-work/week9/03_06_GloVe_visualizations_CEO.png)

###### Superlatives

![superlatives](https://github.com/the-deep-learners/study-group/blob/master/weekly-work/week9/03_07_GloVe_visualizations_superlatives.png)

##### Analogy Evaluation and Hyperparameters

* improve accuracy by:
	* increasing dimensionality of vector space up to ~300 
	* window size of *eight* around each center word suits GloVe vectors well
	* asymmetric context (e.g., only words to the left) underperforms symmetric context
* more training time (i.e., iterations) improves accuracy
* more data improves accuracy(e.g., [Common Crawl with 42B tokens] > [Wikipedia with 1.6B tokens])
* N.B.: better results could potentially be obtained on downstream tasks with different hyperparameters

##### Resolving Ambiguity

* [Huang, Socher, Manning & Ng (2014)](https://open.spotify.com/track/7hndTIGqgv9od4XdhkkJoZ) makes strides toward resolving word ambiguity (i.e., having the same word in multiple locations of vector space)


## Up Next

1. the next three lectures of the course, which cover the use of neural networks to learn word-vector features
