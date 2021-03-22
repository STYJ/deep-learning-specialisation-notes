- You pass the output of 1 layer as input into the next layer
- Training set contains multiple tuples of (input e.g. a vector of features, an output)
- The hidden layer is not observed.
- X can alternatively be represented as a superscript [0] i.e. a[0] where a stands for the activation function and [0] stands for layer 0.
- When counting number of layers, we don't include the input layer so if the hidden layer has 4 layers, it is a 5 layer NN since you have to add 1 for the output layer.
- Tanh as an activation function is almost always superior to the sigmoid function because the mean is closer to 0 (tanh goes between 1 and -1). This makes training subsequent layers easier. The only time when a sigmoid activation function might be better is for the last layer of binary classification since binary classification is about returning 0 or 1 so by returning a value between 0 or 1 (sigmoid), you can just round to the closest integer to get 0 or 1.
- different layers can have different activation functions. Just denote as g[layer #]
- A disadvantage of both sigmoid and tanh is that if Z returns a large value, the gradient is close to 0 so this will slow down gradient descend.
- ReLU is the most common activation function.
- If you're not sure which activation function to use best, try them all then evaluate the prediction.
- A composition of multiple linear activation functions is still a linear function so might as well not have hidden layers.
- The only situation where it might make SOME ssense to use a linear activation function is for linear regression problems e.g. predicting the price of a house but even then, you only use it at the last layer.
- sometimes just ensuring that your dimensions match up will eliminate a lot of bugs
- notation = a superscript [2](12) subscript (6) = layer 2, 12th training example, node 6 in layer 2.

# Dimensions
W1 = (number of nodes in layer 1, number of inputs from prev layer i.e. number of inputs)
X = (number of inputs from prev layer, number of training sets)
b1 = (number of nodes in layer 1, number of training sets)
Z1 = W1.X + b = same dims as b1 = A1

W2 = (number of nodes in layer 2, number of inputs from prev layer i.e. number of nodes in layer 1)
A1 = same as Z1 = (number of nodes in layer 1, number of training sets)
b2 = (number of nodes in layer 2, number of training sets)
Z2 = W2.A1 + b = same dims as b2 = b2


- When initialising the values for W1 and W2, remember to initialise with random values instead of zeroes and multiply it with a really small number e.g. 0.001. Sometimes you might use other small values. The reason for the random values because if you use zeros, all nodes in the hiddle layer will effectively compute the same values i.e. 100 nodes has the same performance as 1 node. The reason for multiplying it with a small value is because if we use a big value then the outputs of the activation functions e.g. sigmoid, tanh would be a large value i.e. the derivative of it is close to 0 so learning will be very slow.
- If there are too many nodes in the hidden layer, the model is prone to overfitting. You can use regularization to somewhat work around this.

The general algorithm is still the same:
1. Initialise W1, b1, W2, b2 = params
2. Loop for the number of iterations
    - calc forward propagation(X, params), returns A2, cache (A1, Z1, A2, Z2)
    - compute cost(A2, Y, params), returns cost (average mistakes in %)
    - calc gradients with backwards propagation(params, cache, X and Y), returns grads (dW1, db1, dW2, db2)
    - update params(params, grads) e.g. w = w - learning_rate * dW1, returns updated params
    - optionally print 
3. Once training is done, return the params
4. With the final set of params, use it to do forward propagation to predict Y hat
5. If you want binary then if Y hat is a value > 0.5, you might give it a value of 1 etc.