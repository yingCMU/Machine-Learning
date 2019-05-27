
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
L2 regularization:   <img src="https://latex.codecogs.com/svg.latex?\Large&space;\frac{ \lambda}{2m} \times \left \| w \right \|^{2}" title="\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}" />


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