## Background On Embeddings
In a number of Natural Language Processing (NLP) applications classic methods for language modeling that represent words as high-dimensional, sparse vectors have been replaced by Neural Language models that learn word embeddings, i.e. low-dimensional representations of words, through the use of neural networks. The networks are trained by directly taking into account the word order and their co-occurrence, based on the assumption that words frequently appearing together in the sentences also share more statistical dependence. With the development of highly scalable continuous bag-of-words and Skip-gram language models for word representation learning, the embedding models have been shown to obtain state-of-the-art performance on many traditional language tasks after training on large text data.
More recently, the concept of embeddings has been extended beyond word representations to other applications outside of NLP domain. Researchers from the Web Search, E-commerce and Marketplace domains have realized that just like one can train word embeddings by treating a sequence of words in a sentence as context, the same can be done for training embeddings of user actions by treating sequence of user actions as context. Examples include learning representations of items that were clicked or purchased or queries and ads that were clicked. These embeddings have subsequently been leveraged for a variety of recommendations on the Web.

## application
**YMN** for recommendation
1. [airbnb listing recommendation](https://medium.com/airbnb-engineering/listing-embeddings-for-similar-listing-recommendations-and-real-time-personalization-in-search-601172f7603e)
Real time personalization in Search using Embeddings:
- show to the guest more listings that are similar to the ones we think they liked since starting the search session
- ewer listings similar to the ones we think they did not like.
To achieve this, for each user we collect and maintain in real-time (using Kafka) two sets of short-term history events:

Hc : set of listing ids that user clicked in last 2 weeks.
Hs : set of listing ids that user skipped in last 2 weeks, where we define skipped listings as ones that were ranked high but skipped by user in favor of a click on a lower positioned listing

## papers
[E-commerce in Your Inbox: Product Recommendations at Scale](https://arxiv.org/pdf/1606.07154.pdf)
[Scalable Semantic Matching of Queries to Ads
in Sponsored Search Advertising](https://arxiv.org/pdf/1607.01869.pdf)
[Distributed Representations ofWords and Phrases
and their Compositionality](https://papers.nips.cc/paper/5021-distributed-representations-of-words-and-phrases-and-their-compositionality.pdf)

