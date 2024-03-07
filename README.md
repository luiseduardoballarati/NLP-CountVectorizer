# NLP-CountVectorizer
Machine Learning simple model to classify documents based on the content using NLP algorithm Count Vectorizer. The labels are "business", "entertainment", "politics", "sports" and "tech".

# How it works

The Count Vectorizer approach is one of the simplest algorithms there is for NLP. It basically counts the number of appearances each word has on a document and creates a sparse matrix (similar to a regular matrix but has better performance for null values), where the columns are the words (our vocabulary size) and the rows are the documents. Documents are any piece of text. So, say for example we want to organize the documents in our company between AI documents and Software Engineering ones. Words like "Software", "Engineering", "Design Patterns", "Tests" and so on may be more common in SE documents and words like "Machine Learning", "AI", "Deep Learning", may be more common in AI documents. Being so, the matrix will be populated differently for documents of different labels and, next time a new document comes to be analyzed, if it contains more words that relates to AI documents, it will be classified as an AI document and vice versa.

A simple example:

Doc1: I like AI. 
Doc2: I have two Machine Learning Models.
Doc3: I love sofware engineering and programming.
Doc4: I hate design patterns.

Vocabulary size (V): I [1], like [2], AI [3], have [4], two [5], Machine [6], Learning [7], Models [8], love [9], sofware [10], engineering [11], and [12]...

Sparse Matrix:

 docs/words   |       I       |      Like     |    AI      |    have    |    two    |...
              | ------------- | ------------- |------------| -----------| ----------|
 doc1         |      1        |       1       |     1      |     0      |      0    |
 doc2         |      1        |       0       |     0      |     1      |      1    | 
...

How does counting the words help? Given a new document, count up #AI and #Software, for example, plot it on a graph and determine which side of the line the vector falls on (the AI or the SE)!


Count Vectorizer does not take the order of the words in consideration, so it is said to be a "bag of words" approach. Another important note is that Count Vectorizer ignores punctuation.

# Some helpfull tips when using Count Vectorizer

- Normalization: if our corpus (dataset) has very short and very large documents the vectors will have big size disparities (more words = higher counts). Count Vectorizer does not implement Normalization, but we can do it by hand, using either L2-norm 1 or simply dividing each word by the sum of all words in the document.
- Casing: use the hyper parameter "lowercase=True" to convert all the words in the documents to lowercase and therefore "AI" and "ai" will have the same token and will be the same word.
- Accents: Use the hyper parameter "strip_accents=True" to ignore accents and treat words like "programação" and "programaçao" as the same!
- Stopwords: words like "and", "or", "it", "Is", "the" are very common in almost every document and are not useful as they do not bring any special information about the document. Recall that our understanding of feature vectors involves their distance to each other and if we count all the "and"s, "the"s... the vectors ehich will be close will simply be the ones with similar number of these words! They might overshadow more important words, like "AI" or "software". Thus, stopwords are the words we wish to ignore. In addition, the more words we have in our matrix,, the higher the dimensionality of the vector, which increases the computation. To avoid that, we can use the hyper parameter "stop_words='english'", or create the list ourselves and pass it as a parameter.

  # Stemming and Lemmatization

With basic word tokenization, each variation of a word will have its own vector compnent: "walk", "walking", "walked", "walks"... And "walk" is no closer to "walking" than it is to "car" (unless similarity can be learned from the data).

This also leads to high-dimensional vectors.

The solution for that is converting words to their root word and we are going to discuss two methods for that: Stemming and Lemmatization.

- Stemming is very crude and it just chops off the end og the word: the result is not necessarily a real word.
- Lemmatization is more sophisticated and uses actual rules of language to return the true root.


# Vector Similarity

Vector Similarity is basically a function that takes as input 2 vectors and outputs a single number which tell us how similar those 2 vectors are. It’s like a score.
This is important because we can match similar documents using this, for example. We can also do that with words, for example, making “king” and “queen” being similar, “car” and “automobile”… 

When 2 vectors are close together in distance, they are similar. When they are far, they are dissimilar. And to calculate this distance we can use Euclidian Distance and the Coisine Distance, that it is not the excact distance between the vectors, but more like a metric. In other words, the cosine distance is not a true distance metric as it does not satisfy the triangle inequality. Basically, it just states that if the cosine of the angle is close to 0, it means that the points are parallel and the distance close to 0 as well. If the points are far from each other, close to 180°, the cosine is close to -1 and therefore the distance between the points is close to -2. This metric is more used in NLP.

