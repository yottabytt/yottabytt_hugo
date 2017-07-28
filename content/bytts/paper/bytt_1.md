+++
title = "Paper Bytt #1 - Identifying Multiple Topics in Texts"
date = "2017-07-07"
tags = ["text classification", "text similarity"]
+++

{{% paperlink src="Identifying_Multiple_Topics_in_Texts.pdf" text="Here" %}}
is the link to the actual paper.

#### Good to know

Lucene, Item-Based Collaborative Filtering, Document Similarity, \
Multi-label text classification.

#### Gist
Multiple topics are assigned to a document based on the topics of similar
documents present in the corpus. The paper explains about various different
approaches in the process of finding similar documents and in the selection of
appropriate topics from the similar documents and assigning them to the input
document.

#### Brief Summary

There are three methods which are discussed in the paper. They are,

1. _A discriminative algorithm using Lucene._

    {{% spaces "4" %}}In this method, for every document in the training set,
    the text and its labelled multiple topics are indexed into Lucene as
    documents with two seperate fields namely _text_ and _topics_. Now, for a
    given input document, similar documents are found from the Lucene index
    using appropriate search query. The resulting documents have a similarity
    score associated with them. Following steps are done to assign the topics to
    the input document,

    * As there is a _topics_ field in each document in the result, the similarity score of the documents are applied to the topics it contain.
    * Now, all the topics in the _topics_ field of all the resulting documents have a score tied to them.
    * Same topics may be present in more than one resulting document, so their scores are added. For example, consider the result contains three documents Doc 1, 2 and 3. Doc 1 has a _topics_ field with values P, Q, R and Doc 2 has _topics_ field with values Q, R and Doc 3 has _topics_ field with values P,S.

        > Now finally we have four different topics P,Q,R,S with different scores.

        > Score(P) = Score(Doc 1) + Score(Doc 3)\
        > Score(Q) = Score(Doc 1) + Score(Doc 2)\
        > Score\(R) = Score(Doc 1) + Score(Doc 2)\
        > Score(S) = Score(Doc 3)

    * Topics are sorted based on their scores and the top-n are chosen and are assingned to the input document.




2. _An adaption of item-based recommendation algorithm on top of Lucene results._

    {{% spaces "4" %}} The process of finding similar documents is the same as the previous method. But, instead of considering all the topics in the resulting documents, they chose half of the best topics and apply an adaptation of item-based recommendation algorithm. Sadly, there is not enough details which explains the recommendation algorithm per se. It is just said that, for every topic in the chosen best topics, the recommendation algorithm returns the topic which has the highest probability of occuring with that topic. By this way, the rest half of the topics are found. However,
    * The basis for the recommendation algorithm is the metric which is the number of co-occurences of two topics among all the documents, i.e., If there are two topics topicX and topicY, the number of co-occurences (NCo) of topicX and topicY is the number of documents which has both topicX and topicY.
    * So with that, we can form a topic-topic matrix with NCo as the cell values.
    * Then we can find the closeness between two topics by comparing their NCo vectors in the topics space, by using any of the similarity measures like the cosine similarity.
    * Finally, we would get a topic-topic matrix with similarity scores as the cell values from which the highly correlating topic for any topic is chosen.

3. _A Noun-Phrase based approach._

    {{% spaces "4" %}} In the earlier methods, the text per se was indexed into Lucene. In this method, instead of the complete text, only the Noun Phrases (NP) are indexed. It is a two step process,

    * First, for every document, NPs are extracted and the topics associated with the document are assigned to the NPs. Now, for all the NPs present in all the documents across the corpus, there would be one to many topics associated to it.
    * Second, an intersection of topics for every distinctive NPs is found out, and the intersection set is assigned to the NPs. Now, all of them, the NPs and the associated topics are indexed into Lucene.

        > * Consider, for example two documents, doc1 and doc2\
        > * doc1 has NPs X,Y and doc2 has NPs X,Y,Z\
        > * doc1 has topics topic1, topic2 and doc2 has topic1, topic3\
        > * Now across the corpus, we have NP X associated to topic1 and topic2 in one document and to topic 1 and topic 3 in the other.\
        > * Finally, X is associated with the intersection of \
        {topic1, topic2} and {topic1, topic3} which is topic1. Similarly,
        Y = {topic1} and Z = {topic1, topic3}

    Now, as the index is ready, for a given input document, NPs are extracted and similar NPs are searched for in the Lucene index and their topics are attributed to the input document.






#### Result Claims
* Noun-Phrase based approach seems to perform better than the other two with all Precision, Recall and F-Scores of this approach edging others approximately by 0.5 to 0.10

#### Unclear Areas
* No details about the exact working of the recommendation algorithm.


#### Limitations
* Human Labeling of the documents with topics.
