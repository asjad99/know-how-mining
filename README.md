# know-how-mining

Most data mining techniques focus on extracting declarative knowledge, which describes objects and events by specifying the properties which characterize them; it does not pay attention to extract the actions needed to obtain a result, but only on its properties ‘Many knowledge bases such as Wikipedia or Wikidata that have been widely utilized contain a huge amount of descriptive knowledge.  Procedural knowledge [2, 18], also known as know-how, is the knowledge exercised in the accomplishment of a task, i.e. how to do things, which is usually acquired by experience and considered tacit and not easily shared, compared to descriptive knowledge.  However, shared explicit procedural knowledge lays a foundation for efficiently coordinated action, which is often referred to as best practices or business rules within communities or organizations.’


After the model has been trained, every word in the training corpus has been
assigned a unique vector. But this assigned isn’t random. If we visualize
the vectors in space using something likeT-SNE we’ll find out that words
that are semantically similar have been projected nearby(are close to each
other). 

"Vector space models (VSMs) represent (embed) words in a continuous vector space where semantically similar words are mapped to nearby points ('are embedded nearby each other'). VSMs have a long, rich history in NLP, but all methods depend in some way or another on theDistributional Hypothesis, which states that words that appear in the same contexts share semantic meaning. The different approaches that leverage this principle can be divided into two categories: count-based methods (e.g. Latent Semantic Analysis), and predictive methods (e.g.neural probabilistic language models)." 

After training the model(or loading a pretrained one), we can input a
certain word and the model will give us back its vector(which is a 300
dimensional 1d array in this case)
>
>  model.wv['computer']  # numpy vector of a word
> array([-0.00449447, -0.00310097,  0.02421786, ...], dtype=float32)

>     3.  Further gensim provides us with various functions that can be used
> to query the model. so for example we can find out the semantic similarity
> between two words.

>>>> model.wv.similarity('woman', 'man')
> 0.73723527

0.73 shows the similarity score(usually the score is based on the cosine of
the angle between their vectors).

computing similarity between phrases is slightly harder using word2vec,as in
its not designed to handle phrases(there is doc2vec for that..), but there
are hacks that can get us decent results. i found a script on the internet
that computes an average vector of a given phrase and then we can do the
same for the second phrase and then compare the two in a similar fashion.

e.g

Type the phrase1: i bake food
Type the phrase2: i bake food
###############################################################
Similarity Score:  1.0
###############################################################
Type the phrase1: make cake batter
Type the phrase2: make cake mix
###############################################################
Similarity Score:  0.730352

Type the phrase1: Human machine interface for lab abc computer applications
Type the phrase2: Human computer interaction
###############################################################
Similarity Score:  0.676366

The above result is remarkable in a sense that our model has learned in an
unsupervised way that 'human machine interface' phrase is semantically very
close to the second phrase and that there is nothing common between 'pigs
fly' and me liking cricket.

 Type the phrase1: i like cricket
 Type the phrase2: pigs fly
 ###############################################################
Similarity Score:  0.146697
 ###############################################################

The score of the first result could have been better if we used some other
training corpus. so we can say that there is a limitation that comes with
the kind of training corpus we use... for example our model might not know
 much about the vocabulary/jargon used in software domain. e.g


----------
