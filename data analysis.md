# exploratary data analysis
## priciple of analytical graphics
1. principle 1:  show comparison
- evidence for a hypothesis is always relative to another competing hypothesis
- always ask compare to what
e.g box plot of air cleaner home vs control home
2. principle 2: show causality, mechanism, explanation, systematic structure
- what is your causal framework for thinking about a question, how do you draw to show data explanation
e.g  draw box plot of particle matter levels
3. principle 3: show multivariate data
- real world is multivariate
- need to escapte flatland
e.g. draw  the data between mortality and PM concentration(compounding))vs draw it separately for each season (postivie relationship)

## why use graphs for data exploration
- understand data properties, find features
- explore basic questions and hypotheses (perhaps rule them out)
- find patterns in data
- suggest modeling strategies
- debug anayslis
- communicate results

## graphs
box plot: 6 number summary, min, 1st quntile, median, mean, 3rd qantile, max
histogram: show distribution , rug for fine details. tune the breaks parameter to see different granularity
scatter plots:

> 2 dimensions: 
 - overlap multiple 2-D plots; coplots
 - use color, shape, size to add dimensions,
 - spinning plots

 ## clustering analysis
 gives idea of relationship between variables , especially high-dimensional data
 1. choose a distance metric that make sense for the problem
 - continuous: euclidean distance
 - continuous: correlation similarity
 - Binary: manhattan distance
 2. draw hierachy with dendrogram/ heatmap

# reproducible research

 # importance
 question > data > feature > algorithm
 ## properties of good features:
 - lead to data compression
 - contain all relevant information
 - created based on domain knowledge
 common mistakes:
 - trying to automate feature selection
 - not paying attention to data-specifict quirks
 [Statistics for Genomcs: Distances and Clustering](https://www.youtube.com/watch?v=wQhVWUcXM0A)

 # Model selection:
 best ML method: Model Selection: Accuracy and other considerations
 - interpretable
 - simple
 - accurate
 - fast (to train and test)
 - scalable
 Accuracy1 is the main objective and a lot of effort goes towards raising it. But in practice tradeoffs have to be made, and other considerations play a role in model selection. Speed (to train/score) is important if the model is to be used in production. Interpretability is critical if a model has to be explained for transparency2 reasons (“black-boxes” are always an option, but are opaque by definition). Simplicity is important for practical reasons: if a model has “too many knobs to tune” and optimizations have to be done manually, it might be too involved to build and maintain it in production.
 Chances are a model that’s fast, easy to explain (interpretable), and easy to tune (simple), is less4 accurate.
 **rediction is about accuracy tradeoff**

 # train and test sample
 in sample error vs out of sample error (generalization error)
 generalization error is what really matters. train error is always less than generalization errors due to overfitting for sample noise. 
 data has two parts:
 1. signal
 2. noise

 sometimes give up some accuracy in the sample to get accuracy on new dataset
 ## prediction study design 
 or how to minimize the problems that can be caused by in sample verses out of sample errors. 

