## Background On Embeddings
In a number of Natural Language Processing (NLP) applications classic methods for language modeling that represent words as high-dimensional, sparse vectors have been replaced by Neural Language models that learn word embeddings, i.e. low-dimensional representations of words, through the use of neural networks. The networks are trained by directly taking into account the word order and their co-occurrence, based on the assumption that words frequently appearing together in the sentences also share more statistical dependence. With the development of highly scalable continuous bag-of-words and Skip-gram language models for word representation learning, the embedding models have been shown to obtain state-of-the-art performance on many traditional language tasks after training on large text data.
More recently, the concept of embeddings has been extended beyond word representations to other applications outside of NLP domain. Researchers from the Web Search, E-commerce and Marketplace domains have realized that just like one can train word embeddings by treating a sequence of words in a sentence as context, the same can be done for training embeddings of user actions by treating sequence of user actions as context. Examples include learning representations of items that were clicked or purchased or queries and ads that were clicked. These embeddings have subsequently been leveraged for a variety of recommendations on the Web.

## application
[airbnb listing recommendation](https://medium.com/airbnb-engineering/listing-embeddings-for-similar-listing-recommendations-and-real-time-personalization-in-search-601172f7603e)

## papers
[E-commerce in Your Inbox: Product Recommendations at Scale](https://arxiv.org/pdf/1606.07154.pdf)
[Scalable Semantic Matching of Queries to Ads
in Sponsored Search Advertising](https://arxiv.org/pdf/1607.01869.pdf)

