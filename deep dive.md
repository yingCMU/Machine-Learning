# feature engineering
1. derived features
    1. Given the user’s short-term search history, we can infer useful information that can help us personalize future searches: 
    2. Time of Day Fit between the user’s time-of-day percentages and the Experience’s time of day,
    3.  intensity and recency of that Experience category.

# feature bank
example | feature
---|---
spam email |frequency of the word 'Buy' and 'Money'

- spam email
  - frequency of the word 'Buy' and 'Money'
  - ^ as part of a feature if you would combine it with more words.
- whether one is a friend of yours
  - the amount of 'common' friends 
- Airbnb experience ranking
    - personalization based on booked Airbnb Homes
        - Home location
        - Trip dates
        - Trip length
        - Number of guests
        - Trip price (Below/Above Market)
        - Type of trip: Family, Business
        - First trip or returning to location
        - Domestic / International trip
Lead days   

# model selection
- **what**: choose between models with different degress of flexibility. example of model selection is to choose K for a KNN classifier
- **Techniques**:
    - cross validation   
- online and offline training: The idea behind online training is that you add training data to an already existing model, whereas with offline training you generate a new model from scratch. For performance reasons, online training would be the most preferable method. However for some algorithms this is not possible.
- tbd
- 



# validation techniques
Validation set is used for selecting the model complexity. We fit all the models on the training set, and evaluate their performance on the validation set, and pick the best. Once we have picked the best, we can refit it to all the available data. 

1. 80-20% weakness: if training data is small, it will run into problems because it won't have enough data to train on, and we won't have enough data to make a reliable estimate of the future performance. 
1. cross validation: 
    1. **what**: Its essence is to ignore part of your dataset while training your model, and then using the model to predict this ignored data. Comparing the predictions to the actual value then gives an indication of the performance of your model, and the quality of your training data.The most important part of this cross validation is the splitting of data. You should always use the complete dataset when performing this technique. In other words you should not randomly select X datapoints for training and then randomly select X datapoints for testing, because then some datapoints can be in both sets while others might not be used at all.
        2. split data into K folds (usually 5-fold CV). 
        3. For each fold, train on all the fold but k, and test on the k'th fold, in a round-robin fashion. 
        4. compute the error averaged over all the folds, and use this as a proxy for the test error. 
    2. **strenght**: each point gets predicted only once, used for training K-1 times


# common pitfalls
- Golden rule: (I think he means never use test data to tune model directly but use it as measurment to decide on model)Never use test dataset for model fitting or model selection, this will lead to unrealistically optimistic estimate of performance. Test dataset is only to report performance of model. then what should be used?
overfitting
underfitting
not taking into account how the model handles extrapolation and interpolation: 
- offline training limitation:
offline testing often has too many assumptions, e.g. in our case it was limited to re-ranking what users clicked and not the entire inventory, we conducted an online experiment, i.e. A/B test, as our next step. We compared the Stage 1 ML model to the rule-based random ranking in terms of number of bookings.
- mismatch of test and test distribution
e.g. training set is from cat pictures from webpages, but test set is cat picture from user upload on mobile. The resolution is different. They are from different distribution
make sure data sets are from the same distribution

# workflow
### For shared entities(like Airbnb experience ranking):
1. simple baseline model(usually with limited training data): it can simply the same ranking model and even same ranking result for all users. This also makes the implementation super simple. How much this can improve?
2. personalization: The next step in our Search Ranking development was to add the Personalization capability to our ML ranking model. why it is important? is it important for all domains ? From the beginning, (Airbnb)we knew that Personalization was going to play a big role in the ranking of Experiences because of the diversity of both the inventory and the guest interest.
3. dd

### for personalized contents (like FB feeds)
No user have the same contents

# implementaion
1. In Airbnb experience search ranking simple stage, our ML model was limited to using only Experience Features, and as a result, the ranking of Experiences was the same for all users. In addition, all query parameters (number of guests, dates, location, etc.) served only as filters for retrieval (e.g. fetch Paris Experiences available next week for 2 guests), and ranking of Experiences did not change based on those inputs.

Given such a simple setup, the entire ranking pipeline, including training and scoring, was implemented offline and ran daily in Airflow. The output was just a complete ordering of all Experiences, i.e. an ordered list, which was uploaded to production machines and used every time a search was conducted to rank a subset of Experiences that satisfied the search criteria.

# Practical Examples

# Industry Examples
[Airbnb experiences search ranking](https://medium.com/airbnb-engineering/machine-learning-powered-search-ranking-of-airbnb-experiences-110b4b1a0789)
- At first launch, the best choice was to just randomly re-rank Experiences daily, until a small dataset is collected for development of the Stage 1 ML model.
    - Labeling training data: When labeling training data, we were mainly interested in two labels: experiences that were booked (which we treated as positive labels) and experiences that were clicked but not booked (which we treated as negative labels). In this manner, we collected a training dataset of 50,000 examples.
    - features:  In Stage 1 of our ML model, we decided to rank solely based on Experience Features. In total we built 25 features, some of which were:
        -  Experience duration (e.g. 1h, 2h, 3h, etc.)
        - Price and Price-per-hour
            Category (e.g. cooking class, music, surfing, etc.)
            Reviews (rating, number of reviews)
            Number of bookings (last 7 days, last 30 days)
            Occupancy of past and future instances (e.g. 60%)
            Maximum number of seats (e.g. max 5 people can attend)
            Click-through rate
    - model: GBDT. we treated the problem as binary classification with log-loss loss function.
        - tricks: When using GBDT, one does not need to worry much about scaling the feature values, or missing values (they can be left as is). However, one important factor to take into account is that, unlike in a linear model, using raw counts as features in a tree-based model to make tree traversal decisions may be problematic when those counts are prone to change rapidly in a fast growing marketplace. In that case, it is better to use ratios of fractions. For example, instead of using booking counts in the last 7 days (e.g. 10 bookings), it is better to use fractions of bookings, e.g. relative to the number of eyeballs (e.g. 12 bookings per 1000 viewers). 
        - validation: Specifically, we re-ranked the Experiences based on model scores (probabilities of booking) and tested where the booked Experience would rank among all Experiences the user clicked (the higher the better).

# empirical take-away
1. pick the model and infrastructure with the right level of complexity for the amount of data available and the size of the inventory that needs to be ranked. Very complex models will not work well when trained with small amounts of data, and simple baselines are sub-optimal when large amounts of training data are available. [article](https://medium.com/airbnb-engineering/machine-learning-powered-search-ranking-of-airbnb-experiences-110b4b1a0789)
2. Things to consider for application/practice with real world examples
    - what heuristics may impact this domain?  What is perception of human being? Are they able to discern the difference? 
        - e.g.  Airbnb expericne Personalization was going to play a big role in the ranking of Experiences because of the diversity of both the inventory and the guest interest. Unlike our Home business, where two Private Rooms in the same city at a similar price point are very similar, two randomly chosen Experiences are likely to be very different, e.g. a Cooking Class vs. a Surf Lesson. At the same time, guests may have different interests and ideas of what they want to do on their trip, and it is our goal to capture that interest fast and serve the right content higher in search results.
    - What is social value
3. When creating personalization features it is very important not to “leak the label.i.e. expose some information that happened after the event used for creating the label. Therefore, we only used user clicks that happened before bookings
4.  to reduce leakage further, when creating training data we computed the personalization features only if the user interacted with more than one Experience and category (to avoid cases where the user clicked only one Experience / category, e.g. Surfing, and ended up booking that category).


## miscellaneous
1. PCA
    1. **what**: convert a set of correlated columns into a smaller set of uncorrelated columns, reducing the amount of features of a problem. This smaller set of columns are called the principal components. This technique is mostly used in exploratory data analysis as it reveals internal structure in the data that can not be found with eye-balling the data.
    2. **usage**: compress data, reduce features,  With PCA a new value is calculated for each datapoint, based on its original dimensions(not simply just drop dimensions).
    3. **weakness**: A big weakness of PCA however are outliers in the data. These heavily influence its result, thus looking at the data on beforehand, eliminating large outliers can greatly improve its performance.

# course
[course practical ml](https://www.coursera.org/learn/practical-machine-learning/supplement/xWt3R/syllabus)

# reference

[machine-learning-self-study-resources](https://ragle.sanukcode.net/articles/machine-learning-self-study-resources/)

[Machine Learning for Developers ](https://xyclade.github.io/MachineLearning/#labeling-isps-based-on-their-downupload-speed-k-nn-using-smile-in-scala)
[gentle-introduction-to-predictive-modeling](https://machinelearningmastery.com/gentle-introduction-to-predictive-modeling/)
[machine-learning-is-fun part 2](https://medium.com/@ageitgey/machine-learning-is-fun-part-2-a26a10b68df3)

[machine-learning-for-programmer](https://machinelearningmastery.com/machine-learning-for-programmers/)


