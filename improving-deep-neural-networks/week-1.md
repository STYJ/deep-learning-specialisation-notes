- Applied machine learning is an interative process, you need to keep tweaking the hyperparameters to see what gives the best results. You almost always never get it right the first time round.
- If you have a lot of data, you don't need to stick to the 70/30 or 60/20/20 ratio for train / dev / test set. As long as your datasets are representative of future data and came from the same distribution (e.g. if you train w/ high quality images, don't test using low quality images.)
- High variance = overfitting i.e. low train set error but high dev set error because the NN cannot generalise well enough.
- High bias = underfitting i.e. high train set error and high dev set error.
- Low train set error and low dev set error means the model is performing well and can be used on the test set.
- Be aware of optimal (bayes) error. If optimal error is high e.g. 10% and train set error is 11%, this doesn't mean your model has high bias.

# Basic framework

1. Start by reducing variance (error in the train set). You can use more nodes / layers or even train longer.
2. Then you want to try reduce bias (error in the dev set). You can get more data or use regularization.

- Nowadays not much bias-variance tradeoff. We have tools that lets us modify one without really impacting the other.
- Regularization is used to reduce overfitting on a model that has overfitted.
- When the lambda value for l2 regularization becomes very big, it makes a lot of weights close to 0 so this means that the network effectively becomes a "smaller" network which turns high variance (overfitting) to high bias (underfitting) so perhaps somewhere along the way while you are cranking the lambda value up, you end up in the sweet spot where it's just right between variance and bias. 
- Dropout regularization is about probabilistically eliminating nodes in a layer. Since your network is going to be half the size (e.g. if you use 50% probability) then your network is going to overfit less thus moving from high variance -> high bias.
- Dropout regularization is only used during training. Once training is done, remove it when you are testing it with the dev set. 
- At every iteration, dropout regularization picks a different combination of nodes to zero. This ensures that all features are taken into consideration. 
- When you use dropout regularization, you need to also scale the other values by the dividing them by keep-prob. The purpose for this is to ensure that Z didn't decrease by 1 - keep-prob amount. 
- For example if you had 50 units and a keep-prob of 0.8 then on average, 10 nodes will be 0 in this layer. When looking at expected values (which is what the dot product does), the value of Z = W.a + b will be reduced by 20% so in order to not reduce Z, we should scale the other units up by dividing by keep-prob.
- You can also have different keep-prob for diff layers. These would be part of the hyperparameters.
- You can also stop learning earlier once you detect that your dev set error is increasing the more you train. The problem with this approach is that the task of reducing variance and the task of reducing bias are coupled together. This makes it very hard to modify one without affecting the other.
- An easier approach would be to use orthogonalization. This means that you treat them as separate tasks and use diff tools to optimise / solve these tasks separately.
- You can also augment your data with more data by modifying the original data e.g. flipping it across the Y axis, rotating it a little, cropping it a little etc.
- Normalization is to ensure that the scales of W and b are similar. This prevents an elongated bowl shaped cost function. Normalization causes the bowl to be more symmetrical and spherical and this allows you to reach the minimum w/ gradient descent much quicker.
- How you initialize your weights can have a big impact on z. There are instances where Z can get really really huge or really really small. Training becomes very slow when z is small cause the derivative of g(z) is close to 0.
- Sometimes it's hard to verify that your code is actually implemented correctly so you should do something like approximation of gradients to quickly calculate your gradients to ensure you're on the right track.