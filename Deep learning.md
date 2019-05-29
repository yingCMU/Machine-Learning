
# Hyperparameter tuning, Regularization and Optimization
highly iterative process
- how many layers
- how many hidden units
- learning rate
- activation function

## Train / Dev / Test sets
Dev set: holdout, cross-validation. for model selection
test set: final portion to be test set. GIve a confident estimate
previous: 60/20/20
but now with big data, the dev and test portion is becoming smaller (like 10k , 1% for 1m examples)
now: 98/1/1
it might be ok to not having test set(only dev set, call it test set now)

## bias and variance
by comparing traing and test error , you will differenciate
high bias: when underfitting
high variance: when overfitting
assuming human classification is almost 0%
|   train error     | test error | cause |
| :-----------: |:-------------:| :-----:|
|  1%    | 10% | high variance |
|  15%    | 16% | high bias |
|  15%    | 30% | high bias  & variance|
|  0.5%    | 1% | low bias  & variance|

when will high bias and high variance happen: high bias in some regions and high variance in other regions, caused by too much flexibility in model

## recipie 
1. first do you have high bias?
to get rid of bias training problem:
- try bigger network, more layers, more hidden units
- train longer
- try more advanced optimization algorithm
- try better/advanced NN architecture
if human can do well, try abovel but if it is blured which means human can not do well, this probably won't help much
2. after fixing bias, do you have high variance？
- get more data
- regularization
- find better NN architecture
at this point, you need to iterate through step 1 and 2 util you find low bias and low variance method
the key is to choose appropriate solution based on your problem. e.g getting more data will not solve high bias problem.
back in the pre-deep learning era, we didn't have many tools, we didn't have as many tools that just reduce bias or that just reduce variance without hurting the other one. But in the modern deep learning, big data era, so long as you can keep training a bigger network, and so long as you can keep getting more data, which isn't always the case for either of these, but if that's the case, then getting a bigger network almost always just reduces your bias without necessarily hurting your variance, so long as you regularize appropriately. And getting more data pretty much always reduces your variance and doesn't hurt your bias much. So what's really happened is that, with these two steps, the ability to train, pick a network, or get more data, we now have tools to drive down bias and just drive down bias, or drive down variance and just drive down variance, without really hurting the other thing that much. And I think this has been one of the big reasons that deep learning has been so useful for supervised learning, that there's much less of this tradeoff where you have to carefully balance bias and variance, but sometimes you just have more options for reducing bias or reducing variance without necessarily increasing the other one as long as you have a well regularized network

### regularization
for linear regression:
1. L2 regularization:   <img src="https://latex.codecogs.com/svg.latex?\Large&space;\frac{\lambda}{2m}\times\left\|w\right\|^{2}" title="\Large x=\frac{ \lambda}{2m} \times \left \| w \right \|^{2}" />
2. L1 regularization:   <img src="https://latex.codecogs.com/svg.latex?\Large&space;\frac{\lambda}{2m}\times\left\|w\right\|" title="\Large x=\frac{ \lambda}{2m} \times \left \| w \right \|" />

for NN:
1. <img src="https://latex.codecogs.com/svg.latex?\Large&space;\frac{\lambda}{2m}\times\sum_{l=1}^{L}\left\|w^{[l]]}\right\|^{2}" title="\Large x=\frac{ \lambda}{2m} \times \left \| w \right \|^{2}" />
forbenius normalization = <img src="https://latex.codecogs.com/svg.latex?\Large&space;\left\|w^{[l]]}\right\|^{2} = \left\|w^{[l]]}\right\|^{2}=..." title="\Large x=\frac{ \lambda}{2m} \times \left \| w \right \|^{2}" />


# ML strategy

you've gotten your system to have 90% accuracy, but this isn't good enough for your application. You might then have a lot of ideas as to how to improve your system. For example, you might think well let's collect more data, more training data. Or you might say, maybe your training set isn't diverse enough yet, you should collect images of cats in more diverse poses, or maybe a more diverse set of negative examples. Well maybe you want to train the algorithm longer with gradient descent. Or maybe you want to try a different optimization algorithm, like the Adam optimization algorithm. Or maybe trying a bigger network or a smaller network or maybe you want to try to dropout or maybe L2 regularization. Or maybe you want to change the network architecture such as changing activation functions, changing the number of hidden units and so on and so on

## Orthogonalization
 e.g TV tunning example, each knob doew only one thing. car control: steering, brake and acce

 ## chain of assumption in ML
 1. fit training set well on cost function
 (to fix this)
 - train on bigger network
 - better optimization like Adam
 2. fit dev set well
(if work on train set well but not here, to fix this)
- regularization (prevent overfitting)
- or have bigging training set to generalize better
 3. fit test set well
 - bigger dev set
 4. perform well in real world
 - change devset
 - change cost function

## set up the goal
1. have a single real number evaluation metric
progress will be much faster and lets you quickly tell if the new thing you just tried is working better or worse than your last idea.
e.g1
There is often trade offs between precision and recall. So use F1 score (average of P and R), harmonic mean of P and R = ... 2/(1/p + 1/R)
e.g2
accuracy in 6 countries. So use average number as a single number
2. if it is not possible to have a single number, then setup satisfying and optimizing metric
e.g you care about accuracy, run time as well, so you can use:
cost = accuracy - 0.5 X run_time
maximizing metric : accuracy (meaning the higher the better)
satisfying metric: run_time <= 100ms (meaning it just need to be good enough )

if have N metrics, pick on as optimization, then N-1 to be satisfying metrics, within threshold
Another e.g： wakeup word
'Hi Alexa'
Maximising: accuracy
satisfying metirc: <=1 false positive every 24 hours

## setup train/dev/test data set to maximize efficiency
e.g if data from different regions, US,UK,China...
using some region as dev and others as test because data is from different distribution. This would mean your optimization on dev set won't generalize well on test set.
The solution is to randomly shuffle the data
Always choose dev and test set (from same distribution)to reflect data you expect to get in the future and consider important to do well on
### size of dev/test set
if you have 1 million data, 1% dev 1% test may be enough (10k each)
set your test set to be big enough to give high confidence in the overall performance of the system
### When to change dev/test sets and metrics
If what your metric prefers is different from what you prefer, you may consider changing metrics and refining metrics.
e.g cat image classifier, your metric is error rate. But it is not acceptable to see porn images. So you can update your error metrics to be higher weight if it is porn images.

## Compare to human-level performance
why?
1. First is that because of advances in deep learning, machine learning algorithms are suddenly working much better and so it has become much more feasible in a lot of application areas for machine learning algorithms to actually become competitive with human-level performance. 
2. Second, it turns out that the workflow of designing and building a machine learning system, **the workflow is much more efficient when you're trying to do something that humans can also do**. So in those settings, it becomes natural to talk about comparing, or trying to mimic human-level performance. Let's see a couple examples of what this means.
 after surpassing human level performance it can still get better, but the slope slows down. And the hope is it achieves some theoretical optimum level of performance. Bayes optimal error (Bayes error)  is the very best theoretical function for mapping from x to y.

why it slows down after passing human-level performance?
1.  One reason is that human level performance is for many tasks not that far from Bayes' optimal error. People are very good at looking at images and telling if there's a cat or listening to audio and transcribing it. So, by the time you surpass human level performance maybe there's not that much head room to still improve.
2. But the second reason is that so long as your performance is worse than human level performance, then there are actually certain tools you could use to improve performance that are harder to use once you've surpassed human level performance. So here's what I mean. For tasks that humans are quite good at, and this includes looking at pictures and recognizing things, or listening to audio, or reading language, really natural data tasks humans tend to be very good at.
  -  get labeled data: For tasks that humans are good at, so long as your machine learning algorithm is still worse than the human, you can get labeled data from humans. That is you can ask people, ask higher humans, to label examples for you so that you can have more data to feed your learning algorithm. Something we'll talk about next week is manual error analysis.
  -  manual error analysis: But so long as humans are still performing better than any other algorithm, you can ask people to look at examples that your algorithm's getting wrong, and try to gain insight in terms of why a person got it right but the algorithm got it wrong. And we'll see next week that this helps improve your algorithm's performance.
  - better analysis of bias/variance: And you can also get a better analysis of bias and variance which we'll talk about in a little bit. But so long as your algorithm is still doing worse then humans you have these important tactics for improving your algorithm. Whereas once your algorithm is doing better than humans, then these three tactics are harder to apply.

### Avoidable bias
 you don't actually want to do too well and knowing what human level performance is, can tell you exactly how well but not too well you want your algorithm to do on the training set. e.g. if your classifer has 8% training error and 10% dev error, but human error is 1%, this means you need to improve your training first to reduce bias.
 But if human error is 7.5%, maybe data set is so blured so even human can't tell. This means you need to focus reducing variance.
 For CV task, it is reasonable to assume humna error as a proxy for Bayes error because human is really good at CV

 to summarize:
 - avoidable bias: gap bettwen train error and human level error
 - reduce viarance: gap between dev error and train error

