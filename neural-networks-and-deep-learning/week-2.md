- Logistic regression is an algo for binary classification.
- A binary classification is tries to predict if the input is category A or category B e.g. is the picture a cat or not a cat.
- Loss vs cost function. Former computes the error for a single training example. The latter is the average of loss functions of the entire training set.
- When training your logistic regression model, we want parameters w and b that minimises the overall cost function J.
- Logistic regression can be viewed as a very small neural network.
- The cost function is in the shape of a 3d cone so the x and y axis represents w and b while the J represents the height on that cone.
- It doesn't matter how you initialise w and b since it's a cone, it should eventually converge to the global minimum.
- Gradient descent is about finding the steepest slope to take at each iteration.
- Derivative is basically referring to the slope of the function.
- Derivatives are equivalent to backwards propagation on a computation graph.
- In code, d(j) / d(var) should be named "dvar"
- Forward propagation is used to calculate the value of the loss function.
- Deep learning has a lot of data so if you have nested for loops, it's going to be very slow. Use vectorisation to remove for loops. See demo of vectorisation in the vectorization lesson.

# Lab
- The main steps for building a Neural Network are:
    1. Define the model structure (such as number of input features)
    2. Initialize the model's parameters
    3. Loop:
        - Calculate current loss (forward propagation)
        - Calculate current gradient (backward propagation)
        - Update parameters (gradient descent)
You often build 1-3 separately and integrate them into one function we call model().