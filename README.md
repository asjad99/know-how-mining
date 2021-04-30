## About: 

Goal models play an important role by providing a hierarchic representation of stakeholder intent, and by providing a representation of lower-level subgoals that must be achieved to enable the achievement of higher-level goals. A goal model can be viewed as a composition of a number of goal refinement patterns that relate parent goals to subgoals. In this paper, we offer a means for mining these patterns from enterprise event logs and a technique to leverage vector representations of words and phrases to compose these patterns to obtain complete goal models. The resulting machinery can be quiote powerful in its ability to mine know-how or constitutive norms. We offer an empirical evaluation using both real-life and synthetic datasets.

## Approach(text-similatity): 

Most modern methods in statistical NLP are built on the idea of distributional hypothesis which states that any two words will share same semantic meaning if they appear in the same context. Two popular approaches that leverage this principle are count-based methods such as Latent Semantic Analysis and predictive methods. e.g neural probabilistic language models. Predictive models try to directly predict a word(e.g ‘mat’) from its context words(e.g “the cat sits on the”). The words are represented as fixed n-dimensional dense vectors and can be considered as parameters of the model. Word2vec proposed by Mikolov et al. 2013 is a computationally-efficient predictive model for learning word embeddings(vector representation of words) using which we can, from a given raw text corpus, learn a representation which encodes syntactic as well semantic relationships between words. If we visualize the learned vectors it is clear that semantically similar words are in fact projected close to each other in vector space.  

see paper for more details: 

> Santiputri, Metta, et al. "Mining goal refinement patterns: distilling know-how from data." International Conference on Conceptual Modeling. Springer, Cham, 2017.


### Evaluation:  

For evaluation we rely on Google’s pre-trained word2vec model which they have publicly made available[2]. It includes word vectors for a vocabulary of 3 million words and phrases that has been trained on approximately 100 billion words from a Google News dataset.  

 

We ran our program on a large amazon EC2 instance with 16GB RAM using 64-Bit Python. For querying the model, our program first loads the 3.6 GB pre-trained model in memory using the word2vec module of the Gensim Library[1]. Then given two input phrases it computes the average vector for both and calculates the cosine similarity between the two phrase vectors. Common English words(stop words) are removed during the similarity calculation.  

 

## Results: 
| Sub-Goal Text                                                   | Sub-Goal (Alternative Text)                                                  | Similarity Score |
| --------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------- |
| create new customer service ticket                              | open new repair issue for the customer                                       | 0.623894         |
| Print repair receipt for the customer                           | Print customer service repair order                                          | 0.863028         |
| Send out courtesy product check-in confirmation email           | Email repair order confirmation                                              | 0.742585         |
| perform a series of standard diagnostic tests to identify fault | troubleshoot the problem by following a step-by-step testing methodology     | 0.635703         |
| Assign a label to the issue after defect assessment             | specify fault type by adding a tag to the issue after diagnosing the problem | 0.637491         |
| Seek Customer approval for complex repairs                      | Ask permission from customer if a part replacement is required               | 0.640503         |
| Order replacement parts if repair type is complex               | Send out replacement request for new components                              | 0.645564         |
| log labor hours for billing                                     | Track technician time for charging the customer                              | 0.469291         |
| Change issue status to ‘fixed’                                  | update issue status to ‘ready to review’                                     | 0.819758         |

