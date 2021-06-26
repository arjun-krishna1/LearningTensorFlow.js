# My notes from [Deep Learning with JavaScript](https://www.manning.com/books/deep-learning-with-javascript) Chapter 2
# 2.2 Gradient Descent
- what happens when the model is being trained?
## Intuition behind gradient-descent optimization
- one-layer model is fitting a line function, f(input), which is:
`output = kernel * input + bias = f(input)`
- the kernel and bias are being tuned in the model, they are weights
- the weights contain the info learned by the network from the data
- they start with small random values
- as the slope and intercept fit to the data, the loss will be low
- as the weights change, they will get worse
- the loss of the function of all the weights represents the `loss surface`
- there is a global minimum (the bottom of the bowl) which represents the best parameter settings
- we start on a random location when the weights are randomly initialize
- next we gradually adjust the parameters based on the feedback signal
- this gradual adjustment  is training
- happens in the raining loop

## Training loop
- iterates through the loop for the number 
    1. make a batch of training samples and their answers
    2. run the network on the batch and obtain the networks predictions
    3. get the difference between the answers and predictions, this is the loss
    4. update the weights to slightly reduce the loss on this batch
- how can we determine which weights should be increased, and which to decrease
- random selection will take a lot of time
- all the operations in the network are `differentiable`
- we can compute the `gradient` of the loss with regard to the network's parameters

## Gradient
- gradient is `A direction such that if you move the weights by a tiny bit in that direction, you will increase the loss function the fastest, out of all the possible directions
- gradient is a vector
- has the same number of elements as the weights
- is a function of the current weight values, as weights change, gradient changes
- gradient is the direction where loss increases, thus we move the weights in the opposite gradient
- this process is **gradient descent**
stochastic means we draw random samples from data instead of using each for efficiency
more epochs had less loss because we followed the gradient descent path further

## Learning Rate
- if too small, reaching optimum parameters will take too long
- if too big, might skip over the minimum, may end up with higher loss

## Backpropagation
- how are the directions of updates computed?
- steps:
    - assuming x and y stay the same, how much change in the loss value will we get if v is increased by a unit amount
        - this is th gradient of loss wrt v
        - once we know in which direction it increases, we move in the opposite direction to decrease the loss
    - go back through the network
        - calculate the gradient of loss wrt a unit change of the edge value
            - what does this edge value need to be if the loss is one?
            - the amount of increase in loss we'll get if this edge value is increased by 1
            - this is the chain rule
    - in tf backpropogation, many values are batched at once